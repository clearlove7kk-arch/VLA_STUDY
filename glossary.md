# VLA 术语表

> 遇到新术语随时补进来，保持生长。

## 核心概念

- **VLA (Vision-Language-Action)**：输入图像（+语言指令），直接输出机器人动作的模型。RT-2 首次提出这个叫法。
- **VLM (Vision-Language Model)**：视觉-语言模型（如 CLIP、LLaVA），VLA 的 backbone。
- **Embodied AI（具身智能）**：有身体、能与环境交互的智能体。VLA 是其核心技术路线。
- **Manipulation（操作）**：机械臂抓取、放置、装配等任务（vs locomotion 行走）。
- **Dexterous manipulation（灵巧操作）**：多指手精细操作，VLA 最难的战场。

## 动作表示（VLA 最核心的技术分叉）

- **Action tokenization（动作离散化）**：把连续动作离散成 token（RT-1/RT-2/OpenVLA 用）。可与 LLM 词表统一，但精度受限。
- **Diffusion action head**：用扩散模型生成连续动作（Diffusion Policy、RDT 用）。擅长多模态动作分布，推理慢。
- **Flow matching action head**：流匹配生成动作（π0 用）。效果类似 diffusion 但更快。
- **Action chunking（动作分块）**：一次预测未来 N 步动作而非单步，减少误差累积（ACT 提出，Octo/π0 沿用）。
- **Multimodal action distribution（多模态动作分布）**：同一观测下多种合理动作。MSE 回归会取平均 → 失败。这是动作生成的核心难题。

## 数据

- **Behavior cloning (BC)**：模仿学习，从（观测，动作）对监督学习。主流 VLA 的训练方式。
- **Teleoperation（遥操作）**：人远程操控机器人采集数据，真机数据的主要来源。
- **Open X-Embodiment**：跨机构机器人操作数据集合集（RT-X 论文）。
- **Cross-embodiment（跨本体）**：一个策略控制不同形态的机器人。
- **Co-finetuning**：web 数据 + 机器人数据混合微调（RT-2 的关键配方）。
- **Sim2real**：仿真训练 → 真机部署的迁移。

## 评测

- **LIBERO**：一组操作任务 benchmark，VLA 论文标配。
- **SIMPLER**：仿真评测 OpenVLA/RT-1-X 的标准化环境（真机评测太贵，大家都用这个报告复现数字）。
