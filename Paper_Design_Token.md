---
version: v1
name: InternDiscovery-paper-warm
description: >
  暖纸（Light · Warm · 默认）单主题 token，抽取自 discoveryos-style-guide v2.3
  （.md 规范 + .tweakcn.css 导出）。本模块只保留暖纸一套 —— 已剥离冷纸（cool）与暖夜（dark）。
  场域是暖纸而非显示器：#fdfcf8 暖米背景为底，#1554a8 朱砂蓝主色仅用于关键操作与视觉重音；
  字体即语义角色，悬停是温度递进而非层级抬升，平面是默认、纵深是稀缺资源。
  含完整暖纸色彩 token + 结构参数（字体 / 字阶 / 间距 / 圆角 / 阴影 / 动效 / 层级 / 断点 / 栅格 / 图标）。
  ⚠️ 相对源规范的唯一立场改动：圆角由原「2px 唯一锐角」改为 5 阶阶梯（2 / 4 / 8 / 999px / 50%）。
radius:
  xs: 2px      # 最小（少数）· 滚动条滑块 / 进度条填充
  base: 4px    # 常用（主力）· 按钮 / 输入框 / 标签 / chip / tab / CTA / 二级菜单项
  card: 8px    # 卡片 · 卡片 / 面板 / 横幅 / composer / 下拉浮层 / banner
  pill: 999px  # 胶囊（克制）· 筛选 / 分页圆点 / 微型计数 / 状态徽章
  circle: 50%  # 圆形 · 头像 / 状态圆点
colors:
  # 表面 Surface
  paper: "#fdfcf8"
  paper-warm: "#f7f4ec"
  paper-cool: "#fafaf7"
  # 文字 Text
  ink: "#1a2332"
  ink-soft: "#3a4556"
  ink-mute: "#7a8394"
  ink-faint: "#a8afbb"
  # 分隔线 Rule
  rule: "#e8e4d9"
  rule-soft: "#efece3"
  # 主色 Brand · 朱砂蓝 7 阶
  vermilion-6: "#1554a8"
  # 语义 Semantic（default）
  success: "#6b7a3a"
  warning: "#a8864b"
  error: "#c03030"
  rec-red: "#e74c3c"
---

# InternDiscovery · 暖纸 Paper (Warm) Token — V1

> 模块：`Design Token / 03_Paper`　·　范围：暖纸单主题（已剥离冷纸 / 暖夜）
> 来源：`discoveryos-style-guide.v2.3.md` + `discoveryos-style-guide.v2.3.tweakcn.css`
> 配套：可粘贴的 tweakcn / shadcn CSS 导出见同目录 `Paper_V1.tweakcn.css`

---

## 0. 设计立场（暖纸 · 硬约束）

任何视觉判断与代码取舍都回退到下列五条立场。

### 0.1 场域是暖纸，不是显示器
主背景永远 `#fdfcf8`（暖米色），主色 `#1554a8`（朱砂蓝）仅用于关键操作与视觉重音。**温度感优先于通量感**。

### 0.2 几何承诺 · 圆角 5 阶（本模块改写）
> ⚠️ **与源规范的唯一立场差异**：源规范 v2.3 主张「`border-radius: 2px` 是唯一锐角」。本模块改为 **5 阶圆角阶梯**（见 §4）。
> 阶梯外**禁止再创造圆角值**（如 6 / 10 / 12 / 16px）—— 任意圆角必先归类至 5 阶之一。

```
2px   · 最小（少数）· 滚动条滑块 / 进度条填充
4px   · 常用（主力）· 按钮 / 输入框 / 标签 / chip / tab / CTA / 二级菜单项
8px   · 卡片        · 卡片 / 面板 / 横幅 / composer / 下拉浮层 / banner
999px · 胶囊（克制）· 筛选 / 分页圆点 / 微型计数 / 状态徽章
50%   · 圆形        · 头像 / 状态圆点
0     · 直角        · 表格 / 分隔器 / 整页区块（不参与圆角阶梯）
```

### 0.3 字体即语义角色（Type-as-Semantics）
| 字体 | 语义角色 |
|---|---|
| JetBrains Mono / Uppercase | 元信息（分类、状态、计数、区段标签） |
| Noto Serif SC 600 | 内容标题（用户实际要阅读的标题） |
| Cormorant Garamond Italic | 品牌印记（仅 Logo 占用） |
| Inter 400 / 500 | 正文与控件文本 |

