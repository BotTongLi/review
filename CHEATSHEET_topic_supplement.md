# UML4SS Cheatsheet — 补遗（按重要性从上到下）

补 `CHEATSHEET_topic.md` 漏掉的内容。
风格沿用：英文术语 bold + 中文做连接。
⭐ = 高频考点；⚠️ = 陷阱。

---

# 🔴 一、Recommender Systems & Spatial Voting（整章补）

选择题最可能至少出 2–3 道。

## 推荐问题设置 ⭐

| 概念 | 必记 |
|---|---|
| 矩阵规模 | 用户 × 物品，99% 缺失 |
| **Explicit feedback** | 评分（1–5 星、👍/👎）|
| **Implicit feedback** | 点击、观看时长 |
| Implicit 没有什么 | **没有负样本**（没点击 ≠ 不喜欢）|
| **MNAR** | missing not at random：人爱评强观点 |

## Baseline（必先建）⭐

预测 = **global mean** + **user bias** + **item bias**

- Netflix 上 baseline 已解释**大部分**可解释方差
- ⚠️ MF 提升应**相对 baseline** 报告，不是相对零预测

## Matrix Factorization (MF) ⭐

- 用户向量 **p_i** + 物品向量 **q_j**，预测 = **inner product** + baseline
- 维度 K 一般 10–200
- 全观测时 = **truncated SVD**（Eckart-Young 最优低秩）
- 有缺失时**只在 observed 上**最小化平方误差 + regularization
- 对 P、Q **联合非凸**、分别凸 → **ALS**

## ALS vs SGD ⭐

| | **ALS** | **SGD** |
|---|---|---|
| 方法 | 交替最小二乘 | 随机梯度下降 |
| 并行 | **可并行** | 难 |
| 适合 | 中等规模、生产主力 | **超大规模** |
| 每步 | 解小 ridge | 更新单个 (p_i, q_j) 对 |

## Probabilistic MF (PMF)

- 高斯似然 + 高斯先验，**MAP = ridge MF**
- 优势：给**预测不确定性**；推广到非高斯似然
  （**Bernoulli** for binary、**Poisson** for counts）

## MF 变体 ⭐

| 变体 | 关键 |
|---|---|
| **NMF** (Non-negative MF) | P、Q ≥ 0；部件式、稀疏、可解释 |
| **Implicit feedback (HKV)** | confidence-weighted；所有未观测对计入 |
| **BPR** (Bayesian Personalized Ranking) | 优化**排序**（pair-wise）；适合 **top-k 推荐** |
| **Factorization Machines** | 加 side info + 所有 pairwise interactions |
| **Neural CF** (NeuMF, Wide&Deep) | 内积换 MLP；表达力↑、丢 SVD 性质 |

⭐ **BPR vs MF**：MF 优化评分（**RMSE**）；BPR 优化排序（**precision@k**）。
看到 "top-k" → BPR。

## 评估 ⭐

| 任务 | 指标 |
|---|---|
| **评分预测** | **RMSE**（重罚大错）、**MAE** |
| **Top-k 推荐** | **Precision@k**、**Recall@k**、**NDCG**、**MAP** |

⚠️ 评估必在 **held-out** 上做，不是整个矩阵。

## Exploration vs Exploitation
- 纯 exploit → 推荐被困在已知好物品
- **Bandit 算法**：**Thompson sampling** / **UCB** 平衡 explore-exploit
- 目录翻新快（新闻、社交流）时尤重要

## Spatial Voting（推荐系统的孪生兄弟）⭐

- 数据：议员 × 议案（yea/nay/abstain）
- 每议员有 **ideal point**（x_i）
- 每议案有 **yea 位置**和 **nay 位置**
- 议员投给**距离更近**的位置

### Poole-Rosenthal 模型
- 概率化：受效用 + 噪声
- 噪声高斯 → **probit**；逻辑 → **logit**
- 经典实现：**NOMINATE**、**W-NOMINATE**
- R 包：**pscl** (W-NOMINATE)、**MCMCpack** (Bayesian)

### 识别问题 ⭐
- 全局 **rotation / reflection 等价** → 距离不变
- 需要**锚定**：把已知自由派固定在左、已知保守派固定在右
- 没锚定 → 轴的实质意义事后才能解释

### 扩展
- **Dynamic ideal points** (Martin-Quinn)：法官立场随时间游走
- **State preferences** (Bailey 等)：UN 投票
- **Ideological mapping at scale** (Bonica)：竞选捐款

