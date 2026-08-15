# Bento 布局库(Layouts)

8 种 Bento Grid 布局组合,每种都是完整可粘贴的 `<section class="slide">` 代码块,直接替换文案/图片即可。

---

## ⚠️ 生成前必读(Pre-flight)

### A. 类名必须来自 template.html

layouts.md 用到的类(`bento` / `b-card` / `b-card.glass|elev|grad|img` / `b-12x8` / `b-12x3` / `b-8x8` / `b-6x8` / `b-6x4` / `b-4x8` / `b-4x5` / `b-4x4` / `b-3x8` / `b-3x4` / `c-head` / `c-kick` / `c-title` / `c-foot` / `hero-num` / `stat-num` / `hu` / `kpi-row` / `kpi-l` / `kpi-v` / `feat-list` / `feat-item` / `dot` / `ft` / `icon-row` / `sticker` / `sticker.accent|flame|mint` / `kicker` / `lead` / `body` / `caption` / `meta-row` / `h-hero` / `h-hero-zh` / `h-xl` / `h-lg` / `h-md` / `h-sm` / `gtext` / `gtext-aurora|sky|flame|mint` / `frame-img` / `img-slot` / `chrome` / `foot`)**全部在 `assets/template.html` 的 `<style>` 块中已定义**。

**不要发明新类名**。如需自定义,用 `style="..."` inline 写。生成前若不确定,grep template.html 确认。

### B. Bento Grid 网格规范

每页 `.bento` 容器是 **12 列 × 8 行** 内部网格(`grid-template-columns:repeat(12,1fr);grid-template-rows:repeat(8,1fr)`),卡片用 `grid-column:span N` + `grid-row:span M` 填充,**总和必须 = 12×8 = 96 单元**(可以有空隙,但不能超)。

提供了快捷类:
| 快捷类 | grid-column / grid-row | 等于 |
|---|---|---|
| `.b-12x8` | span 12 / span 8 | 整页 |
| `.b-12x4` `.b-12x5` `.b-12x3` | span 12 / span N | 顶/底 banner |
| `.b-8x8` `.b-8x4` | span 8 / span N | 主卡 |
| `.b-6x8` `.b-6x4` `.b-6x5` | span 6 / span N | 半宽 |
| `.b-4x8` `.b-4x5` `.b-4x4` `.b-4x3` | span 4 / span N | 三分之一 |
| `.b-3x8` `.b-3x4` | span 3 / span N | 四分之一 |

**不在快捷类里的尺寸用 inline**:`<div class="b-card" style="grid-column:span 5;grid-row:span 4">`。

### C. 卡片密度节奏(本 skill 特殊规则)

guizang 强制 dark/light 主题交替,**本 skill 改成"卡片密度交替"**,因为 Apple keynote 通常一套主题贯穿:

- ✅ **推荐**:稠密页(4-7 卡)+ hero 页(1-3 卡)交替,3-4 张稠密插入 1 张 hero 喘息
- ❌ **禁止**:连续 5 页以上无 hero(节奏太密)
- ❌ **禁止**:连续 3 页以上单卡 hero(节奏太空)
- ✅ **首页用 Layout 1 单卡 hero**,**末页用 Layout 1 / 2 收尾**

主题色统一用同一个(见 `themes.md`),不强制切换。

### D. 图片处理(简单)

bento 卡里的图片用两种方式:
1. **占满整张卡**:用 `.b-card.img` 变体,内部 `<img class="img-fill">` 自动 `object-fit:cover`,文字用 `.img-overlay` 浮在底部
2. **作为卡内的部分内容**:用 `<figure class="frame-img">` + 内部 `<img>`,自动占满剩余空间

### E. 动效系统(默认 cascade)

- 不写 `data-animate` = `cascade`(每个 `[data-anim]` 元素逐个淡入,最适合 bento 多卡片)
- 单卡 hero 页(Layout 1):`data-animate="hero"`,节奏更慢更仪式感
- 大引用页:`data-animate="quote"`,逐行揭示
- 流水线 / 分步推进:`data-animate="pipeline"`(本 skill 较少用,bento 不适合分步推进)

---

## Layout 1 · Single Focus(单卡 hero)

**用途**:开场封面 / 章节幕封 / 单一有力金句 / 收尾页
**密度**:1 卡 · hero 页

```html
<section class="slide" data-theme="dark" data-animate="hero">
  <div class="chrome">
    <div>Bento Deck · 2026</div>
    <div>VOL.01</div>
  </div>
  <div class="bento">
    <div class="b-card glass b-12x8" style="justify-content:center" data-anim>
      <div class="sticker accent" data-anim>NEW · KEYNOTE</div>
      <div style="height:3vh"></div>
      <div class="kicker" data-anim>Bento Grid PPT</div>
      <h1 class="h-hero-zh" data-anim>把 PPT,<br>排成 <span class="gtext gtext-aurora">便当</span>。</h1>
      <div style="height:3vh"></div>
      <p class="lead" style="max-width:55vw" data-anim>
        卡片为最小单元,12 × 8 网格自由组合。Apple keynote / SaaS 路演 / AI demo 通用。
      </p>
      <div style="height:3vh"></div>
      <div class="meta-row" data-anim>
        <span>SUBTITLE OR PRESENTER</span><span>·</span><span>2026.04</span>
      </div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 1 · Single Focus</div>
    <div>— · —</div>
  </div>
</section>
```

**要点**:
- 用 `.b-card.glass` 让 mesh gradient 透出
- `style="justify-content:center"` 让内容垂直居中
- gradient text 只在 1-2 个关键词上,不要整段都 gradient
- sticker 在最顶可作"标签"(NEW / DEMO / VOL.01 等)

---

## Layout 2 · 50/50 Symmetric(对称双卡)

**用途**:产品并列 / 旧 vs 新对比 / 两个核心特性
**密度**:2 卡

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>双产品对比 · Compare</div>
    <div>02 / 12</div>
  </div>
  <div class="bento">
    <div class="b-card grad b-6x8" data-anim>
      <div class="sticker accent">PRODUCT A</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-kick">DESKTOP · MAC</div>
        <div class="c-title">MacBook Pro M5</div>
      </div>
      <p class="body">14 寸 · 18 小时电池 · 神经网络引擎升级 40%。专业创作者的全速工作台。</p>
      <figure class="frame-img" style="margin-top:auto" data-anim>
        <img src="images/macbook.jpg" alt="MacBook Pro">
      </figure>
      <div class="c-foot">FROM ¥14,999</div>
    </div>
    <div class="b-card grad b-6x8" data-anim>
      <div class="sticker flame">PRODUCT B</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-kick">MOBILE · iPHONE</div>
        <div class="c-title">iPhone 17 Pro</div>
      </div>
      <p class="body">A19 仿生 · 2x 长焦 · ProRes 视频。一台口袋里的电影摄影机。</p>
      <figure class="frame-img" style="margin-top:auto" data-anim>
        <img src="images/iphone.jpg" alt="iPhone 17 Pro">
      </figure>
      <div class="c-foot">FROM ¥7,999</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 2 · 50/50 Symmetric</div>
    <div>— 02 / 12 —</div>
  </div>
