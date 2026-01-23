# RAMS.css Design System PRD

> **Product Requirements Document**  
> Version: 1.0  
> Last Updated: 2026-01-23  
> Status: Ready for Implementation

---

## Executive Summary

本文档定义了 **RAMS.css** —— 一套致敬 Dieter Rams 在 Braun 时期工业设计语言的数字设计系统。目标是将实体硬件的质感、交互逻辑和视觉语言转译为可复用的 Web 组件库，使开发者能够构建具有"硬件整体感"的数字界面。

**核心定位**: 介于 Skeuomorphism（拟物主义）与 Flat Design（扁平设计）之间的"New Physicality"——保留物理隐喻的功能性，但以现代技术栈实现。

---

## 1. Background & Motivation

### 1.1 设计哲学来源

Dieter Rams 在 Braun 的设计工作（1961-1995）定义了现代工业设计的范式。其著名的 **"Good Design 10 Principles"** 中，与本设计系统最相关的原则包括：

| 原则 | 在数字设计中的转译 |
|------|-------------------|
| Good design is innovative | 用 CSS 技术突破传统 UI 组件的视觉边界 |
| Good design makes a product useful | 组件的视觉设计服务于功能可见性（affordance） |
| Good design is aesthetic | 追求视觉上的精致与克制 |
| Good design is honest | 不伪装功能，按钮看起来像按钮，屏幕看起来像屏幕 |
| Good design is as little design as possible | 移除所有非必要的视觉元素 |

### 1.2 为什么现在需要这套设计系统

1. **Flat Design 的审美疲劳** — 过度扁平化导致界面缺乏层次和触感
2. **AI 生成界面的同质化** — 需要有强烈视觉特征的设计语言来区分
3. **硬件复兴趋势** — Teenage Engineering、Playdate 等产品证明了"硬件美学"在数字时代的吸引力
4. **Bento Grid 布局的流行** — 需要配套的组件系统来填充这种模块化布局

### 1.3 参考案例

- **Primary Reference**: https://drams.framer.website/ （Dieter Rams tribute site）
- **Visual Reference**: 小红书用户"鹿言"的 Braun Skeuomorphic Icon 系列（见附录图片）
- **Technical Reference**: 
  - Apple's system.css（系统级设计令牌）
  - Vercel's Geist Design System（组件架构）
  - Teenage Engineering's visual language（硬件美学转数字）

---

## 2. Visual Analysis — 从参考图片提取设计语言

### 2.1 图片素材清单

本设计系统基于以下参考图片进行视觉元素提取：

| 图片 | 内容 | 提取的关键元素 |
|------|------|----------------|
| ventilator.jpg | Braun 风扇 | 圆形网格穿孔、橙色电源按钮、product label 排版 |
| clock.jpg | 数字时钟 | LCD 屏幕、七段数字、多时区显示、侧边开关 |
| tuner.jpg | 收音机调谐器 | 大旋钮、FM/AM 按钮、频率显示 |
| speaker.jpg | 扬声器 | 矩形网格穿孔、品牌标识位置 |
| camera.jpg | 相机 | 镜头环、取景器、快门按钮 |
| collection.jpg | 产品全家福 | 整体设计语言一致性、产品线视觉系统 |
| isometric.jpg | 等轴测视图集 | 3D 形态、阴影方向、产品比例 |
| in-framer.jpg | 自制致敬作品 | 点阵显示、中文日期、"DRAUN In Framer"变体 |

### 2.2 色彩系统提取

#### 主色板 — 暖灰系列（设备外壳）

```
从图片中使用取色器提取的精确色值：

┌─────────────────┬───────────┬────────────────────────────────────┐
│ Token Name      │ Hex       │ Usage                              │
├─────────────────┼───────────┼────────────────────────────────────┤
│ --rams-white    │ #FAFAF8   │ 背景、高光区域                      │
│ --rams-cream    │ #F5F3EF   │ 页面背景、卡片背景                  │
│ --rams-shell    │ #E8E4DE   │ 设备外壳主色（最重要）              │
│ --rams-shell-dark│ #D9D4CC  │ 设备外壳暗部、渐变终点              │
│ --rams-warm-gray│ #C4BEB5   │ 次要元素、旋钮底色                  │
│ --rams-mid-gray │ #9A958C   │ 文字次要色、禁用状态                │
│ --rams-dark-gray│ #5C5854   │ 文字主色、图标                      │
│ --rams-charcoal │ #3A3835   │ 深色背景、网格穿孔内部              │
│ --rams-black    │ #1A1918   │ 最深色、强调文字                    │
└─────────────────┴───────────┴────────────────────────────────────┘
```