## Recsys ↔ Spatial Voting 对应 ⭐⭐ 经典考点

| | Recsys | Spatial Voting |
|---|---|---|
| 行 | 用户 | 议员 |
| 列 | 物品 | 议案 |
| 值 | rating | yea/nay |
| 用户因子 | **p_i** | **ideal point x_i** |
| 物品因子 | **q_j** | **(yea, nay) 位置** |
| Link | identity / logit | **probit** |
| 估计 | ALS / SGD / MCMC | MLE / MCMC |
| 识别 | 很少关心 | **必须锚定** |
| 目标 | **prediction** | **measurement** |

→ 同一个低秩矩阵分解，**不同实质解释**。

---

# 🔴 二、Distance Metrics（聚类前提，常考）

## 连续数据 ⭐

| Metric | 性质 | 何时用 |
|---|---|---|
| **Euclidean** | 平方和开根 | default；先 standardize |
| **Manhattan** | 绝对差和 | **对 outlier 稳健**（无平方）|
| **Mahalanobis** | 用 covariance 校正 | 特征间有相关 |
| **Cosine similarity** | 单位向量内积 | **忽略 magnitude**；text 标准 |

## 重要等价 ⭐
**ZCA whitening 后的 Euclidean = 原数据的 Mahalanobis**。

## 二元数据
| Metric | 定义 |
|---|---|
| **Jaccard** | \|A∩B\| / \|A∪B\| |
| **Hamming** | 不匹配位置数 |

## 混合类型 ⭐
**Gower's coefficient**：
- 连续特征按 range 归一
- 有序特征按 rank
- 名义特征按 exact match
- 综合成单一不相似度
- R: `cluster::daisy(df, metric = "gower")`

## 选择题套路
| 题目场景 | 用哪个 |
|---|---|
| 文本相似度 | **Cosine** |
| Outlier 多 | **Manhattan** |
| 特征有相关 | **Mahalanobis** |
| 混合连续+类别 | **Gower** |
| 二元集合重叠 | **Jaccard** |

---

# 🔴 三、Foundation Models / Modern Text 补遗

## Transformer Block 结构 ⭐

每层 4 步：
1. **Multi-head self-attention**
2. **Residual connection + Layer normalization**
3. **Position-wise feed-forward**（FFN）
4. **Residual + Layer normalization**

⚠️ 必加 **position embedding** —— 否则 attention 对顺序无感。

## BERT 双任务预训练 ⭐

| 任务 | 做什么 |
|---|---|
| **Masked Language Modelling (MLM)** | mask **15%** token，从两侧预测 |
| **Next-Sentence Prediction (NSP)** | 判断两句是否相邻；后继多放弃 |

→ MLM 是 BERT 的**核心**，NSP 贡献小。

## Foundation Models 定义
- 单一大网络在广语料预训练，可适配多任务
- **Scale 是定义性特征**
- 涌现行为：新能力随规模出现

## Scaling Laws ⭐

- **Kaplan**：test loss = (params, data, compute) 的幂律
- **Chinchilla (Hoffmann)**：每个 compute budget 有**最优分配**
- 早期大模型相对参数量**训练不足**
- Chinchilla 修正：训更小模型但用更多 token

## In-Context Learning ⭐
- 模型够大后 → **从 prompt 几个示例学新任务**
- **无需梯度更新**
- 与 scale 可靠相关
- ⚠️ **验证不可商量**：看起来正确 ≠ 正确

## Few-shot vs Zero-shot ⭐
| | 内容 | 适合 |
|---|---|---|
| **Few-shot** | prompt 含示例 | 格式重要的任务 |
| **Zero-shot** | 只有任务描述 | 探索性 |

## Chain-of-Thought (CoT) ⭐⭐

- 示例里含**中间推理步骤**，不只最终答案
- 多步推理任务（算术、逻辑）上**显著提升**
- "Let's think step by step" = 零样本 CoT 触发语
- **Self-consistency**：采样多条 CoT 路径，多数投票
- **Tree-of-thoughts**：分支推理搜索

⚠️ **关键警告**：CoT trace 与模型实际计算**不保证忠实**。
- 提升精度 ✓
- **但别当作真实解释** ✗
- 经典选择题陷阱：问"CoT 给的解释是不是模型真实推理过程"，
  答 **不一定**。

