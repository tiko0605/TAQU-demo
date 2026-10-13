# TAQU 上传 GitHub 指南

这份项目是原生 HTML/CSS/JavaScript 静态 Demo，不需要 `npm install`、数据库或后端服务。上传前请先确认你有权将项目代码、文案和图片链接放到个人 GitHub 仓库。建议第一次使用个人账号时创建 Private 仓库。

## 方法一：用 GitHub 网页上传

1. 登录个人 GitHub，点击右上角 `+` → `New repository`。
2. 填写仓库名，例如 `taqu-demo`，可见性先选择 `Private`，不要勾选自动创建 README。
3. 进入新仓库，点击 `Add file` → `Upload files`。
4. 解压本项目压缩包，把压缩包内的文件和文件夹拖入上传区域。需要保留根目录的 `README.md`、`outputs` 文件夹和其他迁移文档。
5. 在页面底部填写提交说明，例如 `Add TAQU product demo`，点击 `Commit changes`。

网页上传适合第一次上传少量文件。以后修改文件时，建议使用下面的 Git 命令，能够保留提交记录并更容易回滚。

## 方法二：用 Git 命令上传

先安装 Git，然后在解压后的项目根目录打开 PowerShell：

```powershell
cd "C:\path\to\TAQU-GitHub-ready\TAQU-GitHub-ready"
git init
git add .
git status
git commit -m "Add TAQU product demo"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_NAME/YOUR_REPOSITORY_NAME.git
git push -u origin main
```

请把 `YOUR_GITHUB_NAME` 和 `YOUR_REPOSITORY_NAME` 换成你自己的值，再执行最后两行。第一次推送时 GitHub 可能要求浏览器登录或使用 Personal Access Token；Token 只用于登录，不要写入任何项目文件。

如果远程地址已经存在，使用：

```powershell
git remote -v
git remote set-url origin https://github.com/YOUR_GITHUB_NAME/YOUR_REPOSITORY_NAME.git
git push -u origin main
```

以后更新项目：

```powershell
git add .
git commit -m "Update TAQU demo"
git push
```

## 上传后如何运行

GitHub 仓库中的当前网页入口位于 `outputs/index.html`。本地运行时进入 `outputs` 文件夹：

```powershell
cd .\outputs
py -m http.server 8000
```

然后访问 `http://localhost:8000/`。

GitHub 的仓库文件预览页不能代替网页服务器。若要公开访问 Demo，请按 `DEPLOYMENT.md` 配置 GitHub Pages 或其他静态托管平台，并将发布目录设为 `outputs`。

## 上传前检查

- 不要上传 `.env`、浏览器 localStorage 导出文件、密码、Token 或真实用户数据。
- 不要把 `outputs/TAQU-demo/` 旧副本复制回当前版本；继续开发请使用 `outputs/index.html`、`outputs/app.js`、`outputs/styles.css`。
- 检查图片、字体和图标的使用许可。当前 Demo 运行时会请求 Unsplash、Google Fonts 和 unpkg CDN。
- 如果代码、文案或素材来自公司、合作方或第三方，公开或迁移前先确认授权。