</section>
```

**要点**:
- 两卡用相同变体(都 `.grad` 或都默认),保证视觉对称
- 用不同 `.sticker` 颜色(accent vs flame)制造区分
- `figure.frame-img` 配 `margin-top:auto` 让图自动贴到卡底

---

## Layout 3 · Asymmetric 8/4(主辅卡)

**用途**:1 个主内容 + 1 个数据/小图佐证
**密度**:2 卡

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>核心叙事 + 关键数字</div>
    <div>03 / 12</div>
  </div>
  <div class="bento">
    <div class="b-card glass b-8x8" data-anim>
      <div class="sticker accent">KEY MESSAGE</div>
      <div class="c-head" style="margin-top:2vh">
        <div class="c-kick">THE STORY</div>
      </div>
      <h2 class="h-xl" style="margin-top:1vh">
        AI 让一个人的<br><span class="gtext gtext-aurora">产能</span>,
        变成一个公司的体量。
      </h2>
      <p class="lead" style="margin-top:3vh; max-width:38vw">
        过去十年,SaaS 让 5 人公司拥有 50 人的销售能力。
        过去 1 年,AI 让 1 人公司拥有 10 人的开发能力。
      </p>
      <div class="c-foot">— Garry Tan, YC President · 2026</div>
    </div>
    <div class="b-card grad b-4x8" data-anim>
      <div class="sticker mint">PROOF</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">实证</div>
      </div>
      <div class="kpi-row">
        <div class="kpi-l">独立开发者</div>
        <div class="kpi-v">11<span class="hu" style="font-size:.5em;color:var(--text-2)">万行代码</span></div>
      </div>
      <div class="kpi-row">
        <div class="kpi-l">交付时间</div>
        <div class="kpi-v">64<span class="hu" style="font-size:.5em;color:var(--text-2)">天</span></div>
      </div>
      <div class="kpi-row">
        <div class="kpi-l">GitHub Stars</div>
        <div class="kpi-v">5,166</div>
      </div>
      <div class="kpi-row">
        <div class="kpi-l">下载量</div>
        <div class="kpi-v">41K+</div>
      </div>
      <div class="c-foot">CodePilot · 2026.04</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 3 · Asymmetric 8/4</div>
    <div>— 03 / 12 —</div>
  </div>
</section>
```

**要点**:
- 8 列主卡承载叙事 + 大标题,4 列辅卡承载 KPI 列表
- 主卡用 glass 让背景透出,辅卡用 grad 增加视觉重量

---

## Layout 4 · 3-Column Equal(三方案并列)

**用途**:3 个套餐 / 3 个特性 / 3 个核心理念
**密度**:3 卡

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>三套版本 · Plans</div>
    <div>04 / 12</div>
  </div>
  <div class="bento">
    <div class="b-card b-4x8" data-anim>
      <div class="sticker">FREE</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">Hobby</div>
      </div>
      <div class="hero-num" style="font-size:5vw">
        $0<span class="hu" style="font-size:.4em">/mo</span>
      </div>
      <ul class="feat-list" style="margin-top:3vh">
        <li class="feat-item"><span class="dot"></span><span class="ft">100 次 / 月</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">基础模型</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">社区支持</span></li>
      </ul>
      <div class="c-foot">START FREE</div>
    </div>
    <div class="b-card grad b-4x8" data-anim>
      <div class="sticker accent">RECOMMENDED</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">Pro</div>
      </div>
      <div class="hero-num gtext gtext-sky" style="font-size:5vw">
        $20<span class="hu" style="font-size:.4em;-webkit-text-fill-color:var(--text-2);background:none">/mo</span>
      </div>
      <ul class="feat-list" style="margin-top:3vh">
        <li class="feat-item"><span class="dot"></span><span class="ft">无限次调用</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">最新模型 + 优先队列</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">邮件支持 24h</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">API 访问</span></li>
      </ul>
      <div class="c-foot">MOST POPULAR</div>
    </div>
    <div class="b-card b-4x8" data-anim>
      <div class="sticker flame">TEAMS</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">Enterprise</div>
      </div>
      <div class="hero-num" style="font-size:5vw">
        Custom
      </div>
      <ul class="feat-list" style="margin-top:3vh">
        <li class="feat-item"><span class="dot"></span><span class="ft">SSO + SCIM</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">私有部署</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">SLA 99.9%</span></li>
        <li class="feat-item"><span class="dot"></span><span class="ft">专属客户成功经理</span></li>
      </ul>
      <div class="c-foot">CONTACT SALES</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 4 · 3-Column Equal</div>
    <div>— 04 / 12 —</div>
  </div>
</section>
```

**要点**:
- 中间卡用 `.grad` + accent sticker 强调"推荐版本"
- gradient text 只用在中间卡的价格上,凸显焦点

---

## Layout 5 · Hero + 2 Side(主次结合)

**用途**:1 个主产品 + 2 个补充信息(规格/价格/特性)
**密度**:3 卡

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>主推产品 · 关键参数</div>
    <div>05 / 12</div>
  </div>
  <div class="bento">
    <div class="b-card img b-6x8" data-anim>
      <img class="img-fill" src="images/airpods.jpg" alt="AirPods Pro 3">
      <div class="img-overlay">
        <div class="sticker accent" style="margin-bottom:1.4vh">FLAGSHIP</div>
        <h2 class="h-lg">AirPods Pro 3</h2>
        <p class="body" style="margin-top:1vh">主动降噪 + 心率监测 + 实时翻译。</p>
      </div>
    </div>
    <div class="b-card grad b-3x8" data-anim>
      <div class="sticker mint">SPECS</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">关键参数</div>
      </div>
      <div class="kpi-row"><div class="kpi-l">续航</div><div class="kpi-v">8h</div></div>
      <div class="kpi-row"><div class="kpi-l">充电盒</div><div class="kpi-v">36h</div></div>
      <div class="kpi-row"><div class="kpi-l">重量</div><div class="kpi-v">5.3g</div></div>
      <div class="kpi-row"><div class="kpi-l">芯片</div><div class="kpi-v">H3</div></div>
    </div>
    <div class="b-card b-3x8" data-anim>
      <div class="sticker flame">PRICE</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">价格 · 上市</div>
      </div>
      <div class="hero-num gtext gtext-flame" style="margin-top:auto">
        ¥1,899
      </div>
      <div class="c-foot">2026.05.10 上市</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 5 · Hero + 2 Side</div>
    <div>— 05 / 12 —</div>
  </div>
</section>
```