## LLM 推理短板
擅长流利语言、模式补全。
弱于：**多步算术**、**形式逻辑**、长链中间状态。
应对：
- CoT scaffolding
- **Tool use**（计算器 / Python interpreter）
- 训 reasoning corpus + RL

## Agents
- LLM + **tool calls** = agent
- 模型决定调什么工具、解析结果、决定下一步
- 把标注 10,000 文档从"重劳动"变成"prompt 工程"
- ⚠️ **仍需分层抽样人工审查**

## 可复现性（LLM 必钉死）⭐
- **模型版本号**：同名 "gpt-4o" 不同月份是**不同 artifact**
- **Temperature**：分类 = **0**；生成 = 更高
- **随机种子**
- 提示词记录

## Sentence-BERT 为什么需要
- 直接平均 BERT token 向量 → 效果差
- Sentence-BERT 用 **siamese** 架构 fine-tune
- 得到固定大小句嵌入，**cosine 可比**

---

# 🟡 四、Ch 3 Measurement 补遗

## Stevens Measurement Levels ⭐

| Level | 允许操作 | 例 |
|---|---|---|
| **Nominal** | count、mode | 性别、政党 |
| **Ordinal** | rank、median | Likert、学历 |
| **Interval** | mean、SD | 摄氏温度、IQ |
| **Ratio** | 所有 arithmetic | 身高、reaction time |

⚠️ **Nominal** 上算 mean = **category error**。
**Interval** 上算 geometric mean 无意义（零点 arbitrary）。

## Reliability 类型表

| Type | 测什么 |
|---|---|
| **Test-retest** | 时间稳定性 |
| **Parallel forms** | 等价版本一致 |
| **Internal consistency** | items 一致（α、ω）|
| **Inter-rater** | raters 一致（**Cohen's κ**、**ICC**）|

→ **Cohen's κ** 用于 categorical ratings；**ICC** 用于 continuous。

## MTMM (Multitrait-Multimethod) Matrix ⭐

| 关系 | 应该是 |
|---|---|
| 同 trait 不同 method | **高**（convergent evidence）|
| 不同 trait 同 method | 中等（method bias 膨胀）|
| 同 trait 同 method | test-retest 对角 |
| 不同 trait 不同 method | **低**（discriminant evidence）|

→ Construct validity 证据：**convergent > discriminant**，
且 **trait effect > method effect**。

## DeVellis 八步量表开发

最重要的几步：
1. 清晰定义 construct
2. 生成**冗余**的 item pool
3. 选择 response format（Likert 数量、anchors）
4. **专家评审**
5. 开发样本（**每 item ≥ 10 人**）
6. 探索性分析
7. 修订
8. ⚠️ **独立样本验证** —— 最常被跳过

## Factor Extraction 方法

| 方法 | 性质 | 适合 |
|---|---|---|
| **ML** (Maximum Likelihood) | 假设 MVN | 给标准误、χ²；**CFA 标准** |
| **Principal Axis** | 迭代估 communality | 对非正态稳健；EFA 默认 |
| **Minres** (Minimum Residual) | 最小化残差 | 无分布假设 |

## Factor Rotation ⭐

| 类型 | 例 | 假设 |
|---|---|---|
| **Orthogonal** | **Varimax** | factors **不相关** |
| **Oblique** | **Oblimin / Promax** | factors 相关 |

- **多数 psychological constructs → oblique**
- 目标：**simple structure** —— 每 item 主载一个 factor

## Item Information & CAT ⭐

- Item 在 **difficulty b 附近**信息最大
- **Test information** = 各 item 信息之和
- **SE(θ) = 1/√I(θ)** → reliability 随 θ 变
- **CAT** (Computerized Adaptive Testing)：按当前 θ 估计选下一题，
  用**更少 items** 达到目标精度

## CFA 拟合指标 ⭐

| 指标 | 阈值 |
|---|---|
| **CFI** | > 0.95 |
| **TLI** | > 0.95 |
| **RMSEA** | < 0.06 |
| **SRMR** | < 0.08 |

→ 选择题可能问"哪个指标越小越好"：RMSEA、SRMR 越小；CFI、TLI 越大。

---

# 🟡 五、Ch 5 Manifold 方法细节

## Manifold Hypothesis ⭐

- 高维数据通常在**低维 manifold** 附近
- **Intrinsic dimension** = 实际自由度数 ≪ ambient dimension
- 例：手写数字 784 维像素，内在维 **10–20**
- 例：旋转茶壶图像 23028 维，内在维 **1**（旋转角）

