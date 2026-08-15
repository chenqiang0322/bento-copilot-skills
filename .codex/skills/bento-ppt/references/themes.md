# 主题色预设(Themes · v2)

5 套主题,4 套**精校自真实站点的 design tokens**(数据来源:[VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md) · 命令 `npx getdesign@latest add <site>`),1 套自创(Vision Aurora)。

完整原始 DESIGN.md 在 `references/design-md/{apple,vercel,claude}/DESIGN.md`,可作进一步定制时的参考。

**不允许用户自定义颜色** — 色彩搭配错了画面瞬间垮,5 套预设保护美学下限。

---

## 使用方法

1. 基于内容主题推荐一套,或直接问用户选哪一套
2. 打开 `assets/template.html` 的 `<style>` 块,找到开头 `:root{` 块
3. **整体替换**标有"主题"注释的 `--bg-base` / `--card` / `--text` / `--accent-*` / `--gtext-*` 这一组变量
4. 字体配套(部分主题需要):见每套主题下"配套字体"小节
5. 其他 CSS 都走 `var(--...)`,无需任何其他改动

---

## 1. 🌑 Apple Dark(默认 · 精校 v2)

**数据来源**:apple.com homepage / iPhone 17 Pro buy page / accessories — 真实 design tokens。
**适合**:科技产品发布、企业 keynote、追求"premium without gradients"的内敛风。
**调性**:近黑 tile + 系统灰阶白 + Sky Link 蓝。**Apple 官方零渐变 token**,所有视觉冲击靠 photography + 留白。

```css
:root{
  --bg-base:#000000;       /* Pure Black · 全局 nav / video 背景 */
  --bg-elev:#1d1d1f;       /* Near-Black Ink · 段落背景 */
  --card:#272729;          /* Tile 1 · homepage 主 dark 卡 */
  --card-elev:#2a2a2c;     /* Tile 2 · 微亮一档,创造分隔 */
  --card-border:rgba(255,255,255,0.08);
  --card-glow:rgba(255,255,255,0.04);
  --text:#ffffff;          /* On Dark */
  --text-2:#cccccc;        /* Body Muted · 暗底次要文字 */
  --text-3:rgba(255,255,255,0.45);

  --accent-1:#2997ff;      /* Sky Link Blue · 暗底专用更亮蓝 */
  --accent-2:#bf5af2;
  --accent-3:#ff453a;
  --accent-4:#30d158;

  --gtext-aurora:linear-gradient(135deg,#2997ff 0%,#bf5af2 50%,#ff453a 100%);
  --gtext-sky:linear-gradient(135deg,#2997ff 0%,#0071e3 100%);
  --gtext-flame:linear-gradient(135deg,#ff9f0a 0%,#ff453a 100%);
  --gtext-mint:linear-gradient(135deg,#30d158 0%,#2997ff 100%);
}
```

**配套字体**:Inter(Google Fonts · 已默认加载)是 SF Pro 的最佳开源替代。Apple DESIGN.md 明确推荐:`system-ui, -apple-system, BlinkMacSystemFont` 第一回退,Inter weight 600 + `font-feature-settings:"ss03"` 模拟 SF Pro 圆"a"。

**默认 slide 主题标记**:`<section class="slide" data-theme="dark">`

---

## 2. ☀️ Apple Light(精校 v2)

**数据来源**:apple.com light 模式 + Parchment 体系。
**适合**:消费品发布、product page 风、需要"reading not scanning"节奏。
**调性**:Parchment 米白 + Pure White 卡 + Action Blue 单一品牌色。

```css
:root{
  --bg-base:#f5f5f7;       /* Parchment · Apple 标志性 off-white */
  --bg-elev:#ffffff;       /* Pure White · 卡片底 */
  --card:#ffffff;
  --card-elev:#fafafc;     /* Pearl Button · 二级 ghost 表面 */
  --card-border:#e0e0e0;   /* Hairline · 1px 描边色 */
  --card-glow:rgba(0,0,0,0.02);
  --text:#1d1d1f;          /* Near-Black Ink · 不用纯黑保持 photographic */
  --text-2:#333333;        /* Ink Muted 80 */
  --text-3:#7a7a7a;        /* Ink Muted 48 · 禁用文字 / fine-print */

  --accent-1:#0066cc;      /* Action Blue · Apple 唯一品牌交互色 */
  --accent-2:#5e5ce6;
  --accent-3:#ff3b30;
  --accent-4:#34c759;

  --gtext-aurora:linear-gradient(135deg,#0066cc 0%,#5e5ce6 50%,#ff3b30 100%);
  --gtext-sky:linear-gradient(135deg,#0071e3 0%,#0066cc 100%);
  --gtext-flame:linear-gradient(135deg,#ff9500 0%,#ff3b30 100%);
  --gtext-mint:linear-gradient(135deg,#34c759 0%,#0066cc 100%);
}
```

**配套字体**:同 Apple Dark · Inter。
**默认 slide 主题标记**:`<section class="slide" data-theme="light">`