### 0.4 悬停是温度递进，不是层级抬升
90% 以上的 hover 仅修改 `background` 至 `--paper-warm`。**禁止**通过边框加深、阴影投射或几何位移表达 hover。

### 0.5 平面是默认 · 纵深是稀缺资源
`box-shadow` 仅出现在 §5 登记的两类场景中（浮层投影 / 模态投影）。**未登记的 shadow 即为反模式**。

### 0.6 AI 输出的可信度是视觉一等公民
AI 生成的内容在视觉上必须：**可识别**（AI vs 人）/ **可追溯**（来源文档与引用）/ **可置信度量**（高 / 中 / 低 / 推断）/ **可流式反馈**（生成中 vs 已完成 vs 中断）。这四条是组件解剖的必备槽位。

> **自检触发器**：若产出代码接近 Material Design / Tailwind UI / Antd 默认样式 —— 大概率违反了上述某条立场。

---

## 1. 色彩 Token（Warm Paper）

> 暖纸单主题：所有颜色为 light·warm 取值，**不含** dark / cool 覆盖。
> 主色 7 阶（朱砂蓝）色相 H≈214° 真蓝域；语义色四阶（default / soft / bg / deep）。

### 1.1 文字色阶（Ink）

| Token | HEX | 角色 | 对 `--paper` 对比度 |
|---|---|---|---|
| `--ink` | `#1a2332` | L1 · 主文字 / 墨色 | 13.5:1 (AAA) |
| `--ink-soft` | `#3a4556` | L2 · 次级文字 | 8.2:1 (AAA) |
| `--ink-mute` | `#7a8394` | L3 · 辅助文字 | 4.6:1 (AA) |
| `--ink-faint` | `#a8afbb` | L4 · 弱化文字 / placeholder | 2.9:1（仅非关键信息） |

### 1.2 表面色阶（Surface）

| Token | HEX | 角色 |
|---|---|---|
| `--paper` | `#fdfcf8` | 主背景 / 暖米纸 |
| `--paper-warm` | `#f7f4ec` | 悬停渗透 / 卡片底色 |
| `--paper-cool` | `#fafaf7` | 次级容器 / 中性区块 |

### 1.3 分隔线（Rule）

| Token | HEX |
|---|---|
| `--rule` | `#e8e4d9` |
| `--rule-soft` | `#efece3` |

### 1.4 主色 · 朱砂蓝 7 阶（Brand · H≈214°）

> 由浅至深 · **色阶 6 为常规主色**。新组件优先使用编号 token，旧别名仅回填既有组件。

| 色阶 | Token | HEX | 角色 | 典型用途 |
|---|---|---|---|---|
| 1 | `--vermilion-1` | `#f4f7fb` | 浅色白色悬浮 | 浅底极弱 tint / `--ai-tint` 类底色 |
| 2 | `--vermilion-2` | `#dde7f4` | 禁用 | disabled 控件背景 / 弱化区块 |
| 3 | `--vermilion-3` | `#b8ceea` | 小面积填充 | pill-bg / 标签底 / `.mark--note` |
| 4 | `--vermilion-4` | `#88addd` | 特殊场景 | 装饰边线 / 引导插图 / focus-soft |
| 5 | `--vermilion-5` | `#3f7dcf` | 悬浮 | 控件 `:hover` 填充态 / `.cite:hover` |
| 6 | `--vermilion-6` | `#1554a8` | **常规（主色）** | `.btn-primary` / `border-left` 重音 / 链接 |
| 7 | `--vermilion-7` | `#0c3c80` | 点击 | 控件 `:active` / pressed / 主按钮 hover-deep |

**兼容别名**：`--vermilion` ≡ L6 · `--vermilion-soft` ≡ L5 · `--vermilion-bg` ≡ L2 · `--vermilion-deep` ≡ L7。

> **严格约束**：不允许在 7 阶之外私造主色变体（rgba 透明叠加 / 临时 HSL 调整）—— 任意主色用色场景必先归类至某一阶。

### 1.5 语义色（Semantic · 四阶：default / soft / bg / deep）

