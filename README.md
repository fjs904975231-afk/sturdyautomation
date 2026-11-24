# Sturdy Automation 官网（sturdyautomation.com）

一个纯静态、全英文的单页官网，不需要任何后台或数据库，可直接放 GitHub Pages 免费托管。

## 目录结构

```
index.html      # 整个网站（首页 / 关于我们 / 产品 / 行业 / 品牌 / 联系我们）
assets/         # 图片（必须和 index.html 放在同一层）
README.md       # 本说明文件
```

## 本地预览

双击 `index.html` 用浏览器打开即可，不需要装服务器。只要 `assets` 文件夹和它在一起，图片就能正常显示。

## 上传到 GitHub Pages（免费，约 5 分钟）

1. 登录 GitHub，右上角 **+ → New repository**，名字随意（例如 `sturdy-site`），可见性选 **Public**，创建。
2. 进入仓库，点 **Add file → Upload files**，把 `index.html` 和整个 `assets` 文件夹一起拖进去（保持 `assets` 在根目录，不要嵌套一层文件夹），提交。
3. 仓库 **Settings → Pages**，Source 选 **Deploy from a branch**，Branch 选 **main**、目录选 **/(root)**，Save。
4. 等 1–2 分钟，访问 `https://你的用户名.github.io/sturdy-site/`，网站就上线了。
5. 绑定域名 `sturdyautomation.com`：**Settings → Pages → Custom domain** 填 `sturdyautomation.com` 保存（会自动生成 CNAME 文件）。再到域名商处加 DNS：
   - `A` 记录 `@` → `185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`
   - `CNAME` 记录 `www` → `你的用户名.github.io`
   - 证书签发后（一般几分钟到几小时），在 Pages 页面勾选 **Enforce HTTPS**。
6. 用 `https://sturdyautomation.com` 访问即完成。国内访问 GitHub Pages 偶尔不稳，如需更稳可换 Cloudflare Pages（上传方式相同）。

## 以后怎么改内容

- **产品类别 / 行业 / 品牌**：`index.html` 最下方 `<script>` 里有三组数据，直接改文字就行：
  - `PRODUCTS`：8 个产品分类（标题、简介、标签、明细列表、配图）
  - `INDUSTRIES`：行业列表
  - `DEFAULT_BRANDS`：品牌名称
- **联系方式**：全局搜索并替换 `Josh@sturdyautomation.com`、`8618670106660`（WhatsApp 链接里没有 + 号）、`live:.cid.48ad120e68d127c0`。顶栏、联系我们页、页脚、表单发送逻辑都有。
- **统计数字**（10,000+ / 30+ / 24h / 15+）：首页 “Why Choose Us” 区块，按实际情况改。
- **地址、营业时间**：搜索 `Shenzhen`、`GMT+8`。

## 品牌滚动 LOGO（已接入 34 个）

- 34 个 LOGO 已统一处理：自动裁掉白边、等比缩放到 **240×80 透明画布**（视觉大小对齐），存放在 `assets/brands/`，文件名就是品牌英文小写（如 `siemens.png`）。
- 首页和 Brands 页的横向滚动条已经直接显示这些真实 LOGO，数量由脚本自动统计。
- **替换某个 LOGO**：用同名文件覆盖 `assets/brands/` 里的图片即可，建议透明底 PNG、比例接近 3:1、内容尽量撑满画布。
- **新增加品牌**：把图片放进 `assets/brands/`，在 `index.html` 里 `DEFAULT_BRANDS` 数组加一行：
  `{ name:'Brand Name', img:'assets/brands/brand-name.png' }`
- **临时预览**：页面上的 **Upload brand logos / Add manage brand logos** 可以直接选图看效果（仅当前浏览器有效），并给出可直接粘贴的代码。
- **改回纯文字版**：把数组条目换成 `{ name:'SIEMENS' }`（不带 img），滚动条就显示文字标识。

## 关于询价与表单

- 所有产品卡片、按钮的「Request a Quote / 询价」都会跳到 `#/contact` 联系我们页面，并自动把对应产品填进「Product interest」和留言框。
- **客户提交表单会直接发邮件到 `Josh@sturdyautomation.com`**：用的是免费服务 FormSubmit（`https://formsubmit.co`），不需要任何后台或服务器，提交后邮件以表格形式发到邮箱，客户填的邮箱会作为「回复地址」，你直接点回复即可。
- **需要你做一次激活**：网站上第一次有人提交后，`Josh@sturdyautomation.com` 会收到一封 FormSubmit 的确认邮件（标题类似 *Activate Form*），**点一下里面的 Activate 链接**，之后就永久自动发送。这次我已经帮你触发过一次，请到邮箱里找这封信点激活。
- 注意：直接双击本地 `index.html`（file:// 方式）时 FormSubmit 会拒绝，页面会自动改成「用邮件发送」的备选方式；**部署到 GitHub Pages / 正式域名后才会真正自动发邮件**。
- 表单下方还有 **Send via WhatsApp** 按钮，内容会一并带到 WhatsApp 对话里。
- 想换成别的表单服务（Formspree、Web3Forms、企业邮件网关），只改 `index.html` 里的 `FORM_ENDPOINT` 常量和 `quoteForm` 的提交逻辑即可。

## 需要你确认或替换的地方

- `assets/` 里的图片目前是 AI 生成的示意图，**建议换成真实的产品照片或工厂/仓库实拍**（同名替换即可，建议宽度 ≤1200px 的 JPG，整站控制在 2MB 内）。
  - `hero.jpg` 首页大图、`about.jpg` 关于我们、`control.jpg` 控制室配图
  - `plc / vfd / flow / gas / ipc / hvac / servo / comm` 八个产品分类图
- 品牌名称仅用于说明「可以帮忙寻货的范围」，若要展示品牌官方 LOGO，请先确认授权，避免侵权。
- 统计数字、地址门牌、营业时间目前都是通用写法，请按公司实际情况修改。


