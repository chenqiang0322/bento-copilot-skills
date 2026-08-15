---
name: bento-ppt
description: 生成"Apple keynote × 现代 SaaS"风格的横向翻页 Bento Grid 网页 PPT(单 HTML 文件),含 CSS gradient mesh 背景、12×8 网格的卡片系统、玻璃质感、超大数字 + 渐变文字、5 套主题色(Apple Dark / Apple Light / Vision Aurora / Vercel Geist / Claude Warm)、L9 商业表格、L10/L11/L12 三层目录系统。当用户需要做产品发布会 / SaaS 路演 / AI demo / 数据 dashboard / 功能矩阵展示型 PPT,或提到"bento PPT"、"Apple keynote 风"、"产品发布会风格 PPT"、"卡片网格演讲稿"时使用。
license: MIT
metadata:
  upstream: https://github.com/by4hp/bento-ppt-skill
---

# Bento PPT Skill

## 这个 Skill 做什么

生成一份**单文件 HTML**的横向翻页 PPT,视觉基调是:

- **Bento Grid × 现代科技** 风(Apple keynote / Vercel / Linear / OpenAI 谱系)
- **CSS gradient mesh 背景**(无 WebGL,纯 CSS 渐变 + 漂浮 blob)
- **12 列 × 8 行内部网格** 的卡片系统,卡片用 `.b-NxM` 快捷类自由组合
- **玻璃质感卡片**(backdrop-filter blur)+ **超大数字** + **gradient text**
- **sans-serif 字体**(Inter + Manrope + Noto Sans SC + JetBrains Mono),不用衬线
- **横向左右翻页**(键盘 ← →、滚轮、触屏、底部圆点、ESC 索引)
- **入场动效**(Motion One 驱动,本地 + CDN 双保险,离线可用)
- **5 套精选主题**(Apple Dark / Apple Light / Vision Aurora / Vercel Geist / Claude Warm)

这个 skill 不是"杂志"也不是"汇报模板",它像 **Apple keynote 上的产品 spec 页 + Linear changelog 的混血**。

## 何时使用

**合适的场景**:
- 产品发布会 / 功能更新展示
- SaaS / 开发者工具的 launch pitch
- AI demo day / 模型发布
- 数据 dashboard 型 PPT(KPI 矩阵 / 多维数据展示)
- 团队 / 公司年度 review / OKR 复盘
- 需要"现代科技感 + 信息密集"的网页 deck

**不合适的场景**(用其他 skill):
- 个人分享 / 私享会 / 行业观察
- 培训课件 / 教学材料(信息层级线性,不需要网格)
- 用飞书 / 企业内部协作
- 视频 / 动画演示

## 工作流

### Step 1 · 需求澄清(动手前必做)

如果用户已给完整大纲就跳到 Step 2。如果只给主题或模糊想法,用以下 7 问对齐:

| # | 问题 | 为什么问 |
|---|---|---|
| 1 | **受众是谁?分享场景?**(产品发布 / 内部路演 / 投资人 pitch / 客户演示) | 决定语言风格和信息密度 |
| 2 | **分享时长?** | 15 分钟 ≈ 10-12 页,30 分钟 ≈ 18-22 页,45 分钟 ≈ 25-30 页 |
| 3 | **内容类型?**(产品发布 / 数据 dashboard / 路演 pitch / 功能矩阵) | 决定布局倾向(产品图 vs 数据 vs 文本) |
| 4 | **有原始素材吗?**(文档 / 数据 / 旧 PPT / 设计稿) | 有素材就基于素材,没有就帮搭 |
| 5 | **有产品截图 / 设备图吗?放哪?** | 见下方"图片约定" |
| 6 | **想要哪套主题?** | 5 套预设挑一(见 `references/themes.md`) |
| 7 | **硬约束?**(必须包含 XX 数据 / 不能出现 YY) | 避免返工 |

#### 大纲协助(用户没大纲时)

用"产品发布弧"骨架:

```
钩子(Hook)         → 1 页    : 一句话或一个数字抛出冲击
背景(Context)      → 1-2 页  : 我们是谁 / 为什么做这个
问题(Problem)      → 1-2 页  : 痛点 / 现状的不足
方案(Solution)     → 5-10 页 : 产品 / 功能 / 特性矩阵展示
证据(Proof)        → 2-3 页  : 数据 / 案例 / 客户证言
路线(Roadmap)      → 1-2 页  : 接下来做什么
收束(Call to Action) → 1 页   : 行动建议 / 联系方式
```

#### 图片约定

- **位置**:`项目/XXX/ppt/images/` 下,与 `index.html` 同级
- **命名**:`{页号}-{语义}.{ext}`,如 `01-cover.jpg` / `05-airpods.png` / `08-dashboard.png`
- **规格**:单张 ≥ 1600px 宽,JPG 用照片/截图,PNG 用透明 UI / 图表
- **替换**:同名覆盖最稳;若改名,全局搜 `images/旧名` 改

