# UML4SS Cheatsheet — 概念版（Ch 3–12）

考试不考公式、不考推导。
重点：概念、直觉、方法选择、常见陷阱。

---

## Ch 3. Measurement, similarity, proximity

### Stevens 测量层级
| 层级 | 允许操作 | 例子 |
|---|---|---|
| Nominal | 计数、众数 | 性别、政党 |
| Ordinal | 排序、中位数 | Likert、学历 |
| Interval | 减法、均值、SD | 摄氏温度、IQ |
| Ratio | 所有算术 | 身高、反应时间 |

名义变量算均值是范畴错误；
区间变量算几何均值无意义（零点随意）。

### Scale vs. Index（最常考的概念区分）
- **Scale（反映性 reflective）**：潜变量 *引起* 项目。
  项目应相关、可互换。用 α、因子分析。例：焦虑量表。
- **Index（形成性 formative）**：项目 *构成* 潜变量。
  项目不必相关，删一项改变定义。
  α 和因子分析**不适用**。例：SES。
- **判别**：构念能在项目不变时变化吗？
  能 → 反映性；不能 → 形成性。

### Classical Test Theory (CTT)
- 观测分 = 真分 + 误差。
- **Reliability（信度）**：真分方差占观测分方差的比例。
- 信度是效度的**必要不充分条件**。
  浴室秤永远多 10 磅：reliable 但 invalid。

### Cronbach's α
- 内部一致性最常用系数。
- 阈值：0.7 够、0.8 好、0.9 优秀。
- **三个常见批评**：
  1. 项目越多 α 越高（机械效应）。
  2. 假设 **tau-equivalent**（所有项目同等载荷）。
  3. 高 α **不等于** 单维度。

### McDonald's ω
- 从因子模型直接算信度，比 α 稳健。
- **ω_t**：所有公共因子解释的方差比例。
- **ω_h**：bifactor 模型中**一般因子**的比例。
  ω_h/ω_t 高 → 即使多维，总分仍可辩护。

### 信度类型
| 类型 | 测什么 |
|---|---|
| Test-retest | 时间稳定性 |
| Parallel forms | 等价版本一致 |
| Internal consistency | 项目一致（α、ω）|
| Inter-rater | 评分者一致（κ、ICC）|

### Validity（效度）
效度是**论证**，不是系数。五类证据：
- Content、Internal structure、
- Relations to other variables、
- Response processes、Consequences。

**Face validity 是最弱的证据**，易被社会期望污染。

### MTMM
- 同特质不同方法 → 应高（聚合证据）。
- 不同特质同方法 → 中等（方法偏差）。
- 不同特质不同方法 → 应低（区分证据）。

### DeVellis 八步量表开发
关键点：
- 题目池要冗余；
- 专家评审；
- 每项至少 10 个受访者；
- **最后用独立样本验证（最常被跳过）**。

### PCA vs Factor Analysis
| | PCA | FA |
|---|---|---|
| 性质 | 描述性 | 概率模型 |
| 分解 | 总方差 | 公共+唯一方差 |
| 用途 | 降维、复合分数 | 测试潜在原因 |

### 决定因子数
- Scree plot（找拐点）。
- Kaiser（λ > 1，常**过度保留**）。
- **Parallel analysis**：与随机数据比，**最稳妥**。

### 因子旋转
- **Varimax**（正交）：因子不相关。
- **Oblimin / Promax**（斜交）：允许因子相关，
  多数心理学构念应用斜交。
- 目标：**简单结构**——每项主载一个因子。

### Bifactor vs Hierarchical
- **Hierarchical**：一阶因子上有二阶通用因子（中介）。
- **Bifactor**：通用因子和特定因子**并列**载荷在项目上。

### EFA vs CFA
- **EFA**：探索，发现结构。
- **CFA**：验证，强加结构，给拟合指标。
- **标准流程**：EFA → CFA 在**独立样本**上。
  同样本同时做 = chance capitalization。

### Item Response Theory (IRT)
- 处理二分、有序响应。
- **2PL** 两个参数：
  - **difficulty (b)**：50% 认可的特质水平。
  - **discrimination (a)**：ICC 斜率，区分能力。
- **3PL** 加 guessing 参数（多选题猜对）。
- **Graded Response Model**：有序多分类。

### Item information
- 项目在难度 b 附近提供最多信息。
- Test info = 各项目信息之和。
- **CAT**（自适应测验）：按当前 θ 估计选题。

### Differential Item Functioning (DIF)
- 同 θ 不同群体对项目认可概率不同。
- **不等于群体均值差异**。
- 包含 DIF 的量表跨组直接比较是**误导**的。