**要点**:
- 主卡用 `.b-card.img` 让产品图占满,`.img-overlay` 浮在底部
- 右侧两张窄卡(3 列宽 × 8 行高)分别承载规格 + 价格

---

## Layout 6 · Top Hero + Grid(顶 banner + 3 卡)

**用途**:章节标题 + 3 个分支特性 / 3 个核心理由 / 3 个步骤
**密度**:4 卡(本 skill 主推之一)

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>三个核心理由 · Why</div>
    <div>06 / 12</div>
  </div>
  <div class="bento">
    <div class="b-card grad b-12x3" data-anim>
      <div class="kicker">THE PITCH</div>
      <h2 class="h-xl" style="margin-top:1vh">
        为什么是 <span class="gtext gtext-sky">Bento</span>?
      </h2>
      <p class="lead" style="margin-top:1.4vh; max-width:62vw">
        不是单页大块文本,不是僵硬的"标题 + 三栏",而是按内容驱动的卡片网格。
      </p>
    </div>
    <div class="b-card b-4x5" data-anim>
      <div class="sticker mint">01 · FLEX</div>
      <div class="c-head" style="margin-top:2vh">
        <div class="c-title">灵活</div>
      </div>
      <p class="body">
        卡片数量取决于内容如何更好地呈现,1, 2, 3, 4, 5 张都可以。
      </p>
      <div class="c-foot">FLEXIBILITY</div>
    </div>
    <div class="b-card b-4x5" data-anim>
      <div class="sticker accent">02 · SCALE</div>
      <div class="c-head" style="margin-top:2vh">
        <div class="c-title">层级</div>
      </div>
      <p class="body">
        最重要的信息放最大的卡上,次要的散在周边。视觉一眼分主次。
      </p>
      <div class="c-foot">HIERARCHY</div>
    </div>
    <div class="b-card b-4x5" data-anim>
      <div class="sticker flame">03 · SPACE</div>
      <div class="c-head" style="margin-top:2vh">
        <div class="c-title">留白</div>
      </div>
      <p class="body">
        卡间至少 20px 间距,卡内 ≥ 24px padding。呼吸感是 bento 的灵魂。
      </p>
      <div class="c-foot">BREATHING</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 6 · Top Hero + Grid</div>
    <div>— 06 / 12 —</div>
  </div>
</section>
```

**要点**:
- 顶部 12×3 banner 占据 3 行高,留 5 行给下方 3 张卡
- 3 张子卡用三种 sticker 颜色(mint / accent / flame)区分
- 这是本 skill 最常用的"章节型"布局

---

## Layout 7 · Mixed Free Grid(自由混合)

**用途**:数据 dashboard / 信息密集页 / 多维度同屏展示
**密度**:5-7 卡(本 skill 主推之一)

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>数据全景 · Dashboard</div>
    <div>07 / 12</div>
  </div>
  <div class="bento">
    <!-- 左上:大数据卡 6×4 -->
    <div class="b-card grad b-6x4" data-anim>
      <div class="sticker accent">REVENUE</div>
      <div class="c-head" style="margin-top:1vh">
        <div class="c-title">营收</div>
      </div>
      <div class="hero-num gtext gtext-sky" style="font-size:6vw">
        30.3<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">亿元</span>
      </div>
      <div class="c-foot">2025 · 同比 +2.4%</div>
    </div>
    <!-- 右上:KPI 卡 6×4 -->
    <div class="b-card b-6x4" data-anim>
      <div class="sticker">METRICS</div>
      <div class="c-head" style="margin-top:1vh">
        <div class="c-title">关键指标</div>
      </div>
      <div class="kpi-row"><div class="kpi-l">毛利率</div><div class="kpi-v">33.5%</div></div>
      <div class="kpi-row"><div class="kpi-l">净利率</div><div class="kpi-v">3.39%</div></div>
      <div class="kpi-row"><div class="kpi-l">ROE</div><div class="kpi-v">3.37%</div></div>
    </div>
    <!-- 中:全宽 banner 12×2 -->
    <div class="b-card glass b-12x2" data-anim>
      <div class="icon-row" style="font-size:max(15px,1.2vw)">
        <span class="sticker mint" style="margin-right:1em">INSIGHT</span>
        <span>2025 增收不增利 · 汇兑损益 + 拓展投入 + 应收账款共同挤压利润</span>
      </div>
    </div>
    <!-- 底排 4 张 stat 小卡 3×2 -->
    <div class="b-card b-3x2" data-anim>
      <div class="caption">PATENTS</div>
      <div class="stat-num" style="font-size:3vw">981</div>
    </div>
    <div class="b-card b-3x2" data-anim>
      <div class="caption">DATA · 万份</div>
      <div class="stat-num gtext gtext-mint" style="font-size:3vw">890</div>
    </div>
    <div class="b-card b-3x2" data-anim>
      <div class="caption">BCG · 亿份</div>
      <div class="stat-num" style="font-size:3vw">4</div>
    </div>
    <div class="b-card b-3x2" data-anim>
      <div class="caption">REPORTS · 万</div>
      <div class="stat-num gtext gtext-flame" style="font-size:3vw">1000+</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 7 · Mixed Free Grid</div>
    <div>— 07 / 12 —</div>
  </div>
</section>
```

**要点**:
- 总共 7 卡:6×4 + 6×4 + 12×2 + 4×(3×2)= 24 + 24 + 24 + 24 = 96 单元 ✅
- 中间 12×2 全宽 banner 适合放一句洞察 / 总结句
- 底排 4 张窄卡用更小的 caption + 简化 stat,密度感强
- `.b-3x2` 不在快捷类里,用 inline:`<div class="b-card" style="grid-column:span 3;grid-row:span 2">`(注:已在 template.html 中定义为快捷类,可直接用)

**网格计算助记**:
```
┌──────────┬──────────┐  6×4 + 6×4
│ 6×4 stat │ 6×4 KPI  │
├──────────┴──────────┤  12×2 banner
│   12×2 insight     │
├──────┬──────┬──────┬──────┤  4×(3×2)
│ 3×2  │ 3×2  │ 3×2  │ 3×2  │
└──────┴──────┴──────┴──────┘
```

---

## Layout 8 · Stat Showcase 2×2(4 大数字)

