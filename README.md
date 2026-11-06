# Awesome Shadow Removal

**去阴影论文、官方代码与数据集精选。**

A curated reading list on single-image shadow removal, with links to papers, official implementations, and concise Chinese notes.

从近期关注的方法开始整理，重点包括扩散去阴影、软掩膜、阴影分解与合成数据。每篇保留英文原题、发表信息和一句话说明，便于快速找到原文与代码。

**最近整理：2026-11-06 · 7篇去阴影/阴影合成方法 + 3篇相关恢复基础方法 + 1篇综述**

## 目录

- [扩散去阴影](#扩散去阴影)
- [软掩膜与阴影分解](#软掩膜与阴影分解)
- [阴影合成与训练数据](#阴影合成与训练数据)
- [相关扩散恢复基础](#相关扩散恢复基础)
- [综述](#综述)
- [常用数据集](#常用数据集)
- [评估时看什么](#评估时看什么)
- [补充条目](#补充条目)
- [致谢](#致谢)

## 扩散去阴影

- **ODDR** · `NeurIPS 2026`  
  **ODDR: One-Step Deshadow Diffusion via Reward Guidance**  
  [论文](https://arxiv.org/abs/2610.01291) · [官方代码](https://github.com/junsung6140/ODDR) · [项目主页](https://junsung6140.github.io/oddr_project_page/)  
  基于 Stable Diffusion 的单步去阴影模型，先用合成配对数据学习恢复，再以 ShadowReward 引导适配真实阴影；推理不需要外部阴影mask。

- **StableShadowRemoval / SSR** · `CVPR 2025`  
  **Detail-Preserving Latent Diffusion for Stable Shadow Removal**  
  [论文](https://arxiv.org/abs/2412.17630) · [官方代码](https://github.com/Hiahia1369/StableShadowRemoval)  
  用潜空间扩散完成去阴影，再通过细节保留机制改善重建；重点关注生成先验与图像细节之间的平衡。

- **ShadowDiffusion** · `CVPR 2023`  
  **ShadowDiffusion: When Degradation Prior Meets Diffusion Model for Shadow Removal**  
  [论文](https://arxiv.org/abs/2212.04711) · [官方代码](https://github.com/GuoLanqing/ShadowDiffusion)  
  将预训练网络估计的退化先验、阴影mask和扩散采样结合，在迭代去噪中引入数据一致性约束。

- **Refusion** · `CVPR Workshops 2023 · NTIRE`  
  **Refusion: Enabling Large-Size Realistic Image Restoration With Latent-Space Diffusion Models**  
  [论文](https://openaccess.thecvf.com/content/CVPR2023W/NTIRE/html/Luo_Refusion_Enabling_Large-Size_Realistic_Image_Restoration_With_Latent-Space_Diffusion_Models_CVPRW_2023_paper.html) · [arXiv](https://arxiv.org/abs/2304.08291) · [官方代码](https://github.com/Algolzw/image-restoration-sde)  
  面向真实图像恢复改进扩散网络、噪声与训练配置，包含去阴影实验及潜空间扩展。官方仓库同时提供 IR-SDE、Refusion 和 Latent-Refusion，使用时需核对具体配置。

## 软掩膜与阴影分解

- **SoftShadow** · `CVPR 2025`  
  **SoftShadow: Leveraging Soft Masks for Penumbra-Aware Shadow Removal**  
  [论文](https://openaccess.thecvf.com/content/CVPR2025/html/Wang_SoftShadow_Leveraging_Soft_Masks_for_Penumbra-Aware_Shadow_Removal_CVPR_2025_paper.html) · [arXiv](https://arxiv.org/abs/2409.07041) · [官方代码](https://github.com/Xinrui014/SoftShadow)  
  利用 SAM 先验与半影形成约束学习连续软mask，区分全阴影与半影，改善阴影边缘的过渡与恢复。

- **SP+M / SID** · `ICCV 2019`  
  **Shadow Removal via Shadow Image Decomposition**  
  [论文](https://arxiv.org/abs/1908.08628) · [官方代码](https://github.com/cvlab-stonybrook/SID)  
  将去阴影分解为阴影参数估计与matte预测，通过亮度变换和融合恢复图像，为理解补偿强度与边界过渡提供直观参考。

## 阴影合成与训练数据

- **SynShadow** · `IEEE TCSVT 2021`  
  **Learning from Synthetic Shadows for Shadow Detection and Removal**  
  [论文](https://arxiv.org/abs/2101.01713) · [官方代码与数据](https://github.com/naoto0804/SynShadow)  
  提供阴影图、无阴影图和matte三元组合成流程与数据集，并研究合成数据如何用于阴影检测和去除。

## 相关扩散恢复基础

以下三篇是理解上述方法时有用的**通用图像恢复文献**，单独列为背景阅读；其任务范围不等同于专门去阴影。

- **RDBM** · `CVPR 2026`  
  **Residual Diffusion Bridge Model for Image Restoration**  
  [论文](https://arxiv.org/abs/2510.23116) · [官方代码](https://github.com/MiliLab/RDBM)  
  在退化图与目标图之间建立残差扩散桥，研究如何减少全局加噪与重建对未退化区域的扰动。

- **GOUB** · `ICML 2024`  
  **Image Restoration Through Generalized Ornstein-Uhlenbeck Bridge**  
  [论文](https://proceedings.mlr.press/v235/yue24d.html) · [官方代码](https://github.com/Hammour-steak/GOUB)  
  利用广义 Ornstein–Uhlenbeck 过程和桥约束建立低质量图到高质量图的恢复路径。

- **IR-SDE** · `ICML 2023`  
  **Image Restoration with Mean-Reverting Stochastic Differential Equations**  
  [论文](https://proceedings.mlr.press/v202/luo23b.html) · [官方代码](https://github.com/Algolzw/image-restoration-sde)  
  以退化图为均值状态构建随机微分方程，通过学习逆向过程恢复图像，是理解 Refusion 的基础工作。

## 综述

- **Single-Image Shadow Removal Using Deep Learning: A Comprehensive Survey** · `arXiv 2024`  
  [论文](https://arxiv.org/abs/2407.08865) · [作者维护的文献合集](https://github.com/GuoLanqing/Awesome-Shadow-Removal)  
  从学习策略、网络结构、损失、数据集和评估等角度梳理单幅图像去阴影，适合作为入门索引。

## 常用数据集

| 数据集 | 用途与注意点 | 来源入口 |
| --- | --- | --- |
| **ISTD** | 阴影图、阴影mask和无阴影图三元组，可用于检测与去阴影。 | [ST-CGAN作者仓库](https://github.com/DeepInsight-PCALab/ST-CGAN) |
| **ISTD+ / Adjusted ISTD** | 对ISTD无阴影参考图做光照/颜色调整，比较结果时需说明使用哪个版本。 | [SID作者仓库](https://github.com/cvlab-stonybrook/SID) |
| **SRD** | 常用的成对去阴影数据集；mask的来源应按具体方法单独说明。 | [ShadowDiffusion数据与模型说明](https://github.com/GuoLanqing/ShadowDiffusion) |
| **SynShadow** | 合成阴影/无阴影/matte三元组，适合研究数据合成与迁移。 | [数据说明](https://github.com/naoto0804/SynShadow/tree/main/datasets) |

## 评估时看什么

| 指标 | 通常方向 | 主要反映 |
| --- | --- | --- |
| PSNR | 越高越好 | 与参考图的像素重建一致性 |
| SSIM | 越高越好 | 局部结构、亮度和对比度的一致性 |
| MAE / RMSE | 越低越好 | 平均绝对误差 / 均方根误差，二者定义不同 |
| LPIPS | 越低越好 | 深层特征衡量的感知差异 |

比较论文结果时，先对齐**数据划分、图像尺寸、颜色空间和评价区域**。建议同时看全图、阴影区域和非阴影区域：去掉阴影与保留正常内容同样重要。

注意：部分早期去阴影工作将实际计算的MAE记为“RMSE”；[SID作者说明](https://github.com/cvlab-stonybrook/SID)指出了这一问题，应以具体评估代码为准。

## 补充条目

欢迎通过 Issue 或 Pull Request 补充论文、修正链接。建议提供：

```text
方法简称：
论文完整标题：
年份与会议/期刊（或arXiv）：
论文链接：
官方代码/项目主页：
一句话方法说明：
```

优先链接论文原站与作者仓库；会议主会、Workshop和预印本分别标注。仓库存在不代表全部训练代码、权重和复现环境都已完备，资源使用以作者说明为准。

## 致谢

本合集的组织方式参考了 [GuoLanqing/Awesome-Shadow-Removal](https://github.com/GuoLanqing/Awesome-Shadow-Removal)。感谢各论文作者公开原文、代码与数据。这里整理阅读入口与简要说明，论文、代码和数据的权利及使用条款归各原作者。
