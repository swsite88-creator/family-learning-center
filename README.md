# 家庭学习中心

面向小学四至六年级的独立静态学习入口。内置英语主题词汇（每年级 36 个）、词汇小测、句型练习、听力、分级阅读和录音跟读自评。无构建依赖、无需账号或后端，学习记录仅存于当前设备浏览器，可导出 JSON 备份。

## 本地预览

可直接打开 `index.html`。测试 PWA 离线缓存时，请通过本地静态服务器访问（例如 `python -m http.server 8000`），再打开 `http://localhost:8000`。

## GitHub Pages 部署

网站已部署到 `https://swsite88-creator.github.io/family-learning-center/`。仓库使用 GitHub Actions 发布 Pages；后续推送到 `main` 会自动更新。通过 GitHub 网页登录、Git Credential Manager 或 SSH 密钥授权；不要把密码、令牌或私钥写入文件。

源码仓库：[swsite88-creator/family-learning-center](https://github.com/swsite88-creator/family-learning-center)。

PWA 安装需 HTTPS 或 localhost；跨设备同步暂不提供。英语跟读录音在当前页面内暂存、不会上传；支持设备端识别的浏览器可提供词句匹配参考分，其他设备可回放自评。完整核查见 [项目可行性报告](REPORT.md)。

## 思维进阶课程

首页“思维进阶课”新增四至六年级分层任务：语文证据阅读与论证、数学多步建模、英语分级阅读表达、科学探究和跨学科项目。每项包含任务、提示、参考思路，完成后记录到本机。原创内容参考教育部 2022 版课程标准，详见 [项目可行性报告](REPORT.md)。静态运行，无新增依赖或外部服务。

## 绑定自定义域名

准备使用 `020c.cc.cd`。GitHub Pages 仓库设置里的 Custom domain 填写此域名；DNS 根域名需要配置 GitHub Pages 官方列出的四条 A 记录（可按 DNS 提供商支持情况一并添加四条 AAAA 记录）。详细步骤见项目对话说明和 GitHub Pages 文档。HTTPS 证书签发后，在 Pages 设置启用 Enforce HTTPS。

GitHub Pages 根域名 DNS（在 DNS 服务商处，主机记录通常填 `@`）：添加 A 记录 `185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`。如服务商支持并需要 IPv6，可添加 AAAA：`2606:50c0:8000::153`、`2606:50c0:8001::153`、`2606:50c0:8002::153`、`2606:50c0:8003::153`。不要删除域名已有的邮件/MX 记录。
