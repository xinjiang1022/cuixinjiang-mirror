# www.cuixinjiang.cn 海外静态镜像（GitHub Pages）

## 用途

frpee 内网穿透服务商只服务中国大陆——海外 DNS 解析被污染为 127.0.0.1、海外 TLS 连接被 RST，导致 Bing（美国）无法抓取 EdgeOne 回源后的真实站点（海外节点 525）。

本仓库是网站的全量静态快照，部署到 GitHub Pages 后供 Bing / 海外搜索引擎抓取收录。**国内用户访问不变，仍走 EdgeOne 真站。**

## 结构

```
/
├── index.html              # 首页快照
├── sitemap.xml             # 318 个有效 URL（已剔除 4 个无效页）
├── robots.txt              # 允许抓取 + Sitemap 声明
├── CNAME                   # www.cuixinjiang.cn（GitHub Pages 自定义域）
├── .nojekyll               # 禁止 Jekyll 处理（保留下划线目录）
├── archives/<slug>/        # 文章页（170 篇）
├── tags/<slug>/            # 标签页（133 个）
├── categories/<slug>/      # 分类页（5 个）
└── about/                  # 关于页
```

每页保存为 `<路径>/index.html`，URL 无后缀即可命中。

## 数据

- 快照时间：2026-09-09
- 页面数：318（sitemap 322 个 URL 中 4 个已确认 404 的无效页被剔除）
- 总大小：约 47 MB

## 更新方法

重新下载全站快照：

```powershell
# 1. 更新 sitemap.xml（从 https://www.cuixinjiang.cn/sitemap.xml 下载）
# 2. 用 download_chunk.ps1 分块下载：
powershell -ExecutionPolicy Bypass -File download_chunk.ps1 -Start 0 -Count 40
# 依次跑 -Start 40/80/120/160/200/240/280 直到覆盖全部 URL
# 3. 重新提交推送：
git add -A && git commit -m "update snapshot" && git push
```

## 后续

- [ ] 推送 GitHub 并启用 Pages
- [ ] DNS 海外线路 CNAME → <user>.github.io
- [ ] Bing Webmaster 重新提交 sitemap
- [ ] （可选）GitHub Actions 定时自动更新快照