**色彩特征分析**：
- 所有灰色都带有轻微的暖色调（黄/橙底色），这是 Braun 产品的标志性特征
- 色彩过渡非常微妙，相邻色阶之间的差异约为 5-8% 明度
- 不使用纯灰（#808080 等），所有灰色都经过"染色"

#### 强调色 — Braun Orange

```
┌─────────────────────┬───────────┬────────────────────────────────┐
│ Token Name          │ Hex       │ Usage                          │
├─────────────────────┼───────────┼────────────────────────────────┤
│ --rams-orange-light │ #FF7F54   │ 按钮悬停、高光                  │
│ --rams-orange       │ #FF5F2E   │ 主强调色、CTA按钮               │
│ --rams-orange-dark  │ #E54A1A   │ 按钮按下、渐变暗部              │
│ --rams-orange-glow  │ rgba(255,95,46,0.3) │ 发光效果、阴影      │
└─────────────────────┴───────────┴────────────────────────────────┘
```

**橙色使用原则**：
- 仅用于主要交互元素（电源按钮、主 CTA）
- 每个设备/卡片中最多出现 1-2 个橙色元素
- 橙色元素应该是用户视觉焦点的落点

#### LCD 屏幕色

```
┌─────────────────────┬───────────┬────────────────────────────────┐
│ Token Name          │ Hex       │ Usage                          │
├─────────────────────┼───────────┼────────────────────────────────┤
│ --rams-lcd-bg       │ #C5CDB8   │ LCD 屏幕背景（标志性绿）        │
│ --rams-lcd-segment  │ #2D3A2A   │ LCD 数字/文字（激活状态）       │
│ --rams-lcd-segment-off │ rgba(45,58,42,0.08) │ LCD 数字（未激活） │
└─────────────────────┴───────────┴────────────────────────────────┘
```

### 2.3 形态语言提取

#### 圆角半径系统

```
观察图片中的设备，圆角遵循以下规律：

设备外壳外圆角: 约 28px (--radius-device)
设备外壳内圆角: 约 20px (--radius-device-inner)
屏幕圆角: 约 12px (--radius-screen)
按钮圆角: 50% / 完全圆形 (--radius-button)
小组件圆角: 8px (--radius-md)

关键洞察：内部元素的圆角总是小于容器圆角，形成视觉"嵌套"感
```

#### 阴影系统

Braun 产品的实体感来自精细的光影处理。在数字界面中，需要多层阴影来模拟：

```css
/* 设备外壳阴影 - 5层渐进式 */
--shadow-device: 
    0 1px 1px rgba(0,0,0,0.02),   /* 接触阴影 */
    0 2px 4px rgba(0,0,0,0.03),   /* 近距离柔和阴影 */
    0 8px 16px rgba(0,0,0,0.04), /* 中距离扩散 */
    0 16px 32px rgba(0,0,0,0.05), /* 远距离大面积 */
    0 32px 64px rgba(0,0,0,0.06); /* 环境光遮蔽 */

/* 按钮阴影 - 带内发光 */
--shadow-button: 
    0 2px 4px rgba(0,0,0,0.1),
    0 4px 8px rgba(0,0,0,0.08),
    inset 0 1px 0 rgba(255,255,255,0.3); /* 顶部高光 */

/* 凹陷效果（屏幕、滑槽） */
--shadow-inset-screen: 
    inset 0 2px 4px rgba(0,0,0,0.08),
    inset 0 0 0 1px rgba(0,0,0,0.05);
```

#### 边缘高光

所有 Braun 产品都有微妙的边缘高光，模拟塑料外壳的反光。在 CSS 中通过 pseudo-element 实现：

