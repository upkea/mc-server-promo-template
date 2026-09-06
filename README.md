# ⛏️ MC 服务器宣传站 · 万能方案（一套搞定，¥0）

> 一个仓库 = **懒人向导 + 完整项目 + 掉线微信提醒**，全部免费。
> 宣传站内容：首页横幅 / 服务器信息 / 特色 / 三步加入 / 规则 / **FAQ** / 一键加群 / 在线状态秒查 / 手机适配。

本方案由一套真实在用的 MC 服务器宣传方案整理而来，已去除原服务器信息，任何 Java 版服务器服主都能直接用，**不会写代码也没关系**。

> 🛠️ **技术支持 QQ 群：1107711066**
> 使用本方案遇到问题（搭建 / 部署 / 掉线提醒配置 / 定制），加群咨询即可：
> [点此一键加群](https://qun.qq.com/universal-share/share?ac=1&authKey=yl%2BgEDRbTe%2FP06c%2FSRcxj%2BootHd3ba2ce%2BgNr7cZTyzfCy%2FfOma1l2J8c2TLLiPh&busi_data=eyJncm91cENvZGUiOiIxMTA3NzExMDY2IiwidG9rZW4iOiI3STd3aEZpdjRlSUpxVkswUzhNUkVUdnNxcklucno3SVN2dEpkSENpdmxUM0pKZmV6V3NWZjlHSHBZWmwvOTIzIiwidWluIjoiMTk1NDQ5NTM5MiJ9&data=A3tvyKbE9Tn2HPwtYas1UdySpJ_4fcueKZMwAnxHsi9JNzzqNQu4xy9VF4_PyJkWHcsDvcYhNmnL6wbZNuim6Q&svctype=4&tempid=h5_group_info)
> （或在 QQ 中直接搜索群号 **1107711066** 加入）

---

<p align="center">
  <a href="https://upkea.github.io/mc-server-promo-template/图文演示教程.html">
    <img src="图文教程按钮.png" alt="打开图文演示教程" width="460">
  </a>
  <br><small>🖼️ 配截图、一步一步做的演示教程，点上方按钮在线打开（无需下载）</small>
</p>

## 🚀 用法一（最省事，推荐）：用「配置向导」

双击打开本仓库根目录的 **`配置向导.html`**（建议 Chrome / Edge）：

1. 填：服务器名称 / 地址（含端口）/ 版本 / QQ 群号 / 官方加群链接（可空）
2. 点「🚀 生成完整宣传站」→ 下载得到一个 **`index.html`**
3. 把 `index.html` 部署到免费托管（三选一）：
   - **Cloudflare Pages**：dash.cloudflare.com → Workers & Pages → Upload assets → 拖入文件
   - **Netlify**：app.netlify.com/drop → 拖入文件
   - **GitHub Pages**：新建仓库（Public）→ 上传 `index.html` → 仓库 Settings → Pages → Source 选 Deploy from a branch → 分支 main → Save；等 1~3 分钟构建完成后，回到 Settings → Pages，顶部绿色横幅就是你的网址：`https://你的用户名.github.io/仓库名/`（点它打开即网站，Actions 标签里也能看到）
4. 拿到网址发到 QQ 群，完成 🎉

向导页里还内置了 **FAQ** 和「掉线自动微信提醒」的启用说明，一条龙讲完。

## 📁 用法二（进阶）：直接使用完整项目文件

> 📘 **新手请先看这份详细教程：[完整版详细教程.md](完整版详细教程.md)** —— 从复制仓库到改配置、开网站、开掉线提醒、验证，一步步带做，约 20 分钟。

想要**掉线自动微信提醒**（公益服常自动停服/忘开服）或长期维护项目时：

- `index.html` / `css/` / `js/`：完整宣传站（和向导生成的一模一样，可手工微调 `js/main.js` 顶部的 SERVER/GROUP 配置）
- `.watchdog/check.sh` + `.github/workflows/watchdog.yml`：**掉线哨兵**

**开启掉线提醒步骤：**
1. 点本仓库右上角 **Use this template** 生成自己的仓库（哨兵文件会一起带上）
2. 改 `.watchdog/check.sh` 顶部 `SERVER` 为你的服务器地址
3. 拿 Server酱 SendKey：sct.ftqq.com → 微信扫码登录关注服务号 → 复制 SendKey
4. 仓库 Settings → Secrets and variables → Actions → New repository secret：名称 `SERVERCHAN_KEY`，值粘贴 SendKey
5. 仓库 Actions 页 → `server-watchdog` → Enable / Run workflow
6. 之后每 5 分钟云端检测，掉线/恢复自动微信通知（GitHub 定时可能有几分钟延迟，正常）

## 🚀 用法三（一键上线 · 最省事）：自动创建网站并发布

> 不用会 GitHub/Cloudflare，**填信息点一下，自动生成 + 上线，直接给网址**（托管在腾讯云 COS，国内访问快）。

**步骤：**
1. 打开 `配置向导.html` → 填好：服务器名称 / 地址 / 版本 / QQ 群号
2. 找到 **「🚀 一键上线」**（AI 风格区下方）→ 点一下
3. 约 5~10 秒 → 页面出现网址 → **点它在浏览器打开**（带样式，不下载）→ 发给玩家即可 ✅

**说明：**
- 网站托管：腾讯云 COS 静态站点（公开只读），数据量极小、免费额度内
- **收费：目前暂不收费**；以后收费标准待定（暂定 **0.2r**，可适当调整，但需询问 **upke** 确认后再改）
- 卡密机制已就绪（一人一码、用后作废），待正式收费时启用
- 想在样式上先定制（三风格/AI 看图）？用「生成完整宣传站」本地生成查看；一键上线当前使用内置默认风格（明亮简洁）

## 📁 文件结构

```
├── 配置向导.html            # ★ 用法一入口：双击它，填表即出完整宣传站
├── index.html               # 完整宣传站（用法二，可手改）
├── css/style.css            # 样式
├── js/main.js               # ★ 手工改地址/版本/群号在这里（SERVER/GROUP）
├── .github/workflows/watchdog.yml   # 掉线哨兵定时任务
├── .watchdog/check.sh               # 掉线哨兵脚本
└── README.md
```

## ❓ 常见问题（详见向导页内 FAQ）

- 向导页本身不是宣传站，生成下载的 `index.html` 才是
- 状态显示"离线"？检测走海外免费接口（双接口交叉验证），部分国内服被误报，刷新/稍后再看即可
- 不能做"全自动签到+自动开服"：**如果你是公益服务器（如简幻欢 SimpFun 这类公益开服平台）**，平台的签到问答、先签到后开服、时长机制都是防滥用设计——绕过签到 / 模拟答题属违规，会**封号甚至服务器被停**。正确做法：每天手动签到一次（约 30 秒），配合本方案的「掉线哨兵」兜底提醒，既安全又不漏开服。
- 双击 .js 弹"脚本宿主"错误是正常现象，用记事本打开改代码即可

## 💰 成本

| 项目 | 价格 |
|---|---|
| 网站托管（Cloudflare/Netlify/GitHub Pages） | ¥0 |
| 在线状态检测（mcstatus.io + mcsrvstat.us） | ¥0 |
| 掉线微信提醒（Server酱免费版） | ¥0 |
| 可选自定义域名 | 首年 ¥1~15，续费 ¥15~90/年 |

## 📤 分享给其他服主

直接把本仓库链接发给对方：**Use this template** → 用「配置向导」生成或直接改 `js/main.js`，10 分钟搞定。