| 状态 | default | soft | bg | deep |
|---|---|---|---|---|
| Success | `#6b7a3a` | `#a4ad7e` | `#f1f3e8` | `#4d5826` |
| Warning | `#a8864b` | `#cba87b` | `#f8f1e3` | `#7a5e2c` |
| Error | `#c03030` | `#df7878` | `#fdeaea` | `#9a2020` |

> **色弱兼容**：`--success` / `--error` 不允许单独靠色相区分，必须同时附图标或文字（`✓` `!` `×`）。

### 1.6 录制专用红 / AI 置信度 / AI tint

| Token | HEX | 用途 |
|---|---|---|
| `--rec-red` | `#e74c3c` | 唯一非朱砂红 · 仅 `.badge-live` / `pulse-rec` / 录音中状态 |
| `--ai-trust-high` | `var(--success)` | 高置信 · 来源充足 |
| `--ai-trust-mid` | `var(--warning)` | 中置信 · 部分推断 |
| `--ai-trust-low` | `var(--ink-mute)` | 低置信 · 灰化呈现 |
| `--ai-tint` | `#f5f8fc` | AI 消息底色（极弱朱砂） |
| `--ai-tint-rule` | `#d8e4f3` | AI 消息边线（朱砂 → rule 过渡） |

### 1.7 辅助色色板 · 4 色相 × 5 阶（v2.4）

> 用于学科分类、数据可视化、用户头像、标签、分组徽章等「多色区分」场景。与主色 / 语义色错峰分布（≥25° 色环距离）。
> **使用规约**：不承担语义信息（语义独占 success/warning/error）· 不替代品牌锚点（链接 / CTA 走 vermilion）· 同页 ≤4 种 · L3–L5 不用作大面积背景。

| 色相 (H) | L1 极浅填充 | L2 浅色描边 | L3 Icon/中强调 | L4 字体/深描边 | L5 最深强调 |
|---|---|---|---|---|---|
| Mint 160° | `#e4f0ec` | `#9bd5be` | `#40bf95` | `#259675` | `#125c47` |
| Cyan 185° | `#e4f0f0` | `#9bd0d5` | `#40b5bf` | `#258e96` | `#12575c` |
| Violet 270° | `#ece4f0` | `#be9bd5` | `#8c40bf` | `#6d2596` | `#42125c` |
| Magenta 325° | `#f0e4e9` | `#d59bb8` | `#bf4082` | `#962566` | `#5c123f` |

### 1.8 可粘贴 `:root` 块（暖纸）

```css
:root {
  /* ── 文字色阶 ── */
  --ink: #1a2332; --ink-soft: #3a4556; --ink-mute: #7a8394; --ink-faint: #a8afbb;
  /* ── 表面色阶 ── */
  --paper: #fdfcf8; --paper-warm: #f7f4ec; --paper-cool: #fafaf7;
  /* ── 分隔线 ── */
  --rule: #e8e4d9; --rule-soft: #efece3;
  /* ── 主色 · 朱砂蓝 7 阶 ── */
  --vermilion-1: #f4f7fb; --vermilion-2: #dde7f4; --vermilion-3: #b8ceea; --vermilion-4: #88addd;
  --vermilion-5: #3f7dcf; --vermilion-6: #1554a8; --vermilion-7: #0c3c80;
  --vermilion: var(--vermilion-6); --vermilion-soft: var(--vermilion-5);
  --vermilion-bg: var(--vermilion-2); --vermilion-deep: var(--vermilion-7);
  /* ── 语义色（四阶）── */
  --success: #6b7a3a; --success-soft: #a4ad7e; --success-bg: #f1f3e8; --success-deep: #4d5826;
  --warning: #a8864b; --warning-soft: #cba87b; --warning-bg: #f8f1e3; --warning-deep: #7a5e2c;
  --error: #c03030; --error-soft: #df7878; --error-bg: #fdeaea; --error-deep: #9a2020;
  /* ── 录制红 / AI ── */
  --rec-red: #e74c3c;
  --ai-trust-high: var(--success); --ai-trust-mid: var(--warning); --ai-trust-low: var(--ink-mute);
  --ai-tint: #f5f8fc; --ai-tint-rule: #d8e4f3;
  /* ── 辅助色 4×5 ── */
  --aux-mint-1: #e4f0ec; --aux-mint-2: #9bd5be; --aux-mint-3: #40bf95; --aux-mint-4: #259675; --aux-mint-5: #125c47;
  --aux-cyan-1: #e4f0f0; --aux-cyan-2: #9bd0d5; --aux-cyan-3: #40b5bf; --aux-cyan-4: #258e96; --aux-cyan-5: #12575c;
  --aux-violet-1: #ece4f0; --aux-violet-2: #be9bd5; --aux-violet-3: #8c40bf; --aux-violet-4: #6d2596; --aux-violet-5: #42125c;
  --aux-magenta-1: #f0e4e9; --aux-magenta-2: #d59bb8; --aux-magenta-3: #bf4082; --aux-magenta-4: #962566; --aux-magenta-5: #5c123f;
}
```