```css
.device::before {
    content: '';
    position: absolute;
    inset: 0;
    border-radius: inherit;
    padding: 1px;
    background: linear-gradient(
        145deg,
        rgba(255,255,255,0.4) 0%,   /* 左上高光 */
        rgba(255,255,255,0.1) 50%,
        rgba(0,0,0,0.05) 100%       /* 右下暗角 */
    );
    -webkit-mask: linear-gradient(#fff 0 0) content-box, 
                  linear-gradient(#fff 0 0);
    mask-composite: exclude;
}
```

### 2.4 排版系统

#### 品牌字体

```
BRAUN logo 特征：
- 全大写
- 字重: Bold (700)
- 字间距: 0.15em (较宽)
- 特殊处理: 'A' 字母无横杠（品牌标识）

在 CSS 中，我们无法精确复刻无横杠的 A，但可以通过字体选择和 letter-spacing 接近原效果。
推荐字体: DM Sans (Google Fonts) - 几何感强，接近 Braun 使用的 Futura
```

#### 产品标签

```
Product label 特征（如 "ventilator 1", "tuner 1"）：
- 全小写
- 字重: Regular (400)
- 字间距: 0.05em
- 字号: 极小（约 10-12px）
- 位置: 设备右下角
```

#### LCD 字体

```
LCD 数字特征：
- 七段显示器风格
- 等宽
- 字重: Bold
- 推荐: Space Mono 或专用的 DSEG 字体
```

### 2.5 网格穿孔图案

扬声器和风扇的网格穿孔是 Braun 产品的视觉签名：

```
方形网格（扬声器）：
- 孔形状: 圆角矩形（radius 1-2px）
- 孔尺寸: 约 6x6px
- 孔间距: 约 3px
- 排列: 规则正交网格

圆形网格（风扇）：
- 容器: 正圆形
- 孔排列: 同心圆或正交网格裁切为圆形
- 孔密度: 中等（约 40-50% 开孔率）

实现方式：
1. CSS Grid + 循环生成 div
2. SVG pattern
3. CSS background-image (radial-gradient repeat)
```

---

## 3. Technical Specification

### 3.1 技术栈选择

| 层面 | 推荐技术 | 备选 | 理由 |
|------|---------|------|------|
| 核心样式 | Pure CSS (CSS Variables) | SCSS/Sass | 最大兼容性，无编译依赖 |
| 组件框架 | Vanilla JS | React/Vue | 保持轻量，可被任何框架包装 |
| 构建工具 | None (single file) | Vite | 便于分发和 CDN 引用 |
| 字体 | Google Fonts CDN | Self-hosted | 快速接入 |

### 3.2 文件结构

```
rams-css/
├── rams.css              # 完整单文件版本（推荐）
├── rams.min.css          # 压缩版本
│
├── src/                  # 源码拆分版本（可选）
│   ├── tokens/
│   │   ├── colors.css
│   │   ├── typography.css
│   │   ├── spacing.css
│   │   └── shadows.css
│   ├── base/
│   │   ├── reset.css
│   │   └── typography.css
│   ├── components/
│   │   ├── device.css
│   │   ├── button.css
│   │   ├── screen.css
│   │   ├── knob.css
│   │   ├── grille.css
│   │   ├── switch.css
│   │   ├── slider.css
│   │   └── input.css
│   └── layouts/
│       └── bento.css
│
├── examples/
│   ├── clock.html
│   ├── tuner.html
│   ├── calculator.html
│   └── dashboard.html
│
└── docs/
    └── index.html        # 交互式文档
```

### 3.3 CSS 命名规范

采用 **BEM-like** 命名，但以 `rams-` 为前缀：

```
组件: .rams-{component}
    例: .rams-device, .rams-btn, .rams-screen

修饰符: .rams-{component}--{modifier}
    例: .rams-btn--lg, .rams-screen--dark

子元素: .rams-{component}-{element}
    例: .rams-device-switch, .rams-slider-thumb

状态: .is-{state}
    例: .is-on, .is-active, .is-disabled
```

### 3.4 响应式断点

