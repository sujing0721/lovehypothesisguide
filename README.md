# Love Hypothesis Guide — 部署与变现手册

电影 2026-09-23 上线 Prime Video,本站吃这波搜索流量、Google AdSense 变现。
纯静态站,**零构建**,直接把整个文件夹当网站根目录部署即可。

## 页面清单

| 文件 | 作用 |
|---|---|
| `index.html` | 主指南页(全部 schema + trailer 嵌入 + 3 个广告位) |
| `where-to-watch.html` | 长尾:哪里能看 / Netflix 问题 / 费用 |
| `book-vs-movie.html` | 长尾:书影对比(**核心壁垒页,需后续人工扩充**) |
| `reading-order.html` | 长尾:阅读顺序 + 代餐书单 |
| `about/privacy/contact.html` | AdSense 审核必需的三个法务页 |
| `robots.txt` / `sitemap.xml` / `ads.txt` | 收录与广告配置 |

## 上线步骤(按顺序)

### 1. 买域名
候选(品牌化优先,方便复用到整个 Hazelwood 改编宇宙):
`hazelwoodhype.com` / `lovehypothesisguide.com` / `tlhguide.com`

> ⚠️ 全站用占位域名 `lovehypothesisguide.example.com`,拿到真域名后**全局搜索替换**(canonical、og、sitemap、robots、contact 邮箱)。

### 2. 部署(Cloudflare Pages,免费 + 自动 HTTPS)
```
dash.cloudflare.com → Workers & Pages → Create → Pages → Direct Upload
把本文件夹拖上去 → 绑定域名
```
Netlify / Vercel 同理。**不要用 GitHub Pages**,Cloudflare 全球更快。

### 3. 提交收录(决定这波流量的生死,今天就做)
- Google Search Console:验证域名 → 提交 `sitemap.xml` → 主 4 页用 URL Inspection 逐个「请求编入索引」
- Bing Webmaster Tools:提交 sitemap(Bing 审核快,AdSense 部分流量来自这里)
- 手动访问一遍每个页面,让 Google 爬虫撞见真实访问

### 4. 接 AdSense
1. [adsense.google.com](https://adsense.google.com) 申请 → 站点放入已验证的域名
2. 审核看:原创内容量 ✅ / 导航结构 ✅ / 法务三页 ✅ / **无版权图** ✅(全站没用房图剧照,只用 youtube-nocookie 嵌入)
3. 通过后:
   - `ads.txt` 里替换 `pub-XXXXXXXXXXXXXXXX` 为你的发布商 ID(AdSense > 设置 > 帐户信息)
   - 每个 HTML `<head>` 注释处粘 loader:
     ```html
     <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-你的ID" crossorigin="anonymous"></script>
     ```
   - 把 `<div class="ad-slot">…</div>` 整行替换为真实广告单元(自适应展示广告):
     ```html
     <ins class="adsbygoogle" style="display:block"
          data-ad-client="ca-pub-你的ID" data-ad-slot="单元ID"
          data-ad-format="auto" data-full-width-responsive="true"></ins>
     <script>(adsbygoogle = window.adsbygoogle || []).push({});</script>
     ```

### 5. 本周必做的内容更新(流量天花板取决于此)
- [ ] **看完电影**(1h52m),把 `book-vs-movie.html` 的对比表做成逐场级——这是全网都没做透的独家页面,是你真正的 SEO 壁垒(文件里有 TODO 标记)
- [ ] 核实 post-credits 问题,更新 FAQ 的 `Last checked` 日期
- [ ] 用你现有的 AI 生图管线做 6–10 张 Pinterest pin(书影差异对比图、阅读顺序图),**pin 里只放文字 + 自创插画,绝不用剧照**

## 收入预期(现实版)
- 美国/英国流量 AdSense 小说/影视类 RPM 大约 $3–10
- 峰值窗口是上映后 2–4 周,长尾(`book vs movie`、`reading order`)能续 6–12 个月
- 下一波:`Problematic Summer Romance` 若被 Amazon 预订,同站直接发新页,老域名权重复用

## 风险与红线
1. **版权**:不下载、不截图、不转存任何官方物料;文字是原创评述,嵌入是官方渠道 —— 这是 fan site 的安全线
2. **AI 内容判罚**:Google 打击规模化 AI 垃圾站。已写的两页(index、book-vs-movie)掺了真实观点和人工待办;继续加页时保持"有判断、有比较、有更新记录",别批量灌水
3. **不要**刷量、不要买流量、不要往 Reddit 硬广(会被 ban 且伤品牌)