### Step 2 · 拷贝模板

```bash
mkdir -p "项目/XXX/ppt/assets" "项目/XXX/ppt/images"
cp "<SKILL_ROOT>/assets/template.html" "项目/XXX/ppt/index.html"
cp "<SKILL_ROOT>/assets/motion.min.js" "项目/XXX/ppt/assets/motion.min.js"
```

`template.html` 已是完整可运行的种子,含 3 个示例 slide(封面 / Top Hero+3 卡 / 2×2 Stats),拷贝后:

#### 2.1 必改占位

打开浏览器 Tab 不要显示"[必填] 替换为 PPT 标题":

```html
<title>[必填] 替换为 PPT 标题 · Bento Deck</title>
                ↓ 改成
<title>实际标题 · 实际公司或人名</title>
```

grep 一下 `[必填]` 确认全部替换。

#### 2.2 选定主题色(5 套预设,不允许自定义)

详见 `references/themes.md`。基于内容推荐:

| 内容 | 推荐主题 |
|---|---|
| 不知道选啥 / 第一次用 | 🌑 Apple Dark |
| 浅色官网风 / 消费品 | ☀️ Apple Light |
| AI 大模型 / 沉浸感 | 🌌 Vision Aurora |
| 开发者工具 / SaaS | ⬛ Vercel Geist |
| AI 工具 / 研究内容 | 🌿 Claude Warm |

操作:打开 template.html `<style>` 块,**整体替换** `:root{` 里标有"主题色"注释的那一组变量(`--bg-base` / `--card` / `--text` / `--accent-1/2/3/4` / `--gtext-*`)。其他 CSS 全走 `var(--...)`,无需任何其他改动。

### Step 3 · 填充内容

#### 3.0 类预检(最重要)

**所有用到的类必须在 `assets/template.html` 的 `<style>` 块中已定义**。生成 slide 前先 Read template.html,对照 layouts.md 的 Pre-flight 列表确认。常见类:

- 网格:`.bento` / `.b-NxM`(22 个快捷类)
- 卡片:`.b-card` + 变体 `.glass` / `.elev` / `.grad` / `.img`
- 标题:`.h-hero` / `.h-hero-zh` / `.h-xl` / `.h-lg` / `.h-md` / `.h-sm`
- 数字:`.hero-num` / `.stat-num` / `.hu`
- 卡内:`.c-head` / `.c-kick` / `.c-title` / `.c-foot` / `.kpi-row` / `.feat-list`
- 标签:`.sticker` / `.sticker.accent|mint|flame`
- 渐变:`.gtext` / `.gtext-aurora|sky|flame|mint`

**不要发明新类名**。需要自定义用 inline `style="..."`。

#### 3.0.4 默认骨架(必装的 3 类页 · 无需用户主动要求)

**只要满足条件,就自动放进 deck**(下表是默认行为,不是可选):

| 默认页 | 触发条件 | 放在哪 | 用什么 layout |
|---|---|---|---|
| **大纲页** | 章节数 ≥ 3 | **P1 封面后第 1 页(即 P2)** | L12 Outline Overview(章节数选 12A 4 章 / 12B 5 章 / 12C 6 章) |
| **章节预告页** | 单章 ≥ 3 页内容 | **每个长章节开头** | L11 Chapter Preview(左大章节名 + 右本章小节列表) |
| **章节封面 hero** | 任何章节 | 章节 L11 之后 / 内容前 | L1 Single Focus(单卡章节标题) |

**反例**:不要把 L12 大纲放在 deck 末尾作 BONUS — 它是听众的"地图",必须在最前 ;不要因为"章节简单"就跳过 L11 — 长章节没预告 = 听众迷路;不要每章只用 L1 hero 而不放 L11 — L1 只给标题,L11 才给小节地图。

**判断条件用 deck 章节数,不用页数**:
- 4 章 deck = 1 张 L12(P2)+ 4 张 L11(每章入口)+ 4 张 L1(可选,L11 已经够仪式感了)
- 整 deck 占比:目录系统页(L11 + L12)≈ 全 deck 25%-30%。听众的"路标"远比"内容"重要

#### 3.0.5 卡片密度规划(本 skill 节奏规则)

不像 guizang 强制 dark/light 主题交替,本 skill **统一一种主题色,靠卡片密度交替**:

- ✅ 每页卡数 ∈ [1, 7],主推 4-7 卡稠密页
- ✅ 每 3-4 页插入 1 个 Layout 1 单卡 hero 喘息
- ❌ 禁止连续 5 页以上无 hero
- ❌ 禁止连续 3 页以上单卡 hero