```css
/* 移动优先 */
--breakpoint-sm: 640px;   /* 小屏手机 → 大屏手机 */
--breakpoint-md: 768px;   /* 手机 → 平板 */
--breakpoint-lg: 1024px;  /* 平板 → 桌面 */
--breakpoint-xl: 1280px;  /* 桌面 → 大屏 */
```

Bento Grid 响应式行为：
- `< 640px`: 单列
- `640px - 1024px`: 2列
- `> 1024px`: 4列

---

## 4. Component Specification

### 4.1 Device Shell（设备外壳）

**用途**: 所有硬件风格组件的容器

**HTML 结构**:
```html
<div class="rams-device">
    <div class="rams-device-switch"></div> <!-- 可选：侧边开关 -->
    <!-- 内容区域 -->
</div>
```

**变体**:
| Class | 描述 |
|-------|------|
| `.rams-device` | 默认尺寸 |
| `.rams-device--sm` | 小尺寸（padding 减少） |
| `.rams-device--lg` | 大尺寸（padding 增加） |

**视觉要求**:
- 背景: 145° 渐变，从 `--rams-shell` 到 `--rams-shell-dark`
- 圆角: `--radius-device` (28px)
- 阴影: `--shadow-device`
- 边缘高光: pseudo-element gradient border
- 悬停: 向上位移 4px + 阴影加深

### 4.2 Physical Button（物理按钮）

**用途**: 主要交互元素，模拟实体按钮的按压感

**HTML 结构**:
```html
<button class="rams-btn-physical"></button>
```

**变体**:
| Class | 尺寸 |
|-------|------|
| `.rams-btn-physical--sm` | 32x32px |
| `.rams-btn-physical` | 56x56px（默认） |
| `.rams-btn-physical--lg` | 80x80px |
| `.rams-btn-physical--xl` | 120x120px |
| `.rams-btn-physical--gray` | 灰色变体 |

**交互状态**:
- Default: 凸起感，顶部高光
- Hover: 向上位移 1px，阴影扩大
- Active: 向下位移 1px，阴影变为 inset

**视觉要求**:
- 形状: 完美圆形
- 背景: 145° 渐变，橙色三阶（light → base → dark）
- 顶部高光: pseudo-element 椭圆形白色渐变
- 阴影: 带有橙色色调的 drop-shadow + inset 高光

### 4.3 LCD Screen（液晶屏幕）

**用途**: 显示数字、文字等信息

**HTML 结构**:
```html
<div class="rams-screen">
    <span class="rams-lcd-text rams-lcd-text-lg">10:45</span>
</div>
```

**变体**:
| Class | 描述 |
|-------|------|
| `.rams-screen` | 默认 LCD 绿色背景 |
| `.rams-screen--glow` | 带发光效果 |
| `.rams-screen--scanlines` | 带扫描线效果 |
| `.rams-screen--dark` | 深色背景（如 OFFLINE 状态） |

**文字变体**:
| Class | 字号 |
|-------|------|
| `.rams-lcd-text` | 默认 |
| `.rams-lcd-text-lg` | 2.441rem |
| `.rams-lcd-text-xl` | 3.052rem |

### 4.4 Knob/Dial（旋钮）

**用途**: 连续值调节（音量、频率等）

**HTML 结构**:
```html
<div class="rams-knob"></div>
```

**变体**:
| Class | 描述 |
|-------|------|
| `.rams-knob` | 灰色旋钮 |
| `.rams-knob--orange` | 橙色旋钮 |

**交互**:
- 需要 JS 处理拖拽旋转
- 旋转时应用 CSS transform: rotate()
- 可选：添加物理惯性动画

### 4.5 Speaker Grille（扬声器网格）

**用途**: 装饰性元素，模拟扬声器/散热孔

**实现方式 1 — CSS Background**:
```css
.rams-grille--dots {
    background-image: radial-gradient(
        circle at center,
        var(--rams-charcoal) 3px,
        transparent 3px
    );
    background-size: 12px 12px;
}
```

**实现方式 2 — DOM Elements**:
```html
<div class="rams-grille rams-grille--square" style="--grille-cols: 14;">
    <!-- 通过 JS 生成 14*N 个 .hole 元素 -->
    <div class="rams-grille-hole"></div>
    ...
</div>
```

### 4.6 Switch（开关）

