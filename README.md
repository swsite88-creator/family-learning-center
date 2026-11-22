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

GitHub Pages 自定义域名设为 `www.020c.cc.cd`。DNSHE 添加一条 CNAME：记录名称 `www`，记录内容 `swsite88-creator.github.io`，TTL 自动。不要把 CNAME 指向根域名或添加 A 记录到 `www`。如果还希望访问不带 www 的 `020c.cc.cd` 并自动跳转到 www，可另外保留根域名的 GitHub Pages A 记录。DNS 传播后，在 Pages 设置启用 Enforce HTTPS。