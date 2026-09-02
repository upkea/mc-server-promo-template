# ⛏️ MC 服务器宣传站 · 服主通用模板（0 元方案）

> 一个页面 = **宣传网站 + 在线状态秒查 + 一键加群**
> 附赠 = **「掉线哨兵」**：云端每 5 分钟检测服务器，掉线自动微信提醒你
> 全部花费：**¥0**（GitHub 免费托管 + 免费检测接口 + 免费微信推送）

本模板由一套**真实在用的 MC 服务器宣传方案**整理而来，已去除原服务器信息，任何我的世界
Java 版服务器服主都能直接复用。不会写代码也没关系，按本手册照做即可。

---

## 📁 文件结构

```
你的文件夹/
├── index.html            # 网页内容（改文案在这里）
├── css/style.css         # 样式（颜色/布局，一般不用动）
├── js/main.js            # ★★ 最重要的配置文件（地址/版本/群号都在这）
├── robots.txt            # 搜索引擎收录许可
├── .github/workflows/watchdog.yml   # 掉线哨兵（定时任务）
└── .watchdog/check.sh               # 掉线哨兵（检测+推送脚本）
```

---

## 🚀 快速上手（总共 3 件事）

### 第 1 步：改配置（5 分钟）

用**记事本**（不要双击 .js 文件）打开 `js/main.js`，改最上面这一段：

```js
var SERVER = {
  address: 'play.example.com:25565', // ★改成你的服务器地址（含端口）
  version: 'Java 版 1.20 – 1.21.8',  // ★改成你的服务器支持的版本范围
  group: ''                          // ★填你的 QQ 群号（纯数字）
};

var GROUP = {
  ...
  officialUrl: ''  // ★可选：你的官方加群链接
};
```

- 改完地址/版本/群号，**网页上所有对应位置会自动同步**，不用逐处改。
- 再打开 `index.html`，用「查找替换」把所有的 **【服务器名】** 换成你的服务器名
  （记事本：Ctrl+H；建议一次全替换）。
- 官方加群链接怎么拿：QQ 群里 → 群管理 → 加群设置 → 加群链接，复制 `qm.qq.com/q/xxxx`
  之类链接填进 `officialUrl`。不填也能用（手机自动跳 QQ 群卡片，电脑自动复制群号）。
- 想改页面文案（简介/特色/规则）、换图标颜色，都在 `index.html` 和 `css/style.css` 里，纯文字，随意改。

### 第 2 步：本地预览（1 分钟）

直接**双击 `index.html`** 就能在浏览器里看到效果（状态检测、复制、加群按钮都可试）。

### 第 3 步：免费上线（10 分钟，三选一）

**方案 A：GitHub Pages（推荐，可绑自定义域名）**
1. 注册 https://github.com （免费）
2. 右上角 + → **New repository**，名字随意（如 `mc-server-site`），选 Public，创建
3. 仓库页面 → **Add file → Upload files**，把文件夹里所有文件拖进去上传
4. 仓库 **Settings → Pages** → Source 选 `Deploy from a branch` → 分支 `main` → Save
5. 等 1~2 分钟，访问 `https://你的用户名.github.io/仓库名/` 🎉

**方案 B：Cloudflare Pages（国内访问更好）**
1. 注册 https://dash.cloudflare.com
2. Workers & Pages → Create → Pages → Upload assets → 把文件夹拖进去 → Deploy

**方案 C：Netlify（最简单）**
1. 打开 https://app.netlify.com/drop
2. 把文件夹直接拖进页面，完事。

---

## 📡 掉线哨兵（强烈推荐启用，全免费）

**它是干嘛的**：你的服务器如果在公益面板上（如简幻欢/SimpFun），经常会自动停服或忘记开服。
哨兵部署在 GitHub 云端（不用你电脑开机），**每 5 分钟检查一次**，发现服务器从在线变掉线，
就**推微信**提醒你去开服；服务器恢复也会通知你。

**启用步骤：**

1. **拿 SendKey**：打开 https://sct.ftqq.com → 微信扫码登录 → 关注「Server酱」服务号 → 复制 SendKey
2. **部署前先改** `.watchdog/check.sh` 顶部 `SERVER="play.example.com:25565"` 改成你的地址
   （顺手把两处推送文案里的 `【服务器名】` 改成你的服务器名）
3. 按上面「快速上手第 3 步」把**所有文件**（包括 `.github`、`.watchdog` 隐藏文件夹）上传到 GitHub 仓库
4. 加密钥：仓库 **Settings → Secrets and variables → Actions → New repository secret**
   - Name 填：`SERVERCHAN_KEY`
   - Secret 填：你复制的 SendKey
5. 去仓库 **Actions** 页：找到 `server-watchdog`，第一次要手动点 **Enable**（或 Run workflow 测试一次）
6. 完事。之后每 5 分钟自动检测，掉线/恢复都会微信通知你

**小知识：**
- GitHub 定时任务可能有几分钟延迟，属正常（想更快得用付费/Cloudflare Worker，对公益服没必要）
- GitHub 会暂停「超过 60 天没有仓库活动」的定时任务——如果提醒停了，去 Actions 页重新 Enable 即可
- 想改检测频率：编辑 `.github/workflows/watchdog.yml` 里的 `cron: '*/5 * * * *'`（最短 5 分钟）

---

## ❓ 常见问题

**Q：页面显示"离线/无法检测"，但我服务器明明开着？**
检测走海外免费接口，部分国内服务器会被误报。模板已做双接口交叉检测（任一在线即显示在线），
若仍异常，可先 F5 刷新（有 60 秒缓存），仍不行就换用 mcstatus.io 接口或忽略该状态。

**Q：一键加群按钮点了没反应？**
手机需安装 QQ；电脑端会自动复制群号，去 QQ 搜索加群即可。最好填上官方加群链接（见上）。

**Q：为什么不能"全自动签到+自动开服"？**
公益开服平台（如简幻欢）的签到带防脚本问答、开服要求先签到，都是平台反滥用的设计。
绕过它属于违反平台规则，有封号+服务器被停的风险。哨兵只负责"提醒你"，签到启动还是手动一下，
每天 30 秒，安全省心。

**Q：双击 .js 文件弹"Windows 脚本宿主"错误？**
正常现象：浏览器脚本不能在 Windows 里双击运行。想改代码请右键 .js → 打开方式 → 记事本。

**Q：以后想换自己的域名？**
买个便宜域名（首年几块到十几块）绑到 GitHub Pages 或 Cloudflare 即可，和本方案不冲突。

---

## 💰 成本总结

| 项目 | 价格 |
|---|---|
| 宣传网站托管 | ¥0（GitHub Pages / Cloudflare Pages / Netlify） |
| 在线状态检测 | ¥0（mcstatus.io + mcsrvstat.us 免费 API） |
| 掉线微信提醒 | ¥0（Server酱免费版，每天有推送条数上限） |
| 可选：自定义域名 | 首年 ¥1~15（.top/.com 促销），续费 ¥15~90/年 |

## 📤 分享给其他服主

- **直接发文件夹**：把本文件夹压缩成 zip 发给对方，让对方按本 README 操作即可
- **做成 GitHub 模板仓库**：把文件推到 GitHub 仓库后，Settings → 勾选 **Template repository**，
  别人新建仓库时就能一键 `Use this template`，省去上传步骤
