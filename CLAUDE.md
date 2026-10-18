# 本仓自治规则（内容层：自停 · 自愈 · 英文泄漏自查）

TOPICS.md 是本仓选题的**唯一真相源**。以下三条每次运行都适用；trigger 的启用/停用由外部 `verify-routine-caps` 守卫按 N_pub vs N_top 统一管，**你不要去改 trigger**。

## 1. 自停（写完 TOPICS 就不再生成）
运行开头先算：
- `N_pub` = 已发布页最高编号：`ls *-day*.html`（或本仓命名 week/issue/book/topic）去 `.en.html`、去前导零取最大。
- `N_top` = TOPICS.md 最大编号：`grep '^[-*#]* *(Day|Week|Issue|Book|Topic) *[0-9]+'` 取最大。

**若 N_pub ≥ N_top（TOPICS 已全部写完）**：本次**不生成任何页面、不修改 TOPICS.md、绝不自己发明新主题**；直接结束（至多发一条『本站已写完 TOPICS 路线图，补充新主题后自动续写』的通知，且仅在你判断这是刚写完的当次时发，不要每次都发）。**这条优先级高于本仓 routine prompt 里任何"超表就自造新主题"的旧措辞。** 新主题只由 BigCat 手动或 deep-research 反哺加进 TOPICS.md；加了之后守卫会自动重开、routine 自然续写。

## 2. 自愈（保持 TOPICS ⊇ 已发布）
**只在越界时动手**：若本期 Day/编号按 TOPICS 计划写、TOPICS 里本就有这行 → 不动。只有当你发布的编号是 **TOPICS.md 里没有的**（用户手动指定主题、或 deep-research 反哺内容，当时漏记进 TOPICS）时：
1. 用本期页面标题/副标题，在 TOPICS.md **末尾 append** 一行 `- Day N: <主题> — <要点>`（前缀 Day/Week/Issue/Book/Topic 随本仓约定，先 `grep` 看已有行照抄）。
2. 与本期内容改动**一并 commit / push 到 main**。
3. **只 append，绝不修改已有行。** 否则越界页占了 `dayN`、TOPICS 缺行，日后往 TOPICS 补的 Day N 新主题会撞车永远写不出。

## 3. 英文页中文泄漏自查
生成 `*.en.html` 后、publish 前，对它 grep 这些指纹（命中=模板槽把中文漏进了英文页）：
`class="en">[一-鿿]` / `class="name-en">[一-鿿]` / `class="name-zh">[一-鿿]` / `class="cn">[一-鿿]` / `Reflections — [一-鿿]` / `class="lang-tag">ZH`
命中就修掉（删中文节点或译成英文）再 publish。**正常情况不算泄漏**：经文/古典原典+英译、孙子兵法原文+英译、term(中文) 括注、代码/分词演示、语言切换标签『中文』、主题本身是中文的页。

## 新页面必带共享脚本（免触发 inject-comments 机器人提交）

生成任何 `*.html`（含 `.en.html`）时，在 `</body>` 前直接写入这 4 行，勿遗漏：

```html
<script src="https://hub.cissychen.com/comments.js" defer></script>
<script src="https://hub.cissychen.com/search.js" defer></script>
<script src="https://hub.cissychen.com/index-button.js" defer></script>
<script src="https://hub.cissychen.com/i18n-tts.js" defer></script>
```

这样 CI 的 inject-comments 不会再对新页面追加自动提交。

## 配色：深色由 CI 兜底，不用你操心

本仓是睡前读物，全站深色。**生成页面时照常写你觉得合适的浅色配色**——
push 之后 `darken.py` 会把内联 `<style>`、`style=""` 和内联 SVG 的 `fill=`/`stroke=`
一起按亮度推到深色，幂等，已经转过的页面会跳过。

不要为了"配合深色"自己手写死一套黑：那会让每篇文章长得一模一样。
darken.py 保留色相和彩度，原设计的性格还在，只换明暗。

**别在 `<style>` 顶部手写 `/* bigcat-dark v1 */`。** 那是"已转换"的标记，
写上去这一页就永远跳过转换、永远停在浅色。

`darken.py` 顶部的 `TINT_HUE` 是**本站的身份色相**（本仓 248°，靛蓝）。
四个睡前读物仓的原始底色都是近白的米色，几乎不带彩度，照原色相推暗会全部
收敛成同一种暖黑、四个站长得一模一样；所以「接近中性」的面改用这个色相
重新上色，真正有颜色的元素保持自己的颜色。改它等于改本站的整体调性，
不要顺手动。

