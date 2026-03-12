---
title: 🏗️ 施工图纸:Quartz博客全自动化配置方案
created: 2026-03-12T14:51:33
tags: [教程]
---

### 1. 存储层：数据心脏 (Cloudflare R2)

这是整个系统的物理基础，负责存储你的博文原稿、图片附件及历史版本。

* **Bucket 配置**：
* **名称**：建议使用 `blog-content` 或自定义名称。
* **版本控制 (Versioning)**：**必须开启**。这是实现“版本回滚”和“后悔药”功能的物理前提。


* **网络层 (国内访问优化)**：
* **自定义域名**：在 R2 桶设置 -> `Public Access` 中，绑定一个你自己的二级域名（例如 `sync.yourdomain.com`）。
* **CDN 加速**：在 Cloudflare DNS 页面确保该域名的“小云朵”图标为**橙色 (Proxied)**。
* **优势**：手机端 Obsidian 同步时，流量会经过 Cloudflare 全球 CDN 节点。即使在国内，也能极大改善由于直连 R2 API 域名导致的超时和连接失败。


* **权限设置 (API Token)**：
* 生成一个 R2 令牌，权限赋予 `Object Read & Write`。
* **注意**：在手机 Obsidian 的 Remotely Save 插件中，`Endpoint` 需填写为你的**自定义域名地址**。



### 2. 调度层：逻辑大脑 (Trigger Worker)

这是系统的“指挥官”，负责监听变动并管理 15s 的时间规则。

* **部署环境**：Cloudflare Workers。
* **依赖组件**：
1. **KV Namespace**：创建一个名为 `BLOG_SYNC_KV` 的命名空间（用于记忆冷却时间）。
2. **Cloudflare Queues**：创建一个队列（用于精准实现 15s 延迟，防止 Worker 因挂起超时被杀）。


* **核心逻辑流程**：
1. **事件监听**：通过 R2 `Event Notifications` 接收文件新增/修改信号。
2. **机器人过滤**：检查 Metadata 标签。若 `source == "github-action"`，则判定为网页端后台修改触发的反馈，**直接终止**，防止死循环。
3. **15s 冷却 (Cooldown Check)**：
* 从 KV 中读取 `last_trigger_timestamp`。
* 若 `当前时间 - 上次时间 < 15秒`，则判定为频繁保存，**丢弃当前任务**。


4. **15s 延迟 (Delay Queue)**：
* 若通过冷却检查，将任务推入 Queue 队列，并设置 `delay_seconds: 15`。


5. **信号发送**：15秒后，Queue 唤醒 Worker，向 GitHub 发送 `repository_dispatch` 信号（携带 Token 和 Repo 信息）。



### 3. 安全门禁：Zero Trust (防盗门)

* **路径保护**：在 Cloudflare Zero Trust 中创建 `Application`，将路径指向 `yourblog.com/admin/*`。
* **身份验证**：配置邮箱验证码或独立密码登录，替代传统的 OAuth 授权。

### 4. 生产层：自动化流水线 (GitHub Actions)

当 GitHub 接收到 Worker 发来的信号后，开始执行 `.github/workflows/sync.yml`。

* **步骤 1：双向环境同步 (Rclone)**
* 使用 Rclone 从你的自定义域名（R2）拉取 `content/` 文件夹。
* **关键参数**：同步时必须带上 `--s3-metadata '{"source":"github-action"}'`，这是防止系统死循环的“身份牌”。


* **步骤 2：多媒体自动化处理**
* **图片压缩/转码**：扫描 `attachments/`，使用 `Sharp` 库将 `.jpg/.png` 增量转换为 `WebP` 或 `AVIF` 格式，并自动替换 Markdown 中的引用后缀。
* **OG 海报生成**：调用 `Satori` 或 `Canvas` 脚本，抓取博文 YAML 里的 `title`，自动渲染一张 `1200x630` 的海报图，存入 `public/og-images/`。


* **步骤 3：数据提取与 Notion 视图生成**
* 运行一个 Python/Node 脚本遍历全站 Markdown 的 YAML 区。
* 提取 `status`（阅读状态）、`rating`（评分）、`updated`（更新时间）。
* 输出为 `db.json`，供 Quartz 的自定义组件读取，在首页渲染出类似 Notion 的多维表格。


* **步骤 4：全站快照清单 (Manifest)**
* 在 Quartz 构建完成后，扫描当前所有生成的 HTML/MD 文件及其对应的 R2 Version ID。
* 生成 `manifest_{timestamp}.json`。
* **存入 R2**：将其发送到 R2 桶的 `/_backups/` 目录下。这不仅记录了时间，也记录了该时刻全站的“指纹”。



### 5. 管理层：网页后台 (Decap CMS) 与中转逻辑

解决你在外面想改博文且不想折腾登录的问题。

* **中转 Worker (Option A 落地)**：
* 在 Cloudflare 部署一个名为 `cms-auth-proxy` 的 Worker。
* **逻辑**：Worker 内部通过环境变量持有你的 `GITHUB_TOKEN`。
* 当你在后台点“保存”时，后台向这个 Worker 发请求，由 Worker 替你完成 Git Commit。


* **后台 UI 增强**：
* **容量仪表盘**：通过 JavaScript 调用 Cloudflare API 接口（`/client/v4/accounts/{id}/r2/buckets/{name}`），在后台顶部实时显示：“已用容量 / 总容量”。
* **版本来源追踪**：在版本显示区域，通过读取 `manifest.json` 里的 `parent_version` 字段，展示：“当前版本源自 [2026-03-04 10:00]”。



### 6. 维护层：生命周期自动管理 (Cron Worker)

解决 R2 存储费用和版本过杂的问题。

* **执行方式**：Cloudflare Worker Cron Triggers（建议每天凌晨 3 点）。
* **逻辑**：
1. 读取用户设定的 `CLEANUP_STRATEGY`（'COUNT' 或 'DAYS'）。
2. 调用 `list-object-versions` 接口。
3. **按数量**：如果某文件版本 > 50，删除最旧的。
4. **按时长**：如果版本时间 > 30天，删除。
5. **手动开关**：在后台管理页提供一个按钮，点击可立即触发此 Worker 运行。



---

## 🚦 施工路线总结 (Final)

1. **地基**：Cloudflare R2 (开版本控制 + 绑自定义域名)。
2. **管道**：Obsidian $\rightarrow$ R2 (使用 Remotely Save 插件)。
3. **发令枪**：Worker A (Queue 15s 延迟 + KV 15s 冷却)。
4. **加工厂**：GitHub Action (Rclone 同步 + 图片海报处理 + 生成清单)。
5. **前台**：Quartz 渲染 (含 Notion 视图与双向链接)。
6. **监控**：Decap CMS + 增强 Worker (容量统计 + 版本回滚 UI)。
