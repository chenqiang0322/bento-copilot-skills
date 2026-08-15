# 组件手册(Components)

bento-ppt-skill 的所有组件都已在 `assets/template.html` 的 `<style>` 块预定义。本文档是查询手册 — **不要发明新类名**,所有自定义用 inline `style` 实现。

---

## 1. 字体系统(Type)

四种字体,每种角色明确:

| 变量 | 字体 | 用途 |
|---|---|---|
| `--display-en` | Manrope / Inter | 大数字、英文大标题(`.h-hero` / `.hero-num` / `.stat-num`) |
| `--sans-en` | Inter / SF Pro | 英文正文、副标 |
| `--sans-zh` | Noto Sans SC / 苹方 | **所有中文文字**(标题 + 正文) |
| `--mono` | JetBrains Mono | 元数据、kicker、sticker、caption、foot |

**硬规则**:
- 中文统一用 `var(--sans-zh)`,**不用衬线**(这是和 guizang 最大的区别)
- 大数字必须用 `var(--display-en)` + `font-feature-settings:"tnum"`(等宽数字)
- mono 字体只用于"元数据感"位置(角标、tag、底部说明),不要用在正文

### 标题层级

| 类 | 字号 | 用途 |
|---|---|---|
| `.h-hero` | 9.2vw | 英文 / 数字大标题(单卡 hero 页) |
| `.h-hero-zh` | 8vw | 中文大标题(单卡 hero 页) |
| `.h-xl` | 5vw | 章节标题 / banner 标题 |
| `.h-lg` | 3.2vw | 大卡内主标题 |
| `.h-md` | 2.1vw | 中卡内主标题 |
| `.h-sm` | 1.4vw | 小卡内主标题 |

### 正文层级

| 类 | 字号 | 用途 |
|---|---|---|
| `.lead` | 1.5vw | 卡内引语 / 副标 |
| `.body` | max(13px, 1.05vw) | 正文段落 |
| `.caption` | max(10px, .78vw) | 角标 / 小标签 / 底部说明 |
| `.kicker` | max(11px, .78vw) | 卡顶引导句(kicker = 大标题前的小帽子) |
| `.meta-row` | max(11px, .85vw) | 元数据行(横排,逗号分隔) |

---

## 2. 主题色系(Color)

5 套主题,见 `themes.md`。所有颜色通过 CSS 变量驱动:

| 变量 | 用途 |
|---|---|
| `--bg-base` | 页面主底 |
| `--card` / `--card-elev` | 普通卡 / 浮起卡 |
| `--card-border` | 卡边框 |
| `--text` / `--text-2` / `--text-3` | 主文 / 副文 / 三级文(opacity 1.0 / 0.7 / 0.45) |
| `--accent-1/2/3/4` | 4 个 accent 色,用于 sticker / dot / gradient |
| `--gtext-aurora/sky/flame/mint` | 4 套 gradient text 预设 |

**永远走变量**,不要写死 hex(除了警示性文字如 `style="color:var(--accent-3)"` 标红负值)。

---

## 3. Bento Grid System

### `.bento` 容器

```html
<div class="bento">
  <!-- 卡片们 -->
</div>
```

- 12 列 × 8 行内部网格
- gap = `max(20px, 1.6vw)`(响应式留白)
- `flex:1` 占满 slide 剩余高度

### `.b-card` 卡片

```html
<div class="b-card b-6x4">...</div>
```

- 默认背景 `var(--card)`,圆角 24px,内边距 `max(28px, 2.2vw)`
- 必须配尺寸快捷类(`.b-12x8` / `.b-6x4` / `.b-4x5` ...)或 inline `style="grid-column:span N;grid-row:span M"`

### 卡片变体

| 变体类 | 视觉 | 用途 |
|---|---|---|
| (default) | 实底色 + 细边 | 普通信息卡 |
| `.b-card.glass` | 半透 + backdrop-blur | 让背景渐变透出,适合 hero 页 |
| `.b-card.elev` | 浮起阴影 | 强调单一卡的层级 |
| `.b-card.grad` | 卡内带微弱径向渐变 | KPI / 重点数据卡 |
| `.b-card.img` | 内部图片占满 + 文字浮在底 | 产品图卡 |

**组合规则**:variant 类只能选一个,不要同时 `.glass.grad`(冲突)。

### 网格快捷类完整列表

```
.b-12x8 .b-12x5 .b-12x4 .b-12x3 .b-12x2
.b-8x8 .b-8x5 .b-8x4 .b-8x3
.b-6x8 .b-6x5 .b-6x4 .b-6x3
.b-4x8 .b-4x5 .b-4x4 .b-4x3 .b-4x2
.b-3x8 .b-3x4 .b-3x3 .b-3x2
```

不在列表里的尺寸用 inline:`style="grid-column:span 5;grid-row:span 4"`。

---

## 4. 卡内组件

### Card Header(`.c-head`)

```html
<div class="c-head">
  <div class="c-kick">SECTION · KICKER</div>
  <div class="c-title">卡内主标题</div>
</div>
```

- `.c-kick`:mono 小角标
- `.c-title`:衬线... 不,sans-serif 的 1.7vw 标题

