# 质量检查清单(Checklist)

生成完一份 deck 后,**逐项对照**。P0 必须 100% 通过。

---

## P0 · 必须通过(否则视觉直接垮)

### P0-1 · 类预检防线

**所有用到的类必须在 `assets/template.html` 的 `<style>` 块中定义**。常见漏检:

```bash
# 在生成的 HTML 上跑(把 index.html 替换成实际路径):
grep -oE 'class="[^"]*b-[0-9]+x[0-9]+[^"]*"' index.html | sort -u
```

确认每个 `b-NxM` 都在 22 个快捷类内:
```
b-12x8/5/4/3/2  b-8x8/5/4/3  b-6x8/5/4/3
b-4x8/5/4/3/2   b-3x8/4/3/2
```
不在的必须用 inline `style="grid-column:span N;grid-row:span M"`,**不要发明新类名**。

### P0-2 · 主题色一致

- ✅ `:root` 的 6 项主题变量(`--bg-base` / `--card` / `--text` / `--accent-1/2/3/4` / `--gtext-*`)只能整体复制 `themes.md` 的某一套
- ❌ 禁止混搭(如 bg 取 Apple Dark,accent 取 OpenAI Warm)
- ❌ 禁止用户给任意 hex 值

```bash
# 自检:抓出所有写死的 hex,应该只有 themes.md 里那一套,无散落
grep -oE '#[0-9a-fA-F]{6}' index.html | sort -u
```

### P0-3 · 卡片密度 + 节奏

- 单页卡片数 ∈ [1, 7] · 超过 7 = 视觉过密,必须拆页
- 不允许连续 5 页以上无 hero(hero = Layout 1 单卡)
- 不允许连续 3 页以上单卡 hero
- 首页用 Layout 1,末页用 Layout 1 / 2

```bash
# 自检卡片数:每页 .b-card 数量
awk '/<section class="slide/{p++; c=0} /<div class="b-card/{c++} /<\/section>/{print "Page "p": "c" cards"}' index.html
```

### P0-4 · 不用 emoji

- 不用 emoji(🎉 🚀 等)替代图标 / 标签
- 用 `.sticker` 文字标签 + `lucide` 线性图标 + 4 套 accent 色

```bash
# 自检 emoji:LC_ALL=C 让正则按字节判断
LC_ALL=C grep -nP "[\xF0-\xF7][\x80-\xBF]{3}" index.html | head -20
# 命中 = 有 4 字节 unicode(emoji 多在此范围),需检查
```

### P0-5 · 中文用 sans-serif

- 中文文字一律用 `var(--sans-zh)`(已 CSS 默认)
- 不要 inline `font-family:serif` 之类覆盖

### P0-6 · gradient text 克制

- 一页 ≤ 2 处 `.gtext`
- 只用在大字号上(`.h-hero` / `.h-xl` / `.hero-num`)
- 配数字单位时,单位必须 inline 取消渐变(否则单位也染色,丑):
  ```html
  <div class="hero-num gtext gtext-sky">
    30.3<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">亿元</span>
  </div>
  ```

### P0-7 · sticker 颜色协调

- 一页内 sticker 颜色 ≤ 3 种(从 default/accent/mint/flame 4 种里挑)
- 不要每张卡都用 accent — 失去强调意义
- 推荐:中心卡 accent,周边卡 default + 1-2 个 mint/flame 点缀

---

## P1 · 强烈建议(影响美学水准)

### P1-1 · Hero Number 单位独立设色

不要让单位也跟着 gradient 染色,看起来像彩虹病:

```html
<!-- ❌ 错 -->
<div class="hero-num gtext gtext-sky">30.3<span class="hu">亿元</span></div>

<!-- ✅ 对 -->
<div class="hero-num gtext gtext-sky">
  30.3<span class="hu" style="-webkit-text-fill-color:var(--text-2);background:none">亿元</span>
</div>
```

### P1-2 · 负数 / 警示数据用 accent-3 标红

```html
<div class="c-foot" style="color:var(--accent-3)">2025 · 同比 -32.8%</div>
```

正向用 `var(--accent-4)`(默认 mint 绿)。

### P1-3 · Card variant 互斥

`.glass` / `.elev` / `.grad` / `.img` 选一个,不要叠加。叠加会冲突。

### P1-4 · 图片 cover 模式

- 占满整张卡 → `.b-card.img` + `<img class="img-fill">`
- 卡内一部分 → `<figure class="frame-img">` + `<img>`
- 不要在卡里写死 `aspect-ratio` — 用 `flex:1` + `object-fit:cover`

### P1-5 · chrome / kicker / footer 不要重复

- chrome 左上 = 栏目级(跨页可重复,如 "Act II · Workflow")
- kicker = 页面级(每页独一份,如"BUT")
- foot 左下 = 页面说明(如"Layout 6 · Top Hero + Grid")
- 三者不要写同一句话

### P1-6 · 网格总和 ≤ 96 单元

12 列 × 8 行 = 96。每页所有卡的 `(span-col × span-row)` 之和 ≤ 96。
超过 = 卡片溢出网格,会互相挤压。

```
Layout 7 计算示例:
6×4 + 6×4 + 12×2 + 4×(3×2) = 24+24+24+24 = 96 ✅
```

---

## P2 · 推荐(细节打磨)

- **大数字字号**:hero-num 默认 8vw,小卡(`.b-3x2`)里可缩到 3-4vw,inline 调
- **首页 hero 一定要 `data-animate="hero"`**,节奏更慢更仪式感
- **每章节用 1 页 Layout 1** 作幕封,中间稠密页 3-4 张交替
- **Lucide icon 颜色**:用 `currentColor` 自动跟随主题
- **冷暖配色**:同一页里冷色卡(sky/mint)和暖色卡(flame/accent)不要 1:3 失衡,推荐 2:2 或 3:1

---

## P3 · 可选(锦上添花)

- 给 deck 起一个明确的代号(如"Vol.01 · Q4 Roadmap"),写在 chrome 右上,跨页保持
- 末页加 contact CTA(邮箱 / 网址 / Twitter handle)
- 视情况调 `.bg-blob` 的 opacity / animation duration,营造特定氛围

---

## 跨设备验证

- Chrome / Safari / Edge 都打开测一次
- Safari 对 `backdrop-filter` 支持稍弱,如果 glass 卡看起来像普通卡,加 `-webkit-backdrop-filter` 兜底(已在 template 中)
- 1280px / 1920px / 2560px 三种宽度下,bento 网格的 `vw` 单位换算正常,卡片不溢出
- 移动端(<900px)CSS 已自动降级为 6 列 × 12 行(单列长 deck)

---

## 离线兜底验证

```bash
# 关掉网络刷新,看是否还能用
# 1. Lucide icon 不显示 — 可接受(只是图标缺失)
# 2. Google Fonts 不加载 — 字体 fallback 系统字,可读
# 3. Motion 本地优先加载,失败兜底显示 — [data-anim] 仍可见
# 4. WebGL 替代品(CSS gradient)不需要联网 — 永远工作
```

---

## 速查 · 最常踩的 3 个坑

1. **卡片溢出网格**:总和超过 96 单元,某张卡被挤到下一行 → 重新计算 span,确保 ≤ 96
2. **gradient 数字单位也染色**:`hu` 没 inline 取消渐变 → 加 `style="-webkit-text-fill-color:var(--text-2);background:none"`
3. **某页全是 default sticker**:看起来很灰 → 至少 1-2 个 accent / mint / flame 点缀
