# 3d_interactive_particle_system
# 🪄 Cosmic Spark: AI Gesture-Controlled 3D Particle Mirror
### AI 手勢感應 3D 粒子魔鏡系統

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Three.js](https://img.shields.io/badge/Three.js-000000?style=for-the-badge&logo=three.js&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-4285F4?style=for-the-badge&logo=google&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)

本專案是一個基於**邊緣端 AI 電腦視覺（Edge AI）**與 **WebGL 3D 渲染技術**的網頁互動視覺藝術系統。使用者無需購買昂貴的外部硬體設備（如 Leap Motion），僅需透過標準家用視訊鏡頭（Webcam），即可利用「手掌張合」實時控制 15,000 個高畫質粒子的擴散、旋轉與形態演變。

## 🌟 核心特色

- **AI 即時手勢偵測**：整合 Google MediaPipe Hands，在網頁端高速估算手掌 21 個 3D 關鍵點骨架。
- **動態歸一化演算法**：自主設計 Palm-Size Metric 演算法，自動消除使用者離鏡頭遠近造成的辨識誤差。
- **15,000+ 粒子流暢形變**：利用 Three.js 的 `BufferGeometry` 將大量粒子封裝至 GPU 緩衝區，並使用 Additive Blending 創造極致的發光疊加效果。
- **6 種精美數學幾何幾何形態**：包含立體愛心（Volumetric Heart）、土星系統（Saturn）、幸運草（FlowerCurve）、3D 煙火（Fireworks）、經典星體（Sphere）以及高規格的**生物科技 DNA 雙螺旋（DNA Helix）**。
- **高完整度 UI/UX 介面**：採用 Glassmorphism（玻璃擬物化）風格控制面板，支援響應式網頁設計（RWD）、全螢幕模式，並在無相機時自動切換為「手勢模擬滑桿」。

---

## 🛠️ 技術架構

### 1. 手掌張合度計算演算法 (Normalized Openness)
為了實現精準的張合控制，系統以手腕（第 0 點）到中指根部（第 9 點）的 3D 歐式距離作為基準尺（$PalmScale$），並計算四指尖端到根部的相對比例，最後透過指數移動平均（EMA）進行平滑化過渡，公式如下：

```javascript
// 基線錨定消除前後距離誤差
const palmScale = getDistance3D(landmarks[0], landmarks[9]);
// 映射 [0.5, 1.1] 至 [0.0, 1.0] 的超靈敏響應區間
let normValue = (avgRatio - 0.5) / 0.6;
normValue = Math.max(0.0, Math.min(1.0, normValue));