**用途**:4 个核心 KPI / 4 个关键里程碑 / 4 个产品参数
**密度**:4 卡(数字驱动)

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>核心数字 · Numbers</div>
    <div>08 / 12</div>
  </div>
  <div class="bento">
    <div class="b-card grad b-6x4" data-anim>
      <div class="sticker accent">REVENUE</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">营收</div>
      </div>
      <div class="hero-num gtext gtext-sky">
        30.3<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">亿元</span>
      </div>
      <div class="c-foot">2025 · 同比 +2.4%</div>
    </div>
    <div class="b-card b-6x4" data-anim>
      <div class="sticker">NET PROFIT</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">归母净利</div>
      </div>
      <div class="hero-num">
        1.05<span class="hu">亿元</span>
      </div>
      <div class="c-foot" style="color:var(--accent-3)">2025 · 同比 -32.8%</div>
    </div>
    <div class="b-card b-6x4" data-anim>
      <div class="sticker mint">PATENTS</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">累计专利</div>
      </div>
      <div class="hero-num gtext gtext-mint">
        981<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">项</span>
      </div>
      <div class="c-foot">含发明专利 200+ 项</div>
    </div>
    <div class="b-card grad b-6x4" data-anim>
      <div class="sticker flame">DATA</div>
      <div class="c-head" style="margin-top:1.4vh">
        <div class="c-title">睡眠数据样本</div>
      </div>
      <div class="hero-num gtext gtext-flame">
        890<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">万份</span>
      </div>
      <div class="c-foot">+ 4 亿份 BCG 心冲击图</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 8 · Stat Showcase 2×2</div>
    <div>— 08 / 12 —</div>
  </div>
</section>
```

**要点**:
- 4 张等大卡(`6×4`),sticker 颜色形成"四角呼应"
- 数字大小 = `hero-num`(默认 8vw)
- 每张卡的 `gtext` 渐变方向不同(sky / 无 / mint / flame)制造彩色角点
- 负向数据(同比下降)用 `style="color:var(--accent-3)"` 标红,正向用 `var(--accent-4)` 标绿(本例中只标红)

---

## Layout 9 · Table-Centric(商业表格主导)

**用途**:财务三年对比 / 竞品功能矩阵 / 价格套餐表 / SLA 对比 / 任何 ≤ 8 行 × 6 列的对比表
**密度**:3 卡(顶 banner + 中表格 + 底 insight)
**默认主题**:dark / light 都可,看主题色

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>财务 3 年对比 · Financial Comparison</div>
    <div>09 / 18</div>
  </div>
  <div class="bento">
    <!-- 顶部:标题 banner b-12x2 -->
    <div class="b-card grad b-12x2" data-anim>
      <div class="kicker">FY 2023-2025 · 三年纵向对比</div>
      <h2 class="h-lg">营收回升 · 利润<span class="gtext gtext-flame">承压</span></h2>
    </div>
    <!-- 中部:表格主卡 b-12x5 -->
    <div class="b-card b-12x5" data-anim>
      <table class="bt">
        <thead>
          <tr>
            <th>指标</th>
            <th class="num">2023</th>
            <th class="num">2024</th>
            <th class="num hl">2025</th>
            <th class="num">YoY</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>营业收入(亿元)</td>
            <td class="num">31.03</td>
            <td class="num">29.58</td>
            <td class="num hl">30.30</td>
            <td class="num pos">+2.4%</td>
          </tr>
          <tr>
            <td>归母净利润(亿元)</td>
            <td class="num">1.78</td>
            <td class="num">1.56</td>
            <td class="num hl">1.05</td>
            <td class="num neg">-32.8%</td>
          </tr>
          <tr>
            <td>毛利率</td>
            <td class="num">38.2%</td>
            <td class="num">37.4%</td>
            <td class="num hl">33.5%</td>
            <td class="num neg">-3.9pp</td>
          </tr>
          <tr>
            <td>净利率</td>
            <td class="num muted">5.7%</td>
            <td class="num">5.2%</td>
            <td class="num hl">3.4%</td>
            <td class="num neg">-1.8pp</td>
          </tr>
          <tr>
            <td>经营现金流(亿元)</td>
            <td class="num muted">2.10</td>
            <td class="num">2.57</td>
            <td class="num hl">3.86</td>
            <td class="num pos">+50.2%</td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- 底部:insight 横条 b-12x1 -->
    <div class="b-card glass b-12x1" data-anim>
      <div style="display:flex;align-items:center;gap:1em;height:100%">
        <span class="sticker mint">INSIGHT</span>
        <span class="body">现金流改善是唯一正向信号 · 应收账款占归母净利润 513.5% 是关键议题</span>
      </div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 9 · Table-Centric</div>
    <div>FINANCIAL COMPARISON</div>
  </div>
</section>
```

### `.bt` 表格类速查

| 类 | 用途 |
|---|---|
| `<table class="bt">` | 启用 bento 表格样式 |
| `<th class="num">` | 数字列表头(右对齐) |
| `<th class="hl">` | 高亮列表头(accent-1 色 + 加粗下划线) |
| `<td class="num">` | 数字单元格(等宽 + 右对齐 + Manrope) |
| `<td class="hl">` | 高亮列单元格(背景填 accent-1 半透) |
| `<td class="pos">` | 正向数据(绿色 + 加粗) |
| `<td class="neg">` | 负向数据(粉红色 + 加粗) |
| `<td class="muted">` | 弱化数据(text-3) |
| `<td class="center">` | 居中对齐 |

第一列(标签列)自动用 sans-zh 字体 + 稍粗 + 主文色。

### 硬约束

- ≤ 8 行 × 6 列(再大就拆页或换 dee-ppt-skill)
- **每页 ≤ 1 张 `.bt` 表格**(2 张表 = 商业 PPT 表格页观感,丢掉 bento 美学)
- 表格永远在 `.b-card` 里,不要直接放在 `.bento` grid 上

### 变体 · 大表格(竞品功能矩阵)

如果是 6 列 × 6-8 行的竞品功能对比,把中部主卡改成 `b-12x6`,顶部 banner 缩成 `b-12x1`,底部 insight 缩到 `b-12x1`:

```
顶部 b-12x1(只有标题一行)
中部 b-12x6(大表格)
底部 b-12x1(insight)
```

---

## Layout 10 · TOC(章节目录)

**用途**:开场后的"内容大纲"页,告诉听众接下来要讲什么
**密度**:1 banner + N 章节卡(N = 3 / 4 / 5 / 6)
**默认主题**:dark(对仪式感更友好)

### 10A · 列表式 TOC(推荐 · 适合 4-6 章)

