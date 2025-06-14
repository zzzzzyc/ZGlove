# Project ZGlove 🧤

<p align="center">
  <img src="https://placehold.co/600x300.png?text=Project+Z-Glove" alt="Project Banner">
</p>
<h1>大饼</h1>
<p align="center">
  <b>一款开源、高精度（雾）的VR数据手套，采用IMU与磁感应融合技术实现全指追踪。</b>
  <br><br>
  <a href="#-核心技术">核心技术</a> •
  <a href="#-主要特性">主要特性</a> •
  <a href="#-硬件清单">硬件清单</a> •
  <a href="#-安装与使用">安装与使用</a> •
  <a href="#-开发路线图">开发路线图</a> •
  <a href="#-贡献">贡献</a>
</p>

<p align="center">
  <img alt="GitHub stars" src="https://img.shields.io/github/stars/zzzzzyc/ZGlove?style=for-the-badge">
  <img alt="GitHub forks" src="https://img.shields.io/github/forks/zzzzzyc/ZGlove?style=for-the-badge">
  <img alt="GitHub issues" src="https://img.shields.io/github/issues/zzzzzyc/ZGlove?style=for-the-badge">
  <img alt="WTFPL" src="https://img.shields.io/badge/License-WTFPL-blue.svg?style=for-the-badge">
</p>

---

## 📖 项目简介

**Project Z-Glove** 是一个DIY项目，旨在打造一套能够与SteamVR无缝集成的、可与商业产品媲美（大雾）的VR数据手套。

与依赖昂贵传感器或复杂视觉追踪的方案不同，本项目采用了一种极具性价比和创新性（？）的**IMU（惯性测量单元）+ 磁感应**融合方案。这种设计不仅显著降低了硬件成本和制造复杂性，还保证了高精度和低延迟的手指追踪效果。

我们的目标是为VR爱好者、开发者和创客们提供一套完全开源的硬件、固件和软件解决方案，让每个人都能以较低的成本，打造属于自己的沉浸式VR交互设备。

## 🛠️ 核心技术

本项目的追踪魔法在于对IMU传感器功能的极致利用：

1.  🖐️ **手掌追踪 (6DoF Anchor):** 手背的主控模块（**a模块**）作为手部的绝对“锚点”。为实现完整的空间移动（6DoF），推荐在其上固定一个**Vive Tracker**。

2.  👆 **第一关节追踪 (IMU Pose):** 每根手指的第一关节（掌指关节）上安装一个**b模块**（内置IMU传感器）。IMU通过自带的陀螺仪和加速度计，精确计算出该关节相对于手掌的旋转姿态。

3.  🤏 **第二关节追踪 (Magnetic Sensing):** 
    * 在手指的第二关节上，我们只放置一颗无源的**c模块（永磁铁）**。
    * **b模块**中的IMU（如BNO085）内置了高精度**磁力计**。当手指弯曲时，磁铁靠近磁力计，引起局部磁场的剧烈变化。
    * 我们通过独特的校准算法，将磁场读数的变化精确地**映射**为第二关节的弯曲角度。

4.  ✨ **末端关节追踪 (Procedural Inference):** 手指最末端的关节运动是根据第二关节的角度，通过生物力学模型在软件中**程序化推算**得出的，以极低的成本实现了逼真的跟随效果。

5.  ⚙️ **数据融合 (Forward Kinematics):** 所有关节的角度数据被无线发送到PC。PC端的OpenVR驱动程序利用**正向运动学（FK）**算法，将这些角度数据实时重建为SteamVR中完整、流畅的手部姿态。

## ✨ 主要特性

* **高性价比:** 相比商业手套，成本极低。
* **高精度:** 融合IMU和磁感应，提供稳定、低延迟的关节追踪。
* **开源开放:** 全部硬件设计、固件代码和PC驱动源码开放。
* **易于复现:** 采用常见的开发板和传感器，降低了DIY门槛。
* **SteamVR 兼容:** 通过模拟Valve Index手柄，原生支持大量VR游戏和应用。
* **耐用性高:** 无接触式的磁感应方案，无物理磨损，使用寿命长。

## 硬件清单

| 类别 | 物件名称 | 规格/型号 | 数量 |
| :--- | :--- | :--- | :--- |
| **核心** | 微控制器 (MCU) | ESP32-WROOM-32 开发板 | 2 |
| | IMU传感器 | Adafruit BNO085 | 6 |
| | 磁铁 | 钕磁铁 (Neodymium Magnet) | 5 |
| **电源** | 锂电池 | 3.7V LiPo 电池 (300-500mAh) | 1 |
| | 充电模块 | TP4056 充电板 | 1 |
| **其他** | 手套 | 贴身的黑色手套 | 1双 |
| | 线缆 | 30AWG 超软硅胶线 | 若干 |
| | 3D打印 | PLA/PETG/TPU 耗材 | 若干 |
| **可选** | VR追踪器 | HTC Vive Tracker (3.0) | 1 |

*详细的3D模型（`.stl`文件）和电路图请见 `/hardware` 目录。*

## 🚀 安装与使用

**(WIP)**

## 🗺️ 开发路线图

-   [x] **Phase 0: 环境搭建与基础测试** - 工具链与传感器测试通过。
-   [x] **Phase 1: 核心技术原型验证** - 单指IMU+磁感应方案验证成功。
-   [ ] **Phase 2: 手套硬件集成** - 完成手套的最终硬件组装。
-   [ ] **Phase 3: 固件与无线通信开发** - 稳定采集和无线发送数据。
-   [ ] **Phase 4: OpenVR驱动开发** - 实现完整的PC驱动和校准工具。
-   [ ] **Phase 5: 文档完善与发布** - 编写详细的制作和使用文档。

## 🤝 贡献

我们欢迎所有形式的贡献！无论是提交代码、报告Bug、改进3D模型，还是完善文档，都对这个项目至关重要。

1.  Fork 本仓库
2.  创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3.  提交你的更改 (`git commit -m 'Add some AmazingFeature'`)
4.  推送到分支 (`git push origin feature/AmazingFeature`)
5.  开启一个 Pull Request

## 🙏 致谢

本项目的开发受到了以下优秀开源项目的启发，在此表示诚挚的感谢：
* [LucidVR](https://github.com/LucidVR/lucidgloves)
* [OpenVR and SteamVR Community](https://github.com/ValveSoftware/openvr)

## 📄 许可证

本项目采用 WTFPL 许可证，干你他妈像干的任何事的
<br><br><br><br>
我本来想叫fucking higvr的 想了想还是算了吧（雾）