### CTT vs IRT
| | CTT | IRT |
|---|---|---|
| 分数 | 总分 | 潜在 θ |
| 难度 | 样本依赖 | 样本不变 |
| SE | 区间常数 | 随 θ 变化 |
| 样本量 | 几百 | 500+ |

### 统一的潜变量观点
| 指标 \ 潜变量 | 连续 | 离散 |
|---|---|---|
| 连续 | 因子分析 | Latent Profile |
| 类别 | IRT | Latent Class |

### 距离选择
- **Euclidean**：默认；先标准化。
- **Manhattan**：对异常值稳健。
- **Mahalanobis**：用协方差校正特征相关。
- **Cosine**：忽略模长；文本标准。
- **Jaccard**：二元集合相似度。
- **Gower**：混合类型数据。

---

## Ch 4. Recommender systems & spatial models

### 推荐问题
- 用户 × 物品矩阵，大部分缺失。
- **Explicit**（评分）vs **Implicit**（点击）。
- Implicit 没有"负样本"。
- 数据 **MNAR**：人更愿评强观点项目。

### Baseline 必先建
预测 = 全局均值 + 用户偏置 + 物品偏置。
**MF 提升应相对基线报告**，不是相对零预测。

### Matrix Factorization
- 每个用户/物品一个低维向量，预测 = 内积+基线。
- 维度 K 一般 10–200。
- 全观测时等价于**截断 SVD**。
- 有缺失时只在观测项上最小化平方误差 + 正则。
- 对 P、Q 联合**非凸**，分别凸 → ALS。

### ALS vs SGD
- **ALS**：交替最小二乘，可并行，生产主力。
- **SGD**：随机挑观测项更新，超大规模更适合。

### Probabilistic MF
- 高斯似然 + 高斯先验，MAP = ridge MF。
- 优点：预测不确定性；推广到非高斯似然。

### 变体
- **NMF**：非负 P、Q。部件式、稀疏、可解释。
- **Implicit feedback**：观测交互正样本+置信度；
  未观测对作低置信负样本，全部计入损失。
- **BPR**：优化排序，适合 top-k 推荐。
- **Factorization Machines**：加辅助信息和交互。
- **Neural CF**：内积换神经网络；
  表达力↑，可解释性↓，SVD 性质丢。

### 评估
- 评分预测：RMSE、MAE。
- Top-k：Precision@k、Recall@k、NDCG、MAP。
- 必须在留出项上评估。

### Spatial voting（孪生兄弟）
- 议员 × 议案投票矩阵。
- 议员有 ideal point；议案有 yea/nay 位置。
- 议员投给更近的位置。
- 经典实现：W-NOMINATE、Poole-Rosenthal。
- **识别问题**：旋转/反射等价 → 锚定已知议员。

### Recsys ↔ Spatial 对应
代数几乎相同：
用户 ↔ 议员；物品 ↔ 议案；评分 ↔ 投票。
推荐优化**预测**；空间模型优化**测量**。

---

## Ch 5. Nonlinear dimensionality reduction

### Manifold hypothesis
- 高维数据通常位于低维**流形**附近。
- **Intrinsic dimension**：实际自由度数，
  远小于环境维度。手写数字 784 维，内在 10–20 维。

### Geodesic vs Euclidean
Swiss roll 上：同弧上两点 geodesic 近、Euclidean 远。
几乎所有流形方法都在某种方式上替换 Euclidean。

### 七种方法一览
| 方法 | 保留什么 | OOS 支持 |
|---|---|---|
| Isomap | 图最短路径距离 | 无 |
| LLE | 局部线性重构权重 | 无 |
| Laplacian Eigenmaps | 邻居+热核权重 | 无 |
| Kernel PCA | 核诱导内积 | **有** |
| MVU | 局部距离精确 | 无 |
| t-SNE | 邻居概率 | 无 |
| UMAP | 密度归一化模糊图 | **有** |

只有 KPCA 和 UMAP 原生支持 OOS。

### Isomap
1. 构 k 近邻图，边权 = Euclidean。
2. 全对最短路径（Dijkstra）= 估 geodesic。
3. classical MDS。

只有 k 一个超参。k 太小图断；k 太大短路穿过卷层。

### LLE
- 用 k 近邻的线性重构权重描述每点。
- 找低维位置，让相同权重仍能重构。
- 保留**局部仿射结构**（旋转、平移、缩放不变）。
- 现在比 LE 不常用。

### Laplacian Eigenmaps
- 在热核加权邻居图上，让强连接的点在嵌入靠近。
- 解：图拉普拉斯最小非零特征值对应的特征向量。
- **关键**：UMAP 的初始化就是 LE。

