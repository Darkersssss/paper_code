# 项目需求文档：端到端多机器人探索框架

## 1. 项目概述
| 项目 | 内容 |
|------|------|
| 项目名称 | zlr-explore |
| 核心目标 | 使用端到端的网络结合深度强化学习实现多无人机未知环境探索 |
| 在设计任务时，主要借鉴/home/zlr/paper_code/IR2-Multi-Robot-RL-Exploration和/home/zlr/paper_code/MARVEL |

---

## 2. 任务设定

### 2.1 机器人类型
- 同构多机器人（所有机器人相同且为无人机）
- 数量范围：数量可变化，不固定

### 2.2 感知与视野
- 传感器类型：深度相机
- 视野约束：
  - 有限FoV，参考/home/zlr/paper_code/MARVEL中的设计方法
- 感知范围：参考/home/zlr/paper_code/MARVEL中的设计方法
- 是否考虑传感器噪声：否

### 2.3 环境模型
- 维度：（2D栅格地图 ）
- 地图表示：
  - 占用栅格（Occupancy Grid），参考/home/zlr/paper_code/MARVEL中的设计方法
- 环境动态性：
  - 静态环境

---

## 3. 方法设计

### 3.1 核心网络架构
- 编码器
    - 参考项目/home/zlr/paper_code/IR2-Multi-Robot-RL-Exploration和/home/zlr/paper_code/MARVEL，采用GAT与GCN结合的方法对特征进行编码
- 解码器
    - /home/zlr/paper_code/IR2-Multi-Robot-RL-Exploration和/home/zlr/paper_code/MARVEL，但是动作空间不一样

### 3.2 学习范式
- 强化学习（RL）
  - 采用SAC算法设计网络
  - 

### 3.3 关键创新模块
- 显式通信机制（机器人间信息交换）
- 分层策略（高层路径规划 + 底层控制）
- 注意力机制改进（如自监督注意力）
- 地图编码器（CNN / ViT / 其他）

---

## 4. 输入输出定义

### 4.1 观测空间（Observation）
- 
- 图节点特征：维度 __
- 其他特征：（相对位置 / 历史轨迹 / 队友位置 / 等）

### 4.2 动作空间（Action）
- 离散：从候选节点中选择下一个目标点
- 连续：直接输出坐标 (x, y) 或速度指令 (v, ω)
- 混合：选择节点 + 连续朝向
- 动作维度：__

---

## 5. 训练与评估

### 5.1 训练设置
- 采用基于Ray的分布式训练方式，与/home/zlr/paper_code/IR2-Multi-Robot-RL-Exploration和/home/zlr/paper_code/MARVEL 保持一一致
- 要支持从加载预训练权重
- 决策频率
- 课程学习

### 5.2 仿真环境
- 地图来源：地图数据集来源于
- 地图规模：是基于地图的复杂程度进行排序

### 5.3 评价指标
- 探索覆盖率（Exploration Rate）
- 完成时间 / 路径长度
- 机器人间重复探索比例（Overlap）

---

## 6. 代码结构需求

### 6.1 复用策略
- 从 MARVEL 复用的模块：（如：sensor.py / env.py / 整体结构）
- 完全重写的模块：（如：model.py / 全新的网络架构）

### 6.2 依赖与工具
- 深度学习框架：（PyTorch / PyTorch Geometric / 其他）
- 日志系统：（TensorBoard / WandB / SwanLab / 不需要）
- 可视化：（实时渲染 / 仅保存GIF / 不需要）

### 6.3 项目规模
- [ ] 研究原型（快速验证想法，代码精简）
- [ ] 完整框架（可复现、可扩展、文档完整）
- [ ] 工程级（单元测试、配置化、易于部署）

---

## 7. 其他说明
（任何额外的特殊需求、参考论文、或约束条件）


不使用层次图了