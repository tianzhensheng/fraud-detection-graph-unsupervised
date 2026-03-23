# fraud-detection-graph-unsupervised
Advanced Fraud Detection System based on Unsupervised Learning &amp; Graph Theory. 专为极度不平衡数据 (Imbalanced Data) 设计，融合 Isolation Forest, LOF 及 Connected Components 算法，实现高召回率异常检测。

# ️‍️ Advanced Fraud Detection with Unsupervised & Graph Learning
> **基于无监督学习与图论的进阶欺诈检测系统**

本项目构建了一个鲁棒的 **Anomaly Detection Framework**，专门解决工业界痛点：**标签稀缺 (Label Scarcity)** 和 **极度不平衡数据 (Highly Imbalanced Data)**。
通过融合 **Unsupervised Learning** (Isolation Forest, LOF)、**Semi-supervised Self-training** 以及 **Graph-based Clustering**，我们在缺乏大量标注样本的情况下，依然能精准捕捉异常模式。

## 🎯 Core Features (核心亮点)

- **🚀 Unsupervised Anomaly Detection**: 
  集成 `Isolation Forest` 和 `Local Outlier Factor (LOF)` 进行初筛，无需标签即可识别离群点 (Outliers)。
  
- **🕸️ Graph-Based Clustering (图聚类)**: 
  基于异常得分构建 **K-NN Graph**，利用 `Connected Components` 算法识别潜在的“欺诈团伙”或“故障关联簇”。这是本项目的核心创新点。
  
- **🔄 Semi-Supervised Enhancement**: 
  引入 **Self-Training** 机制，利用少量已知 Label 迭代优化模型，显著提升泛化能力。
  
- **⚖️ Imbalanced Data Optimized**: 
  不只看 Accuracy，重点优化 **PR-AUC** 和 **Recall@LowFalsePositiveRate**，这才是真实业务场景 (Real-world Scenario) 的关键指标。

## 📊 Dataset Overview

使用类 Kaggle Credit Card Fraud 的模拟数据：
- **Features**: Time, Amount, V1-V28 (PCA transformed)
- **Target**: `Class` (0 = Normal, 1 = Fraud/Anomaly)
- **Challenge**: 正负样本比例 < 1:500 (Extreme Imbalance)

## 🧠 Methodology Pipeline (技术路线)

1. **Data Preprocessing**: 特征缩放 (Scaling) + 欠采样 (Undersampling) 处理不平衡。
2. **Base Models**: 独立训练 IF 和 LOF，通过 **Ensemble Averaging** 融合得分。
3. **Graph Construction**: 选取 Top-N 异常点构建 k-NN 图。
4. **Cluster Analysis**: 提取连通分量 (Connected Components) 作为高风险簇。
5. **Iterative Refinement**: 利用高置信度预测结果进行 **Self-Training** 闭环优化。

## 📈 Performance Metrics (性能表现)

| Model Strategy | Precision | Recall | F1-Score | PR-AUC |
| :--- | :---: | :---: | :---: | :---: |
| Isolation Forest (Base) | 0.76 | 0.68 | 0.72 | 0.78 |
| LOF (Base) | 0.74 | 0.65 | 0.69 | 0.75 |
| **Ensemble (IF+LOF)** | 0.79 | 0.71 | 0.75 | 0.80 |
| **+ Graph Clustering** | 0.82 | 0.73 | 0.77 | **0.81+** |
| **+ Self-Training** | 0.84 | 0.75 | 0.79 | **0.83** |

> 💡 **Note**: 最终指标取决于随机种子 (Random Seed) 和超参数调优 (Hyperparameter Tuning)。

## 🛠️ Environment Setup (环境配置)

核心依赖见 [`requirements.txt`](requirements.txt)。快速安装：

```bash
pip install -r requirements.txt
```

主要库 (Key Libraries):  
pandas, numpy: 数据处理  
scikit-learn: 机器学习基座  
networkx: 图论分析核心  
matplotlib, seaborn: 可视化  

🚀 How to Run (运行指南)

Clone Repo:
```bash

git clone https://github.com/tianzhensheng/fraud-detection-graph-unsupervised.git
cd fraud-detection-graph-unsupervised
Install Dependencies:
```bash


pip install -r requirements.txt
Launch Jupyter:
bash

```



jupyter lab
打开文件：Advanced-Fraud-Detection-with-Unsupervised-and-Graph-Learning-0309.ipynb
💡 Industrial Application (工业落地潜力)
虽然本项目以 Fraud Detection 为例，但其架构可无缝迁移至以下领域：
🏭 Predictive Maintenance (预测性维护):
利用传感器时序数据，检测设备早期故障 (Early Failure Detection)。图算法可识别多传感器耦合异常。
🛡️ Cybersecurity (网络安全):
识别恶意网络流量模式 (Malicious Traffic Patterns)。
🏥 Healthcare Monitoring (医疗监控):
在 ICU 场景中标记异常生命体征。
Core Idea: 当异常不是孤立发生，而是以“群体”或“关联”形式出现时，Graph Topology (图拓扑) 分析具有降维打击的优势。
📄 License
MIT License — 欢迎 Fork, Modify 和 Share。
👤 Author
Tian Zhen Sheng
GitHub Profile
⚠️ Disclaimer: 本项目使用合成/模拟数据演示。Production Deployment 前请务必在垂直领域数据集验证，并遵守 GDPR/HIPAA 等隐私合规要求。