### 1.9 操作按钮色彩层级（Action Button Tiers）

> 来源：Figma `§ 3.1 · BUTTON FAMILY`。
> **规范**：当前页面**最重要**的操作按钮 = 白字 + **墨色**（梯度）填充；**次级重要**的按钮 = 白字 + **主色朱砂蓝**（梯度）填充；**普通**操作 = **边框 + 白底**。
> 蓝色**不进入**最高层级操作 —— 主操作 = 墨色 Solid、次级 = 朱砂蓝（与「中性 Solid 主操作、蓝色作强调」立场一致）。
> 「梯度」指同一色相沿色阶在 default / hover / pressed 间切换（**始终单色填充，非 CSS 线性渐变**）；disabled = 在按钮上施加 `opacity: .5`。

| 层级 | 类名 | 填充 / 边框 | 文字 | DEFAULT | HOVER | PRESSED | DISABLED |
|---|---|---|---|---|---|---|---|
| **主操作**（最重要） | `.btn-primary` | 墨色填充 | 白字 | `--ink` `#1a2332` | `--ink-soft` `#3a4556` | `--ink` `#1a2332` | `--ink-mute` `#7a8394` · `opacity .5` |
| **次级操作** | `.btn-secondary` | 朱砂蓝填充 | 白字 | `--vermilion-6` `#1554a8` | `--vermilion-7` `#0c3c80` | `--vermilion-7` `#0c3c80` | `#1554a8` · `opacity .5` |
| **普通操作** | `.btn` | 边框 + 白底 | `--ink-soft` | bg `--paper` / 边 `--rule` | bg `--paper-warm` | bg `--paper` | `opacity .5` |
| 无形态 | `.btn-ghost` | 透明（hover 才显边） | `--ink-soft` | 透明底 | bg `--paper-warm` / 边 `--rule` | 透明底 | `opacity .5` |
| 破坏性 | `.btn-danger` | 白底 + error 边框 | `--error` | 边/字 `--error` `#c03030` | 边/字 `--error-deep` `#9a2020` | 边/字 `--error` | `opacity .5` |

按钮基线：`padding: 7px 14px` · `font: 500 13px` · 圆角 **4px**（见 §4 · 控件阶）。对应 CSS token 见 `Paper_V1.css` 的 `--btn-*` 段。

```css
/* 主操作 · 墨色 + 白字 */
--btn-primary-bg: #1a2332; --btn-primary-bg-hover: #3a4556; --btn-primary-bg-active: #1a2332; --btn-primary-fg: #ffffff;
/* 次级操作 · 朱砂蓝 + 白字 */
--btn-secondary-bg: #1554a8; --btn-secondary-bg-hover: #0c3c80; --btn-secondary-bg-active: #0c3c80; --btn-secondary-fg: #ffffff;
/* 普通操作 · 边框 + 白底 */
--btn-bg: #fdfcf8; --btn-bg-hover: #f7f4ec; --btn-border: #e8e4d9; --btn-fg: #3a4556;
/* 破坏性 · 白底 + error 边框/字 */
--btn-danger-border: #c03030; --btn-danger-border-hover: #9a2020; --btn-danger-fg: #c03030;
```

> ⚠️ 本层级以本平台 Figma `§3.1 BUTTON FAMILY` 现状为准，**区别于源规范 v2.3**（源规范 `.btn-primary` 为朱砂底、且无 `.btn-secondary`）。
> 同时区别于 shadcn 的 `--primary`（=朱砂，承担「品牌强调 / focus ring」语义）—— 主操作按钮填充走**墨色**，二者不可混用。

---

## 2. 字体与排版（Type）

### 2.1 字体栈

