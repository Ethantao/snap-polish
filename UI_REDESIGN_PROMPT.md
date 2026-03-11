---
title: SnapPolish UI 功能点分析 & 重设计 Prompt
date: 2026-03-05
project: snap-polish
type: design-brief
tags:
  - ui-redesign
  - screenshot-tool
  - prompt
description: SnapPolish 网页截图美化工具的 UI 功能点拆解与 AI 重设计 Prompt
---

# SnapPolish UI 功能点分析 & 重设计 Prompt

## 当前 UI 功能点清单

### 🖼️ 1. 图片输入区域（Preview Stage）

- **剪贴板粘贴**：全局监听 `Cmd/Ctrl + V`，直接从剪贴板导入截图
- **文件上传**：点击 "Upload" 按钮手动上传图片
- **空状态引导**：无图片时展示虚线边框占位卡片 + 文字提示 + 上传按钮
- **实时预览**：棋盘格透明背景上实时展示带边框/阴影/圆角的截图
- **预览画布自适应**：图片居中显示，外层可滚动

### 🎨 2. 背景选择器（Background Presets）

9 种预置背景，每种以色块按钮展示：

| 类型 | 名称 |
|------|------|
| 液态渐变 | Liquid Aurora、Liquid Candy、Liquid Neon |
| Apple 风格 | Apple Bloom |
| 纯暗色 | Midnight、Graphite |
| macOS 风格 | macOS Light、macOS Dark |
| 透明 | Transparent |

- 选中态：`ring` 高亮环
- 2 列网格布局，Transparent 跨 2 列

### 🎛️ 3. 参数调节滑块（4 个 Range Slider）

| 参数 | 范围 | 默认值 | 说明 |
|------|------|--------|------|
| Padding（边距） | 20–220px | 32px | 截图与背景框的内边距 |
| Frame Radius（背景圆角） | 0–80px | 24px | 外层背景框的圆角 |
| Screenshot Radius（截图圆角） | 0–56px | 12px | 截图本身的圆角 |
| Shadow（阴影） | 0–90 | 36 | 截图的投影深度 |

- 每个滑块右侧实时显示当前值
- 自定义滑块样式（渐变轨道 + 玻璃质感滑块头）

### 🔄 4. 重置功能（Reset）

- 一键恢复所有参数到默认值
- 带 Toggle 开关动画反馈（轨道变色 + 滑块位移）
- 配有文字说明

### 📤 5. 导出操作（Actions）

- **复制图片**：渲染为高清 PNG → 写入系统剪贴板（带 `pulse-ring` 成功动画）
- **下载 PNG**：渲染为高清 PNG → 触发浏览器下载
- 操作状态反馈文字（成功/失败/渲染中...）
- 按钮禁用态：无图片时自动禁用

### 🌐 6. 多语言切换（i18n）

- 中文 / English 双语切换
- localStorage 持久化语言偏好
- 所有 UI 文案动态切换

### 🎭 7. 视觉设计系统

- **暗色主题**：`bg-[#020617]` 深空背景
- **毛玻璃卡片**：`backdrop-blur-xl` + 半透明边框
- **背景光晕**：3 个绝对定位的模糊圆形光斑（`blur-3xl`）
- **入场动画**：`stagger-card` 交错 fade-up 动画
- **字体**：Space Grotesk（正文） + JetBrains Mono（等宽/数值）
- **布局**：桌面端左右分栏（预览区 + 侧边栏控制面板），移动端上下堆叠

---

## 重设计 Prompt

> 以下 prompt 可直接用于 AI 设计工具或 UI 开发：

```
Redesign the UI for "SnapPolish" — a clipboard-first screenshot beautifier web app. The app runs entirely in the browser (single HTML file, no backend). Here are the functional requirements to preserve:

**Core Workflow:**
1. User pastes a screenshot via Cmd/Ctrl+V or uploads an image file
2. The screenshot is displayed in a real-time preview area with a decorative background frame
3. User customizes the look using controls in a side panel
4. User exports the result by copying to clipboard (as PNG) or downloading as a high-res PNG file

**Feature Inventory:**
- Image input: clipboard paste (global Cmd/Ctrl+V listener) + file upload button
- Empty state: guided placeholder with instructions and upload CTA
- Background presets: 9 options — 3 liquid gradients, 1 Apple-style gradient, 2 dark solids, 2 macOS-style solids, 1 transparent — displayed as color swatch buttons in a 2-column grid
- 4 adjustment sliders with real-time preview:
  • Padding (20–220px): space between screenshot and background edge
  • Frame Radius (0–80px): corner radius of the background frame
  • Screenshot Radius (0–56px): corner radius of the screenshot itself
  • Shadow (0–90): depth of the drop shadow on the screenshot
- One-click reset to defaults (with toggle-switch animation feedback)
- Export actions: "Copy Image" (to clipboard as PNG) + "Download PNG", with status messages (success/error/loading)
- Bilingual support: Chinese / English toggle with localStorage persistence
- All controls update the preview in real time with smooth transitions

**Design Direction for Redesign:**
- Modern, premium dark-mode aesthetic (current: deep space dark with glassmorphism)
- Responsive layout: side-by-side on desktop (preview left, controls right), stacked on mobile
- Use fluid animations and micro-interactions for a polished feel
- Background glow orbs or gradient mesh for visual depth
- Clean typography: a geometric sans-serif for headings, monospace for numeric values
- Controls should feel tactile: custom-styled range sliders, color swatch buttons with active ring indicators
- Action buttons should have distinct visual hierarchy (copy = primary green, download = secondary blue)
- Status feedback: inline text with color-coded tones (success/error/default)
- Staggered entrance animations for card sections
- The preview area should use a checkerboard pattern for transparent backgrounds
- Footer with GitHub + X (Twitter) social links

**Tech Constraints:**
- Single HTML file with inline CSS and JS
- Tailwind CSS via CDN
- html2canvas for rendering
- No backend, no build tools, fully static
- Must support clipboard API (with Safari fallback handling)
```
