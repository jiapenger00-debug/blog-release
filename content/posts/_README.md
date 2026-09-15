文章正文放这里，文件名建议用小写英文短横线，例如 `hermes-kanban-swarm.md`。

frontmatter 必填：`title` / `date` / `tags` / `author`；可选 `cover`。

- `cover` 形如 `/images/xxx.png`（站点根路径，模板自动加 baseURL 前缀，**不要**写 `/blog-release/images/...`）。
- 正文内联图同样用 `/images/xxx.png`，由 `layouts/_default/_markup/render-image.html` 补前缀。
  详见 `static/images/README.md`。