**Apple 设计原则借鉴**:
- 标题 letter-spacing 用 `-0.012em` 至 `-0.025em`(Apple tight)
- body 文字尺寸建议 17px 而非 16px(Apple 标志性"reading"节奏)
- weight 阶梯只用 300 / 400 / 600 / 700(故意跳过 500)

---

## 3. 🌌 Vision Aurora(自创 · 不变)

**适合**:Vision Pro 类沉浸式发布、AI 大模型发布、未来感强的 demo。
**调性**:深空蓝主底 + 紫粉 mesh + 高玻璃感卡片。

```css
:root{
  --bg-base:#05071a;
  --bg-elev:#0a0e2a;
  --card:#101535;
  --card-elev:#161c42;
  --card-border:rgba(180,160,255,0.12);
  --card-glow:rgba(180,160,255,0.08);
  --text:#f0eeff;
  --text-2:rgba(240,238,255,0.72);
  --text-3:rgba(240,238,255,0.45);

  --accent-1:#7b9eff;
  --accent-2:#c084fc;
  --accent-3:#f472b6;
  --accent-4:#22d3ee;

  --gtext-aurora:linear-gradient(135deg,#22d3ee 0%,#7b9eff 35%,#c084fc 70%,#f472b6 100%);
  --gtext-sky:linear-gradient(135deg,#22d3ee 0%,#7b9eff 100%);
  --gtext-flame:linear-gradient(135deg,#f472b6 0%,#c084fc 100%);
  --gtext-mint:linear-gradient(135deg,#22d3ee 0%,#7b9eff 100%);
}
```

**配套字体**:同默认 Inter + Manrope。
**默认 slide 主题标记**:`<section class="slide" data-theme="dark">`

---

## 4. ⬛ Vercel Geist(原 Vercel Mono · 精校 v2)

