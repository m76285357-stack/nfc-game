# 🎪 益智游乐场 —— 写进 NFC 的网页小游戏

给小学生玩的益智小游戏合集，可托管到 GitHub Pages，把网址写进 NFC 标签后，
小朋友用手机贴一下标签就能打开玩（离线也能玩）。

## 文件说明

| 文件 | 作用 |
|------|------|
| `index.html` | 游戏本体（打地鼠、记忆翻牌、灯光记忆、接水果、随机冒险），所有代码都在一个文件里 |
| `manifest.json` | PWA 配置，让网页可以"添加到主屏幕"变成 App 图标 |
| `sw.js` | 离线缓存，第一次联网打开后，没网也能继续玩 |
| `icons/` | App 图标 |

## 一、把网站发布到 GitHub Pages

### 方式 A：网页上传（最简单，推荐）

1. 注册并登录 [github.com](https://github.com)。
2. 点右上角 **+** → **New repository**，仓库名填 `nfc-game`（或随便起），设为 Public，创建。
3. 进入仓库，点 **uploading an existing file**（或 Add file → Upload files），
   把本文件夹里的这些文件**全部拖进去**：
   `index.html`、`manifest.json`、`sw.js`、`icons/` 整个文件夹。
4. 提交（Commit）。
5. 点仓库的 **Settings → Pages**，在 "Build and deployment" 里：
   - Source 选 **Deploy from a branch**
   - Branch 选 **main**、目录选 **/ (root)**
   - 点 **Save**
6. 等 1～2 分钟，页面上会显示网址，形如：
   `https://你的用户名.github.io/nfc-game/`
   用手机浏览器打开这个网址测试一下。

### 方式 B：用 git 命令上传

```bash
cd nfc-game
git init
git add .
git commit -m "益智游乐场"
git branch -M main
git remote add origin https://github.com/你的用户名/nfc-game.git
git push -u origin main
```

推上去后再按方式 A 的第 5 步开启 Pages。

## 二、把网址写进 NFC 标签

**需要准备：**
- NFC 标签（NTAG213 / 215 / 216 贴纸或卡片均可，淘宝几毛～几块钱）
- 一台支持 NFC 的**安卓**手机

**步骤：**
1. 应用商店下载免费的 **NFC Tools** App。
2. 打开 App → **写入(Write)** → **添加记录(Add a record)** → **URL / URI** → 输入网址
   （例如 `https://你的用户名.github.io/nfc-game/`）→ **确定**。
3. 点 **写入**，把手机背面贴近 NFC 标签，听到提示音即写入成功。
4. 完成！之后任何安卓手机（亮屏甚至黑屏状态）贴一下标签，就会自动打开浏览器进入游戏。

> **小提示**：可以顺便把这个网址生成一个**二维码**（微信/草料二维码都行），
> 打印出来贴在标签旁边——iPhone 或没有 NFC 的手机扫码一样能玩。

## 三、iPhone 的注意事项

⚠️ **iPhone 不能像安卓那样"贴一下就自动打开网页"**。iOS 对 NFC 后台读取限制很严。
iPhone 用户需要：
- 打开 NFC Tools 之类的 App 扫描标签，或
- 用系统"快捷指令"App 创建"扫描 NFC 时打开网址"的自动化。

所以如果面向 iPhone 用户，**强烈建议同时准备二维码**。

## 四、离线玩法

- 第一次打开时**需要联网**（网页会自动缓存下来）。
- 之后即使没有网络，也能正常打开和游玩。
- 想让游戏变成桌面 App 图标：安卓 Chrome 打开后点菜单 → **"添加到主屏幕"**，
  之后从桌面图标点开就是全屏游戏，体验和 App 一样。

## 五、自定义

- 改翻牌动物：编辑 `index.html` 里的 `EMOJIS` 数组。
- 改打地鼠速度 / 接水果难度：编辑 `index.html` 里的 `MoleGame` / `CatchGame`。
- 改鼓励语：编辑 `index.html` 里的 `PRAISES` 数组。
- 改图标颜色：改 `tools/gen-icons.js` 里的 `TOP`/`BOT`/`STAR` 颜色后运行 `node tools/gen-icons.js`。