## 文末两节：越界 + 十条要点（2026-10-17 起）

本仓的页面结构（4 张思想家卡片 → 「合奏」综合卡片 → 「深入思考」折叠问答）由 routine prompt 规定；**2026-10-17 起**在其中插入两节，routine prompt 若没写，以本节为准。位置：**「合奏」卡片之后、「深入思考」之前**，先越界、后十条要点。中英两页都写（英文页用英文写，标题见下）。

1. **越界 · 跨学科的联想**（`.crossx`，2026-10-17 起，**必写，3–5 条**）：本期某位思想家的某个想法，和另一个领域的什么东西是**同一个结构**——像在哪、不像在哪。每条约 60–90 字（一两句），只有展开的那 1 条可到约 120 字。往读者的深度兴趣上挂：意识、佛学、量子力学、神经科学、心理学、生物进化、复杂性科学、分布式系统；旁支领导力、投资、商业。**别挂回哲学本身**（东西方哲学互相对照是卡片正文的活）。具体研究、人物、年份必须真实准确，拿不准就换一条。**每张卡片里已有「跨学科联系」小节：文末越界框是全期收拢的 3–5 条，不与卡片内的跨学科联系重复**（换一个联想，或把卡片里只点到的一条换角度写透，不要复述）。思想家原典自己点名的东西进卡片正文；我们联想到的才进越界。
   ```html
   <div class="crossx">
     <div class="label">越界 · 跨学科的联想</div>
     <ul>
       <li><b>神经科学 · 预测编码</b>：……像在……；不像在……</li>
       <!-- 3–5 条 -->
     </ul>
   </div>
   ```
   英文页标题 `Crossovers`。

2. **十条要点**（`.takeaways`，2026-10-17 起，**必写，正好 10 条**）：读者拿它直接记笔记。每条一句完整的话，约 20–45 字，**单独抄出去也能看懂**（写出概念名，不用「这一观点」「他」这类靠上下文的代词）。**人名不必每条都当主语开头：全组里每位思想家的名字出现一两次、合计不超过四五次就够，其余各条直接写观点、论证或事实**（写「最深的支配是让被支配者觉得本该如此」，不写「马克思认为……」）。覆盖四张卡片和合奏卡片里最值得记的命题，可含越界里的一两条；顺序跟正文走。**只总结正文已经写过的东西**，不加新信息，不放引语。
   ```html
   <div class="tk">
     <div class="label">十条要点</div>
     <ol class="takeaways">
       <li>……</li>
       <!-- 正好 10 条 -->
     </ol>
   </div>
   ```
   英文页标题 `Ten takeaways`。

**CSS**（2026-10-17 起，追加到每篇新页 `<style>` 末尾、`@media` 之前；照常写浅色，深色由 darken.py 兜底。越界用东方金、要点用西方薰衣草，跟卡片的两种传统色一致）：
```css
.crossx{border:1px solid rgba(201,178,122,.45);border-radius:12px;padding:16px 24px 6px;margin:36px 0 22px;background:rgba(201,178,122,.07)}
.crossx .label,.tk .label{font-size:0.95rem;font-weight:700;letter-spacing:1.5px;margin-bottom:4px}
.crossx .label{color:#8b7355}
.crossx ul{list-style:none;margin:0;padding:0}
.crossx li{margin:12px 0;font-size:0.93rem;color:#4a4a4a;line-height:1.8}
.crossx b{color:#8b7355}
.tk{margin:28px 0 36px}
.tk .label{color:#a29bfe;margin-bottom:12px}
.takeaways{counter-reset:tk;list-style:none;margin:0;padding:0;border:1px solid rgba(162,155,254,.35);border-radius:12px;background:rgba(162,155,254,.05)}
.takeaways li{counter-increment:tk;position:relative;margin:0;padding:11px 18px 11px 52px;border-top:1px solid rgba(162,155,254,.18);font-size:0.93rem;line-height:1.75;color:#2d3436}
.takeaways li:first-child{border-top:none}
.takeaways li::before{content:counter(tk,decimal-leading-zero);position:absolute;left:18px;top:12px;font-family:"SF Mono",Menlo,monospace;font-size:0.78rem;color:#a29bfe}
```

**篇幅**（2026-10-17 起）：越界约 400 字、十条要点约 350 字。`.maxchars` 为这两节从 3000 上调到 3750；其余各节照旧，别借新额度把卡片写长。

**publish.sh 闸门**（2026-10-17 起，只查从未提交过的新页，中英都查）：`<ol class="takeaways">` 正好 10 个 `<li>`；`<div class="crossx">` 3–5 个 `<li>`。
