# 家庭学习中心

面向小学四至六年级的独立静态学习入口。无构建依赖、无需账号或后端，学习记录仅存于当前设备浏览器，可导出 JSON 备份。

## 本地预览

可直接打开 `index.html`。测试 PWA 离线缓存时，请通过本地静态服务器访问（例如 `python -m http.server 8000`），再打开 `http://localhost:8000`。

## GitHub Pages 部署

在自己的 GitHub 账号创建独立仓库 `family-learning-center`，将本目录文件推送到仓库根目录，在 Settings → Pages 选择从 `main` 分支根目录部署。通过 GitHub 网页登录、Git Credential Manager 或 SSH 密钥授权；不要把密码、令牌或私钥写入文件。

当前工作区尚未关联 Git 仓库或 GitHub remote，文件已准备好，但未创建远程仓库、推送或发布。

PWA 安装需 HTTPS 或 localhost；跨设备同步暂不提供。完整核查见 [项目可行性报告](REPORT.md)。