**用途**: 二元状态切换

**HTML 结构**:
```html
<div class="rams-switch"></div>
<div class="rams-switch is-on"></div>
```

**交互**: 点击切换 `.is-on` class

### 4.7 Bento Grid（便当网格）

**用途**: 模块化布局容器

**HTML 结构**:
```html
<div class="rams-bento">
    <div class="rams-bento-item">1x1</div>
    <div class="rams-bento-item rams-bento-item--2x1">2x1</div>
    <div class="rams-bento-item rams-bento-item--2x2">2x2</div>
</div>
```

**Span 变体**:
| Class | Grid Span |
|-------|-----------|
| `.rams-bento-item` | 1x1（默认） |
| `.rams-bento-item--2x1` | 2列 1行 |
| `.rams-bento-item--1x2` | 1列 2行 |
| `.rams-bento-item--2x2` | 2列 2行 |
| `.rams-bento-item--3x1` | 3列 1行 |
| `.rams-bento-item--4x1` | 4列 1行（全宽） |

---

## 5. Prototype Devices — 高保真原型规格

以下设备应作为设计系统的"showcase"，证明组件的组合能力：

### 5.1 Digital Clock

```
功能要求：
- 显示当前时间（实时更新）
- 显示闹钟时间
- 显示世界时钟/秒表
- 底部功能图标

组件组合：
- rams-device (外壳)
- rams-device-switch (侧边开关)
- rams-screen (LCD 屏幕)
- rams-lcd-text (数字显示)
- SVG icons (底部控制)
```

### 5.2 Radio Tuner

```
功能要求：
- 频率显示（FM 87.5-108 MHz）
- 可拖拽旋转的调谐旋钮
- FM/AM 切换按钮

组件组合：
- rams-device
- rams-screen
- rams-knob--orange (大旋钮)
- custom band buttons
```

### 5.3 Calculator

```
功能要求：
- 基础四则运算
- 可点击的数字键盘
- 显示计算结果

组件组合：
- rams-device
- rams-screen (结果显示)
- custom keypad grid
```

### 5.4 Speaker

```
功能要求：
- 纯展示（无交互）
- 网格穿孔图案

组件组合：
- rams-device
- rams-grille--square
- rams-device-switch
```

### 5.5 Camera

```
功能要求：
- 可按压的快门按钮
- 镜头视觉效果

组件组合：
- rams-device
- custom lens element (多层圆形渐变)
- custom viewfinder
- rams-btn-physical (快门)
```

### 5.6 Ventilator

```
功能要求：
- 圆形网格
- 电源按钮

组件组合：
- rams-device
- rams-grille--circular
- rams-btn-physical
```

---

## 6. Implementation Guidelines

### 6.1 给 AI（Claude）的 Prompt 模板

```markdown
# Task: Generate RAMS.css Component

## Context
You are implementing a component for RAMS.css, a design system inspired by Dieter Rams' Braun product designs.

## Design Principles
1. "Less, but better" - Remove all unnecessary visual elements
2. Honest design - Buttons look pressable, screens look like displays
3. Warm gray palette with orange accent
4. Multi-layer shadows for physicality
5. Subtle gradients for depth

## Color Tokens (MUST USE)
--rams-shell: #E8E4DE (primary surface)
--rams-shell-dark: #D9D4CC (gradient end)
--rams-orange: #FF5F2E (accent)
--rams-lcd-bg: #C5CDB8 (screen background)
--rams-lcd-segment: #2D3A2A (screen text)

## Shadow Tokens (MUST USE)
Device shadows must use 5-layer progressive shadows
Button shadows must include inset highlight
Screen shadows must use inset shadows

## Requirements
- Pure CSS, no preprocessors
- Use CSS variables for all values
- BEM-like naming with `rams-` prefix
- Include hover and active states
- Support responsive behavior

## Output
Generate the CSS for [COMPONENT NAME] following the above guidelines.
```

### 6.2 给工程师的 Checklist

**视觉验收标准**:
- [ ] 所有灰色都带有暖色调（对比纯灰 #808080）
- [ ] 橙色元素不超过设计中的 1-2 处
- [ ] 设备外壳有可见的边缘高光
- [ ] 按钮有明显的凸起/按压反馈
- [ ] 屏幕有轻微的凹陷感
- [ ] 悬停时有微妙的位移动画