## Geodesic vs Euclidean ⭐
- Swiss roll 上：同弧两点 **geodesic 近**，**Euclidean 远**
- 几乎所有 manifold 方法都在**替换 Euclidean**

## LLE 步骤 ⭐

**第一步**：每点用 k 邻居线性重构自己
- 求权重 W_ij，约束 **Σ W_ij = 1**（去除平移自由度）
- 闭式解涉及 local Gram matrix

**第二步**：找低维位置，让**相同权重**仍能重构
- 解稀疏 eigenproblem
- 跳掉 λ=0 的常数 eigenvector

LLE **保留 local affine 结构**——旋转、平移、缩放不变。

## Laplacian Eigenmaps 关键 ⭐

- 用**热核权重** k-NN graph：W_ij = exp(−distance²/t)
- 强连接的点在 embedding 中**保持靠近**
- 解 **generalized eigenproblem**：Lv = λDv
- 跳掉 λ_1 = 0；取最小非零的 L 个 eigenvectors
- **Normalized version** 校正 uneven sampling density

## MVU (Maximum Variance Unfolding) ⭐

- 想象 manifold 是卷起的纸，邻居用**刚性杆**连接
- 拉到最远：**maximize trace(K)** = total variance
- 约束：邻居对的距离**精确等于**原距离
- 是 **SDP**（半正定规划）
- ⭐ **eigenvalue gap → intrinsic dimension**：
  d 维流形上，前 d 个 eigenvalue 大，之后骤降
- 实际很少用：O(N^3.5)，~2000 点上限

## Crowding Problem（t-SNE 的动机）⭐

- 高维中很多点可几乎等距（10 维 simplex 上 11 个等距点）
- 2D 上做不到 → 用 Gaussian kernel 强行布局会**挤到中心**
- t-SNE 用 **Student-t (Cauchy)** 重尾 kernel 解决：
  允许中等高维相似度映射到大低维距离

## Perplexity 详解
- 每点的**有效邻居数**（exp of entropy）
- 默认 30；低（5–10）极局部；高（50–100）大邻域
- σ_i 通过二分搜索使每点 entropy 匹配目标
- ⚠️ **没有 principled 选择标准**，跑多个值

## UMAP 关键改进 vs t-SNE ⭐

| 改进 | 是什么 |
|---|---|
| **Density normalization** | 每点距离用最近邻距离归一 |
| ρ_i 减法 | 稀疏区和稠密区可比 |
| **显式 repulsion 项** | 损失函数有 (1−P)·log((1−P)/(1−q)) |
| **LE 初始化** | 暖启动，捕全局结构 |
| **OOS 支持** | 保存模型后 transform 新点 |

## Kernel PCA 细节
- 常用 kernel：**linear**、**polynomial**、**RBF (Gaussian)**
- RBF 带宽 σ：大 → 近线性；小 → 极局部
- **中心化必须在 kernel matrix 上**做（feature space 不可见）
- ⚠️ **Pre-image problem 病态** → **不是 generative**
- VAE 解决了 pre-image（decoder 就是反映射）

---

# 🟡 六、Curse of Dimensionality 细节

## 现象 ⭐
高维中，最远邻和最近邻**距离比**趋近 1：
- 1 维 / 2 维：比值很大
- 1000 维：max ≈ min → 近邻概念失效

## 影响
- **k-means**、**DBSCAN**、所有 Euclidean 聚类都**失败**
- 簇边界融化
- ε 在 DBSCAN 中无法选

## 应对 ⭐
**先降维（UMAP / PCA），再聚类**。
单细胞、文本（contextual embedding）等领域**标准流水线**。

---

# 🟢 七、Ch 8 软聚类小补充

## mclust 的 14 种协方差参数化

记号：**volume / shape / orientation** × **equal / variable**。
| 名称 | 含义 |
|---|---|
| **EII** | Equal volume、Identity（最受限）|
| **VII** | Variable volume、Identity |
| **EEI** | Equal volume、Equal shape、axis-aligned |
| **VVV** | Variable 一切（最一般）|

→ mclust 跑所有 14 种 × 每个 K → 按 **BIC（越高越好）**选。

## Latent Profile Analysis (LPA)
- = **continuous 指标 + discrete latent**
- 与 **diagonal-covariance GMM** 数学上**相同**
- 不同社会学传统、不同命名