### Kernel PCA
- 用核函数把数据隐式映射到高维特征空间做 PCA。
- 常用核：linear、polynomial、**RBF（高斯）**。
- **原生 OOS**：新点核相似度投影到保存的特征向量。
- **Pre-image 问题**：从嵌入反推原始数据病态。
  → KPCA 是特征提取工具，不是生成工具。

### MVU
- 把流形当卷起的纸，邻居用"刚性杆"连，
  拉到最远。半正定规划 (SDP)。
- **特征值谱直接显示内在维度**——清晰的谱间隔。
- **实际很少用**：SDP 太贵，最多 1–2 千点。

### t-SNE
- 高维和低维分别建邻居概率分布，最小化 KL。
- **Perplexity（困惑度）**：有效邻居数。
  默认 30；低（5–10）极局部；高（50–100）大邻域。
- **低维用 Student-t**（重尾）解决 **crowding problem**。

### t-SNE 三大警告
1. **簇间距离没有意义**。
2. **簇大小没有意义**。
3. **全局结构丢失**——只保留邻居身份。

### UMAP
- 类似 t-SNE 但有几个关键差异：
- **高维**：密度归一化——每点的邻域距离用
  最近邻距离归一，稀疏区和稠密区可比。
- **损失函数有显式排斥项**（t-SNE 没有）。
- **初始化**：先做 Laplacian Eigenmap。
- **支持 OOS**：保存模型后嵌入新数据。
- 超参：`n_neighbors`（局部/全局）、
  `min_dist`（簇紧凑度）。

### t-SNE vs UMAP
| | t-SNE | UMAP |
|---|---|---|
| 初始化 | 随机 | LE 暖启动 |
| 显式排斥 | 无 | 有 |
| 全局结构 | 丢失 | 部分保留 |
| OOS | 无 | 有 |

UMAP 现在是默认选择。

### 决策树
1. 先试 PCA。
2. 大规模可视化 → UMAP。
3. 生产 OOS → KPCA 或 UMAP。
4. 验证等距嵌入或估内在维度 → Isomap 或 MVU。

---

## Ch 6. Hard clustering — partitioning & hierarchical

### 三个根本难点
1. **没有 ground truth**。
2. **算法即假设**——每个算法对"簇"有不同假设。
3. **维度灾难**——高维中最近邻和最远邻距离趋同。
   → 标准应对：**先降维再聚类**。

### Kleinberg 不可能定理
聚类函数无法同时满足三性质：
1. **Scale-invariance**：距离整体缩放后划分不变。
2. **Richness**：所有划分都能通过某距离实现。
3. **Consistency**：簇内缩小、簇间拉大后划分不变。

→ k-means 违反 consistency；
single-linkage HAC 违反 richness。

**意义**：算法选择本身是实质性选择。

### k-means
- 目标：最小化簇内平方和（WCSS）。
- **Lloyd 算法**：分配到最近质心 → 更新为均值 → 重复。
  局部极小，有限步收敛。
- **几何**：Voronoi 区，**只能产生直线边界**。
  → 非凸形状失败。

### k-means 必知
- **初始化敏感**：补救：
  - `nstart = 25+` 多起点。
  - **k-means++**：按到最近已选质心的距离概率选种子。
- **永远先 scale！**否则被最大方差特征支配。

### k-means 失败模式
1. 非凸形状 → 用 DBSCAN / spectral。
2. 簇大小或方差差异巨大 → 用 GMM。
3. 异常值 → 用 PAM。

### 降维 + 聚类
高维数据先 UMAP → 再 k-means。
单细胞、文本等领域标准做法。

### k-medoids (PAM)
- 质心换成**真实数据点**——medoid。
- 算法：BUILD（贪心选种子）+ SWAP（试替换）。
- **两大优势**：
  1. Medoid 是真实观测 → 可解释原型。
  2. 支持**任意**不相似度（Manhattan、Gower、编辑距离）。
- 大 N 用 **CLARA**（子样本上跑 PAM）。

### Hierarchical Agglomerative Clustering (HAC)
- 每点单独簇开始 → 合并最相似的两个 → 重复。
- 输出 **dendrogram**。
- **确定性**：无随机、无初始化、无局部极小。
- 切树高度 → 任意数量簇。
  大纵向间隔暗示自然切点。

### 读 dendrogram 警告
- **只有高度轴有意义**。
- 横向位置由绘图算法决定，相邻叶子不一定相似。

