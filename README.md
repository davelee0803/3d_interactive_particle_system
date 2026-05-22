# 3D_interactive_particle_system
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


🚀 快速開始与運行
本專案為純前端架構（無後端依賴），您可以透過以下幾種方式直接運行：

方法一：直接雙擊打開
下載或 git clone 本專案。

在瀏覽器中直接雙擊打開 3d_interactive_particle_system.html 檔案。

允許瀏覽器使用您的相機鏡頭，即可開始互動。

方法二：使用 VS Code Live Server (推薦)
用 VS Code 打開專案資料夾。

安裝擴充功能 Live Server。

點擊右下角的 Go Live 啟動本地伺服器運行。

🎮 操作指南
開啟鏡頭：點擊右下角的「開啟鏡頭」按鈕並授權相機，上方狀態燈轉為綠燈即代表 AI 啟動成功。

手勢操作：

🖐️ 張開手掌：粒子系統將加速旋轉並向外大範圍擴散。

✊ 緊握拳頭：粒子系統將減速並向核心劇烈凝聚。

面板調控：

可自由切換 6 種幾何形態。

開啟/關閉「時光動態漸變」（HSL 彩虹色彩流）。

調整粒子尺寸、基礎旋轉速度。

點擊頂部功能列可隱藏視訊窗或切換至全螢幕模式。

📚 學習反思與收穫 (學習歷程)
跨領域技術整合：成功將「Edge AI 視覺辨識」與「WebGL 3D 渲染」串接，理解異步影像流（Async Frame）與 3D 渲染循環（Render Loop）的資料對接。

空間數學的實際應用：將課本上的三角函數、參數方程、三維空間向量與歐式距離，實際轉化為網頁上具象的動態視覺藝術。

優化思維（Performance Tuning）：透過減少 GPU 繪圖呼叫（Draw Calls）、關閉深度寫入與引入插值（Lerp）平滑化，在保持 15,000 個粒子下依然維持流暢的高影格率（FPS）。
