# 家庭学习中心

面向小学四至六年级的独立静态学习入口。内置英语主题词汇（每年级 36 个）、词汇小测、句型练习、听力、分级阅读和录音跟读自评。无构建依赖、无需账号或后端，学习记录仅存于当前设备浏览器，可导出 JSON 备份。

## 本地预览

可直接打开 `index.html`。测试 PWA 离线缓存时，请通过本地静态服务器访问（例如 `python -m http.server 8000`），再打开 `http://localhost:8000`。

## GitHub Pages 部署

网站已部署到 `https://swsite88-creator.github.io/family-learning-center/`。仓库使用 GitHub Actions 发布 Pages；后续推送到 `main` 会自动更新。通过 GitHub 网页登录、Git Credential Manager 或 SSH 密钥授权；不要把密码、令牌或私钥写入文件。

源码仓库：[swsite88-creator/family-learning-center](https://github.com/swsite88-creator/family-learning-center)。

PWA 安装需 HTTPS 或 localhost；跨设备同步暂不提供。英语跟读录音在当前页面内暂存、不会上传；支持设备端识别的浏览器可提供词句匹配参考分，其他设备可回放自评。完整核查见 [项目可行性报告](REPORT.md)。