```css
--font-sans:  'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Noto Sans SC', sans-serif;
--font-serif: 'Cormorant Garamond', 'Noto Serif SC', serif;
--font-mono:  'JetBrains Mono', ui-monospace, 'SF Mono', monospace;
```

引入：
```html
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,500&family=Noto+Serif+SC:wght@300;400;500;600;700&family=JetBrains+Mono:wght@300;400;500&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

### 2.2 字号阶梯（Type Scale）

仅允许：`10 · 11 · 12 · 13 · 14 · 16 · 20 · 28 · 42`

| 字号 | 用途 |
|---|---|
| 10 | pill / table th |
| 11 | label / timeline-num / live badge |
| 12 | section-label / eyebrow / table td / inline citation |
| 13 | btn / 紧凑正文 / `.title-s` |
| 14 | body / input / chat bubble |
| 16 | `.title-m` |
| 20 | `.title-l` |
| 28 | section hero |
| 42 | hero-title |

### 2.3 字体语义规则

- **Logo**：Cormorant Garamond Italic 22 / 500（仅 Logo 占用），em 朱砂正体 600。
- **内容标题**：Noto Serif SC 永远 **600**；`.title-s` 严格 13px。
- **Hero 标题**：Cormorant 42 / **400**（唯一用 400 的 serif 标题）。
- **letter-spacing**：CJK（Noto Serif SC）永远 `+0.02em`；拉丁（Cormorant）永远 `-0.02em`。
- **正文**：Inter 14 / line-height 1.6 / `--ink`；长文容器 line-height 1.75 / max-width 720px。
- **元信息**：JetBrains Mono Uppercase + `letter-spacing: .18em`。
- **placeholder**：永远 `font-style: normal`（中文 italic 几乎都是劣化）。
- 中英文混排**禁止**为中文单独指定字体，让 Inter 走 fallback。

---

## 3. 间距（Spacing）

```
4 · 6 · 8 · 10 · 12 · 14 · 16 · 20 · 24 · 32 · 40 · 56 · 80
```
**禁止 5 / 7 / 9 / 11 / 13 / 15 / 18 / 22**。

| 用途 | 推荐值 |
|---|---|
| 图标—文字 gap | 6 / 8 |
| 卡片内 padding · 紧凑 | 10 / 12 |
| 卡片内 padding · 标准 | 14 / 16 |
| 卡片之间 | 8 / 12 |
| 区段之间 | 24 / 32 |
| 页面级 padding | 24（左右）/ 40 / 80（上下首屏） |
| 段落之间（长文） | 16 / 20 |

---

## 4. 圆角阶梯 ★（Radius · 本模块核心改动）

> 源规范 v2.3 主张「2px 唯一锐角」；本模块改为 **5 阶阶梯**。阶梯外圆角值**禁止出现**。
> 表格 / 分隔器 / 整页区块保持直角 `0`，不参与本阶梯。

### 4.1 阶梯定义与用途映射

| 阶 | 值 | Token | 用途 |
|---|---|---|---|
| 最小（少数） | **2px** | `--radius-xs` | 滚动条滑块、进度条填充 |
| 常用（主力） | **4px** | `--radius`（base） | 按钮、输入框、标签、chip、tab、CTA、二级菜单项 |
| 卡片 | **8px** | `--radius-card` | 卡片 / 面板 / 横幅 / composer / 下拉浮层 / banner |
| 胶囊（克制） | **999px** | `--radius-pill` | 筛选、分页圆点、微型计数 / 状态徽章（tab 计数「24」、fresh 徽章、skill-level） |
| 圆形 | **50%** | `--radius-circle` | 头像、状态圆点 |

```css
:root {
  --radius-xs: 2px;       /* 最小（少数） */
  --radius: 4px;          /* 常用（主力）· base */
  --radius-card: 8px;     /* 卡片 */
  --radius-pill: 999px;   /* 胶囊（克制） */
  --radius-circle: 50%;   /* 圆形 */
}
```

> shadcn / Tailwind v4 映射见 `Paper_V1.tweakcn.css`：
> `--radius-sm`=2px · `--radius-md`=4px · `--radius-lg`/`--radius-xl`=8px · `--radius-pill`=999px。

### 4.2 组件圆角分配（源规范 `2px` → 新阶梯迁移表）

| 组件 | 源规范圆角 | 新圆角 | 阶位 |
|---|---|---|---|
| 滚动条滑块 `.scroll::-webkit-scrollbar-thumb`、进度条填充 | 2px | **2px** | 最小 |
| 按钮 `.btn` / `.btn-primary` / `.btn-ghost` / `.btn-danger` / CTA | 2px | **4px** | 常用 |
| 输入框 `.input` / textarea / select / `.checkbox` | 2px | **4px** | 常用 |
| 标签 `.pill` / chip / `.cite`（内联引用） | 2px | **4px** | 常用 |
| Tab `.tab`（焦点 / hover 底） | 2px | **4px** | 常用 |
| 二级菜单项 `.dropdown-item` | 2px | **4px** | 常用 |
| 行内 `code` / `.mark` 高亮 | 2px | **4px** | 常用 |
| Tooltip `.tooltip`（紧凑浮层标签） | 2px | **4px** | 常用 |
| 卡片 `.card` / `.card-emphasis` / `.card-info` | 2px | **8px** | 卡片 |
| 下拉浮层 `.dropdown-panel` / `.popover` / `.cite-card` | 2px | **8px** | 卡片 |
| 模态 / 抽屉 `.modal` / `.drawer` | 2px | **8px** | 卡片 |
| Banner / 横幅 / Toast `.toast` | 2px | **8px** | 卡片 |
| Composer（输入合成区） | 2px | **8px** | 卡片 |
| 消息气泡 `.msg--user` / `.msg--ai` / `.msg--system` | 2px | **8px** | 卡片 |
| 代码块 `pre` / `.dropzone` / 引述 `.quote`（右侧角） | 2px | **8px** | 卡片 |
| `.badge-live`（运行中 / live 徽章） | 10px | **999px** | 胶囊 |
| 置信度 `.trust` 徽章 / 微型计数（tab 计数、fresh、skill-level） | 2px | **999px** | 胶囊 |
| 筛选 chip / 分页圆点 / Switch 轨道 `.switch-track` | 2px / 10px | **999px** | 胶囊 |
| 头像 / 状态圆点 `.list-item-dot` / Radio `.radio` / Switch 滑块 / `.timeline-num` | 50% | **50%** | 圆形 |
| 表格 `.table` / 分隔器 / 整页区块 | 0 | **0** | 直角（不参与阶梯） |

> **判定原则**：控件（可点击 / 可输入的原子元素）→ 4px；容器（卡片 / 面板 / 浮层 / 长内容块）→ 8px；纯计数 / 状态徽章 / 筛选 / 分页圆点 → 999px；正圆元素（头像 / 状态点）→ 50%；结构性满幅块（表格 / 整页）→ 0。

---

## 5. 阴影（Shadow · 中性墨黑投影）

阴影**唯二合法**，全部使用中性墨黑色，**不使用品牌色环**：

| Token | 值 | 用途 | 唯一允许组件 |
|---|---|---|---|
| `--shadow-overlay` | `0 8px 24px rgba(0,0,0,.08)` | 浮层投影 | `.dropdown-panel` / `.popover` / `.tooltip` |
| `--shadow-modal` | `0 20px 60px rgba(0,0,0,.12)` | 模态投影 | `.modal` / `.drawer` |

Focus 焦点指示（独立工具 token，非阴影阶梯成员，仅 `:focus-visible`）：
```css
--shadow-focus: 0 0 0 2px rgba(26,35,50,.12), 0 1px 4px rgba(26,35,50,.08);
```

> 任何「卡片悬浮 / 按钮按下」类阴影一律视为反模式。

---

## 6. 动效 / 层级 / 断点 / 栅格 / 图标

### 6.1 时序与缓动（Motion）

| Token | 时长 | 用途 |
|---|---|---|
| `--t-fast` | .12s | 高频小元素：dropdown-item / list-item |
| `--t-base` | .15s | 标准控件：btn / card / input |
| `--t-mid` | .22s | 列表入场：slideUp |
| `--t-slow` | .35s | 浮层 fade / modal |
| `--ease` | `cubic-bezier(.2,0,0,1)` | 默认缓动 |
| `--ease-out` | `cubic-bezier(.16,1,.3,1)` | 重场出场 |

> `transition: all .3s ease-in-out` 一律拒绝；只能引用上述 token 且显式列出过渡属性。已实现 `prefers-reduced-motion` 降级。

### 6.2 z-index 阶梯

```css
--z-base: 0; --z-sticky: 50; --z-overlay: 100; --z-modal: 200; --z-toast: 300;
```

### 6.3 断点（Breakpoints）

```css
--bp-sm: 640px; --bp-md: 960px; --bp-lg: 1280px; --bp-xl: 1600px;
```
> 90% 用户在 1280–1600px 阅读论文。`< 960px` 三栏折叠为两栏，`< 640px` 折叠为单栏 + 抽屉。

### 6.4 栅格（Grid）

| 场景 | 列数 | 槽宽 | 容器 |
|---|---|---|---|
| 三栏工作区 | `260px / 1fr / 1fr` 或 `280px 1fr` | 0（用 `border-right` 分隔） | `100vw` |
| 长文阅读 | 1 列 | — | `max-width: 720–780px` |
| 卡片网格 | 2 / 3 / 4 列响应 | 12 / 14 | `max-width: 1180px` |
| Hero / 表单中心 | 1 列 | — | `max-width: 680px` |

### 6.5 图标系统

- 来源 Lucide 风格 / `stroke-width: 1.8` / 无填充 / `stroke: currentColor`。
- 尺寸阶梯仅四档：`12`（pill / inline）· `14`（btn / input / 默认）· `16`（section header / list 前导）· `20`（empty state / dialog）。
- **禁止**用 `fill` 表达层级；**禁止**用 emoji 充当图标。

---

## 7. 对比度承诺（WCAG · 暖纸）

| 配色 | 对比度 | 等级 | 允许用途 |
|---|---|---|---|
| `--ink` on `--paper` | 13.5:1 | AAA | 主文字 |
| `--ink-soft` on `--paper` | 8.2:1 | AAA | 次级文字 |
| `--ink-mute` on `--paper` | 4.6:1 | AA | 辅助文字 |
| `--ink-faint` on `--paper` | 2.9:1 | ❌ 未达 AA | **仅非关键信息**（label / placeholder / 计数） |
| `--vermilion` on `--paper` | 5.8:1 | AA | 链接、激活态、强调 |
| `#fff` on `--vermilion` | 5.6:1 | AA | 主按钮文字 |

