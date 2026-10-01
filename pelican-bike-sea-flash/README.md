# 鹈鹕骑自行车 · SVG 2D 动画

**Pelican Bike Sea Flash** —— 一个单文件的 SVG 2D 循环动画：一只鹈鹕骑着自行车在原野公路上飞驰，白天有阳光云朵，夜晚有星空月色，车灯照亮前方路面。

> 打开 `index.html` 即可观看，无需构建、无任何外部依赖。

## ✨ 功能特性

### 动画内容

- 🚲 车轮、曲柄与踏板持续旋转，双腿沿踏板圆周轨迹交替蹬踏（左右腿相位相差半圈）
- 🐦 鹈鹕：翅膀扑动、头部轻晃、整车轻微颠簸
- 🌄 背景循环：云朵漂移、太阳光芒缓转、公路虚线滚动、速度线与后轮扬尘

### 交互控制（页面底部悬浮控制条）

| 按钮 | 功能 |
| --- | --- |
| 🌙 切换到夜晚 / ☀️ 切换到白天 | 一键昼夜切换（0.8s 渐变过渡）：太阳淡出，月亮、星空、车灯淡入；车灯照亮前方路面 |
| ⏸ 暂停 / ▶️ 继续 | 冻结全部动画（星星闪烁同步暂停） |
| ⚡ 1× | 倍速循环切换：**1× → 2× → 3× → 0.5×** |

## 🚀 使用方式

用现代浏览器打开 `index.html` 即可：

- 双击文件，或拖拽到浏览器窗口
- 或在 VS Code 中使用 Live Preview 等扩展预览

无需安装依赖、无需本地服务器。

## 🛠 技术实现

- **绘制与动画**：纯 SVG + SMIL（`animate` / `animateTransform`），全部为声明式动画
- **暂停与倍速**：JS 接管 SMIL 时钟——先 `pauseAnimations()` 暂停浏览器时间线，再由 `requestAnimationFrame` 统一驱动 `setCurrentTime()` 推进；所有动画共用一个时钟，因此变速、暂停全局精确生效
- **昼夜切换**：CSS 过渡实现（与 SMIL 时钟相互独立，画面暂停时依然可以流畅切换）
- **星星闪烁**：CSS `@keyframes`；暂停时通过 `animation-play-state` 同步冻结
- **路面照明**：光束渐变（`beamGrad`）+ 落在地面的光斑（`roadLight` 径向渐变），随夜晚一起淡入淡出

## 📁 项目结构

```
pelican-bike-sea-flash/
└── index.html    # 全部内容：HTML + CSS + SVG + 原生 JS（单文件）
```

## 🎨 自定义指南

| 想调整 | 位置 |
| --- | --- |
| 倍速档位 | JS 中 `var speeds = [1, 2, 3, 0.5];` |
| 昼夜过渡时长 | CSS 中 `.sun, .moon, .stars, .veil, .headlight` 的 `transition: opacity 0.8s` |
| 骑行节奏 | SMIL 属性：车轮 `dur="1.4s"`、曲柄/蹬踏 `dur="1.1s"` |
| 夜晚暗度 | `#nightGrad` 渐变的 `stop-opacity`（越大越暗） |
| 车灯与光斑 | `.headlight` 分组内的光束路径、`roadLight` 光斑椭圆与 `#roadLight` 渐变 |

## 📱 兼容性

- Chrome / Edge / Firefox / Safari 等现代浏览器均可运行
- 依赖浏览器对 SVG SMIL 动画的支持（所有现代浏览器均支持）