**代码质量标准**:
- [ ] 所有颜色使用 CSS 变量
- [ ] 所有尺寸使用 spacing tokens
- [ ] 支持 prefers-reduced-motion
- [ ] 通过 WCAG AA 对比度要求
- [ ] 无 !important 使用

---

## 7. Appendix

### 7.1 Reference Images Description

由于图片无法直接嵌入 Markdown，以下是对参考图片的详细文字描述：

**Image 1 - Ventilator**
- 正方形设备，约 280x280px 视觉比例
- 中心: 圆形网格（约 200px 直径），12x12 方孔排列
- 左下: "BRAUN" logo，全大写，黑色
- 右下: "ventilator 1" 标签，小写，灰色
- 右下角: 橙色圆形按钮（约 56px），带电源图标
- 左侧边缘: 橙色侧边开关条（约 8x40px）

**Image 2 - Digital Clock**
- 正方形设备
- LCD 屏幕占据上方 70% 区域
- 屏幕内容: 三行数字显示
  - 第一行: "10:00"（最大）
  - 第二行: "alarm" 标签 + "12 36"
  - 第三行: 闹钟图标 + "7:09"
- 底部: BRAUN logo + 三个控制图标
- 左侧: 橙色开关

**Image 3 - Radio Tuner**
- 横向矩形设备
- 上方: LCD 显示屏，显示 "8.0 MHz"
- 左下: 大号橙色旋钮（约 100px）
- 右下: FM/AM 两个橙色小按钮，垂直排列
- 底部: BRAUN logo + "tuner 1"

**Image 4 - Speaker**
- 竖向矩形设备
- 整个正面是网格穿孔（约 14 列 x 20 行）
- 方孔，深灰色/黑色
- 底部: 居中的 BRAUN logo
- 左侧: 橙色开关

**Image 5 - Camera**
- 正方形设备
- 顶部中央: 橙色快门按钮（凸出）
- 顶部右侧: 小取景器窗口
- 中央: 大号镜头环 + 深色镜头
- 底部: BRAUN + "photo 1"

**Image 6 - Product Collection**
- 20+ 产品的网格排列展示
- 包含: MP3播放器、游戏机、计算器、收音机、时钟、音箱、风扇、相机、微波炉、电饭煲、扫地机器人等
- 统一的设计语言: 暖灰外壳 + 橙色强调 + LCD 屏幕

**Image 7 - Isometric Collection**
- 等轴测视角的产品3D渲染
- 包含: 平板设备、蓝牙音箱、时钟、台灯、地球仪、耳机、收音机、露营灯、录音机等
- 展示产品的立体形态和阴影方向

**Image 8 - In Framer Tribute**
- 竖向矩形设备（类似手机/遥控器比例）
- 顶部: 圆形按钮 + LCD 显示 "OFFLINE" + 中文日期 "1月23日"
- 中央: 点阵显示区域（约 20x20）
- 底部: 大号灰色旋钮 + "DRAUN In Framer" 变体 logo
- 整体为深色主题变体

### 7.2 Color Extraction Notes

```
使用 Figma Eyedropper 从 Image 1 (Ventilator) 提取:

外壳背景亮部: #E8E4DE → --rams-shell
外壳背景暗部: #D9D4CC → --rams-shell-dark
橙色按钮高光: #FF7F54 → --rams-orange-light
橙色按钮中间: #FF5F2E → --rams-orange
橙色按钮暗部: #E54A1A → --rams-orange-dark
网格孔内部: #3A3835 → --rams-charcoal
BRAUN 文字: #1A1918 → --rams-black

从 Image 2 (Clock) 提取:

LCD 背景: #C5CDB8 → --rams-lcd-bg
LCD 数字: #2D3A2A → --rams-lcd-segment
```

---

## 8. Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-01-23 | Initial PRD release |

---

## 9. Contact & Ownership

**Design System Owner**: [Your Name]  
**Repository**: [TBD]  
**Documentation**: [TBD]

---

*"Weniger, aber besser" — Less, but better.*