### Card Footer(`.c-foot`)

```html
<div class="c-foot">FOOTER · DATE / NOTE</div>
```

- 自动 `margin-top:auto` 贴卡底
- mono 字体,小,uppercase

### Sticker(标签)

```html
<div class="sticker">PLAIN</div>
<div class="sticker accent">ACCENT BLUE</div>
<div class="sticker mint">MINT GREEN</div>
<div class="sticker flame">FLAME ORANGE</div>
```

- 圆角胶囊型,放在卡顶或卡内某处
- 4 种颜色变体对应 4 个 accent

### Hero Number(超大数字)

```html
<div class="hero-num">
  30.3<span class="hu">亿元</span>
</div>
<!-- 加渐变文字 -->
<div class="hero-num gtext gtext-sky">
  30.3<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">亿元</span>
</div>
```

- 字号 8vw(默认),`tnum` 等宽数字
- `.hu` 是单位(中文),自动小一号
- 配 gradient 时,**单位要单独 inline 取消渐变**(否则单位也会染色,丑)

### Stat Number(中等数字,适合密集卡)

```html
<div class="stat-num">981</div>
```

- 字号 5.2vw
- 比 hero-num 小,适合 `.b-3x2` / `.b-4x3` 等小卡

### KPI Row(指标行列表)

```html
<div class="kpi-row">
  <div class="kpi-l">毛利率</div>
  <div class="kpi-v">33.5%</div>
</div>
<div class="kpi-row">
  <div class="kpi-l">净利率</div>
  <div class="kpi-v">3.39%</div>
</div>
```

- 一行 = 标签 + 数字,左右两端对齐
- 自动加顶部细线分隔(第一行除外)
- 数字用 mono 等宽

### Feature List(特性列表 · 圆点 + 文本)

```html
<ul class="feat-list">
  <li class="feat-item"><span class="dot"></span><span class="ft">无限次调用</span></li>
  <li class="feat-item"><span class="dot"></span><span class="ft">最新模型 + 优先队列</span></li>
</ul>
```

- 圆点用 `var(--accent-1)`,跟随主题
- 适合 3-5 项的特性列表

### Icon Row(图标 + 文字)

```html
<div class="icon-row">
  <svg viewBox="0 0 24 24"><path d="M5 12l5 5L20 7"/></svg>
  <span>已支持 19 个 AI Provider</span>
</div>
```

- 也可以配 Lucide:`<i data-lucide="check"></i>`(需 `lucide.createIcons()` 后才显示)

---

## 5. 图片处理

### 占满整张卡(`.b-card.img`)

```html
<div class="b-card img b-6x8">
  <img class="img-fill" src="images/airpods.jpg" alt="AirPods">
  <div class="img-overlay">
    <div class="sticker accent">FLAGSHIP</div>
    <h2 class="h-lg">AirPods Pro 3</h2>
  </div>
</div>
```

- 图自动 `object-fit:cover`,文字浮在卡底带渐变遮罩

### 卡内图(`<figure class="frame-img">`)

```html
<div class="b-card b-6x8">
  <div class="c-head">
    <div class="c-title">产品截图</div>
  </div>
  <p class="body">说明文字</p>
  <figure class="frame-img" style="margin-top:auto">
    <img src="images/screenshot.png" alt="">
  </figure>
</div>
```

- 占满卡内剩余空间,圆角 14px
- `margin-top:auto` 贴底

### 占位框(`.img-slot`)

图片还没准备好时:

```html
<figure class="img-slot">+ IMAGE PLACEHOLDER</figure>
```

虚线框,提示设计师位置。

---

## 5.5 表格组件(`.bt`)· 商业用途

`.bt` = bento-table,**用原生 `<table>` 标签**,只需加 `class="bt"` 即可继承 bento 风。

```html
<div class="b-card b-12x5">
  <table class="bt">
    <thead>
      <tr>
        <th>指标</th>
        <th class="num">2024</th>
        <th class="num hl">2025</th>
        <th class="num">YoY</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>营业收入(亿元)</td>
        <td class="num">29.58</td>
        <td class="num hl">30.30</td>
        <td class="num pos">+2.4%</td>
      </tr>
      <tr>
        <td>归母净利润(亿元)</td>
        <td class="num">1.56</td>
        <td class="num hl">1.05</td>
        <td class="num neg">-32.8%</td>
      </tr>
    </tbody>
  </table>
</div>
```

### 单元格修饰类

| 类 | 效果 |
|---|---|
| `<td class="num">` | 等宽数字 + 右对齐 + Manrope 字体 |
| `<td class="hl">` | 高亮列(背景填 accent-1 半透 + 字色 accent-1) |
| `<td class="pos">` | 正向数据(绿) |
| `<td class="neg">` | 负向数据(粉红) |
| `<td class="muted">` | 弱化(text-3) |
| `<td class="center">` | 居中 |
| `<th class="num">` | 表头数字列(右对齐) |
| `<th class="hl">` | 表头高亮列(accent-1 + 加粗下划线) |

第一列(标签列)**自动**用 sans-zh 字体 + 稍粗 + 主文色,不需手动加类。