每章一张全宽窄卡 `.b-12x1`,纵向叠成"目录列表"。这是 Apple keynote 最常见的 TOC 形态。

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>Contents · 章节目录</div>
    <div>02 / 18</div>
  </div>
  <div class="bento">
    <!-- 顶部 banner -->
    <div class="b-card glass b-12x2" data-anim>
      <div class="kicker">CONTENTS · 5 ACTS · 18 PAGES</div>
      <h2 class="h-xl">本场<span class="gtext gtext-aurora">内容</span></h2>
    </div>

    <!-- 已讲过(.done 弱化) -->
    <div class="b-card b-12x1" data-anim>
      <div class="toc-item done">
        <div class="toc-num">01</div>
        <div class="toc-body">
          <div class="toc-name">公司画像</div>
          <div class="toc-desc">基本信息 · 历程 · 品牌矩阵 · 产能布局</div>
        </div>
        <div class="toc-pages">P 02-05</div>
      </div>
    </div>

    <!-- 当前章节(.active 高亮 + grad 卡变体) -->
    <div class="b-card grad b-12x1" data-anim>
      <div class="toc-item active">
        <div class="toc-num">02</div>
        <div class="toc-body">
          <div class="toc-name">行业与市场</div>
          <div class="toc-desc">全球市场规模 · 渗透率反差 · 增长驱动力</div>
        </div>
        <div class="toc-pages">P 06-09 · 当前</div>
      </div>
    </div>

    <!-- 未讲(默认样式) -->
    <div class="b-card b-12x1" data-anim>
      <div class="toc-item">
        <div class="toc-num">03</div>
        <div class="toc-body">
          <div class="toc-name">财务表现</div>
          <div class="toc-desc">三年财务对比 · 客户结构 · 技术与数据资产</div>
        </div>
        <div class="toc-pages">P 10-13</div>
      </div>
    </div>
    <div class="b-card b-12x1" data-anim>
      <div class="toc-item">
        <div class="toc-num">04</div>
        <div class="toc-body">
          <div class="toc-name">竞争格局</div>
          <div class="toc-desc">全球 vs 国内对手 · 优劣势 · 客户集中度风险</div>
        </div>
        <div class="toc-pages">P 14-16</div>
      </div>
    </div>
    <div class="b-card b-12x1" data-anim>
      <div class="toc-item">
        <div class="toc-num">05</div>
        <div class="toc-body">
          <div class="toc-name">战略与展望</div>
          <div class="toc-desc">2025 关键动作 · SWOT · 风险 · 收尾金句</div>
        </div>
        <div class="toc-pages">P 17-20</div>
      </div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 10A · TOC List View</div>
    <div>5 ACTS · 18 PAGES</div>
  </div>
</section>
```

**TOC 状态设计**:
- 默认:平淡(白文 + text-2 副文)
- `.toc-item.active`:当前章节,数字用 aurora 渐变,页码 sticker 染 accent-1 色,卡片用 `.grad` 变体(整张卡微亮)
- `.toc-item.done`:已讲过,opacity 0.45 弱化

**网格规划**(5 章场景):
```
b-12x2 (banner) = 24
b-12x1 × 5      = 60
合计            = 84 ≤ 96 ✅(剩 12 单元留白)
```

### 10B · 网格式 TOC(适合 3-4 章 · 视觉更强)

每章一张大卡 + 大编号 + 章节名 + 描述 + 页码,用 grid 排:

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>Contents · 章节目录</div>
    <div>02 / 16</div>
  </div>
  <div class="bento">
    <div class="b-card glass b-12x2" data-anim>
      <div class="kicker">CONTENTS · 4 ACTS</div>
      <h2 class="h-xl">本场<span class="gtext gtext-aurora">内容</span></h2>
    </div>
    <div class="b-card grad b-6x3" data-anim>
      <div class="hero-num gtext gtext-sky" style="font-size:5vw">01</div>
      <div class="c-head" style="margin-top:1vh">
        <div class="c-title">公司画像</div>
      </div>
      <p class="body" style="margin-top:.6vh">基本信息 · 发展历程 · 品牌矩阵 · 产能布局</p>
      <div class="c-foot">P 02-05</div>
    </div>
    <div class="b-card b-6x3" data-anim>
      <div class="hero-num" style="font-size:5vw;color:var(--text-3)">02</div>
      <div class="c-head" style="margin-top:1vh">
        <div class="c-title">行业与市场</div>
      </div>
      <p class="body" style="margin-top:.6vh">全球规模 · 渗透率反差 · 4 大驱动力</p>
      <div class="c-foot">P 06-09</div>
    </div>
    <div class="b-card b-6x3" data-anim>
      <div class="hero-num" style="font-size:5vw;color:var(--text-3)">03</div>
      <div class="c-head" style="margin-top:1vh">
        <div class="c-title">财务与竞争</div>
      </div>
      <p class="body" style="margin-top:.6vh">3 年对比 · 客户集中度 · 全球 vs 国内</p>
      <div class="c-foot">P 10-13</div>
    </div>
    <div class="b-card b-6x3" data-anim>
      <div class="hero-num" style="font-size:5vw;color:var(--text-3)">04</div>
      <div class="c-head" style="margin-top:1vh">
        <div class="c-title">战略与展望</div>
      </div>
      <p class="body" style="margin-top:.6vh">2025 动作 · SWOT · 风险 · 收尾</p>
      <div class="c-foot">P 14-16</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 10B · TOC Grid View</div>
    <div>4 ACTS · 16 PAGES</div>
  </div>
</section>
```

**网格规划**(4 章网格):
```
b-12x2 (banner) = 24
b-6x3  × 4       = 72
合计            = 96 ✅
```

3 章用 `b-4x6 × 3` + 顶部 `b-12x2`,6 章用 `b-4x3 × 6` + 顶部 `b-12x2`。

### TOC 设计原则

- ✅ TOC 页放在**开场后第 2 页**(第 1 页是封面 hero,第 2 页是 TOC)
- ✅ 章节数 ≥ 3 才值得做 TOC,< 3 章直接跳过(听众一眼就懂)
- ✅ 章节描述 ≤ 1 行,**不要塞段落** — TOC 是地图不是大纲
- ✅ 章节数 ≤ 6 — 超过 6 拆成两层(主章节 + 子章节)或干脆不做 TOC
- ❌ TOC 页不要塞图片 / KPI / 数据卡 — 干净就是 TOC 的本职
- ❌ 不要每个新章节前都重复 TOC(有些 deck 会"今天讲到第 03 章" — 听众不需要,看 ESC 索引即可)

---

## Layout 11 · Chapter Preview(章节预告)