### Linkage 准则
| 名称 | 倾向 |
|---|---|
| Single | **Chaining**；细长簇；噪声敏感 |
| Complete | 紧凑、等径；可能拆分长形 |
| Average | 折中 |
| **Ward** | 紧凑等大；k-means 的层次版 |

R 中用 `ward.D2`，别用 `ward.D`（bug）。

### 选 K
- **Elbow**：WCSS vs K，找肘部。
- **Silhouette**：每点合得来分数，范围 [-1, 1]。
  选最大化平均轮廓系数的 K。
- **Calinski-Harabasz**：簇间/簇内方差比；
  偏向等大球形。
- **Gap statistic**：与随机参考数据对比。**最有原则**。

### 没有自然 K 时
环上均匀分布的点，所有方法都给某个 K，
但毫无实质意义。**判断"无自然 K"是分析者的，
metrics 辅助但不替代**。

### 外部验证（有标签时）
- **ARI**：成对一致性，经偶然校正。**最常报告**。
- **NMI**：归一化互信息。
- **V-measure**：homogeneity + completeness 调和均值。

### Cluster stability
- Bootstrap 重采样，看簇的 Jaccard 重叠。
- >0.85 高稳定；<0.6 可能是 artifact。

---

## Ch 7. Density-based & spectral clustering

### 为什么需要它们
Ch 6 假设簇是凸团。
真实结构是半月、同心圆时 k-means 切错。

### DBSCAN
**前提**：簇 = 通过稠密邻域连接的点集。

两个超参数：**ε（邻域半径）** 和 **minPts**。

三类点：
- **Core**：ε 邻域内 ≥ minPts 个点。
- **Border**：在某 core 的邻域内，自己不是 core。
- **Noise**：都不是，不分配到任何簇。

**Density-reachable**：通过 core 点链传递。
**簇** = 最大密度连通集合。

### DBSCAN 调参
- **minPts**：经验 ≥ D+1，低维 4–5 标准。
- **ε**：**k-distance plot** 找肘部。

### DBSCAN 优势/劣势
- **优**：不需指定 K；任意形状；显式 noise；快。
- **劣**：
  - ε 在中等维度难选（距离集中）。
  - **要求单一密度**。
  - Border 分配依赖访问顺序。

### HDBSCAN
**核心改进**：去掉 ε，自动处理变密度。

- **Mutual reachability distance**：用 core 距离改造的度量，
  把稀疏区的点拉远，稠密区不变。
- 在 mreach 图上构 MST → 层次。
- **Cluster stability**：簇在层次中持续的"面积"。
- 只有 **minPts** 一个超参。

**何时帮**：变密度数据强项。
**何时不帮**：纯均匀噪声背景里的渐变带。
DBSCAN 和 HDBSCAN **互补诊断**而非替代。

### Spectral clustering
**思路**：聚类 = 图切割问题。

**算法**：
1. 构相似性图（k-NN 或高斯全连接）。
2. 计算归一化图拉普拉斯。
3. 取最小 K 个特征值的特征向量。
4. 在这些特征向量上做 k-means。

**为什么有效**：图断成 K 块时，零特征值有 K 重，
对应特征向量是各块的指示向量。
**近乎**断开时近似指示簇成员。

**优**：任意形状、谱间隔诊断 K。
**劣**：N×N 特征分解贵；对图选择敏感；
最后一步 k-means 的问题都继承。

### 三方法对比
| | DBSCAN | HDBSCAN | Spectral |
|---|---|---|---|
| 超参 | ε, minPts | 只 minPts | K + 图参数 |
| 任意形状 | ✓ | ✓ | ✓ |
| 变密度 | ✗ | **✓** | 部分 |
| 显式 noise | ✓ | ✓ | ✗ |

---

## Ch 8. Soft clustering & finite mixtures

### Hard vs Soft
- Hard：每点一个簇标签。
- Soft：每点的**簇成员概率分布**（responsibility）。
- Hard = MAP 规则 = 取 max responsibility 的簇。

### 三种方法的共同骨架
**Finite mixture model**：数据来自少数生成分布。
推断恢复组件参数 + 每观测的后验归属。
算法骨架统一：**EM**——
E 步算 responsibility，M 步用 responsibility 作权重更新。

### Conditional independence 关键假设
**给定潜类别，观测特征条件独立**。
LCA、LDA、对角协方差 GMM 的默认。

**身高-鞋码例子**：合并人群相关高；分性别看相关接近零。
**相关由潜组诱导，组内无结构**。

**当假设成立**：组件干净可解释。
**当假设违反**：算法**把单个真实簇拆成多个**
来吸收组内相关 → K 被人为放大。

