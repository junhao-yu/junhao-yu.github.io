# junhao-yu.github.io

这是一个纯静态的 GitHub Pages 个人主页，无需安装 Node.js 或运行构建命令。网站入口是 `index.html`，样式集中在 `style.css`。

网站地址：<https://junhao-yu.github.io/>

## 文件说明

| 文件或目录 | 用途 |
| --- | --- |
| `index.html` | 页面文字、链接、论文、项目和视频的内容 |
| `style.css` | 页面颜色、字体、布局和移动端适配 |
| `assets/` | 建议新建，用于存放头像、PDF、视频封面等静态资源 |

## 修改个人资料

打开 `index.html`，搜索以下占位文字并替换：

| 内容 | 搜索文字 | 修改示例 |
| --- | --- | --- |
| 姓名 | `Junhao Yu` | 改为你的中英文姓名 |
| 头像字母 | `JY` | 或替换为真实头像，见下方说明 |
| 身份 | `Researcher & Builder` | 如 `Ph.D. Student` |
| 学校/单位 | `在此填写你的学校、公司或实验室` | 如 `浙江大学 · 计算机学院` |
| 邮箱 | `your-email@example.com` | 改为你的公开联系邮箱 |
| GitHub | `https://github.com/junhao-yu` | 改为你的 GitHub 主页 |
| 个人简介 | `我专注于探索…` | 写教育背景、研究兴趣与求职/合作方向 |

例如，将邮箱链接改为：

```html
<a href="mailto:your-name@example.com">Email</a>
```

将 `your-name@example.com` 替换成真实邮箱即可。不要把 GitHub Token、密码、身份证号等敏感信息放进网页或仓库。

## 添加头像

1. 在项目根目录新建 `assets` 文件夹，再将头像命名为 `avatar.jpg` 并放入其中。
2. 在 `index.html` 中找到：

```html
<div class="portrait" aria-label="Junhao Yu 头像占位"><span>JY</span></div>
```

3. 替换成：

```html
<div class="portrait photo">
  <img src="assets/avatar.jpg" alt="Junhao Yu 的头像" />
</div>
```

4. 在 `style.css` 最末尾添加：

```css
.portrait.photo { overflow: hidden; background: transparent; }
.portrait.photo img { width: 100%; height: 100%; object-fit: cover; }
```

建议使用正方形 JPG、PNG 或 WebP 图片，尺寸至少 `400 × 400` 像素。

## 修改动态、论文和项目

### 新增动态

在 `id="news"` 区域的 `<ol class="news-list">` 内复制一行：

```html
<li><time>2026.09</time><p>这里填写动态内容，例如论文被某会议接收。</p></li>
```

最新内容放在最上方。

### 新增论文

在 `id="publications"` 区域复制一个 `<article class="publication">...</article>`，再修改标题、作者、会议、摘要和链接。链接需将 `href="#"` 换成真实网址，例如：

```html
<div class="pub-links">
  <a href="assets/paper.pdf" target="_blank" rel="noreferrer">Paper</a>
  <a href="https://github.com/junhao-yu/project" target="_blank" rel="noreferrer">Code</a>
</div>
```

PDF 可放在 `assets/` 目录中。若论文较大，建议使用 Google Drive、arXiv 或机构页面链接，避免仓库变得过大。

### 修改项目卡片

在 `id="projects"` 区域修改每个项目中的 `<h4>`、`<p>` 和 `<a href="…">`。复制一个 `<article class="project-card">...</article>` 可增加新项目。

## 插入视频

视频有两种推荐方式：使用第三方平台嵌入，或将较小的 MP4 文件直接放在仓库。

### 方式一：嵌入 YouTube 或 Bilibili（推荐）

优点是网页加载快、不占 GitHub 仓库空间。将下列代码放到项目说明、论文或项目卡片后面。

YouTube 示例：

```html
<div class="video-wrap">
  <iframe
    src="https://www.youtube-nocookie.com/embed/视频ID"
    title="项目演示视频"
    loading="lazy"
    allowfullscreen>
  </iframe>
</div>
```

将 URL 末尾的 `视频ID` 替换为 YouTube 分享链接中 `v=` 后的内容。

Bilibili 示例：

```html
<div class="video-wrap">
  <iframe
    src="https://player.bilibili.com/player.html?bvid=BVxxxxxxxxxx&autoplay=0"
    title="项目演示视频"
    loading="lazy"
    allowfullscreen>
  </iframe>
</div>
```

将 `BVxxxxxxxxxx` 改为视频的 BV 号。请使用你有权公开嵌入的视频。

为使视频宽度自动适配手机与电脑，在 `style.css` 末尾添加：

```css
.video-wrap { position: relative; width: 100%; aspect-ratio: 16 / 9; margin: 20px 0; overflow: hidden; background: #16211e; }
.video-wrap iframe, .video-wrap video { width: 100%; height: 100%; border: 0; }
```

### 方式二：上传本地 MP4

1. 新建 `assets/videos/`，将视频放入此目录，例如 `assets/videos/demo.mp4`。
2. 在希望展示视频的位置加入：

```html
<div class="video-wrap">
  <video controls preload="metadata" poster="assets/demo-cover.jpg">
    <source src="assets/videos/demo.mp4" type="video/mp4" />
    你的浏览器不支持 HTML5 视频播放。
  </video>
</div>
```

`poster` 是可选封面图。推荐 MP4（H.264 编码）、16:9 比例、文件尽量小于 25 MB。GitHub Pages 不适合托管大视频；大于约 50 MB 或需要流畅播放的视频，应上传 YouTube、Bilibili、Cloudflare R2、对象存储等平台后使用方式一嵌入。

## 本地预览

在本目录运行：

```bash
python3 -m http.server 8000
```

然后打开 <http://localhost:8000>。完成后在终端按 `Ctrl+C` 停止服务。

## 发布更新

每次修改后，在项目目录执行：

```bash
git add index.html style.css assets
git commit -m "Update homepage content"
git push
```

GitHub Pages 通常会在一两分钟内更新。部署状态可在 GitHub 仓库的 **Actions** 或 **Settings → Pages** 查看。

## 常见问题

**更新后网页没有变化**：等待一两分钟，再使用浏览器强制刷新（Windows/Linux：`Ctrl+Shift+R`；macOS：`Cmd+Shift+R`）。

**图片或视频无法显示**：确认文件已执行 `git add` 并推送；路径大小写必须与文件名完全一致。网页路径使用 `/`，不要使用 Windows 的 `\\`。

**网站打不开**：检查仓库名是否为 `junhao-yu.github.io`，并在 **Settings → Pages** 确认来源为 `main` 分支与 `/(root)` 目录。
