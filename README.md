# cuixinjiang.cn 海外静态镜像

本仓库是 www.cuixinjiang.cn 的**海外静态镜像**，用于解决 Bing/海外搜索引擎无法访问主站（内网穿透 + 国内 CDN 架构，海外不可达）的问题。

## 工作原理

- 主站 www.cuixinjiang.cn 走 EdgeOne CDN + frpc 内网穿透，海外无法访问
- DNS 分线路：海外线路 CNAME 指向本 GitHub Pages 镜像
- Bing 抓取 www.cuixinjiang.cn → 海外 DNS 解析到本镜像 → 抓取 sitemap.xml 和页面静态快照 → 收录

## 目录结构

- `sitemap.xml` — 主站 sitemap 副本（Bing 提交用）
- `robots.txt` — 允许全站抓取，声明 Sitemap
- `index.html` — 首页静态快照
- `archives/<文章>/index.html` — 文章页静态快照

## 更新方法

主站发布新文章后，需要同步本镜像：

1. 重新下载 https://www.cuixinjiang.cn/sitemap.xml 覆盖本文件
2. 新文章路径创建 `archives/<文章名>/index.html`（保存网页源码）
3. 提交推送，GitHub Pages 自动生效

## 注意

- 本仓库只做静态内容镜像，交互功能（评论、搜索、后台）不生效
- 国内用户访问不受影响（走 EdgeOne 默认线路）