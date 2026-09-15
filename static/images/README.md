# 文章配图放这里（PNG/SVG/JPG），本文档说明引用约定

## 正文内联图：写站点根路径 `/images/xxx.png`

```markdown
![alt 文本](/images/xxx.png)
```

部署后由渲染钩子 `layouts/_default/_markup/render-image.html` 自动补上 baseURL 的路径前缀：

| 正文里写 | 渲染结果（baseURL = `…/blog-release/`） |
|---------|--------------------------------------|
| `/images/x.png` | `/blog-release/images/x.png` ✅ |
| `images/x.png` | `/blog-release/images/x.png` ✅ |
| `https://…` / `//…` / `data:` | 原样保留 ✅ |
| `/blog-release/images/x.png` | `/blog-release/blog-release/images/x.png` ❌ 双重前缀 |

**不要写 `/blog-release/images/...`**——站点部署在项目子路径下，仓库名前缀由
`hugo.toml` 的 `baseURL` 统一提供，正文里写死会变成双重前缀。换域名时也只改 `baseURL`。

## 为什么需要那个钩子（别删）

Hugo 的 `relURL` 对**带前导斜杠**的输入**不会**补 baseURL 的路径（0.135 实测：
`relURL "/images/x.png"` → `/images/x.png`，`relURL "images/x.png"` → `/blog-release/images/x.png`）。
所以正文写 `/images/…` 必须在渲染钩子里先去掉前导 `/` 再 `relURL`；钩子被删掉后，
正文内联图会解析到 `https://<user>.github.io/images/…` → 404。

## 其他约定

- 文件名用小写英文短横线，例如 `kanban-swarm-cover.png`；单图建议 < 2 MB。
- frontmatter 封面写同样形式：`cover: "/images/xxx.png"`（模板走同一个 `imgurl.html` 解析）。
- 图片是页面资源（page bundle）时另说——本项目未使用 page bundle，正文图一律放 `static/images/`。