### Gaussian Mixture Model (GMM)
- **生成故事**：先抽组件标签，再从该高斯抽 x。
- **Responsibility**：观测来自每个组件的后验概率。
- **EM 步骤**：
  - E 步：算 responsibility。
  - M 步：用 responsibility 作软计数更新参数。
- 多起点必备（局部极大）。
- **k-means 是 GMM 的极限**：各向同性协方差缩到零。

### 协方差形状
- **Spherical**：圆球。
- **Diagonal**：组内特征不相关。
- **Full**：每组件自己的相关结构。

### GMM vs k-means
| | k-means | GMM |
|---|---|---|
| 分配 | 硬 | 软 |
| 簇形状 | 等径球 | 椭圆 |
| 不确定性 | 无 | 完整后验 |
| 选 K | elbow、silhouette | BIC |

### Latent Class Analysis (LCA)
GMM 的类别变量版本。
- 观测项目是类别。
- **Local independence**：给定潜类别项目独立。
- 选 K 用 BIC（多起点必备）。

### Local independence 失败诊断
- **Bivariate residual**：每对项目的观测 vs 拟合频数。
  大残差 = 类别后仍有依赖。
- 失败时 BIC 偏好**更大 K**（多类吸收类内相关）。

### LCA with covariates
让类别成员概率依赖观测协变量。
问：人口学特征预测类别归属吗？

### 三方法总结
| | GMM | LCA | LDA |
|---|---|---|---|
| 数据 | 连续 | 类别 | 文本 |
| 软分配 | r_ik | r_ik | θ_d |
| 推断 | EM | EM | VEM 或 Gibbs |
| 选 K | BIC | BIC | coherence |

---

## Ch 9. Text — bag-of-words to word embeddings

### 预处理流水线
1. **Tokenize**：
   - Whitespace/规则（Treebank）：社科默认。
   - Subword（BPE、WordPiece）：现代 LM 标配。
2. **Normalize**：
   - 小写、去标点。
   - **Stemming**：砍后缀，会**过度合并**。
   - **Lemmatization**：用词典返回词典形。**首选**。

### Bag-of-words (BoW) 假设
- 丢弃词序。
  "Dog bites man" = "Man bites dog"。
- **DTM**：行=文档、列=词、值=计数。真实语料 99%+ 稀疏。

### TF-IDF
- raw count 过度权重常见词；
  TF-IDF 用文档频率倒数下调它。
- 出现在所有文档的词被压为零。
- **关键警告**：**不要把 TF-IDF 喂给 LDA**——
  LDA 期望离散计数。
  TF-IDF 用来**筛词汇**，然后传 raw count。

### n-grams
- "climate" + "change" 分开丢失短语。
- 把 "climate_change" 作为单 token 包含进 DTM。

### Co-occurrence matrix
- V×V 矩阵，统计窗口内共现次数。
- **分布假设**："上下文相似 → 含义相似"。
- 用作 LSA、GloVe 的输入。

### Word embedding 目标
- 词汇 → 低维稠密向量。
- 相似上下文的词几何上靠近。
- 支持 cosine、聚类、线性运算。
- **"Static"**：每词一个向量，不管上下文。

### word2vec 两个架构
- **CBOW**：用上下文预测中心词。
- **Skip-gram**：用中心词预测每个上下文词。
  **对稀有词更好**（CBOW 把稀有词淹没在平均里）。

### Negative sampling (SGNS)
- 完整 softmax 在百万词汇上归一化不可行。
- Negative sampling：每个真对配 k 个"负样本"，
  做二分类。每次更新只接触 k+1 个向量。

### Levy-Goldberg 结果
SGNS 隐式分解 **shifted PMI** 矩阵。
**意义**：word2vec 是矩阵分解的伪装。

### GloVe
- 直接对共现矩阵的对数做加权最小二乘拟合。
- 比 SGNS 在大语料上**训练快**。
- 嵌入质量相似。

### word2vec vs GloVe
| | SGNS | GloVe |
|---|---|---|
| 输入 | 流式语料 | 预计算共现 |
| 训练成本 | 线性于语料 | 线性于非零共现 |
| 稀有词 | skip-gram 好 | 稳健 |

### Analogies
king − man + woman ≈ queen。
出自分布结构：相似上下文 → 相似位置。

### Static embedding 的致命缺陷：**Polysemy**
- "bank"（河岸 vs 银行）只有一个向量。
- 是各义项的加权平均。
- 需要词义区分时 → contextual embeddings（Ch 11）。

### 社科 text-as-data 两条警告
1. **每个建模选择是实质性选择**——全部报告。
2. **验证不可少**——topic、cluster、embedding 给的是
   **假设**而非发现。

---