**用途**:**进入新章节前的"本章预告"页**(每章开头放 1 张),左侧大字章节名 + 右侧本章所有小节列表
**密度**:2 卡(左大章 + 右小节列表)
**默认主题**:dark · 仪式感更强
**比 L10 好在哪**:L10 列表式扁平,这个左右非对称、视觉层级清晰、信息密度更高

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>第二幕 · 行业与市场</div>
    <div>04 / 18</div>
  </div>
  <div class="bento">
    <!-- 左:大章节名 b-4x8 (glass 让背景透出,仪式感) -->
    <div class="b-card glass b-4x8" data-anim>
      <div class="kicker">ACT 02 · CURRENT CHAPTER</div>
      <div class="hero-num gtext gtext-aurora" style="font-size:8vw;margin-top:1vh">02</div>
      <h2 class="h-xl" style="margin-top:1.5vh">行业与市场</h2>
      <p class="lead" style="margin-top:2vh">
        36 亿美元盘子, <span class="gtext gtext-flame">14% vs 0.2%</span> 的渗透率反差。
      </p>
      <div class="meta-row" style="margin-top:auto">
        <span>P 04-07</span><span>·</span><span>4 PAGES</span>
      </div>
    </div>
    <!-- 右:本章小节详细列表 b-8x8 -->
    <div class="b-card b-8x8" data-anim>
      <div class="c-head">
        <div class="c-kick">CHAPTER 02 · CONTENTS</div>
        <div class="c-title">本章包含 4 节</div>
      </div>
      <ul class="subnav" style="flex:1;justify-content:center;gap:1.6vh;margin-top:2vh">
        <li class="sub-item">
          <div class="sub-name">04 · 全球智能床市场规模(4 机构口径)</div>
          <div class="sub-pg">P 04</div>
        </li>
        <li class="sub-item">
          <div class="sub-name">05 · 区域市场份额 · 14% vs 0.2% 渗透率反差</div>
          <div class="sub-pg">P 05</div>
        </li>
        <li class="sub-item">
          <div class="sub-name">06 · 4 大长期增长驱动力</div>
          <div class="sub-pg">P 06</div>
        </li>
        <li class="sub-item">
          <div class="sub-name">07 · 国内家具行业宏观环境</div>
          <div class="sub-pg">P 07</div>
        </li>
      </ul>
      <div class="c-foot">CHAPTER PREVIEW</div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 11 · Chapter Preview</div>
    <div>ACT II · ENTRY PAGE</div>
  </div>
</section>
```

**网格规划**:`b-4x8` (32) + `b-8x8` (64) = 96 ✅

**用法节奏**:
- 整 deck 有几个章节,就放几个 L11(每章开头 1 张)
- 配合 L12(开场全局大纲)= 双层目录系统:L12 是地图,L11 是地形图
- 不要每章都用 — 短章节(1-2 页)直接进入即可,只有 ≥ 3 页的章节值得用 L11

---

## Layout 12 · Outline Overview(全局大纲)

**用途**:**开场后第 2 页的全局地图**,展示所有章节 + 每章下的小节;比 L10 信息量大得多
**密度**:1 banner + N 章节卡(每卡含小节列表)
**默认主题**:dark
**与 L10 区别**:L10 只列章节名,L12 同时列出每章下的所有小节;L12 是真正"商业 PPT 该有的"完整大纲

### 12A · 4 章版(2x2 最对称 · 推荐)

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>Outline · 完整大纲</div>
    <div>02 / 16</div>
  </div>
  <div class="bento">
    <!-- 顶部 banner -->
    <div class="b-card glass b-12x2" data-anim>
      <div class="kicker">FULL OUTLINE · 4 ACTS · 16 PAGES</div>
      <h2 class="h-xl">完整<span class="gtext gtext-aurora">大纲</span></h2>
    </div>
    <!-- 4 张章节卡 b-6x3 × 4 -->
    <div class="b-card grad b-6x3" data-anim>
      <div style="display:flex;align-items:baseline;gap:1.2vw">
        <div class="hero-num gtext gtext-sky" style="font-size:3vw;margin:0">01</div>
        <div style="flex:1">
          <div class="c-title">公司画像</div>
          <div class="caption" style="margin-top:.3vh">P 02-04 · 3 PAGES</div>
        </div>
      </div>
      <ul class="subnav tight" style="margin-top:1.2vh">
        <li class="sub-item"><div class="sub-name">公司基本信息 + 全球地位</div><div class="sub-pg">P 02</div></li>
        <li class="sub-item"><div class="sub-name">二十年历程 + 7 大品牌</div><div class="sub-pg">P 03</div></li>
        <li class="sub-item"><div class="sub-name">三地产能布局</div><div class="sub-pg">P 04</div></li>
      </ul>
    </div>
    <div class="b-card b-6x3" data-anim>
      <div style="display:flex;align-items:baseline;gap:1.2vw">
        <div class="hero-num" style="font-size:3vw;margin:0;color:var(--text-3)">02</div>
        <div style="flex:1">
          <div class="c-title">行业与市场</div>
          <div class="caption" style="margin-top:.3vh">P 05-07 · 3 PAGES</div>
        </div>
      </div>
      <ul class="subnav tight" style="margin-top:1.2vh">
        <li class="sub-item"><div class="sub-name">全球市场规模(4 机构口径)</div><div class="sub-pg">P 05</div></li>
        <li class="sub-item"><div class="sub-name">14% vs 0.2% 渗透率反差</div><div class="sub-pg">P 06</div></li>
        <li class="sub-item"><div class="sub-name">4 大增长驱动力</div><div class="sub-pg">P 07</div></li>
      </ul>
    </div>
    <div class="b-card b-6x3" data-anim>
      <div style="display:flex;align-items:baseline;gap:1.2vw">
        <div class="hero-num" style="font-size:3vw;margin:0;color:var(--text-3)">03</div>
        <div style="flex:1">
          <div class="c-title">财务与竞争</div>
          <div class="caption" style="margin-top:.3vh">P 08-12 · 5 PAGES</div>
        </div>
      </div>
      <ul class="subnav tight" style="margin-top:1.2vh">
        <li class="sub-item"><div class="sub-name">三年财务对比表</div><div class="sub-pg">P 08-09</div></li>
        <li class="sub-item"><div class="sub-name">技术与数据资产</div><div class="sub-pg">P 10</div></li>
        <li class="sub-item"><div class="sub-name">竞争对手 + 客户集中度</div><div class="sub-pg">P 11-12</div></li>
      </ul>
    </div>
    <div class="b-card b-6x3" data-anim>
      <div style="display:flex;align-items:baseline;gap:1.2vw">
        <div class="hero-num" style="font-size:3vw;margin:0;color:var(--text-3)">04</div>
        <div style="flex:1">
          <div class="c-title">战略与展望</div>
          <div class="caption" style="margin-top:.3vh">P 13-16 · 4 PAGES</div>
        </div>
      </div>
      <ul class="subnav tight" style="margin-top:1.2vh">
        <li class="sub-item"><div class="sub-name">2025 关键动作</div><div class="sub-pg">P 13</div></li>
        <li class="sub-item"><div class="sub-name">SWOT 全景 + 风险</div><div class="sub-pg">P 14-15</div></li>
        <li class="sub-item"><div class="sub-name">二次曲线收尾金句</div><div class="sub-pg">P 16</div></li>
      </ul>
    </div>
  </div>
  <div class="foot">
    <div>Layout 12A · Outline 4-Chapter Grid</div>
    <div>OPENING MAP</div>
  </div>
</section>
```

