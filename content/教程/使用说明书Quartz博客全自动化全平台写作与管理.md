---
title: 📂 使用说明书:Quartz博客全平台写作与管理使用说明书
created: 2026-03-12T14:51:39
tags: [教程]
---

这份**《用户手册》**确保你在搭建好系统后，能像专业编辑一样管理自己的知识库。它包含了从手机端写作、图片处理到后台回滚的所有实操细节。

---

### 1. 写作端的初始化配置

在开始创作前，请确保你的 **Obsidian**（手机/电脑端）已按此标准调教：

* **同步插件配置 (Remotely Save)**：
* **服务商**：选择 `S3 Compliant Storage`。
* **Endpoint (关键)**：请填写你的 **自定义域名**（例如 `https://sync.yourdomain.com`），而非 Cloudflare 默认的长串地址。
* **Bucket 名称**：填写你在 R2 创建的桶名。
* **连接测试**：点击“Check”，确保国内网络环境下无需代理也能秒连。


* **附件管理规范**：
* 进入 `Settings -> Files & Links`。
* `Default location for new attachments`：选择 `Subfolder under current folder`。
* `Subfolder name`：统一填入 `attachments`。
* **禁止 WikiLinks**：关闭 `Use [[Wikilinks]]`，确保图片以标准 Markdown 语法 `![](./attachments/xxx.png)` 插入，以便 GitHub Actions 识别并压缩。



### 2. 标准博文创作规范

为了触发系统的高级功能（如自动海报、Notion 视图），请遵循以下 YAML 模板：

* **模板使用**：点击 Obsidian 的“插入模板”按钮。
* **核心字段说明**：
```yaml
---
title: 文章标题
date: 2026-03-12 10:00
updated: 2026-03-12 10:00
status: reading    # 可选值: drafting(草稿), reading(在读), done(已读)
rating: 5          # 评分 (1-5)，将触发网页端星星显示
cover: auto        # 设为 auto，系统将自动根据标题生成封面图
tags: [技术, 生活]
---

```


* **发布操作**：
1. 写完文章后，点击 Obsidian 侧边栏的“同步”按钮。
2. **“15秒法则”**：点击同步后即可关闭手机。系统会等待 15 秒（防抖）并在 15 秒冷却后自动触发云端构建。



### 3. 多媒体资源的处理

* **图片插入**：直接将图片粘贴到 Obsidian 即可。
* **自动处理**：你无需手动裁剪。当你同步到 R2 后，GitHub Actions 会自动执行以下任务：
1. 将原始大图（JPG/PNG）压缩转换为 **WebP** 格式以节省流量。
2. 自动将网页中的图片链接指向压缩后的版本。