> **严格约束**：`--ink-faint` 不允许承载用户必须理解才能完成任务的文字。
> 所有可交互元素必须显式声明 `:focus-visible` 焦点环（`--shadow-focus`）；键盘 Tab 顺序遵循 DOM 顺序。

---

## 8. 反模式登记表（暖纸 + 新圆角）

| ❌ 反模式 | ✅ 规范实现 |
|---|---|
| 圆角随手取 6 / 10 / 12 / 16px | 归类至 5 阶：2 / 4 / 8 / 999px / 50% |
| 控件（按钮 / 输入 / tab）用 2px | 控件统一 **4px**（最小 2px 仅留给滚动条 / 进度条） |
| 卡片 / 浮层 / 模态用 4px | 容器统一 **8px** |
| 状态徽章 / 筛选 chip 用 4px 直角感 | 微型计数 / 状态 / 筛选用 **999px 胶囊** |
| 头像 / 状态点用 8px | 正圆元素用 **50%** |
| 主色随意挑（`#3b82f6` / `#2563eb`） | `var(--vermilion)` |
| 录制红写成 `#e74c3c` 字面量 | `var(--rec-red)` |
| 标签写成 `<h3 style="font-size:14px">` | mono uppercase 11–12 + `letter-spacing: .18em` |
| 按钮 hover 改 `border-color` / `transform` | hover 仅 `background → paper-warm` |
| 主操作按钮用朱砂蓝填充 | 主操作 = 墨色 Solid + 白字；朱砂蓝降为次级操作 `.btn-secondary`（§1.9） |
| 卡片 / 按钮 `box-shadow` | flat 默认；shadow 仅 §5 两类 |
| 重音用 `background: rgba(vermilion,.1)` 全填充 | 仅 `border-left: 3px solid var(--vermilion)` |
| 中文单独指定 PingFang | 让 Inter 走 fallback |
| placeholder 使用 italic | `font-style: normal` |
| `transition: all .3s ease-in-out` | 引用 §6.1 token + 显式属性 |
| Cormorant 复用至 nav / 标题 | Cormorant Italic 仅 Logo |
| Noto Serif 标题用 `font-weight: 700` | 永远 600 |
| emoji 充当 icon | Lucide 风格 SVG `stroke-width: 1.8` |
| 自由发明 z-index 数字 | 引用 `--z-*` 阶梯 |
| AI 消息缺左朱砂带 / 缺 `--ai-tint` 底 | `.msg--ai` 必须二者皆有 |
| 引用写成 `[1]` 纯文本上标 | 用 `.cite` 组件 + `.cite-card` 浮层 |
| 用色相单独区分 success / error | 必须同时附图标 |
| `--ink-faint` 承载关键信息 | 仅非关键信息使用（§7） |
| 用 dashed 边表达任意分隔 | dashed **仅** `.dropzone` 使用 |