## Ch 10. Probabilistic topic models

### 大画面
- Word embedding 回答词级问题；
  topic model 回答**文档级**问题。
- 文档很少只关于一个东西。
- **Topic = 词汇上的概率分布**，不是标签。

### LDA 生成故事
1. 对每个主题：从 Dirichlet 抽词汇分布 φ_k。
2. 对每个文档：
   - 从 Dirichlet 抽主题分布 θ_d。
   - 对每个词位置：从 θ_d 抽主题，再从 φ_k 抽词。

| 符号 | 含义 |
|---|---|
| K | 主题数（用户指定）|
| θ_d | 文档-主题分布（tidytext "gamma"）|
| φ_k | 主题-词分布（tidytext "beta"）|
| α | θ 的浓度，小 → 文档稀疏 |
| η | φ 的浓度，小 → 主题稀疏 |

### 推断（不需会推导）
- **Variational EM (VEM)**：快、确定性。
- **Collapsed Gibbs sampling**：直觉清楚——
  每词主题概率正比于"该文档已用此主题多少
  × 该主题已用此词多少"，两个力量平衡。

### LDA 预处理决定一切
- **自定义 stopword**：通用列表不够。
  国会演讲会出现 "gentleman、yield、speaker"。
- **n-grams** 合并多词短语。
- **Lemmatize > stem**。
- **TF-IDF 筛词汇**，然后传 raw count。

### 选 K——本章最重要的话题

**Perplexity（困惑度）**：
- 留出文档上的反向几何平均似然，数学上无可指责。
- **但是**：**Chang et al. "Reading Tea Leaves"** 显示
  perplexity **更低**的模型在人类入侵任务上**更差**。
- 优化 perplexity 系统性损害可解释性。

**两个入侵任务**：
- **Word intrusion**：5 个 top words + 1 个外来词，找入侵者。
- **Topic intrusion**：文档 + 3 个高概率主题 + 1 个低概率主题。

**Coherence**：从 top words 算单一分数。
**与入侵任务相关性远好于 perplexity**。

**Exclusivity**：top words 是否独有？
通用词在多主题都出现 → 该主题不有用。

**Cardinality caveat**：coherence 在更大 K 上机械偏高。
不要跨大幅不同的 K 直接比较 coherence。

**工作流**：
1. 钉死预处理。
2. 扫 K（10、20、30、40、50）。
3. coherence vs exclusivity 找 Pareto frontier。
4. 读 top words 挑可解释性最好的。
5. ±20% K 稳定性检查。

### Structural Topic Model (STM)
**问题**：plain LDA 把文档当作可交换，
但社科问题正是关于元数据（党派、年份、实验条件）。

**有缺陷的两步法**：先 LDA 再回归 θ_d。
问题：θ_d 估计不确定 → **系数被衰减**。

**STM 解决方案**：协变量**直接嵌入**生成模型。
- **Topic prevalence**：协变量影响"主题多少"。
- **Topic content**：协变量影响"主题被如何谈论"。
- `estimateEffect()` 给协变量效应及标准误。

### Biterm Topic Model (BTM)
**问题**：LDA 在短文本（tweets、headlines）上失败。
单文档 token 太少。

**解决**：放弃文档级故事，
用全语料的**无序词对（biterm）**作单元，
topic 是 biterm 分布。

**经验法则**：平均文档长度 < 50 → 用 BTM 或 BERTopic。
LDA 在短文本上**沉默失败**，给貌似合理但不可靠的主题。

### Topic models vs Word embeddings
| | LDA / STM | word2vec / GloVe |
|---|---|---|
| 单元 | 文档 | 词 |
| 上下文 | 整个文档 | 局部窗口 |
| Polysemy | 捕捉 | 不捕捉 |

### 2026 工作流
1. **STM** 做结构推断（协变量）。
2. **BERTopic** 做语义探索。
3. 两者分歧 = 最有趣的实质发现。
4. 用人工编码子样本或 LLM 入侵任务验证。

---

## Ch 11. Contextual embeddings & modern topic models

### 大画面
Static embedding 给 "bank" 一个向量；
contextual 让 "bank" 在不同句子里得不同向量。

### Attention 直觉
- BoW 每词贡献相等。
- 滑窗模型固定窗口。
- Attention：每位置输出是**整个序列**的加权平均，
  权重由序列本身计算。

### Query, Key, Value
- 每 token 投影成三个向量：
  - **Query**：位置 i "在找什么"。
  - **Key**：位置 j "能提供什么"。
  - **Value**：位置 j 实际"贡献什么"。
- 权重 = Q 和 K 的相似度。

