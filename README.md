# File Hosting

<p align="center">
  <img alt="HTML" src="https://img.shields.io/badge/html-single%20page-e34f26">
  <img alt="JavaScript" src="https://img.shields.io/badge/javascript-vanilla-yellow">
  <img alt="Vercel" src="https://img.shields.io/badge/deploy-vercel-black">
</p>

File Hosting 是一个用于分享文件下载的静态单页网站，所有页面、样式和脚本都写在 `index.html` 中，文件放在 `files/` 目录，并通过 `vercel.json` 配置部署到 Vercel。项目目前实现了文件列表展示、搜索、排序、列表/网格视图切换、文件详情、复制下载链接，以及基于浏览器 `localStorage` 的下载次数统计。

## 功能特性

- **文件列表**：在 `index.html` 的配置区域中声明文件，页面通过 `HEAD` 请求获取文件大小。
- **类型识别**：按扩展名识别图片、视频、音频、文档、压缩包、代码等类型并显示对应图标。
- **搜索与排序**：按文件名搜索，支持按名称、大小、下载量、日期排序。
- **视图切换**：支持列表视图和网格视图。
- **下载**：点击文件图标、文件名或下载按钮直接下载；`vercel.json` 为 `/files/*` 添加 `Content-Disposition: attachment` 响应头。
- **文件详情与复制链接**：弹窗查看文件详情，并可复制 `/files/<文件名>` 下载链接。
- **下载统计**：在浏览器 `localStorage` 中记录每个文件的下载次数和每日下载量，展示文件总数、总下载次数、热门文件和今日下载。

## 项目结构

```text
.
├── index.html      # 单页应用：页面、样式、脚本和文件配置
├── files/          # 可供下载的文件
│   └── Test_Photo.png
└── vercel.json     # Vercel 响应头配置
```

## 快速开始

### 环境要求

- 现代浏览器
- 本地预览时需要任意静态文件服务器（直接以 `file://` 打开时无法获取文件大小）

### 添加文件

1. 把文件放到 `files/` 目录。
2. 在 `index.html` 的「配置区域」中添加一项：

```js
const files = [
  { name: "Test_Photo.png", size: null, date: new Date().toISOString() },
  // { name: "你的文件名.zip", size: null, date: new Date().toISOString() },
]
```

### 本地预览

在仓库根目录启动任意静态文件服务器，例如：

```bash
python -m http.server 8000
```

然后打开 http://localhost:8000 。

### 部署

将仓库导入 Vercel 即可作为静态站点部署，`vercel.json` 中的响应头配置会自动生效。

## 当前状态

项目已完成文件展示、搜索、排序和下载等基础功能。下载次数保存在访问者自己的浏览器中，并不是全站统计。后续可继续完善：

- 使用服务端或存储服务记录真实的全站下载次数
- 自动生成文件列表，避免手动维护 `index.html` 中的配置
- 为每个文件记录真实的上传日期（目前日期为页面加载时间）