#### 3.1 网格规划(动手前画 ASCII)

写一页 slide 前,用 ASCII 画卡片分布:

```
Layout 7 Mixed Free:
┌──────────┬──────────┐
│ 6×4 stat │ 6×4 KPI  │
├──────────┴──────────┤
│   12×2 insight     │
├────┬────┬────┬─────┤
│3×2 │3×2 │3×2 │3×2  │
└────┴────┴────┴─────┘
总单元 = 24+24+24+(4×6) = 96 ✅
```

确认 `(span-col × span-row)` 之和 ≤ 96,再粘骨架。

#### 3.2 挑布局

打开 `references/layouts.md`,8 个完整 bento 布局骨架直接粘贴改文案:

| Layout | 用途 |
|---|---|
| 1. Single Focus | 开场 / 章节封 / 收尾 |
| 2. 50/50 Symmetric | 双产品对比 |
| 3. Asymmetric 8/4 | 主叙事 + 数据 |
| 4. 3-Column | 三方案 / 三套餐 |
| 5. Hero + 2 Side | 主产品 + 规格 + 价格 |
| 6. **Top Hero + Grid** ★ | 章节标题 + 3 子卡 |
| 7. **Mixed Free Grid** ★ | 数据 dashboard |
| 8. Stat Showcase 2×2 | 4 个核心数字 |

### Step 4 · 对照检查清单

打开 `references/checklist.md`,逐项过 P0(必须)+ P1(强烈建议)。重点:

- 类预检通过(`grep b- index.html` 都在 22 个快捷类内)
- 主题色一致(`grep '#[0-9a-fA-F]' index.html` 应该只有 themes.md 那一套)
- 不用 emoji(`grep -P "[\xF0-\xF7]"` 应为空)
- gradient text 一页 ≤ 2 处,只用在大字号
- 卡数 ∈ [1, 7],密度节奏交替

### Step 5 · 本地预览

```bash
open "项目/XXX/ppt/index.html"
```

不需要本地服务器。键盘 ← → 翻页 / 空格推进 / ESC 看索引。

### Step 6 · 迭代

90% 调整都是改 inline style:
- 字号:`style="font-size:Xvw"`
- 卡片尺寸:换快捷类(`.b-6x4` → `.b-8x4`)或 inline `style="grid-column:span N;grid-row:span M"`
- 间距:`style="gap:Yvh"`
- 颜色:换 sticker 变体或 gradient text 变体

---

## 资源文件导览

```
bento-ppt/
├── SKILL.md              ← 你正在读
├── assets/
│   ├── template.html     ← 完整可运行模板(种子)
│   └── motion.min.js     ← Motion One 本地副本(离线兜底,可选)
└── references/
    ├── themes.md         ← 5 套主题色(只能选不能改)
    ├── layouts.md        ← bento 布局骨架(可直接粘贴)
    ├── components.md     ← 组件手册(字体/网格/卡片/数字/sticker/gradient...)
    └── checklist.md      ← P0-P3 质量清单
```

**加载顺序建议**:
1. 先读 SKILL.md 了解整体
2. Step 1 澄清完成后,读 themes.md 帮选主题
3. **动手前 Read template.html 的 `<style>` 块**(类名唯一来源)
4. 读 layouts.md 挑布局(顶部 Pre-flight + 布局骨架 + 决策树)
5. 细节查 components.md(字体/卡片/数字组件细则)
6. 生成后读 checklist.md 自检

---

## 核心设计原则(哲学)

> 这些原则是 bento 美学的支柱。违反任何一条,视觉感都会垮。

1. **网格优于堆砌** — 卡片必须落在 12×8 网格,不允许 absolute 自由定位
2. **留白即结构** — 卡间 ≥ 20px gap,卡内 ≥ 24px padding(已 CSS 强制)
3. **层级靠尺寸** — 最重要的卡 = 最大的卡,不靠颜色高亮
4. **渐变要克制** — 渐变只用在背景 / 大数字 / 1-3 个关键词,卡身保持中性
5. **图片是真主角** — 产品截图 / 设备图 / dashboard 截屏需占至少 1 张大卡(Layout 5 / 7)
6. **节奏靠密度,不靠主题** — 4-7 卡稠密 + 1-3 卡 hero 交替,主题色一以贯之

## 参考视觉锚点

- Apple WWDC keynote 的 spec 页(产品规格 4 卡 2×2)
- Apple.com 首页的"功能特性"网格(Top Hero + 3 子卡)
- Linear changelog 页(Vercel Mono 风的极简卡片)
- Vision Pro 发布会(Aurora 渐变玻璃卡)
- ChatGPT 产品页(OpenAI Warm 的米白绿色调)
- Vercel.com / vercel.com/templates 的 Bento 网格