---

## 9. 一致性验收 Checklist

**视觉签名**
- [ ] 整页背景为暖米色 `#fdfcf8`，**非**纯白
- [ ] 圆角全部落在 5 阶（2 / 4 / 8 / 999px / 50%），无阶梯外值
- [ ] 控件 4px、容器 8px、徽章/筛选 999px、头像/状态点 50%、滚动条/进度条 2px、表格 0
- [ ] 主色 `#1554a8` 仅用于关键操作与重音
- [ ] 卡片 / 按钮无 `box-shadow`（仅 §5 两类例外）
- [ ] 至少一处「mono uppercase + .18em letter-spacing」label

**排版**
- [ ] Logo 为 Cormorant Italic 22 / 500，em 朱砂正体 600
- [ ] Noto Serif SC 标题永远 600；元信息为 JetBrains Mono Uppercase
- [ ] 中文未单独指定字体；placeholder 不使用 italic

**重音 / 交互**
- [ ] 自陈重音 = `border-left: 3px solid var(--vermilion)`；引述他者 = `border-left: 2px solid var(--ink-faint)`
- [ ] 90% 的 hover 表达为 `background → paper-warm`，无 `transform` / `box-shadow` 类反馈
- [ ] 所有可交互元素有 `:focus-visible` 焦点环；`--ink-faint` 仅承载非关键信息