### Self-attention & Multi-head
- **Self-attention**：Q、K、V 都来自同一序列。
- **Multi-head**：并行多个头学不同关系
  （句法、共指、语义相似）。

### Causal mask
- **Bidirectional**（BERT）：attend 整个序列。
- **Causal**（GPT）：只看自己和之前，用于生成。

### Transformer block
1. Multi-head self-attention。
2. Residual + layer norm。
3. Position-wise feed-forward。
4. Residual + layer norm。

堆叠多层。**Position embedding** 必加，
否则 attention 对顺序无感。

### BERT 预训练
- **Masked Language Modelling (MLM)**：mask 15% token，
  从两侧上下文预测。
- **Next-Sentence Prediction**：后来证明贡献小，
  多数后继模型放弃。

### Sentence-BERT
- 直接平均 BERT token 向量效果差。
- Sentence-BERT 用 siamese 架构 fine-tune，
  得到固定大小句嵌入。cosine 可比。

### BERTopic 流程
1. **Embed**：sentence transformer 编码每文档。
2. **Reduce**：UMAP 压到 5–15 维。
3. **Cluster**：HDBSCAN，自动给 noise 类。
4. **Describe**：**c-TF-IDF**——每簇的文档拼成
   "类文档"，得到该簇相对其他簇的特征词。

### BERTopic 优势 / 局限
- **优**：短文本好；多义词稳健。
- **限**：c-TF-IDF 标签仍是单词；
  **不直接支持协变量建模**——社科仍需 STM。

→ **双 pass workflow**：STM 结构推断 + BERTopic 语义探索。

### Foundation models
- 单一大型网络在广语料预训练。
- **Scale 是定义性特征**。

### Scaling laws
测试损失是模型大小、数据、计算的幂律函数。
**对任何计算预算有最优分配**。

### In-context learning
- 模型足够大后能从 prompt 几个示例
  **学会新任务，无需梯度更新**。
- 社科意义：分类、抽取从 fine-tune 变成 prompt 工程。
- **验证不可商量**——看起来正确不等于正确。

### Few-shot vs Zero-shot
- **Few-shot**：prompt 含示例。
- **Zero-shot**：只有任务描述。

### Chain-of-thought (CoT)
- 在示例里包含**中间推理步骤**。
- 在多步推理任务上显著提升。
- **重要警告**：CoT trace 与模型实际计算
  **不保证忠实**——用 CoT 提升精度，
  **不要把 trace 当真实解释**。

### LLM 推理短板
擅长流利语言，弱于多步算术、形式逻辑。
应对：CoT、工具使用（计算器/Python）、推理语料训练。

### Agents
LLM + 工具调用 = agent。
把标注任务从重劳动变成 prompt 工程。
**仍需分层抽样的人工审查**。

### 可复现性要求
- 模型版本号、temperature（分类用 0）、种子。

---

## Ch 12. Autoencoders, VAEs, AAE

### 该章的位置
- Ch 2/4 线性方法：投影+内积重构。
- Ch 5 流形方法：非线性嵌入但**没有重构映射**。
- **Autoencoder 填洞**：非线性嵌入 + 学到的函数。

### Plain Autoencoder
- **Encoder**：输入 → 低维潜表示。
- **Decoder**：潜表示 → 重构。
- 目标：重构损失。
- 瓶颈维度 L：太小重构差；太大学到平凡复制。

### 关键事实：Linear AE = PCA
- 线性 encoder + decoder + MSE 时，
  AE 优化的子空间**正是 top-L PC 子空间**。
- 轴可能不同（任意基），**子空间相同**。
- **意义**：
  1. 线性关系下 PCA 更简单更好。
  2. **AE 比 PCA 的所有提升都来自非线性激活**。

### 正则化变体
- **Denoising AE**：输入加噪，重构干净。
  强制网络投影到数据流形。
- **Sparse AE**：L1 惩罚瓶颈激活，
  不同输入激活不同少量单元。
- **Contractive AE**：惩罚 encoder Jacobian，
  局部不敏感。

### Variational Autoencoder (VAE)
**关键改变**：编码器输出**概率分布参数**而非单点。
从该分布采样 z 传给解码器。
最大化数据 log-likelihood 的**下界 (ELBO)**。

### VAE 是生成模型
训练后从先验抽 z 解码 →
**像训练数据的合成观测**。
Plain AE 没有生成解释。

### Amortized inference
**一套参数 φ** 通过网络定义每输入的近似后验，
而非每观测一个变分分布——
经典 VI 相比的核心效率提升。

### ELBO 两项的拉锯
- **Reconstruction term**：要 q 编码 x 信息。
- **KL term**：要 q ≈ 先验。
- 训练好的 VAE 是妥协。

