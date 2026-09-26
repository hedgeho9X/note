# 网站部署

本仓库的 `gh-pages` 分支保存 MkDocs 构建后的静态文件，不包含 Markdown 源文档和 `mkdocs.yml`。当前内容为默认欢迎页。

## Dokploy

- 项目：Note；应用：Note Website。
- GitHub 来源：`hedgeho9X/note`，分支 `gh-pages`，推送触发自动部署。
- 构建类型：Static；构建路径：`/`；发布目录：`.`；不启用 SPA 回退。
- 容器端口：80；应用域名：`jiarui.ink`；路径：`/`。
- 当前服务器由 Caddy 接收公网 HTTPS，再转发到 Dokploy Traefik 的 HTTP 入口 8080。应用内域名保持 HTTP，由 Caddy 管理公网证书和续期。
- DNS 根域名指向承载网站的服务器；不要更改 Murmur 子域名记录。

## 内容更新与验收

从 MkDocs 源项目重新生成页面时，将 `site_url` 设置为 `https://jiarui.ink/`，避免 canonical、站点地图和错误页资源仍指向旧的 `/notes/` 路径。

推送后检查 Dokploy 部署成功，并验证首页、CSS、JavaScript、搜索索引和 HTTPS 证书。原有 GitHub Pages workflow 和 CNAME 保留，独立于 Dokploy 的域名路由。
