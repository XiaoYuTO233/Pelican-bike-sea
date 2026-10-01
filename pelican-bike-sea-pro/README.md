# Pelican Bike 🐦🚲

一只鹈鹕骑着自行车在海边兜风的 2D SVG 动画。纯手绘、零依赖 —— 只用原生 HTML + SVG + CSS 实现，不依赖任何外部库、图片素材或构建工具。

## ✨ 特性

- **骑行系统**：车轮匀速旋转、曲柄交替蹬踏（两条腿相位差 180°）、车身随节奏弹跳摇摆
- **鹈鹕细节**：白色身体、会开合的大喉囊、拍打的翅膀、摇摆的尾羽和呆毛
- **趣味彩蛋**：嘴里叼着一条挣扎摆动的小鱼，鱼尾快速摆动
- **海滨场景**：飘动的云、拍翅飞过的海鸥、起伏的海浪、闪烁的波光、摇晃的小帆船、旋转的太阳光芒
- **速度感**：后退的道路虚线、车后掠过的速度线
- **交互控制**：一键暂停 / 播放全部动画

## 🗂 文件结构

```
pelican-bike-sea-pro/
└── index.html    # 全部内容（结构 + 样式 + 动画）都在一个文件里
```

## 🚀 使用方法

无需安装任何依赖，直接用浏览器打开 `index.html` 即可：

```bash
start index.html   # Windows
open index.html    # macOS
```

也可以搭配任意静态服务器（如 VS Code 的 Live Server）预览。

## 🎨 动画实现

| 动画 | 技术 |
| --- | --- |
| 车轮 / 曲柄旋转 | CSS `@keyframes spin`，围绕局部坐标原点 |
| 车身弹跳 | `@keyframes bob` + `transform-box: fill-box` |
| 翅膀拍打、喙开合、鱼尾摆动 | 各自局部坐标系下的 `rotate` 关键帧 |
| 云、海鸥横向移动 | `translateX` 线性循环，负延迟错开相位 |
| 道路虚线后退 | `stroke-dashoffset` 无缝循环 |
| 暂停 / 播放 | 切换 `body.paused` 类，统一控制 `animation-play-state` |

关键技巧：旋转类动画元素都放在一层 `<g transform="translate(...)">` 定位、内层 `<g>` 做 CSS 旋转，从而围绕任意锚点（轮心、中轴、肩部等）旋转。

## 📄 许可

MIT License