### 12B · 5 章版(2 行 · 上 2 下 3)

5 章不能整除 12 列,改用 2 行布局:第一行 2 大卡 `b-6x3`,第二行 3 中卡 `b-4x3`。

```
banner b-12x2  (24)
b-6x3 b-6x3   (18 + 18)
b-4x3 b-4x3 b-4x3 (12 + 12 + 12)
合计 = 96 ✅
```

第一行的两章用 `b-6x3` 显得"重要",第二行 3 章用 `b-4x3` 紧凑展示。适合"前 2 章是基础、后 3 章是深入"的叙事节奏。骨架同 12A,只是把 4 张卡改成 5 张并按上述 grid。

### 12C · 6 章版(3x2 网格)

```
banner b-12x2 (24)
b-4x3 × 6     (12 × 6 = 72)
合计 = 96 ✅
```

6 张等大卡 `b-4x3`,每卡内的 subnav 用 `.tight` 紧凑变体,小节限制 ≤ 3 个/章。

### Subnav 小节列表组件速查

```html
<ul class="subnav tight">  <!-- 加 .tight 用紧凑版,L12 章节卡内推荐 -->
  <li class="sub-item">
    <div class="sub-name">小节标题</div>
    <div class="sub-pg">P 05</div>
  </li>
  <li class="sub-item current">     <!-- .current 高亮当前小节 -->
    <div class="sub-name">当前小节</div>
    <div class="sub-pg">P 06</div>
  </li>
</ul>
```

| 类 | 用途 |
|---|---|
| `<ul class="subnav">` | 标准小节列表(L11 大列表场景) |
| `<ul class="subnav tight">` | 紧凑变体(L12 章节卡内,字稍小) |
| `<li class="sub-item">` | 一行小节(左小节名 + 右页码 sticker) |
| `<li class="sub-item current">` | 当前小节高亮(accent-1 色 + 加粗) |

### TOC 系统三件套对比

| Layout | 用途 | 信息密度 | 何时用 |
|---|---|---|---|
| **L10** TOC List | 简单章节列表(只列章节名) | 低 | 章节多但内容简单的 deck(如 1 章 1 页的极简风) |
| **L11** Chapter Preview | 进入新章节前的预告(左大章 + 右小节) | 中 | **每章节开头放 1 张** · 推荐主推 |
| **L12** Outline Overview | 开场全局大纲(banner + N 章节卡 + 每章小节) | 高 | **开场后第 2 页** · 整场地图 · 推荐主推 |

**双层目录系统建议**:
- 第 2 页放 L12(开场全局地图)
- 每章开头放 L11(本章详细预告)
- L10 仅在"完全不需要小节信息"的简单场景用,日常优先 L11 / L12

---

## Layout 13 · Image Showcase(图片驱动 · 产品家族网格)

**用途**:**3-4 个产品对比**(产品家族 / 套装 / 配件矩阵)、多产品视觉展示
**密度**:1 banner + 3 / 4 / 6 张产品图卡
**默认主题**:dark(产品图通常深底更突出)
**与现有 layout 的差别**:
- L5(Hero + 2 Side)是 1 主 + 2 副 · 偏向"主推 + 规格"
- L13 是平等的 N 张产品图 · 偏向"系列对比"

### 13A · 4 产品 2x2(MacBook 家族 / AirPods 家族 / 4 套餐型号)

```html
<section class="slide" data-theme="dark">
  <div class="chrome">
    <div>产品家族 · MacBook Lineup</div>
    <div>05 / 18</div>
  </div>
  <div class="bento">
    <!-- 顶部 banner -->
    <div class="b-card grad b-12x2" data-anim>
      <div class="kicker">PRODUCT FAMILY · 4 MODELS</div>
      <h2 class="h-xl">MacBook <span class="gtext gtext-sky">家族</span></h2>
    </div>

    <!-- 4 张产品图卡 b-6x3 × 4 -->
    <div class="b-card img b-6x3" data-anim>
      <img class="img-fill" src="images/macbook-air-13.jpg" alt="MacBook Air 13">
      <div class="img-overlay">
        <div class="sticker accent" style="margin-bottom:.6vh">AIR 13"</div>
        <h3 class="h-md">MacBook Air 13</h3>
        <p class="body" style="margin-top:.4vh">M5 · 18 小时 · ¥9,999 起</p>
      </div>
    </div>
    <div class="b-card img b-6x3" data-anim>
      <img class="img-fill" src="images/macbook-air-15.jpg" alt="MacBook Air 15">
      <div class="img-overlay">
        <div class="sticker mint" style="margin-bottom:.6vh">AIR 15"</div>
        <h3 class="h-md">MacBook Air 15</h3>
        <p class="body" style="margin-top:.4vh">M5 · 18 小时 · ¥11,999 起</p>
      </div>
    </div>
    <div class="b-card img b-6x3" data-anim>
      <img class="img-fill" src="images/macbook-pro-14.jpg" alt="MacBook Pro 14">
      <div class="img-overlay">
        <div class="sticker flame" style="margin-bottom:.6vh">PRO 14"</div>
        <h3 class="h-md">MacBook Pro 14</h3>
        <p class="body" style="margin-top:.4vh">M5 Pro · 22 小时 · ¥14,999 起</p>
      </div>
    </div>
    <div class="b-card img b-6x3" data-anim>
      <img class="img-fill" src="images/macbook-pro-16.jpg" alt="MacBook Pro 16">
      <div class="img-overlay">
        <div class="sticker accent" style="margin-bottom:.6vh">PRO 16"</div>
        <h3 class="h-md">MacBook Pro 16</h3>
        <p class="body" style="margin-top:.4vh">M5 Max · 24 小时 · ¥19,999 起</p>
      </div>
    </div>
  </div>
  <div class="foot">
    <div>Layout 13A · Product Family 2×2</div>
    <div>4 MODELS · ONE FAMILY</div>
  </div>
</section>
```

**网格规划**:`b-12x2` (24) + `b-6x3` × 4 (72) = 96 ✅

### 13B · 3 产品横排(套餐 hero / 三色对比)

