# zashboard

<p align="center">
  <img src="./readme/pc.png" height="300">
  <img src="./readme/mobile.png" height="300">
</p>

## **Requirement**

Browser support

- Chrome 111 (released March 2023)
- Firefox 128 (released July 2024)
- Safari 16.4 (released March 2023)
- Not supported on iOS 16.4 jailbroken version.

## **Online**

You can access the online zashboard at the following link:

- [Online zashboard](http://board.zash.run.place)

## **Download**

You can download the zashboard files here:

> By default the builds **do not** include sing-box native API support (the Tools
> page: terminal, Tailscale, network tools, QR code — which pull in extra
> ConnectRPC/protobuf and xterm code). To get a release build **with** it, append
> `-singbox-native` to any variant below, e.g.
> [`dist-singbox-native.zip`](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-singbox-native.zip)
> or `dist-misans-only-singbox-native.zip`. The same suffix works for the
> `gh-pages-*` dev branches too (e.g. `gh-pages-no-fonts-singbox-native`).
>
> The online site at [board.zash.run.place](http://board.zash.run.place) (the
> root `gh-pages` branch) is the one exception: it always ships the full build —
> all fonts **and** sing-box native support.

release:

- [dist.zip (7.81 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist.zip) – Includes better font-loading experience.
- [dist-no-fonts.zip (1.44 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-no-fonts.zip) – No fonts included, uses system fonts only.
- [dist-cdn-fonts.zip (1.44 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-cdn-fonts.zip) – Fonts loaded from unpkg.com, If you have trouble connecting to unpkg.com, **you may experience slow page loading**.
- [dist-firasans-only.zip (1.67 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-firasans-only.zip) – Only with FiraSans Font
- [dist-misans-only.zip (3.54 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-misans-only.zip) – Only with MiSans Font
- [dist-pingfang-only.zip (3.25 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-pingfang-only.zip) – Only with PingFang Font
- [dist-sarasa-only.zip (3.67 MB)](https://github.com/Zephyruso/zashboard/releases/latest/download/dist-sarasa-only.zip) – Only with Sarasa Font

dev:

- [gh-pages.zip (7.81 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages.zip)
- [gh-pages-no-fonts.zip (1.44 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages-no-fonts.zip)
- [gh-pages-cdn-fonts.zip (1.44 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages-cdn-fonts.zip)
- [gh-pages-firasans-only.zip (1.67 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages-firasans-only.zip)
- [gh-pages-misans-only.zip (3.54 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages-misans-only.zip)
- [gh-pages-pingfang-only.zip (3.25 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages-pingfang-only.zip)
- [gh-pages-sarasa-only.zip (3.67 MB)](https://github.com/Zephyruso/zashboard/archive/refs/heads/gh-pages-sarasa-only.zip)

## **部署到 Cloudflare Pages**

### 方式一：通过 Cloudflare Dashboard 连接 Git 仓库（推荐）

1. **Fork 本仓库** 到你的 GitHub 账户（如果不修改代码，也可以直接使用原仓库）。

2. **登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)**，进入左侧菜单 **Workers 和 Pages** > **Pages**。

3. 点击 **"创建项目"**（Create a project），然后选择 **"连接到 Git"**（Connect to Git）。

4. **授权 GitHub 访问**：首次使用需要点击 **"连接 GitHub 账户"**，授权 Cloudflare 访问你的仓库。

5. **选择仓库**：在列表中找到你 Fork 的 `zashboard` 仓库，点击 **"开始设置"**（Begin setup）。

6. **配置构建设置**：
   | 配置项 | 填写内容 |
   |---|---|
   | 项目名称 | `zashboard`（可自定义） |
   | 生产分支 | `main` |
   | 构建命令（Framework preset 选 None） | `pnpm install && pnpm run build` |
   | 构建输出目录 | `dist` |

7. 点击 **"保存并部署"**（Save and Deploy）。Cloudflare 会自动拉取代码、构建并部署。

8. 部署完成后，Cloudflare 会提供一个 `*.pages.dev` 的默认域名，点击即可访问。

### 方式二：本地上传构建产物（手动）

如果你不想连接 Git，也可以在本地构建后手动上传：

```bash
# 1. 安装依赖并构建
pnpm install
pnpm run build

# 2. 构建完成后，dist 文件夹即为部署产物
```

然后进入 Cloudflare Dashboard > Pages > **"创建项目"** > **"直接上传"**，将 `dist` 文件夹拖入上传即可。

### 绑定自定义域名（可选）

1. 进入 Cloudflare Pages 项目，点击 **"自定义域"**（Custom domains）。
2. 点击 **"设置自定义域"**，输入你的域名（如 `dashboard.example.com`）。
3. 按照提示在你的域名 DNS 中添加对应的 CNAME 记录。
4. 等待证书自动签发完成，即可通过 HTTPS 访问你的域名。

### 部署说明

- 本项目使用 **hash 路由**（`createWebHashHistory`），因此不需要额外配置 SPA 路由回退规则。
- `public/_headers` 文件已预置安全响应头和静态资源缓存策略，部署后自动生效。
- 默认构建包含 **全部字体** 和 **sing-box 原生 API 支持**，如需其他构建版本可参考 `package.json` 中的 `build:*` 脚本自行修改构建命令。

## Tips

1. The connection table can be dragged with the left mouse button, and right-clicking can copy cell content.
2. Right-clicking on a node / node group card will perform a speedtest for the node / node group.
3. The proxy group sorting is based on the node order in the GLOBAL group. In Mihomo, it follows the configuration file order, while in sing-box, route.final is placed first, with the rest following the configuration file order. If you need custom ordering, you can specify the order by overriding the GLOBAL group.
4. The dashboard supports PWA (Progressive Web App), which can provide a native app-like experience on mobile devices through "Add to Home Screen".
5. The dashboard's upgrade button and auto-upgrade functionality require proper configuration of the core's UI download path ([mihomo](https://wiki.metacubex.one/config/general/#_9) | [sing-box](https://sing-box.sagernet.org/configuration/experimental/clash-api/#external_ui_download_url)), otherwise clicking update may result in updating to the core's default panel.

## 提示

1. 连接表格可被鼠标左键拖动，右键可复制单元格内容。
2. 右键点击节点/节点组卡片可对节点/节点组进行测速。
3. 面板的节点组排序是根据GLOBAL组中的节点顺序排序的，在Mihomo中会是按配置文件的顺序，在sing-box中会把route.final放到第一位，其余按照配置文件顺序，如果你需要自定义顺序，可通过覆盖GLOBAL组指定顺序
4. 面板支持PWA（Progressive Web App），可以在移动设备上通过"添加到主屏幕"获得类原生app的体验
5. 面板的更新按钮和自动更新功能需要正确的配置核心的ui下载路径 ([mihomo](https://wiki.metacubex.one/config/general/#_9) | [sing-box](https://sing-box.sagernet.org/configuration/experimental/clash-api/#external_ui_download_url)), 否则可能会在点击更新后更新为核心默认面板

## URL params format

#### basic example

http://host:port/#/setup?hostname=ipordomain&port=9090&secret=123456

1. **`http` / `https`**
   - Determines the protocol (`http` or `https`).
   - Default: current page protocol

2. **`hostname`**
   - The Clash API's IP or domain.

3. **`port`**
   - The Clash API port.

4. **`secondaryPath`**
   - Optional path appended to the base URL.
   - Default: An empty string.

5. **`secret`**
   - Password for authentication.

6. **`disableUpgradeCore`**
   - Set '1' to hide upgrade core button

7. **`disableTunMode`**
   - Set '1' to hide tun switch

### I code just for fun, not for money. If you really want to donate, please consider donating to [UNICEF](https://www.unicef.org/) to help hungry children.
