# Awesome-3D-Human-Pose-Estimation
This repository is a collection of recent 3D-Human-Pose-Estimation works

⭐ If you like this list, please give it a star! 😄


[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license)  
[![Last Updated](https://img.shields.io/badge/last%20updated-2025--11--07-blue.svg)](#)  
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-green.svg)](#contributing)  

---

## 📌 快速导航
- [Datasets and Metrics](#Datasets--Metrics)
- [单人：视频/2D→3D 提升](#单人视频2d3d-提升)
- [单人：扩散/多假设](#单人扩散多假设)
- [单人：网格/SMPL 回归（含关键点评测）](#单人网格smpl-回归含关键点评测)
- [多人：单目](#多人单目)
- [多人：多目/多相机](#多人多目多相机)
- [参考资料与贡献指南](#参考资料与贡献指南)

---

## Datasets & Metrics
- **Human3.6M**（H36M）：MPJPE、PA-MPJPE（Protocol #1/#2）。
- **MPI-INF-3DHP**（3DHP）：PCK、AUC、MPJPE。
- **3DPW**（in-the-wild，常用于网格/SMPL方法，同样可导出关节评测）：PA-MPJPE、MPJPE、PVE。

> 备注：不同论文采用的数据预处理、2D检测器、训练协议、是否微调等会影响数值。下表“指标亮点”字段仅给出作者/官方仓库公开的代表性结果，便于初筛；更细对比建议参考各自 README 或论文附录。

---

## 单人：视频/2D→3D 提升

| 方法 | 会议&年份 | 类型 | 代码 | 指标亮点（作者报告） | 备注 |
|---|---|---|---|---|---|
| **MotionBERT** | ICCV 2023 | 2D→3D 提升 / 视频 | https://github.com/WuJie1010/MotionBERT | Human3.6M **MPJPE≈37.2 mm**（微调） | 统一视角（图像/2D骨架）训练；提供丰富模型动物园 |
| **MixSTE** | CVPR 2022 | 视频 Transformer | https://github.com/JinluZhang1126/MixSTE | （作者称在 H36M 有显著提升，详见论文表格） | 简洁的时空分解注意力，复现友好 |
| **MHFormer** | CVPR 2022 | 视频 Transformer（多假设融合） | https://github.com/Vegetebird/MHFormer | Human3.6M **MPJPE≈43.0 mm**（P1） | 提供完整训练/可视化脚本；有后续高效化变体（HoT） |
| **PoseFormerV2** | CVPR 2023 | 视频 Transformer（频域增强） | https://github.com/QitaoZhao/PoseFormerV2 | 在 H36M、3DHP 上优于 PoseFormer（详见仓库/论文） | 长序列高效、对 2D 噪声鲁棒 |
| **MotionAGFormer** | 2023/2024（论文/实现） | 视频 Transformer | https://github.com/OpenGVLab/MotionAGFormer | 在 H36M/3DHP 有竞争力表现（详见仓库） | 结构与训练细节完善，社区复现活跃 |

---

## 单人：扩散/多假设

| 方法 | 会议&年份 | 类型 | 代码 | 指标亮点（作者报告） | 备注 |
|---|---|---|---|---|---|
| **D3DP**（Diffusion-Based 3D Pose w/ Multi-Hypothesis Aggregation） | ICCV 2023 | 扩散模型（多假设融合） | https://github.com/paTRICK-swk/D3DP | H36M/3DHP 上有强竞争力（详见论文） | 多样性与精度兼顾，提供 PyTorch 代码 |
| **DiffPose** | CVPR 2023 | 扩散模型（单/多帧） | https://github.com/GONGJIA0208/Diffpose | 在 H36M、3DHP 上显著优于多项基线 | 提供项目页与代码，易于上手 |
| **GFPose** | CVPR 2023 | 3D 姿态先验（得分/梯度场） | https://github.com/Embracing/GFPose | 作为多假设估计器，H36M 有大幅提升（论文报告） | 同一模型统一多任务：去噪/补全/生成 |

---

## 单人：网格/SMPL 回归（含关键点评测）

> 这些方法常以 SMPL 网格为主目标，同时报告 3DPW 等数据集的**PA-MPJPE/MPJPE**等关节指标，便于与关节方法横向比较。

| 方法 | 会议&年份 | 类型 | 代码 | 指标亮点（作者报告） | 备注 |
|---|---|---|---|---|---|
| **HMR2.0 / 4DHumans** | ICCV 2023 | 单人网格回归 + 跟踪 | https://github.com/shubham-goel/4D-Humans | 3DPW 等数据集表现强势（详见仓库表格） | 提供推理与跟踪 demo，社区关注度高 |
| **TokenHMR** | 2023/2024 | Token 化网格回归 | https://github.com/MailingLi/TokenHMR | 3DPW 有竞争力 SOTA（详见 README 表格） | 训练/推理脚本清晰，易改造 |
| **CLIFF** | ECCV 2022（Oral） | 基于全帧位置信息 | https://github.com/haofanwang/CLIFF | 3DPW **PA-MPJPE≈43.0 / MPJPE≈69.0 / PVE≈81.2**（官方权重命名） | 支持多人、平滑与 SMPLify 拟合 |

---

## 多人：单目

| 方法 | 会议&年份 | 类型 | 代码 | 指标亮点（作者报告） | 备注 |
|---|---|---|---|---|---|
| **BEV**（Putting People in their Place） | CVPR 2022 | 单目多人 3D 深度关系 + 网格 | https://github.com/Arthur151/ROMP | 在 3DPW、CMU Panoptic 等基准具竞争力 | ROMP/BEV/TRACE 同仓库，实时友好

---

## 多人：多目/多相机

| 方法 | 会议&年份 | 类型 | 代码 | 指标亮点（作者报告） | 备注 |
|---|---|---|---|---|---|
| **Faster VoxelPose** | ECCV 2022 | 多目体素融合（加速版） | https://github.com/microsoft/Faster_VoxelPose | 在 CMU Panoptic、Shelf/Campus 等表现稳定 | 工程化程度高，推理速度优

---

## 参考资料与贡献指南
- 欢迎通过 PR 添加：**更高精度的最新方法**、**更多可复现结果**（注明训练协议/是否微调）。
- 统一提交流程：附上**论文链接**、**代码仓库**、**关键指标**（注明数据集与协议）、**stars 截图（可选）**。
- 计划补充：
  - 更细的 **Leaderboard**（按 H36M / 3DHP / 3DPW 分类，统一 Protocol）；
  - **训练配置与环境**复现实用脚本；
  - **工程落地指南**（推理速度、显存、部署建议）。

---
