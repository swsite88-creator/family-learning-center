# AGENTS.md · 给接手这个仓库的 AI 的说明

> 你（任何 AI 或开发者）接手本项目时，**先读这个文件**，再按需读 `README.md`（使用说明）与 `REPORT.md`（项目现状报告）。
> 本文件记录的是"必须遵守的事实与纪律"，优先级高于 README。若两者冲突，以本文件为准。

最后更新：2026-11-22

---

## 1. 项目是什么

面向小学四至六年级孩子的家庭学习入口。**纯静态网站**：没有后端、没有数据库、没有账号系统、没有付费 API、不采集儿童个人信息。所有进度存在访问者自己的浏览器 localStorage 里。

| 项目 | 值 |
|---|---|
| 线上地址 | https://www.020c.cc.cd |
| 英语书架页 | https://www.020c.cc.cd/magic-series.html |
| 仓库 | https://github.com/swsite88-creator/family-learning-center |
| 本机路径 | `D:\CODEX工作区\family-learning-center` |
| 部署方式 | GitHub Pages，由 `.github/workflows/pages.yml` 在推送 `main` 后自动发布 |
| 自定义域名 | `www.020c.cc.cd`（仓库内 `CNAME` 文件） |

---

## 2. 真实文件清单

| 文件 | 作用 | 能否直接改 |
|---|---|---|
| `index.html` | 首页：hero → 学科卡 → 英语站（默认折叠）→ 学习工具 | 可以（保留文案与结构意图） |
| `styles.css` | 基础样式（原版，压缩风格） | 尽量不改，视觉改动走主题层 |
| `cartoon-theme.css` | 卡通主题覆盖层（描边 + 硬阴影 + 纸感底纹） | 可以，视觉改动优先改这里 |
| `app.js` | 首页交互、年级选择、每日练习题库、错题/记录、英语折叠展开 | 可以 |
| `english.js` | 英语站六个 tab、词汇/句型/听力/阅读、录音跟读、进度 | 可以 |
| `english-adventure.html` | 原创"星芽探险社"故事模块（自带内联样式） | 可以（注意未套用卡通主题） |
| `advanced.js` | 兴趣挑战工作室的脚本，**目前没有被任何页面引用** | 保留勿删，见 §6 |
| `magic-series.html` | 哈利·波特魔法英语系列书架页 | 可以（加新书在此加卡片） |
| `hogwarts_english_adventure_grade_4_interactive_book.html` | 用户提供的原版四年级互动书 | **禁止修改**，见 §5 |
| `hogwarts_magic_english_book_10000_pages.html` | 10000 页完整版（10 卷 × 1000 页，10 种练习） | 用户提供的文件，原样保留 |
| `hogwarts_magic_book_3_agents_5000_pages.html` | 魔法特工 5000 页版（5 卷 × 1000 页，5 种练习） | 用户提供的文件，原样保留 |
| `sw.js` | Service Worker，cache-first 离线缓存 | 可以，但**必须按 §4 升版本** |
| `manifest.webmanifest` / `icon.svg` | PWA 元数据与图标 | 可以 |
| `README.md` / `REPORT.md` | 使用说明 / 项目报告 | 可以 |

首页现有 section 顺序：`#subjects` → `#english-learning` → `#tools` → `#records`（`#advanced` 已删除）。

---

## 3. 数据与存储键

全部在浏览器 localStorage，不上传、不跨设备同步。

| 键 | 内容 | 写入方 |
|---|---|---|
| `family-learning-center-v1` | 学习记录、错题、连续天数、每日练习会话 | `app.js` |
| `family-learning-english-v1` | 英语站进度、成绩、单词索引 | `english.js` |
| `family-learning-grade` | 当前选中年级（4 / 5 / 6） | 首页与英语站下拉框 |
| `family-learning-interest` | 兴趣挑战工作室草稿（版块已下架，键仍在） | `advanced.js`（当前无入口） |
| `hogwarts_book3_5000_state_v1` | 魔法特工 5000 页版的页码与 XP | 该书自身 |

年级机制（重要）：年级选择器现在**真的会过滤内容**。
- 每日练习按年级从三套题里取（4/5/6 各 5 道）
- 错题复习、学习记录只显示当前年级；**早期无年级字段的旧记录会保留可见**（这是有意为之，不要"清理"掉）
- 英语站句型/听力/阅读是**严格等于当前年级**，不是累积
- 切换年级时已打开的面板会立即重渲染

---

## 4. 技术红线（踩过坑，务必遵守）

