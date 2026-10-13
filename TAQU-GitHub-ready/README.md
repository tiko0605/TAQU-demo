# 它趣 TAQU

它趣（TAQU）是一个面向城市养宠人群的纯前端产品 Demo。当前版本以成都宠物友好生活为内容场景，展示地点探索、社区互动、流浪动物救助和商户合作等产品流程。

本项目没有后端、用户账号或远程数据库。交互数据为代码内置模拟数据；用户在 Demo 中产生的状态保存在当前浏览器和当前站点来源的 `localStorage` 中，不会自动同步到其他设备或浏览器。

## 当前可运行版本

当前权威源文件位于 `outputs/`：

```text
outputs/
├── index.html       页面入口
├── app.js           页面模板、模拟数据、交互与状态
├── styles.css       页面样式
└── TAQU-demo.zip    上述三份文件的打包副本
```

`outputs/TAQU-demo/` 还留有一份较早的副本，其 `app.js` 和 `styles.css` 与 `outputs/` 根目录版本不同。继续开发、运行或部署时请以 `outputs/index.html`、`outputs/app.js`、`outputs/styles.css` 为准。若重新生成 ZIP，应从这三份文件打包。

## 功能概览

- 地图首页：成都模拟地点、分类筛选、中文搜索、地点预览与详情、收藏、推荐。
- 附近地点：完整地点列表、分类筛选、搜索和地点详情入口。
- 社区：宠物搭子、宠物分享、活动详情与报名等演示流程。
- 救助：领养列表和申请、流浪动物上报与进度、喂养点共建、公益积分及公益记录。
- 收藏与个人页：收藏地点、编辑个人宠物资料、积分记录。
- 商业合作：商户合作方案、申请状态、推广效果模拟。
- 地点信息反馈：政策变化或地点错误反馈、我的上报、反馈详情和模拟处理状态。

这些均为前端演示。表单不会提交到救助机构、商户或其他外部系统；Demo 中的地点、政策、活动、用户、参与人数、积分及商业效果数据不应被理解为实时或经核实信息。

## 技术栈与版本

- HTML：HTML5 静态页面。
- CSS：原生 CSS，无预处理器。
- JavaScript：原生浏览器 JavaScript，无框架或打包器。
- 外部图标：页面运行时从 `https://unpkg.com/lucide@latest` 加载 Lucide。
- 外部字体：Google Fonts 的 Noto Sans SC；无法访问时使用系统字体回退。
- 图片：代码中的 Unsplash 图片 URL；图片不在仓库本地。
- 运行环境：支持现代 JavaScript 的桌面或移动浏览器。

项目未声明最低浏览器版本。代码使用可选链、模板字符串、`FormData` 和 `localStorage` 等现代浏览器 API。项目本身没有 Node/npm 依赖；Node 不是运行此静态 Demo 的必要条件。

## 从零运行

建议使用本地 HTTP 服务，不依赖 `file://` 打开。这样可避免不同浏览器对本地文件来源、存储和资源加载策略的差异。

1. 安装 Python 3（建议 Python 3.10 或更新版本）以及现代浏览器。
2. 获取完整项目文件，并进入源文件目录：

   ```powershell
   cd path\to\project\outputs
   ```

3. 启动静态文件服务器：

   ```powershell
   py -m http.server 8000
   ```

   如果 `py` 命令不可用但 `python` 可用：

   ```powershell
   python -m http.server 8000
   ```

4. 在浏览器访问 `http://localhost:8000/`。
5. 按 `Ctrl+C` 停止服务器。

这里没有 `npm install`、构建或打包步骤。修改 `app.js` 或 `styles.css` 后，刷新浏览器即可看到变更。若要重新创建 ZIP，在项目根目录运行：

```powershell
Compress-Archive -Path outputs\index.html,outputs\app.js,outputs\styles.css -DestinationPath outputs\TAQU-demo.zip -CompressionLevel Optimal -Force
```

## 检查

当前没有自动化测试框架或测试用例。可进行的基础检查：

```powershell
node --check outputs\app.js
```

该命令只检查 JavaScript 语法，不验证页面布局或交互流程。手动验收至少应检查：

- 地图搜索中文输入、筛选和地点详情跳转。
- 地图空白处关闭地点预览。
- “附近地点”列表、筛选、搜索、返回和详情跳转。
- 收藏、宠物资料编辑、领养申请、喂养点参与、上报及其状态反馈。
- 社区内容、活动报名和商户合作流程。
- 地点反馈详情及反馈状态更新。
- 桌面和窄屏布局；以及外部字体、图标和图片不可访问时的表现。

## 数据、隐私与备份

- 地点、领养动物、活动、政策样例和商户方案等静态演示数据位于 `outputs/app.js`。
- 用户操作状态由 `outputs/app.js` 写入浏览器 `localStorage`，键名为 `taqu-state` 和 `taqu-favorites`。
- 该存储属于单一浏览器配置和站点来源。换设备、浏览器、浏览器配置或来源域名后不会自动迁移。
- 项目没有实现数据导出/导入功能。若需保留某台浏览器的 Demo 状态，应先在原浏览器开发者工具中检查并自行安全导出这两个键，再在新环境恢复；其中可能含用户填写的个人或联系信息，应作为敏感数据妥善处理，不要提交到 Git 或发给他人。
- 静态代码仓库不包含访问者浏览器里的 `localStorage` 数据。

## 外部资源与离线限制

页面依赖外部 CDN 和图片来源：

- `unpkg.com` 上的 `lucide@latest` 图标脚本。
- `fonts.googleapis.com` / `fonts.gstatic.com` 字体。
- `images.unsplash.com` 图片。

这些资源目前没有锁定版本或本地备份。网络、服务可用性、CSP 或资源 URL 变化可能导致图标、字体或图片缺失。核心页面代码是本地文件，但不能保证完全离线时视觉资源齐全。

## Git 与个人账号迁移

开始使用 Git 前，先确认你有权将这份代码放入自己的个人仓库，并检查静态演示资料是否适合公开。尤其是宠物昵称、样例账号文案，以及任何后来填入浏览器的联系信息。不要把浏览器存储导出文件、令牌、密码或公司资料加入仓库。

在确认后，可从项目根目录初始化本地仓库：

```powershell
git init
git add .gitignore .env.example README.md HANDOFF.md DEPLOYMENT.md outputs
git status
git diff --cached --stat
git commit -m "Prepare TAQU demo for personal development"
```

先仔细检查 `git status` 和暂存区，再提交。创建个人 GitHub 私有仓库后，将下面占位地址替换成你自己的仓库 SSH 或 HTTPS 地址：

```powershell
git branch -M main
git remote add origin <YOUR_PERSONAL_GITHUB_REPOSITORY_URL>
git push -u origin main
```

不要将占位符原样执行。若项目或素材属于雇主、合作方或受协议限制，请先取得明确授权；本项目文档不能证明代码权属或迁移权限。

## 继续开发

新开发环境先阅读：

1. `README.md`：运行方式和项目边界。
2. `HANDOFF.md`：当前文件版本、已知问题和交接重点。
3. `DEPLOYMENT.md`：个人账号下发布静态站点的选择与限制。

源文件在 `outputs/`，当前架构是单页静态 HTML + 原生 JS 渲染，不要把旧的 `outputs/TAQU-demo/` 副本误当作最新版本。