**AI 模式**
- [ ] AI 消息有 `--ai-tint` + 朱砂左带；流式输出有 `.streaming` caret 或 `.typing-dots`
- [ ] AI 输出可附 `.trust` 置信度（999px 胶囊）；引用使用 `.cite` 组件

**反模式扫描**
- [ ] §8 表中每一项 ❌ 在最终代码中均不出现

---

## 10. 与 `Paper_V1.tweakcn.css` 的对应

| 本规范 token | tweakcn / shadcn 语义 token |
|---|---|
| `--paper` | `--background` |
| `--ink` | `--foreground` |
| `--paper-warm` | `--secondary` / `--accent` |
| `--paper-cool` | `--muted` / `--sidebar` |
| `--ink-mute` | `--muted-foreground` |
| `--vermilion-6` | `--primary` / `--ring` |
| `--rule` | `--border` / `--input` |
| `--error` | `--destructive` |
| `--radius`(4px) | `--radius` → `--radius-md` |
| `--radius-xs`(2px) | `--radius-sm` |
| `--radius-card`(8px) | `--radius-lg` / `--radius-xl` |
| `--radius-pill`(999px) | `--radius-pill` |

---

## 11. 已知缺口 Known Gaps

- 本模块仅覆盖**暖纸（Light · Warm）单主题** —— 冷纸（cool）与暖夜（dark）已剥离；如需多主题请回源规范 `discoveryos-style-guide.v2.3`。
- 组件**完整 CSS** 仍以源规范 §3 / §4 为准；本模块只重定义其**圆角阶位**（§4.2 迁移表）与 token 取值，未复制全部组件片段。
- 对比度数值为标称近似值，落地前请以对比度工具复核（尤其 `--ink-faint` 与各语义 `*-fg`）。
- 圆角 5 阶为本模块相对源规范的立场改动；若需与源规范「2px 唯一」并轨，须显式声明版本差异。
- §1.9 操作按钮层级（主操作 = 墨色 / 次级 = 朱砂蓝 / 新增 `.btn-secondary`）以本平台 Figma `§3.1 BUTTON FAMILY` 现状为准，区别于源规范 v2.3（其 `.btn-primary` 为朱砂底、且无 `.btn-secondary`）；CSS 侧以新增 `--btn-*` token 表达，未改动 shadcn `--primary`（仍为朱砂，承担品牌强调 / ring）。
