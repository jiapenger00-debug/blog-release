# blog-release

Personal blog: GitHub Pages + Hugo static site. Posts in content/posts/ as Markdown (frontmatter: title/date/tags/author). PR flow -> auto deploy on merge to main.

站点部署在项目子路径 `https://jiapenger00-debug.github.io/blog-release/`（由 `hugo.toml` 的 `baseURL` 决定）。

## 图片引用约定

正文内联图与 frontmatter `cover` 都写**站点根路径**，不要带仓库名前缀：

```markdown
![alt](/images/xxx.png)
```

前缀由 `layouts/partials/imgurl.html` + `layouts/_default/_markup/render-image.html` 统一补齐。
改域名/子路径只改 `hugo.toml` 的 `baseURL`。细节与踩坑说明见 `static/images/README.md`。