1. **改任何前端文件，必须同时升 `sw.js` 的缓存版本**（当前 `family-learning-center-v12`）。SW 是 cache-first，只改文件不升版本，已安装 PWA 的老用户永远看旧版。
2. **新增静态文件，必须加进 `sw.js` 的 `FILES` 数组**，否则离线不可用。
3. 不要引入构建步骤、后端、数据库、账号系统、付费 API 或任何儿童数据采集。
4. 不写任何密码、Token、API Key、私钥进文件或提交。
5. `styles.css` 是压缩过的原版，改视觉请优先在 `cartoon-theme.css` 里覆盖，便于一键回滚（删掉 `index.html` 里那一行 `<link>` 即还原）。
6. 本仓库独立，**不要动 `D:\CODEX工作区` 下的其他仓库或项目**。不用 `--force`、不 `reset --hard`、不删分支。
7. `git status` 里可能有用户自己的未提交改动（如 `REPORT.md`），**不要擅自 `add -A`、不要覆盖、不要提交别人的改动**。
8. 不要为了"看得见效果"而编造描述：这几本书的故事页是**模板/场景变体组合生成**的，绝不能写成"5000 篇不同的故事"。这是用户的明确要求。

---

## 5. 不能碰的文件

`hogwarts_english_adventure_grade_4_interactive_book.html` 是用户授权的原版文件，**逐字节保留**，其 SHA-256 应为 `e69700749a38c14203c443e6458f7bac9c5fc236a87da5e29d8b439f308371d6`。
改动它会让"线上与本地一致"的校验失去意义。确实要改，必须先向用户说明改动范围并单独审阅。

另外两本书（10000 页版、5000 页版）也是用户提供的原样文件，更新时用**整文件替换**，不要手改内容。

---

## 6. 已经做过的结构决策（别回退）

- 首页的"兴趣挑战工作室"版块已**整块删除**（section、专用 `challenge-dialog`、`<script src="advanced.js">` 全部移除）。`advanced.js` 文件本身**故意保留在仓库**，以便日后恢复。不要因为"发现一个没被引用的文件"就删掉它。
- 英语学习站默认**收起**，点英语学科卡就地展开，再点收起；`#english-learning` 深链会自动展开。这是用户要求的信息架构，不要改回常显。
- 语文 / 数学 / 科学三张卡都指向同一个外链（`d3nmsqi4n72idj.cloudfront.net`），站内**没有**这三科的内容。用户知情，不要假装有。
- 哈利·波特书目入口已从"首页直达"升级为"书架页中转"：以后加新书 = 往 `magic-series.html` 加一张 `.book-card` 卡片 + 把文件加进 `sw.js` 的 `FILES`，不用动首页。

---

## 7. 本地验证方法

```bash
cd D:/CODEX工作区/family-learning-center
python -m http.server 8123      # 然后访问 http://localhost:8123
node --check app.js english.js sw.js
```

**移动端不要靠直接截图判断"溢出"**，这台机器有 133% 系统缩放，`--window-size` 高度较大时 Edge headless 会横向截断渲染，看起来像溢出、实际没问题。正确做法：

1. 写一个临时页，用 `<iframe width="390">` 载入目标页
2. 在 iframe 里读 `document.documentElement.scrollWidth`，与 390 比较
3. 遍历 `body *` 的 `getBoundingClientRect().right`，找出真正越界的元素
4. 需要文本数据时用 `--dump-dom` 提取，不依赖截图识别

截图命令模板：

```bash
"/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe" \
  --headless=new --disable-gpu --force-device-scale-factor=1 \
  --user-data-dir=<临时目录> --screenshot=<输出.png> \
  --window-size=400,900 --virtual-time-budget=8000 "<url>"
```

验证完**删掉临时文件**（`_verify.html` 之类不要提交）。

---

## 8. 部署与上线核验

```bash
git add <只加你改的文件>
git commit -m "<说明改了什么、为什么>"
git push origin main
```

推送后：

1. 查 Actions：`https://api.github.com/repos/swsite88-creator/family-learning-center/actions/runs?per_page=1`，等 `conclusion: success`
2. 比对线上与本地哈希，确认真的是新版本（Pages CDN 有约 10 分钟缓存，刚推完看到旧内容是正常的）
3. 打开线上域名用 iframe 法复验一次真机宽度

**只有获得用户明确授权才推送。** 改完先把改动文件、验证结果、风险说清楚。

### Pages 间歇性故障（已知问题）

有时 `Upload site artifact` 成功、只有 `Deploy to GitHub Pages` 在 10 秒内快速失败，GitHub 状态页却显示正常。这不是代码问题：连推空提交（`git commit --allow-empty`）重试，通常第 2–4 次就成功。失败日志匿名 API 拿不到，不必反复排查代码。

---

## 9. 待办 / 已知不一致

- `english-adventure.html`（星芽探险社）有自己一整套内联样式、只引 `styles.css`，**没有套用卡通主题**，从首页点进去风格有落差。
- `README.md` 部分小节描述的是已下架的旧版块，属于历史文档，改动前请对照现状。
- `REPORT.md` 长期有用户自己的未提交改动，不要代为决定是否提交。