## Mixture of Factor Analyzers
- GMM 中每组件的协方差由**低秩 factor model** 给出
- 适合**高维**数据（D 大）

## LCA with Covariates
- 让 latent class 成员概率依赖观测协变量
- multinomial logistic regression on **w_i**
- 问：人口学是否预测 class 归属？

---

# 🟢 八、Ch 9 文本小补充

## word2vec 训练技巧

**Subsampling frequent words**：
- 训练前以概率丢弃每个 token
- 频率高的丢得多
- 阈值 t ≈ 10^−5
- 防止"the"主导训练信号

**Noise distribution for negative sampling**：
- 不是 uniform
- = unigram 频率的 **3/4 次幂**
- 上调稀有词、下调高频词
- 3/4 是经验值

## Analogies ⭐
- 经典：**king − man + woman ≈ queen**
- **Paris − France + Italy ≈ Rome**
- 两类：
  - **Syntactic**（walked, walking, ran, running）
  - **Semantic**（country, capital）
- 出自分布结构：similar context → similar geometric position

## Co-occurrence Matrix 用途
- 是 **LSA**（SVD on co-occurrence）的输入
- 是 **GloVe**（log co-occurrence 加权拟合）的输入
- 体现 **distributional hypothesis**："you shall know a word
  by the company it keeps"

---

# 🟢 九、Ch 12 Autoencoder 小补充

## Contractive Autoencoder ⭐
- 第三种正则化变体（plain AE 表里漏了）
- 惩罚 **encoder Jacobian** 的 Frobenius 范数
- 让 encoder 对输入小变动**局部不敏感**
- 与 **denoising AE** 紧密相关
  （denoising = sampled corruption，contractive = 解析）

## AE 三大正则化变体对比

| 变体 | 怎么做 |
|---|---|
| **Denoising AE** | 加噪输入 → 重构干净 |
| **Sparse AE** | L1 惩罚 bottleneck 激活 |
| **Contractive AE** | 惩罚 encoder Jacobian |

→ 三者**不互斥**，常组合 denoising + sparsity。

## VAE 生成用法 ⭐
训练后两个用途：
1. **Sample**：从 prior 抽 z → decode → 合成
2. **Interpolation**：两真实数据点的 z 之间线性插值 → 平滑序列
   （图像 VAE 经典演示）

## Semi-Supervised AE / VAE
- 连续 latent + **categorical latent**（class label）
- 结构先验让 categorical 对应 class
- 小标注 + 大无标注 → 模型**自动分离 class vs style**
- 标注稀缺时的标准范式
- 适用 VAE 和 AAE

## VAE / AAE 解决 plain AE 的什么 ⭐
**Plain AE 的 latent space**：
- 不规整、不连续、不约束到任何分布
- 从中随便采样 → **decoder 给 nonsense**

**VAE / AAE 的目的**：
- **整理 latent space**，让它可采样
- VAE 用 **KL 正则** 约束到接近 standard normal
- AAE 用 **discriminator** 约束到任意 prior

---

# 🎯 补遗的高频考点（10 条）

1. **Recsys ↔ Spatial voting** 同一矩阵分解，不同实质解释。
2. **BPR vs MF**：top-k 用 BPR，评分预测用 MF。
3. **Implicit feedback** 没有负样本；用 confidence-weighted。
4. **ZCA whitening 后 Euclidean = Mahalanobis**。
5. **Gower** = 混合类型数据；**Cosine** = 文本默认。
6. **CoT trace 不一定忠实** —— 提升精度但别当解释。
7. **Chinchilla scaling**：模型大小和数据有**最优配比**。
8. **Cohen's κ** = categorical inter-rater；**ICC** = continuous。
9. **Oblique 旋转**适合心理学（factors 通常相关）。
10. **MVU eigenvalue gap → intrinsic dimension**。

---

## 完整文件清单

现在你有：
- `CHEATSHEET_topic.md` — 主版（按主题）
- `CHEATSHEET_topic_supplement.md` ← **本文件**（补遗）
- `CHEATSHEET_bilingual.md` — 旧版（按章节、中英混合）
- `CHEATSHEET.md` — 最早版（按章节、纯中文）
- `CHEATSHEET_Ch3*.md` — Ch3 单独版

**建议复习顺序**：先扫 `CHEATSHEET_topic.md` → 再过 `CHEATSHEET_topic_supplement.md`。