### 硬约束

- ≤ 8 行 × 6 列
- **每页 ≤ 1 张表格**(2 张 = 退化为传统 PPT 表格页,丢掉 bento 美学)
- 表格永远在 `.b-card` 里,不要直接放在 `.bento` 网格上
- 表格卡推荐用 `.b-12x5` 或 `.b-12x6`(全宽),配顶 banner + 底 insight(见 layouts.md L9)

适合场景:财务三年对比 / 竞品功能矩阵 / 价格套餐表 / SLA 对比 / 任何"行 × 列"的对比信息。

---

## 5.6 TOC 章节目录(`.toc-item`)· 列表式

`.toc-item` 是 L10A TOC 列表式专用组件,放在 `.b-12x1` 全宽窄卡里:

```html
<div class="b-card b-12x1">
  <div class="toc-item">
    <div class="toc-num">02</div>
    <div class="toc-body">
      <div class="toc-name">行业与市场</div>
      <div class="toc-desc">全球规模 · 渗透率反差 · 增长驱动力</div>
    </div>
    <div class="toc-pages">P 06-09</div>
  </div>
</div>
```

### 章节状态

| 类 | 视觉 |
|---|---|
| `.toc-item`(默认) | 未讲,平淡(白文 + text-2 副文) |
| `.toc-item.active` | 当前章节,数字用 aurora 渐变,页码染 accent-1 色;通常配 `.b-card.grad` 增强背景 |
| `.toc-item.done` | 已讲过,opacity 0.45 弱化 |

### 内部结构

| 子元素 | 作用 |
|---|---|
| `.toc-num` | 大编号(3.2vw)· `01` / `02` / `03` |
| `.toc-body` | 中部内容(章节名 + 描述,弹性占满) |
| `.toc-name` | 章节名(1.5vw 加粗) |
| `.toc-desc` | 章节描述(.9vw,1 行最佳,**不要塞段落**) |
| `.toc-pages` | 右侧页码 sticker(mono 小字) |

### 网格规划速查

| 章节数 | 推荐布局 |
|---|---|
| 3 章 | banner `b-12x2` + 3×`b-4x6`(L10B 网格式) |
| 4 章 | banner `b-12x2` + 4×`b-6x3`(L10B 网格式) |
| 5 章 | banner `b-12x2` + 5×`b-12x1`(L10A 列表式) |
| 6 章 | banner `b-12x2` + 6×`b-4x3`(L10B 网格式) |
| 7+ 章 | 拆 deck 或不做 TOC |

详见 layouts.md L10。

---

## 6. 渐变文字(Gradient Text)

```html
<span class="gtext">默认 aurora 渐变</span>
<span class="gtext gtext-sky">蓝</span>
<span class="gtext gtext-flame">橙红</span>
<span class="gtext gtext-mint">翠</span>
<span class="gtext gtext-aurora">蓝紫粉</span>
```

**使用规则**:
- ✅ 只在大字号上用(`.h-hero` / `.h-xl` / `.hero-num`)
- ✅ 只 gradient 1-3 个关键词,不要整段都 gradient
- ❌ 正文 / 小字不要用 — 看不清且没意义
- ❌ 一页不要超过 2 处 gradient text — 视觉太花

---

## 7. Chrome / Foot(页眉页脚元数据)

```html
<section class="slide">
  <div class="chrome">
    <div>左上 · 栏目标签</div>
    <div>右上 · 页号</div>
  </div>
  <div class="bento">...</div>
  <div class="foot">
    <div>左下 · 页面说明</div>
    <div>右下 · 标记</div>
  </div>
</section>
```

- mono 字体,小,uppercase
- 与 kicker 内容**不要重复**(chrome 是栏目级,kicker 是页面级)

---

## 8. 动效系统(Motion)

详见 `layouts.md` 的 E 节。重点:

- 默认 `cascade`(卡片逐个淡入)
- hero 页用 `data-animate="hero"`(更慢、更仪式感)
- 大引用页用 `data-animate="quote"`,逐行揭示
- 对比页用 `data-animate="directional"`,左右进
- pipeline 页(本 skill 较少)用 `data-animate="pipeline"`

每个需要入场动画的元素加 `data-anim`(可加值 `left`/`right`/`line`/`step`)。

加载失败兜底:Motion One 本地 + CDN 都挂时,所有 `[data-anim]` 强制可见,内容永远可读。

---

## 9. 不要做的事

- ❌ 用 emoji 替代 sticker / icon — 用 sticker + 文字 / Lucide
- ❌ 整段文本加 gradient — 只 1-3 个关键词
- ❌ 卡片 padding 小于 24px(已 CSS 强制)
- ❌ 卡间 gap 小于 20px(已 CSS 强制)
- ❌ 在卡里放原图 `aspect-ratio` 写死的图(用 `.frame-img` 占剩余空间或 `.b-card.img` 占满)
- ❌ 用衬线字体写中文(整套 sans 系)
- ❌ 一页超过 7 卡(密度过高,本 skill 上限 7)
- ❌ 一份 deck 中混用两套主题色(只能选一套)