### Reparameterization trick
**问题**：要对 φ 求 reconstruction 梯度，
但采样在 φ 上不可微。

**技巧**：把 z 重写为 φ 的确定函数 + 来自固定分布的噪声。
随机性不依赖 φ；梯度可流。
**让 VAE 可用 SGD 训练的技术创新**。

### VAE 中的三个分布
易混点：
1. **编码器** 输出潜变量分布（近似后验）。
2. **解码器** 输出输入空间分布（条件似然）。
3. **先验** 在潜空间上锚定几何。

### VAE 比 plain AE 多三样
1. **概率嵌入**：每输入一个分布，方差是不确定性。
2. **生成模型**：从先验抽 → 合成数据。
3. **良条件潜空间**：KL 让分布靠近标准正态，
   任意区域解码都合理。

### VAE vs PPCA
**PPCA = VAE 的线性极限**。
换成神经网络 → 表达力↑，失去闭式解。
→ VAE 是因子分析家族的**非线性深度学习表亲**。

### Adversarial Autoencoder (AAE)
- KL 正则换成**鉴别器网络**。
- 编码器训练成"骗过鉴别器"。
- **优势**：先验自由——任何可采样的先验
  （非高斯、多模、结构化离散）。

### 半监督扩展
- 连续潜旁加**类别潜变量**（class label）。
- 小标注 + 大无标注 → 模型分离 class 和 style。

---

## 贯穿全书的家族关系

| 方法 | 与之关联 |
|---|---|
| PCA | 协方差矩阵特征分解 |
| Linear AE | 神经网络伪装的 PCA |
| PPCA | PCA + 高斯潜变量 |
| VAE | PPCA 解码器换成非线性 |
| Classical MDS | PCA 的对偶 |
| Factor analysis | 更灵活的 PPCA |
| IRT | 类别观测的因子模型 |
| LCA | 离散潜变量的因子模型 |
| LDA | 文档上的混合模型 |
| BERTopic | LDA 架构 + contextual embed |
| k-means | 各向同性硬化的 GMM |
| GMM | k-means 的软泛化 |
| Spectral clustering | LE 特征向量 + k-means |
| MF recsys | 稀疏矩阵的低秩近似 |
| Spatial voting | MF 在投票矩阵上 |

**一句话**：所有方法 = 低维潜结构 + 围绕它的变异。
区别在于"什么算低维、结构、变异"。

---

## 考试日决策速查表

| 任务 | 默认工具 |
|---|---|
| 线性降维 | PCA |
| 非线性可视化 | UMAP |
| 出样本嵌入 | KPCA 或 UMAP |
| 凸簇 | k-means（先 scale）|
| 任意形状、单密度 | DBSCAN |
| 任意形状、变密度 | HDBSCAN |
| 图数据 | Spectral |
| 连续 + 不确定性 | GMM + BIC |
| 类别响应 | LCA |
| 长文档主题 | STM（含协变量）|
| 短文本主题 | BTM 或 BERTopic |
| 语义相似 | sentence-BERT cosine |
| 生成低维 | VAE |

---

## 高频考点

1. **Scale vs Index**：因果方向决定能否用 α、FA。
2. **Reliability vs Validity**：信度是效度的必要不充分条件。
3. **PCA vs FA**：描述 vs 模型；总方差 vs 公共+唯一。
4. **EFA vs CFA 同样本** = chance capitalization。
5. **Kleinberg**：scale-inv、richness、consistency 不可同时。
6. **k-means 失败模式** → DBSCAN/spectral、GMM、PAM。
7. **DBSCAN vs HDBSCAN**：单密度 vs 变密度。
8. **Conditional independence 违反 → K 膨胀**。
9. **GMM ↔ k-means**：协方差极限。
10. **Perplexity 误导**：lower ≠ better topics。
11. **STM 的两步法问题**：θ 不确定导致系数衰减。
12. **t-SNE 三大警告**：簇间距离、簇大小、全局结构。
13. **UMAP 比 t-SNE 好**：显式排斥+LE 初始化+OOS。
14. **Static embedding 致命缺陷**：polysemy。
15. **CoT 警告**：trace 不一定忠实。
16. **Linear AE = PCA**：非线性才有额外价值。
17. **VAE 三个分布**：encoder、decoder、prior。
18. **VAE vs PPCA**：PPCA 是 VAE 的线性极限。
19. **AAE vs VAE**：AAE 用鉴别器替代 KL，先验自由。
20. **TF-IDF 不能喂 LDA**：LDA 要离散计数。

考试加油！
