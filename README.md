# SnapPolish

**Clipboard-first screenshot beautifier for polished sharing.**

[Add a screenshot of the tool here if you have one]

## Overview

SnapPolish is a lightweight, single-file frontend tool designed to turn raw screenshots into polished visuals instantly. It focuses on privacy and speed—running entirely in your browser with no server uploads.

## Features

- **Clipboard-First**: Paste screenshots directly (`Cmd/Ctrl + V`).
- **Privacy Focused**: 100% client-side processing. Your images never leave your browser.
- **Real-time Customization**:
  - Beautiful background presets (Liquid gradients, Apple-style, etc.)
  - Adjustable padding, border radius, and shadows.
- **High-Quality Export**:
  - Copy to clipboard as PNG (perfect for Twitter/X, Slack, Notion).
  - Download as high-res PNG.
- **Lightweight**: Zero dependencies using CDN for Tailwind CSS and html2canvas.

## Tech Stack

- **HTML5 & Vanilla JS**
- **Tailwind CSS** (via CDN)
- **html2canvas** (for rendering)

## Usage

### 1. Run Locally

Simply open `index.html` in your browser.

> **Note**: For the best experience with clipboard permissions, it is recommended to serve the file via a local server rather than `file://` protocol.

```bash
# Example using npx and serve
npx serve .
```

### 2. Deployment

Since it's a static HTML file, you can deploy it anywhere:

- GitHub Pages
- Vercel
- Netlify

## License

MIT © [SnapPolish]