**数据来源**:vercel.com / Geist Design System — 真实 hex。
**适合**:开发者工具发布、SaaS 路演、Linear / Vercel / Resend 风格。
**调性**:Vercel Black(#171717,**不是纯黑**)+ Geist 字体 + 极紧 tracking。Workflow 三色:Ship Red / Preview Pink / Develop Blue。

```css
:root{
  --bg-base:#000000;
  --bg-elev:#0a0a0a;
  --card:#0a0a0a;
  --card-elev:#171717;     /* Vercel Black · 略带暖灰 */
  --card-border:rgba(255,255,255,0.1);
  --card-glow:rgba(255,255,255,0.02);
  --text:#ededed;          /* 不用纯白,稍微灰一档 */
  --text-2:#a1a1a1;        /* Gray 600 */
  --text-3:#666666;        /* Gray 500 */

  /* Vercel 三套官方 accent:Workflow / Console / Link */
  --accent-1:#0070f3;      /* Console Blue · 主交互 */
  --accent-2:#7928ca;      /* Console Purple */
  --accent-3:#de1d8d;      /* Preview Pink */
  --accent-4:#ff5b4f;      /* Ship Red */

  --gtext-aurora:linear-gradient(135deg,#0070f3 0%,#7928ca 50%,#de1d8d 100%);
  --gtext-sky:linear-gradient(135deg,#0070f3 0%,#0072f5 100%);
  --gtext-flame:linear-gradient(135deg,#ff5b4f 0%,#de1d8d 100%);
  --gtext-mint:linear-gradient(135deg,#0072f5 0%,#7928ca 100%);
}
```

**配套字体**:**Geist + Geist Mono**(Vercel 官方字体,Google Fonts 已收录)。建议在 template.html 的字体 link 加上:

```html
<link href="https://fonts.googleapis.com/css2?family=Geist:wght@300..900&family=Geist+Mono:wght@300..900&display=swap" rel="stylesheet">
```

然后在 `:root` 里覆写字体变量:
```css
--sans-en:"Geist",-apple-system,system-ui,sans-serif;
--display-en:"Geist","Inter",system-ui,sans-serif;
--mono:"Geist Mono","SF Mono",ui-monospace,monospace;
```

**Vercel 设计原则借鉴**:
- 标题 letter-spacing **极度收紧**(`-2.4px` 至 `-2.88px` on display sizes,这是所有主流设计系统里最激进的负 tracking)
- 字重只用 400 / 500 / 600(700 仅用于 micro badge),靠尺寸拉层级
- 渐变克制 — Vercel 几乎不用 gradient text,bento gradient 用作偶尔点缀即可

**默认 slide 主题标记**:`<section class="slide" data-theme="dark">`

**配套微调**:本主题下 `.bg-blob` 建议关闭(Vercel 风不需要色彩漂浮):
```css
.bg-blob{display:none}
```

---

## 5. 🌿 Claude Warm(原 OpenAI Warm 替换 · 精校 v2)

**数据来源**:claude.ai / anthropic.com — 真实 brand tokens。
**适合**:AI 工具发布(尤其 Claude / Anthropic 类)、研究内容、需要"editorial 温暖"感的 deck。
**调性**:Canvas 米白 + Coral 主色 + Teal 副色。**衬线标题(serif headlines)**是 Claude editorial DNA。

```css
:root{
  --bg-base:#faf9f5;       /* Canvas · 米白(暖) */
  --bg-elev:#ffffff;
  --card:#efe9de;          /* Surface Card · 米色卡 */
  --card-elev:#f5f0e8;     /* Surface Soft */
  --card-border:#e6dfd8;   /* Hairline */
  --card-glow:rgba(40,30,20,0.02);
  --text:#141413;          /* Ink · 暖深灰,不用纯黑 */
  --text-2:#3d3d3a;        /* Body */
  --text-3:#6c6a64;        /* Muted */

  --accent-1:#cc785c;      /* Coral · Anthropic 标志 */
  --accent-2:#5db8a6;      /* Accent Teal */
  --accent-3:#e8a55a;      /* Accent Amber */
  --accent-4:#5db872;      /* Success Green */

  --gtext-aurora:linear-gradient(135deg,#cc785c 0%,#e8a55a 50%,#5db8a6 100%);
  --gtext-sky:linear-gradient(135deg,#5db8a6 0%,#5db872 100%);
  --gtext-flame:linear-gradient(135deg,#e8a55a 0%,#cc785c 100%);
  --gtext-mint:linear-gradient(135deg,#5db8a6 0%,#5db872 100%);
}
```

**配套字体**(关键 · 这是 Claude 风的 editorial 灵魂):

```html
<!-- 在 template.html 字体 link 加上 EB Garamond 作为 Copernicus / Tiempos Headline 的开源替代 -->
<link href="https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
```

```css
/* 在 :root 里加:用 EB Garamond 替代 Manrope 做 display(标题) */
--display-en:"EB Garamond","Cormorant Garamond","Tiempos Headline",Georgia,serif;
/* sans 仍是 Inter(StyreneB 的最佳替代) */
--sans-en:"Inter",-apple-system,system-ui,sans-serif;
```

**Claude 设计原则借鉴**:
- **display 永远用 weight 400(常规)**,绝不加粗 — 衬线本身的字形就有重量
- letter-spacing `-0.5px` 至 `-1.5px`(Copernicus 没有负 tracking 就不像 Anthropic)
- body 用 humanist sans(Inter 是最佳开源替代,绝不用 Helvetica / Arial — 太中性会失去 warm-editorial 感)

**默认 slide 主题标记**:`<section class="slide" data-theme="light">`

---

## 推荐选择参考

| 如果是... | 推荐主题 |
|---|---|
| 不知道选啥 / 第一次用 / 通用科技 | 🌑 Apple Dark |
| 消费品 / 浅色官网风 / 需要"reading"节奏 | ☀️ Apple Light |
| AI 大模型 / 沉浸感 / 未来风 | 🌌 Vision Aurora |
| 开发者工具 / SaaS / Vercel 系科技克制 | ⬛ Vercel Geist |
| AI 工具(尤其 Anthropic / 研究内容) | 🌿 Claude Warm |

---

## 主题切换硬规则

- ✅ **一份 deck 只用一套主题**,不要中途换色
- ✅ **`data-theme` 与主题搭配**:Apple Dark / Vision Aurora / Vercel Geist = `data-theme="dark"`;Apple Light / Claude Warm = `data-theme="light"`
- ❌ **禁止混搭**(例如 bg 取 Apple Dark,accent 取 Claude Warm)— 会彻底违和
- ❌ **禁止用户给任意 hex 值** — 委婉拒绝并展示 5 套让选
- ❌ **不要直接修改 template.html 其他地方的颜色** — 所有散落颜色都走 var(),改 :root 一处即可

---

## 出处文档

每套主题的完整原始 DESIGN.md(包含组件样式、阴影系统、do's and don'ts 等深度细节)在:

```
references/design-md/
├── apple/DESIGN.md       (37KB · Apple HIG-inspired,562 行)
├── vercel/DESIGN.md      (19KB · Geist Design System,310 行)
└── claude/DESIGN.md      (33KB · Anthropic brand,589 行)
```

如需做 deck 时调整某个细节(如:Apple 的阴影系统 / Vercel 的 micro-badge 字体 / Claude 的 surface 命名约定),可直接 Read 对应 DESIGN.md 找精确数据。

来源:[VoltAgent/awesome-design-md](https://github.com/VoltAgent/awesome-design-md)(MIT)· 命令 `npx getdesign@latest add <site>` 自取。

---

## 主题节奏(本 skill 特殊规则)

guizang 强制 light/dark 交替,但**本 skill 不要求**。Bento PPT(Apple keynote / Vercel launch)通常**全程统一一种主题**,靠卡片密度交替制造节奏:

- ✅ 推荐:整个 deck 用同一个 `data-theme`,卡片密度交替(单卡 hero ↔ 4-7 卡稠密)
- ⚠️ 可选:个别 hero 页用相反主题(如全 dark deck 中插入 1 页 light 大引用),但全 deck 不超过 2 页

详细密度节奏规则见 `layouts.md`。