```html
<section class="slide" data-theme="dark">
  <div class="bento">
    <div class="b-card grad b-12x2" data-anim>
      <div class="kicker">FLAGSHIP TRIO</div>
      <h2 class="h-xl">三款<span class="gtext gtext-sky">主打</span></h2>
    </div>
    <div class="b-card img b-4x6" data-anim>
      <img class="img-fill" src="images/iphone-air.jpg" alt="iPhone Air">
      <div class="img-overlay">
        <div class="sticker mint" style="margin-bottom:.6vh">AIR</div>
        <h3 class="h-md">iPhone Air</h3>
        <p class="body" style="margin-top:.4vh">最薄 · ¥7,999</p>
      </div>
    </div>
    <div class="b-card img b-4x6" data-anim>
      <img class="img-fill" src="images/iphone-pro.jpg" alt="iPhone Pro">
      <div class="img-overlay">
        <div class="sticker accent" style="margin-bottom:.6vh">PRO</div>
        <h3 class="h-md">iPhone Pro</h3>
        <p class="body" style="margin-top:.4vh">3 倍长焦 · ¥9,999</p>
      </div>
    </div>
    <div class="b-card img b-4x6" data-anim>
      <img class="img-fill" src="images/iphone-pro-max.jpg" alt="iPhone Pro Max">
      <div class="img-overlay">
        <div class="sticker flame" style="margin-bottom:.6vh">PRO MAX</div>
        <h3 class="h-md">iPhone Pro Max</h3>
        <p class="body" style="margin-top:.4vh">5x · ¥12,999</p>
      </div>
    </div>
  </div>
</section>
```

**网格规划**:`b-12x2` (24) + `b-4x6` × 3 (72) = 96 ✅

### 13C · 单产品满屏 hero(发布会主推页)

```html
<section class="slide" data-theme="dark">
  <div class="bento">
    <div class="b-card img b-12x8" data-anim>
      <img class="img-fill" src="images/vision-pro.jpg" alt="Vision Pro 2">
      <div class="img-overlay" style="padding:8vh 6vw">
        <div class="sticker accent" style="margin-bottom:1.4vh">NEW · 2026</div>
        <h1 class="h-hero-zh" style="font-size:6vw;margin-bottom:1.4vh">Vision Pro 2</h1>
        <p class="lead" style="max-width:50vw;margin-bottom:2vh">
          重量减轻 30%,续航延长一倍,价格更接近一台高端笔电。
        </p>
        <div class="meta-row">
          <span>FROM ¥19,999</span><span>·</span><span>2026.06 上市</span>
        </div>
      </div>
    </div>
  </div>
</section>
```

### 没图怎么办

用占位 `.img-slot`(虚线框 + 文字提示)替代 `<img>`:

```html
<div class="b-card img b-6x3">
  <div class="img-slot" style="position:absolute;inset:0;border-radius:0;border:none">
    PRODUCT IMAGE PLACEHOLDER
  </div>
  <div class="img-overlay">
    <h3 class="h-md">产品名</h3>
  </div>
</div>
```

或者用纯文字卡(`.b-card.grad` 不带图)先占位,等图到位后再替换。

### 图片来源建议

- 产品官方渲染图:apple.com / vercel.com / linear.app 等品牌资源页(Apple Newsroom / GitHub OG image)
- 原型图 / Mockup:Figma 导出 / Mockuuups Studio
- 截图:macOS ⌘+Shift+4 截屏后,放到 `images/{页号}-{语义}.png`

详见 SKILL.md "图片约定" 一节。

---

## Layout 决策树

```
内容是什么?
├─ 开场 / 章节封 / 收尾金句   → Layout 1 (Single Focus)
├─ 双产品 / 旧 vs 新对比     → Layout 2 (50/50)
├─ 1 个核心叙事 + KPI 佐证   → Layout 3 (8/4)
├─ 3 个套餐 / 3 个特性      → Layout 4 (3-Column)
├─ 1 主产品 + 规格 + 价格    → Layout 5 (Hero + 2 Side)
├─ 章节标题 + 3 子点        → Layout 6 (Top Hero + Grid)  ★ 本 skill 主推
├─ 5-7 个维度的 dashboard   → Layout 7 (Mixed Free)      ★ 本 skill 主推
├─ 4 个 KPI / 4 个里程碑    → Layout 8 (Stat Showcase 2×2)
├─ 多列对比表 / 财务三年表   → Layout 9 (Table-Centric)   ★ 商业用途
├─ 章节目录 / 内容大纲       → Layout 10 (简化 TOC) / 11 (章节预告) / 12 (全局大纲)
└─ 产品家族 / 多产品图对比   → Layout 13 (Image Showcase,A 4 卡 / B 3 卡 / C 单卡 hero)
```

---

## 完整 Deck 节奏建议(20 页参考 · 含默认目录系统)

> 这是带 4 个章节的标准模板,包含 **L12 全局大纲(P2 默认)** + **L11 每章预告**。详见 SKILL.md "默认骨架"。

| 页 | Layout | 密度 | 说明 |
|---|---|---|---|
| 1 | L1 Single Focus | hero | 开场封面 |
| **2** | **L12 Outline Overview ★** | banner + N 卡 | **全局大纲 · 默认插入** |
| 3 | **L11 Chapter Preview ★** | 2 卡 | 第 1 章预告 |
| 4 | L7 Mixed Free | 6 卡 | 第 1 章正文 dashboard |
| 5 | L8 Stat Showcase | 4 卡 | 第 1 章关键数字 |
| 6 | **L11 Chapter Preview ★** | 2 卡 | 第 2 章预告 |
| 7 | L5 Hero + 2 Side | 3 卡 | 主产品介绍 |
| 8 | L4 3-Column | 3 卡 | 三个套餐 |
| 9 | **L11 Chapter Preview ★** | 2 卡 | 第 3 章预告 |
| 10 | L9 Table-Centric | 3 卡 | 财务/数据对比表 |
| 11 | L3 Asymmetric 8/4 | 2 卡 | 核心叙事 + 数据 |
| 12 | L2 50/50 | 2 卡 | 旧 vs 新 |
| 13 | **L11 Chapter Preview ★** | 2 卡 | 第 4 章预告 |
| 14 | L13 Image Showcase | 5 卡 | 产品家族图 grid |
| 15 | L6 Top Hero + Grid | 4 卡 | 三个客户案例 |
| 16 | L8 Stat Showcase | 4 卡 | 路线图 Q1/Q2/Q3 |
| 17 | L7 Mixed Free | 5 卡 | 团队 + 融资 + 进度 |
| 18 | L3 Asymmetric 8/4 | 2 卡 | 愿景 + 关键数字 |
| 19 | L1 Single Focus | hero | 大问题 / Call to Action |
| 20 | L1 Single Focus | hero | 收尾金句 / 联系方式 |

★ = **默认骨架页**(skill 自动插入,无需用户主动要求)。

总占比:目录系统(L11×4 + L12×1)= 5 张 / 20 = **25%**。听众的"路标"和"内容"同等重要 — 不要为了塞内容把 L11 / L12 砍掉。

每 3-5 页插入 1 个 hero 喘息,稠密页(4-7 卡)+ hero 页比例约 2:1。
