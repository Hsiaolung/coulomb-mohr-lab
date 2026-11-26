# 应力莫尔圆与三维库仑应力交互实验室

> **Geophysics & Rock Mechanics Interactive Lab · 2D/3D Mohr Circle & 3D** $\Delta CFS$
>
> 🌐 **在线体验 (Live Demo)**：[点击直接运行实验室](https://hsiaolung.github.io/coulomb-mohr-lab/)（开启 GitHub Pages 并将主文件命名为 `index.html` 后生效）

一个**单文件、零构建依赖**的地球物理与岩石力学交互式可视化实验室。通过实时联动的 2D/3D 图形界面，帮助地震学、构造地质学与岩石力学初学者直观理解**二维/三维应力莫尔圆**、**孔隙水压诱发地震机制**以及**三维空间静态库仑破裂应力变化（**$\Delta CFS$**）**。

## ✨ 核心功能模块

### 1. 二维莫尔圆与断层切面 (2D Mohr & Fault)

* **块体与莫尔圆实时联动**：左侧展示受 $\sigma_1$（垂直挤压）与 $\sigma_3$（水平围压）作用的二维岩石块体及内部断层切面受力；右侧同步绘制有效应力莫尔圆与红色库仑破裂包络线。
* **孔隙水压对比**：调节孔隙水压 $P$ 时，保留灰色虚线总应力莫尔圆并标出向左平移的 $-P$ 矢量，直观呈现“注水诱发地震”的几何过程。
* **关键几何标注**：实时显示断层法线夹角 $\theta$、莫尔圆圆心角 $2\theta$ 以及断层应力点到破裂线的垂直距离（库仑应力裕度 $CFS$）。
* **情景预设**：内置「安全稳定」「临界破裂」「注水诱发地震」一键切换。

### 2. 三维莫尔圆与块体受力 (3D Mohr & 3D Block)

* **可交互 3D 岩石立方体**：基于 Three.js 构建，支持旋转、缩放与平移；块体六面以不同颜色和长度的 3D 箭头实时表达 $\sigma_1$（红）、$\sigma_2$（绿）、$\sigma_3$（蓝）主应力大小。
* **精确裁剪的 3D 断层切面**：根据断层走向（Strike）与倾角（Dip），精确计算断层面与立方体的交点多边形，并在切面中心绘制法向矢量 $\mathbf{n}$ 与最大剪应力矢量 $\boldsymbol{\tau}$。
* **三维莫尔圆与轨迹追踪**：绘制由三个主应力圆围成的**月牙形合法三维应力域**；拖动走向或倾角时自动记录应力点轨迹，直观展示中间主应力 $\sigma_2$ 带来的三维走向效应。
* **安德森构造应力场预设**：支持一键切换正断层（$\sigma_1$ 垂直）、逆断层（$\sigma_3$ 垂直）与走滑（$\sigma_2$ 垂直）应力场。

### 3. 三维空间库仑应力触发 (3D Coulomb Stress $\Delta CFS$)

* **纯前端三维弹性位错计算引擎**：内置基于均匀弹性全空间（泊松比 $\nu = 0.25$，剪切模量 $G = 30\text{ GPa}$）的 18 子断层双力偶位错叠加计算，实时求解任意空间点的完整三维应力变化张量。
* **源断层与接收断层自由配置**：支持独立调节源断层的走向、倾角、滑动角（Rake）、滑动量与长度，以及接收断层的三维空间坐标 $(X, Y, Z)$ 与产状。
* **三维应力场可视化**：接收断层表面逐顶点按 $\Delta CFS$ 着色（红-白-蓝发散色标），并配有可自由升降深度、可开关的水平“蝴蝶状”库仑应力切片。
* **莫尔空间应力转移联动**：右侧实时输出接收断层中心的 $\Delta CFS$、$\Delta \tau$、$\Delta \sigma_n$（同时提供 $\text{bar}$ 与 $\text{MPa}$ 单位）及触发阈值判定，并通过迷你莫尔图展示震前到震后的应力转移箭头。

## 🚀 快速开始

本项目采用单文件架构，无需安装 Node.js 或任何打包工具：

1. **本地运行**

   ```bash
   git clone https://github.com/Hsiaolung/coulomb-mohr-lab.git
   cd coulomb-mohr-lab
   ```

   直接用现代浏览器（Chrome / Edge / Firefox / Safari）双击打开 `index.html`（或 `coulomb_mohr_lab.html`）即可体验。

   > 注：页面通过 CDN 加载 Tailwind CSS 与 Three.js，首次打开需保持联网。

2. **通过 GitHub Pages 在线访问**

   * 将 `coulomb_mohr_lab.html` 重命名为 `index.html`。
   * 在 GitHub 仓库中进入 **Settings → Pages**，将 Source 设置为 `Deploy from a branch`，选择 `main` 分支根目录保存，等待约 1 分钟即可通过 [https://hsiaolung.github.io/coulomb-mohr-lab/](https://hsiaolung.github.io/coulomb-mohr-lab/) 访问。

## 📐 物理原理与符号约定

### 1. 莫尔-库仑破裂准则（模块 1 & 2）

在岩石力学莫尔圆坐标系中，规定**挤压为正**。引入孔隙水压 $P$ 后，有效主应力为 $\sigma_i' = \sigma_i - P$。

* **二维断层切面受力**：

  $$
  \sigma_n' = \frac{\sigma_1' + \sigma_3'}{2} + \frac{\sigma_1' - \sigma_3'}{2}\cos(2\theta), \qquad \tau = \frac{\sigma_1' - \sigma_3'}{2}\sin(2\theta)
  $$

* **三维断层切面受力**（主轴法向量为 $(n_1, n_2, n_3)$）：

  $$
  \sigma_n' = \sigma_1' n_1^2 + \sigma_2' n_2^2 + \sigma_3' n_3^2, \qquad \tau = \sqrt{(\sigma_1' n_1)^2 + (\sigma_2' n_2)^2 + (\sigma_3' n_3)^2 - (\sigma_n')^2}
  $$

* **破裂判定**：当库仑应力裕度 $CFS = \tau - (c + \mu \sigma_n') \ge 0$ 时，断层达到破裂极限。

### 2. 静态库仑破裂应力变化（模块 3）

在地震学应力触发分析中，采用习惯符号约定：**剪应力变化** $\Delta \tau$ **沿接收断层滑动方向为正，正应力变化** $\Delta \sigma_n$ **以拉张（松绑）为正**：

$$
\Delta CFS = \Delta \tau + \mu' \Delta \sigma_n
$$

* $\Delta CFS > 0$（红色区域）：应力加载，断层更靠近破裂极限，地震触发概率增加（通常 $+0.1\text{ bar} = +0.01\text{ MPa}$ 即视为显著触发阈值）。
* $\Delta CFS < 0$（蓝色区域）：应力影区（Stress Shadow），断层受到抑制，相对更安全。

## 🛠️ 技术栈

* **视图与样式**：HTML5 + Tailwind CSS (CDN)
* **2D 科学绘图**：原生 HTML5 Canvas 2D（支持高分屏 DPR 自适应与等比例坐标轴）
* **3D 交互渲染**：Three.js (`r128`) + `OrbitControls`
* **数值计算**：纯 JavaScript 实现的三维向量变换、平面-立方体裁剪算法及弹性双力偶位错应力场求解

## ⚠️ 教学近似说明

本工具旨在提供直观的物理概念教学与交互体验。模块 3 中的三维应力场采用**均匀弹性全空间有限断层双力偶叠加近似**（并引入软化半径以避免近场奇点），能够准确再现走滑、逆冲、正断等断层错动引起的红蓝应力加载瓣与应力影区特征；如需开展科研级精确定量反演，建议使用 USGS **Coulomb 3.3 / 4.0** 或基于 Okada (1992) 半空间解析解的专业计算工具。

## 📄 开源协议

本项目基于 [MIT License](LICENSE) 开源，欢迎用于教学演示、个人学习或二次开发。