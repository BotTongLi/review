# UML4SS Cheatsheet — 概念版（Ch 3–12）

考试不考公式推导，重点：概念、直觉、方法选择、常见陷阱。

---

## Ch 3. Measurement, similarity, proximity

### Stevens 测量层级
| 层级 | 允许操作 | 例子 |
|---|---|---|
| Nominal | 计数、众数 | 性别、政党 |
| Ordinal | 排序、中位数 | Likert 量表、教育程度 |
| Interval | 减法、均值、SD | 摄氏温度、IQ（无真零点）|
| Ratio | 所有算术 | 身高、反应时间（有真零点）|

→ 在名义变量上算均值是范畴错误；区间变量上算几何均值无意义（零点是随意的）。

### Scale vs. Index（最常考的概念区分）
- **Scale（反映性 reflective）**：潜变量 *引起* 观测项目。项目应该相关，可以互换。用 Cronbach's α、因子分析。例：焦虑测量。
- **Index（形成性 formative）**：项目 *构成* 潜变量。项目不必相关，删一个会改变定义。α 和因子分析**不适用**。例：社会经济地位（SES）。
- **判别问题**：构念能在项目不变的情况下变化吗？能 → 反映性；不能 → 形成性。

### Classical Test Theory (CTT)
- 核心思想：观测分 = 真分 + 误差。三大假设：误差均值为 0；真分与误差不相关；不同项目误差不相关。
- **Reliability（信度）**：真分方差占观测分方差的比例。
- 信度是效度的**必要不充分条件**：浴室秤永远多 10 磅是 reliable 但 invalid；卷尺每次测不同长度是 unreliable，必然 invalid。

### Cronbach's α
- 内部一致性最常用系数。阈值：0.7 够、0.8 好、0.9 优秀。
- **三个常见批评**：
  1. 项目数越多 α 越高（机械效应）。
  2. 假设 **tau-equivalent**（所有项目同等载荷）。载荷不等时低估信度。
  3. 高 α **不等于** 单维度。两个相关因子的混合也能给高 α。

### McDonald's ω
- 从因子模型直接算信度，比 α 更稳健。
- **ω_t（total）**：所有公共因子解释的方差比例。tau-equivalent 时等于 α；否则 ω_t ≥ α。
- **ω_h（hierarchical）**：bifactor 模型中**一般因子**解释的比例。高 ω_h/ω_t → 即使有多维度，总分仍然是该构念的可辩护测量。

### 信度类型
| 类型 | 测什么 | 适用 |
|---|---|---|
| Test-retest | 时间稳定性 | 稳定特质 |
| Parallel forms | 等价版本一致 | 测试安全 |
| Internal consistency (α, ω) | 项目一致 | 单次施测量表 |
| Inter-rater | 评分者一致 | 编码数据；分类用 Cohen's κ，连续用 ICC |

### Validity（效度）
效度是**论证**，不是系数。当代分类（Standards）五类证据：
1. **Content**：项目是否覆盖构念。
2. **Internal structure**：因子结构匹配理论。
3. **Relations to other variables**：聚合 (convergent) 与区分 (discriminant) 相关。
4. **Response processes**：受访者是否按预期方式思考（出声思维法）。
5. **Consequences of testing**：测量的社会后果是否可辩护。

### MTMM（多特质多方法矩阵）
- 同特质不同方法 → 应高（聚合证据）。
- 不同特质同方法 → 中等（同方法偏差膨胀）。
- 同特质同方法 → test-retest 对角。
- 不同特质不同方法 → 应低（区分证据）。

**Face validity（表面效度）是最弱的证据**，且可能误导（高 face validity 容易被社会期望污染）。

### DeVellis 八步量表开发
1. 清晰定义构念 2. 生成冗余的题目池 3. 选择回答格式 4. 专家评审 5. 开发样本（每项至少 10 人）6. 探索性分析 7. 修订题目 8. **在独立样本上验证（最常被跳过）**

### 因子分析（FA）核心概念
- 观测项目 = 因子载荷 × 潜因子 + 项目特有误差。
- 把每个项目的方差分解为：**公共方差**（因子解释的）+ **唯一方差**（项目特有 + 测量误差）。

### PCA vs Factor Analysis
| | PCA | FA |
|---|---|---|
| 性质 | 描述性 | 概率模型 |
| 分解 | 总方差 | 公共 + 唯一方差 |
| 成分/因子 | 数据的精确线性组合 | 不可观测的随机变量 |
| 用途 | 数据降维、复合分数 | 测试潜在原因的模型 |

### FA 提取方法
- **ML（极大似然）**：假设多元正态，给标准误和 χ² 检验，验证性分析标准选择。
- **Principal axis**：对非正态稳健，探索性分析常用默认。
- **Minres**：最小化残差，无分布假设。

### 决定因子数
- Scree plot 找拐点
- Kaiser 准则（特征值 > 1）——常用但**过度保留**
- **Parallel analysis**：与随机数据比较特征值，**最稳妥**

### 因子旋转
- **正交旋转**（varimax）：因子保持不相关。
- **斜交旋转**（oblimin, promax）：允许因子相关，多数心理学构念应该用这个。
- **简单结构**：每项目重载一个因子，其他轻载，便于解释。

### Bifactor vs Hierarchical
- **Hierarchical**：一阶因子载荷在项目上，二阶通用因子载荷在一阶因子上。通用因子的影响通过一阶 *中介*。
- **Bifactor**：通用因子和特定因子**并列**载荷在项目上，特定因子与通用因子正交。
- 两者回答不同问题：hierarchical 问"一阶因子为何相关"；bifactor 问"通用因子在项目层解释多少方差"。

### EFA vs CFA
- **EFA**：探索性，发现结构。所有项目可以载荷在所有因子。
- **CFA**：验证性，**强加**结构，分析者指定哪个项目载荷在哪个因子。返回 CFI、TLI、RMSEA、SRMR 等拟合指标。
- **标准工作流**：开发样本 EFA → 独立样本 CFA。同样本同时做 EFA + CFA 等于"chance capitalization"。

### Item Response Theory (IRT)
- 线性因子模型假设连续正态响应；IRT 处理二分（对错）、有序类别（Likert）等非连续响应。
- **2PL 模型**两个参数：
  - **difficulty (b)**：受访者有 50% 概率认可该项目的特质水平。
  - **discrimination (a)**：item characteristic curve (ICC) 拐点的斜率，区分能力。
- **3PL** 加 guessing 参数（多选题猜对的概率），高风险教育测验常用。
- **Graded Response Model (Samejima)**：有序多分类，每项 1 个区分度 + (K-1) 个阈值。

### Item information & test information
- 一个项目在哪个 θ 水平提供最多信息？答：靠近其难度 b 处。
- Test information function = 各项目信息之和。**SE(θ) = 1/√I(θ)**，所以信度随 θ 变化。
- **CAT（计算机自适应测验）**：给每个受访者匹配其当前 θ 估计的项目，用少得多的题达到目标精度。

### Differential Item Functioning (DIF)
- 同样 θ 的不同群体（性别、语言、世代）对项目认可概率不同。
- **不等于群体均值差异**——是项目映射到构念的方式不同。
- 包含 DIF 项目的量表**跨组直接比较均值是误导的**。
- 检测：Mantel-Haenszel（有序）、lordif、多组 IRT。

### CTT vs IRT
| | CTT | IRT |
|---|---|---|
| 受访者分 | 总分 | 潜在 θ |
| 项目难度 | 样本依赖（% 正确）| 样本不变参数 |
| SE | 整个区间常数 | 随 θ 变化 |
| 样本量 | 几百够 | 通常 500+ |
| 可比性 | 量表内 | 通过 linking 跨工具 |

### 统一的潜变量观点
| 指标 \ 潜变量 | 连续 | 离散 |
|---|---|---|
| 连续 | 因子分析 | Latent Profile Analysis |
| 类别 | IRT | Latent Class Analysis |

### 距离选择
- **Euclidean**：默认；前提是先标准化。聚类、流形学习的默认假设。
- **Manhattan**：对异常值更稳健（单个坐标不能因平方而支配）。
- **Mahalanobis**：用协方差矩阵校正特征间的相关；ZCA 白化后的 Euclidean = 原始数据的 Mahalanobis。
- **Cosine**：向量模长无关；文本分析的标准选择（文档长度是干扰）。
- **Jaccard**（二元）：交集/并集。**Hamming** 数不匹配数。
- **Gower's coefficient**：连续 + 有序 + 名义混合数据；R 中 `cluster::daisy`。

---

## Ch 4. Recommender systems & spatial models

### 推荐问题设置
- 用户 × 物品矩阵，大部分缺失（典型 99%+ 空）。
- **Explicit feedback**（评分、点赞）vs **Implicit feedback**（点击、观看时长）。
- Implicit 没有"负样本"——没点击 ≠ 不喜欢，也可能没看到。
- 数据 **MNAR**（非随机缺失）：人们更倾向于评价自己有强烈观点的物品。

### Netflix Prize 的方法学遗产
- Matrix factorization 成为主流。
- 强调相对于强基线的提升、保留时间结构的评估、ensemble。

### Baseline（必须先建）
预测 = 全局均值 + 用户偏置 + 物品偏置。在 Netflix 数据上已能解释大部分可解释方差。**所有 MF 提升都应该相对基线报告**，不是相对零预测。

### Matrix Factorization
- 每个用户一个向量 p_i，每个物品一个向量 q_j。预测评分 = 基线 + 用户-物品向量内积。
- 维度 K 一般 10–200。
- **若矩阵完全观测**：等价于截断 SVD（Eckart-Young 最优低秩近似）。
- **有缺失时**：只在观测项上最小化平方误差 + 正则化。目标对 P、Q 联合**非凸**，但分别凸 → **交替最小二乘 (ALS)**。

### ALS vs SGD
- **ALS**：固定 Q 解 P（按行的小岭回归），再固定 P 解 Q，迭代。可并行化，生产环境主力。
- **SGD**：随机挑一个观测项更新对应的 p_i 和 q_j。线性于观测数，超大矩阵更适合。

### Probabilistic MF
- 高斯似然 + 高斯先验，MAP 解 = ridge MF。
- 优点：得到预测的不确定性；干净地推广到非高斯似然（二元用 logistic、计数用 Poisson）。

### 变体
- **NMF（非负 MF）**：P、Q 非负。因子是加法组合的"部件"，自然稀疏可解释。也是 TF-IDF 矩阵主题分解的常用工具（LDA 之外的确定性替代）。
- **Implicit feedback (Hu-Koren-Volinsky)**：每个观测交互视为带置信度的正样本，所有未观测对作为低置信度负样本，全部计入损失。
- **Bayesian Personalized Ranking (BPR)**：目标改成排序——让用户喜欢的物品分数高于随机抽取的没交互物品。适合 top-k 推荐而不是评分预测。
- **Factorization Machines**：加入辅助信息（人口学、时间、物品类别），处理稀疏高维特征。
- **Neural CF (NeuMF, Wide & Deep)**：把内积换成神经网络。表达力↑，可解释性↓，SVD 性质丢失。
- **Bandit (Thompson sampling, UCB)**：探索-利用权衡，目录快速翻新（新闻、社交流）时重要。

### 评估
- **评分预测**：RMSE（重罚大错）、MAE。
- **Top-k 推荐**：Precision@k、Recall@k、NDCG（有序）、MAP。
- 评估必须在留出项上，不在整个矩阵上。

### Spatial voting（政治学中的孪生兄弟）
- 数据：议员 × 议案投票（yea/nay）。
- 模型：每个议员有 ideal point；每个议案有 yea 位置和 nay 位置；议员投给更近的位置。
- **Poole-Rosenthal**：用概率框架形式化，最大似然拟合归结为低秩近似。NOMINATE、W-NOMINATE 是经典实现。
- **识别问题**：旋转、反射等价 → 通过锚定已知自由派/保守派议员固定坐标朝向。

### Recsys ↔ Spatial 对应关系
代数几乎相同：
- 用户 ↔ 议员；物品 ↔ 议案；评分 ↔ 投票；p_i ↔ ideal point；q_j ↔ (yea, nay) 位置。
- 推荐系统优化预测；空间模型优化测量（实质性的轴解释）。

### 空间模型的扩展
- **Dynamic ideal points (Martin-Quinn)**：法官立场随时间演化（高斯随机游走），应用于美国最高法院。
- **State preferences (Bailey 等)**：UN 投票，通过"桥接议案"识别跨年份变化。
- **Ideological mapping at scale (Bonica)**：竞选捐款数据，每笔捐款视为捐款人对受捐人的 yea 投票。

---

## Ch 5. Nonlinear dimensionality reduction

### Manifold hypothesis
- 高维数据通常位于低维**流形**附近。
- **Intrinsic dimension（内在维度）**：实际生成数据的自由度数，远小于环境维度。手写数字 784 维像素，内在维可能 10–20。

### Geodesic vs Euclidean
- Swiss roll 上：同一卷弧上两点 geodesic 近，但 Euclidean 远（直线穿过空气）。
- 几乎所有流形方法都是用某种方式替换 Euclidean。

### 七种方法一览
| 方法 | 保留什么 | 出样本扩展 |
|---|---|---|
| Isomap | 图最短路径距离（geodesic）| 无 |
| LLE | 局部线性重构权重 | 无 |
| Laplacian Eigenmaps | 邻居关系 + 热核权重 | 无 |
| Kernel PCA | 核诱导的内积 | **有** |
| MVU | 局部距离精确 + 最大方差 | 无 |
| t-SNE | 邻居概率 | 无 |
| UMAP | 密度归一化模糊图 | **有（保存模型后）** |

→ 只有 KPCA 和 UMAP 原生支持 OOS，这在生产 pipeline 很重要。

### Isomap
1. 构造 k 近邻图，边权 = Euclidean 距离。
2. 全对最短路径（Dijkstra）= 估计 geodesic。
3. 用得到的距离矩阵做 classical MDS。
- **超参数**：只有 k。太小图断开；太大边"短路"穿过卷层。
- 成本 O(N³)，几千点以内可用。

### LLE（局部线性嵌入）
- 第一步：每个点用 k 近邻线性重构自己（求权重，权重和为 1）。
- 第二步：找低维位置，使**相同权重**仍能重构低维点。
- 保留**局部仿射结构**（旋转、平移、缩放不变）。
- k 太大时邻居跨越折叠，局部线性假设失败 → 嵌入褶皱。
- 比 LE 稍不稳健，现在 LE 更常用。

### Laplacian Eigenmaps
- 用热核权重的 k-NN 图。
- 目标：让强连接的点在嵌入中保持靠近。
- 解：图拉普拉斯 L 的最小非零特征值对应的特征向量。
- **关键应用**：UMAP 的初始化就是 LE。

### Kernel PCA
- 通过核函数把数据隐式映射到高维特征空间，在那里做 PCA。
- 常用核：linear（= 普通 PCA）、polynomial、**RBF（高斯）**——最常用，宽度参数 σ 控制局部性。
- **原生支持 OOS**：新点的核相似度投影到保存的特征向量上即可。
- **Pre-image 问题**：从嵌入坐标反推原始数据是非凸、不适定的 → KPCA 是特征提取工具，不是生成工具。

### Maximum Variance Unfolding (MVU)
- 把流形想成卷起的纸，每对邻居用刚性杆连接（距离锁定），把纸尽量拉开。
- 表述为半正定规划 (SDP)：最大化迹（= 总方差），约束邻居距离精确等于原始。
- **特性**：**特征值谱直接显示内在维度**——在 d 维流形上，前 d 个特征值大，之后骤降。
- **实践中很少用**：SDP 求解器代价 O(N^3.5)，最多 1–2 千点。UMAP 几秒钟做出来质量相当。

### t-SNE
- 把高维和低维的"邻居关系"都表示成概率分布，最小化两者的 KL 散度。
- **Perplexity（困惑度）**：每点的有效邻居数。默认 30。低（5–10）强调极局部；高（50–100）大邻域。
- **关键设计**：低维用 Student-t（Cauchy）核（重尾）而非高斯——这解决 **crowding problem**（高维等距点在低维挤到一起的问题）。
- **Early exaggeration**：前 100 次迭代把 P 放大 4–12 倍让簇先成形。

**t-SNE 三大警告**：
1. **簇间距离没有意义**。
2. **簇大小没有意义**（Student-t 核压缩远距离）。
3. **全局结构丢失**——只保留邻居身份。

### UMAP
- 类似 t-SNE 但理论基础不同（模糊拓扑 + 黎曼几何）。
- **关键差异**：高维用**密度归一化**——每个点的邻域用其最近邻距离归一，稀疏区和稠密区可比。
- 损失函数：模糊交叉熵，**有显式排斥项**（t-SNE 没有），这是它更好保留全局结构的原因。
- 初始化：**先做 Laplacian Eigenmap**——所以用 UMAP 的人都是隐式在用 LE。
- 优化：SGD + 负采样，O(NK)/epoch。
- 超参数：
  - `n_neighbors`（默认 15）：局部 vs 全局平衡。
  - `min_dist`（默认 0.1）：簇紧凑度，小 → 紧团，大 → 均匀铺开。
- **支持 OOS**：保存模型后 `umap_transform` 嵌入新数据。

### t-SNE vs UMAP
| | t-SNE | UMAP |
|---|---|---|
| 高维 kernel | 高斯（perplexity 校准）| 密度归一化指数 |
| 低维 kernel | Student-t | 参数化曲线 |
| 损失 | KL | 模糊交叉熵 + 显式排斥 |
| 初始化 | 随机 | LE 暖启动 |
| 全局结构 | 丢失 | 部分保留 |
| OOS | 无 | 有 |

UMAP 现在是默认选择；t-SNE 主要在计算生物学因历史原因仍流行。

### 决策树
1. 先试 PCA。前两三个 PC 解释大部分方差 → 线性方法够用。
2. 大规模 2D 可视化 → UMAP。
3. 生产 pipeline 需要 OOS → KPCA 或 UMAP（保存模型）。
4. 小数据集暴露局部几何 → LE 或 LLE。
5. 验证等距嵌入声明、估计内在维度 → Isomap 或 MVU。

### 永久警告
- 别把 t-SNE 图上的距离当度量距离读。
- 多种子、多超参运行。
- 簇身份比簇形状、簇大小、簇间几何更可靠。

---

## Ch 6. Hard clustering — partitioning & hierarchical

### 三个根本难点
1. **没有 ground truth**。两种聚类都可辩护时，选择取决于下一步要做什么。
2. **算法即假设**。每个算法对"簇是什么"有不同假设（质心、连通密集区、图社区、概率分布的众数）。同数据不同算法可能给出本质不同的划分。
3. **维度灾难**。维度变大时，最近邻和最远邻距离的比值趋近于 1，簇边界融化。**标准应对：先降维再聚类**。

### Kleinberg 不可能定理
聚类函数无法同时满足三性质：
1. **Scale-invariance**：所有距离乘常数后划分不变。
2. **Richness**：所有可能划分都能通过某种距离实现。
3. **Consistency**：簇内距离缩小、簇间距离拉大后划分不变。

→ k-means 违反 consistency；single-linkage HAC 违反 richness。
**意义**：算法选择本身是实质性选择，"最好的聚类算法"不存在。

### k-means
- **目标**：最小化簇内平方和（WCSS）。等价于最小化簇内成对距离的平均。
- **Lloyd 算法**：分配到最近质心 → 更新质心为均值 → 重复，直到不变。**局部极小**，有限步收敛。
- **几何**：质心两两间垂直平分线把空间分成 Voronoi 区。簇边界**只能是直线超平面**——这就是为什么 k-means 在非凸形状上失败。

### k-means 必知
- **初始化敏感**：不同起点 → 不同 WCSS 的局部极小。补救：
  - `nstart = 25+` 多起点保留最好。
  - **k-means++**：第一个质心随机；之后按到最近已选质心的平方距离概率挑选。期望 WCSS 在最优的 O(log K) 内。
- **永远先 scale！**Euclidean 距离被最大方差特征支配。收入（元）和年龄（岁）不标准化 → 只按收入聚类。

### k-means 失败模式
1. 非凸形状（半月、环）—— 用 Ch 7 的 DBSCAN/spectral。
2. 簇大小或方差差异巨大 —— 大簇拉到小簇里。
3. 异常值 —— 拉走质心。用 PAM。

### 降维 + 聚类的标准流水线
高维数据先 UMAP → 然后 k-means。UMAP 保留邻居结构，正是质心聚类需要的。单细胞、文本（contextual embeddings）等领域标准做法。

### k-medoids (PAM)
- 把质心换成**真实数据点**——medoid 是簇内到其他点总不相似度最小的观测。
- 算法：**BUILD**（贪心选种子）+ **SWAP**（尝试替换每个 medoid）。比 k-means 慢得多。
- **两大优势**：
  1. Medoid 是真实观测 → 可解释的"原型用户"。
  2. 支持**任意**不相似度——Manhattan、Gower（混合类型）、字符串编辑距离等。k-means 只能用平方 Euclidean。
- **CLARA**：大 N 时，PAM 在多个随机子样本上跑，取最好。

### Hierarchical Agglomerative Clustering (HAC)
- 每个点作为单独簇开始 → 合并最相似的两个簇 → 重复，直到一个。
- 输出 **dendrogram（树状图）**。
- **确定性**：无随机性、无初始化、无局部极小。
- 切树高度 → 任意数量的簇。大的纵向间隔暗示自然切点。

### 读 dendrogram 的两个警告
1. **只有高度轴有意义**。横向位置由绘图算法决定，相邻叶子不一定相似。
2. **切高 → 簇数**。低切多小簇，高切少大簇。

### Linkage 准则
| 名称 | 定义 | 倾向 |
|---|---|---|
| Single | 最小距离 | **chaining**；细长簇；噪声敏感 |
| Complete | 最大距离 | 紧凑、等径簇；可能拆分长形 |
| Average (UPGMA) | 均距离 | 折中 |
| **Ward** | 合并后 WCSS 增加最少 | 紧凑、等大；k-means 的层次版 |

**R 中用 `ward.D2`，别用 `ward.D`（实为 bug）。**

### 选 K 的工具
- **Elbow**：WCSS vs K，找肘部。
- **Silhouette**：每个点的"合得来"分数（自己簇内距离 vs 次近簇距离）。范围 [-1, 1]。+1 = 舒服在自己簇；0 = 边界；负 = 离别人更近。**选最大化平均轮廓系数的 K**。
- **Calinski-Harabasz**：簇间/簇内方差比。快（不需所有距离），偏向等大球形。
- **Gap statistic (Tibshirani)**：观测 log-WCSS 与随机参考数据的 log-WCSS 对比。最有原则。**规则：选最小的 K 使 Gap(K) ≥ Gap(K+1) − SE**。

### 没有自然 K 的情况
均匀分布在环上的点，所有方法都会给出某个 K，但这个数字毫无实质意义。**"没有自然 K"是分析者的判断**，metrics 辅助但不替代。

### 外部验证（有标签时）
- **ARI（调整 Rand 指数）**：成对一致性，经偶然校正。1 = 完美；0 = 随机。**最常报告**。
- **NMI**：归一化互信息，[0,1]。
- **Fowlkes-Mallows**：成对 precision × recall 的几何平均。
- **V-measure**：homogeneity（每簇单一类）+ completeness（每类在单簇）的调和均值。

### Cluster stability
- `fpc::clusterboot`：bootstrap 重采样，原簇在重采样中重现的 Jaccard 重叠。
- Hennig 阈值：>0.85 高稳定；0.6–0.75 中等；<0.6 可能是 artifact。

---

## Ch 7. Density-based & spectral clustering

### 为什么需要它们
Ch 6 假设簇是凸团（球形）。当真实结构是**半月、同心圆、长弧+圆团**时，k-means 切错、HAC 受单个桥接点影响合并。

### DBSCAN
**前提**：簇 = 通过稠密邻域连接的点集。

两个超参数：**ε（邻域半径）** 和 **minPts**。

三类点：
- **Core**：ε 邻域内至少有 minPts 个点。
- **Border**：自己不是 core，但在某 core 的 ε 邻域内。
- **Noise**：都不是，不分配到任何簇。

**Density-reachable**：通过 core 点链传递。**Density-connected**：存在第三点对两者都 density-reachable。**簇 = 最大密度连通集合**。

**算法**：遍历点，找到一个 core 就启动新簇，递归扩张到所有可达的 core 和 border，border 处停止递归。

### DBSCAN 调参
- **minPts**：经验法则 ≥ D+1，低维数据 4–5 标准。越大越保守（噪声多）。
- **ε**：**k-distance plot**——对每个点算到第 minPts 个最近邻的距离，排序作图。曲线大部分平坦，**肘部** = 一个好的 ε。

### DBSCAN 优势/劣势
- **优**：不需指定 K；任意形状；显式 noise 类别；低维 O(N log N) 用 kd-tree。
- **劣**：
  - ε 在中等维度难选（距离集中）。
  - **单一密度**：稠密簇旁边稀疏簇时，没有一个 ε 同时合适。
  - Border 点分配依赖访问顺序（部分任意）。

### HDBSCAN
**核心改进**：去掉 ε，自动处理变密度。

- **Core distance**：到第 minPts 个最近邻的距离。
- **Mutual reachability distance**：两点的 max(自己的 core dist, 对方的 core dist, 直接距离)。把稀疏区的点拉远，稠密区不变。
- 用 mreach 构造 MST → 按权重递减切边 = DBSCAN 层次。
- **Condensed tree**：只保留"两侧都≥minPts"的真分裂。
- **Cluster stability**：簇在层次中持续的"面积"。**Flat extraction**：选稳定性大于子簇之和的簇。

只有 **minPts** 一个超参数！

**何时帮 / 不帮**：变密度数据强项；纯均匀噪声背景里的渐变带（非密度模态）解决不了。和 DBSCAN 是互补诊断而非替代。

### Spectral clustering
**思路**：聚类 = 图切割问题，用图拉普拉斯的特征结构求解。

**算法**（Ng-Jordan-Weiss）：
1. 构造相似性图（k-NN 或高斯全连接）。
2. 算度矩阵 D。
3. 归一化拉普拉斯 L_sym = I − D^(-1/2) W D^(-1/2)。
4. 取 L_sym 最小 K 个特征值对应的特征向量。
5. 堆成 N×K 矩阵，行单位归一化。
6. 对行做 k-means。

**为什么有效**：图断成 K 个连通块时，L 的零特征值有 K 重，对应特征向量是各块的指示向量。**近乎**断开时（簇分得开），最小非零特征值很小，对应特征向量近似指示簇成员。

**超参**：K + 图参数（k 或 σ）。
**优**：任意形状、谱间隔诊断（K 的启发式选择）。
**劣**：N×N 拉普拉斯特征分解贵（稀疏求解器可帮）；对图选择敏感；最后一步 k-means 的所有问题都继承。

### 三方法对比
| | DBSCAN | HDBSCAN | Spectral |
|---|---|---|---|
| 超参 | ε, minPts | 只 minPts | K + 图参数 |
| 任意形状 | ✓ | ✓ | ✓ |
| 变密度 | ✗ | **✓** | 部分 |
| 显式 noise | ✓ | ✓ | ✗ |
| 大 N（>10k）| ✓（kd-tree）| ✓ | 慢 |
| 何时用 | 单密度、低维 | 变密度、探索性 | 自然图结构 |

---

## Ch 8. Soft clustering & finite mixtures

### Hard vs soft
Hard 给每点一个簇标签；soft 给每点**簇成员的概率分布**（**responsibility** r_ik）。Hard = MAP 规则 = 取 max responsibility 的簇。

### 三种方法的共同骨架
**Finite mixture model**：数据来自少数生成分布，权重未知。推断恢复组件参数 + 每观测的后验组件归属。算法形状统一：EM——E 步算 responsibility，M 步用 responsibility 作权重更新参数。

### Conditional independence 关键假设
**给定潜类别，观测特征条件独立**。这是 LCA（local independence）、LDA、对角协方差 GMM 的默认。

**身高-鞋码例子**：合并人群，身高鞋码高度相关；分别看男/女，组内相关接近零。相关由潜组诱导，组内无结构。

**当假设成立**：组件干净可解释。
**当假设违反**：算法把单个真实簇拆成多个小簇来吸收组内相关 → 你看到的 K 被人为放大。
**应对**：(a) 放宽假设（GMM 全协方差、LCA 局部依赖项、混合因子分析）；(b) 接受 K 反映"实质组 + 未建模依赖"。

### Gaussian Mixture Model (GMM)
- **生成故事**：先抽组件标签 z_i（multinomial），再从该组件高斯抽 x_i。
- **Responsibility**：贝叶斯规则下 x_i 来自组件 k 的后验概率。
- **EM 算法**：
  - **E**：当前参数下算所有 responsibility。
  - **M**：用 responsibility 作软计数更新 π、μ、Σ。
- 单调非降的 log-likelihood，收敛到局部极大；多起点必备。
- **k-means 是 GMM 的极限**：Σ_k → σ² I 且 σ→0，responsibility 硬化为 0/1。

### 协方差形状
- **Spherical** (σ²I)：圆球。
- **Diagonal**：组内特征不相关（条件独立）。
- **Full**：每个组件有自己的相关结构。

### GMM vs k-means
| | k-means | GMM |
|---|---|---|
| 分配 | 硬 | 软 |
| 簇形状 | 等径球 | 椭圆，参数化协方差 |
| 簇大小 | 隐式 | 显式 π_k |
| 不确定性 | 无 | 完整后验 |
| 模型选择 | elbow、silhouette | BIC |

### `mclust` 的协方差谱
14 种参数化（球形/对角/全 × 等/变 × 体积/形状/方向）。`mclust` 对所有 K 和所有协方差族跑 EM，按 BIC 选最佳。**`mclust` 的 BIC 约定：越高越好**（其他包反过来）。

### Latent Class Analysis (LCA)
GMM 的类别变量版本。
- 观测项目是类别（二元或多分类）。
- **Local independence**：给定潜类别，项目条件独立。
- 参数：类别比例 π_k + 项目-响应概率 ρ_jkr（类别 k 下项目 j 取值 r 的概率）。
- EM 形式与 GMM 平行：E 步算后验类别概率，M 步加权更新。
- 模型选择：**BIC**（poLCA 中越低越好）。多起点必备（似然多局部最大）。

### Local independence 失败诊断
- **Bivariate residual**：对每对项目比较观测与拟合的联合频数表。大残差 = 该对项目类别后仍有依赖。
- 失败时 BIC 会偏好更大 K（多类别吸收类内相关）。
- 解决：BayesLCA 支持局部依赖项；或换 IRT（连续潜变量吸收依赖）。

### LCA with covariates
让类别成员概率依赖观测协变量（multinomial logistic）。可问：人口学特征预测类别归属吗？

### LDA preview（soft-clustering 视角）
- 文档 = K 个主题上的软聚类（θ_d 是混合权重）。
- 主题 = 词汇上的分布（φ_k）。
- 同一模型内两个软聚类结构：文档软聚类到主题，词软聚类到主题。
- Bag-of-words = token 级的条件独立。
- 完整处理见 Ch 10。

### 三方法总结
| | GMM | LCA | LDA |
|---|---|---|---|
| 数据 | 连续 | 类别 | 文本/计数 |
| 软分配 | r_ik | r_ik | θ_d |
| 组件分布 | MVN | 类别乘积 | 词汇 Dirichlet |
| 推断 | EM | EM | VEM 或 Gibbs |
| R 包 | mclust | poLCA | topicmodels |
| 选 K | BIC | BIC | perplexity、coherence |

### 相关扩展
- **Mixture of factor analyzers**：高维数据上，每组件协方差由低秩因子模型给出。
- **Latent profile analysis**：连续指标的 LCA（= 对角协方差 GMM 的不同命名）。
- **Structural topic models (STM)**：LDA + 主题流行度 / 内容的协变量。

---

## Ch 9. Text — bag-of-words to word embeddings

### 文本预处理流水线
1. **Tokenize**：拆字符流为单元。
   - **Whitespace / 规则**（Treebank、regex）：低社科默认。
   - **Subword**（BPE、WordPiece）：现代 LM 标配，处理 OOV 和形态丰富语言；代价是单元不再是语言学的词。
2. **Normalize**：
   - 小写、去标点。
   - **Stemming**（Porter）：rule-based 砍后缀，会过度合并（organize / organ）。
   - **Lemmatization**：用词典+形态分析返回词典形（better → good）。**首选** lemmatize；Schofield 2017 显示激进 stemming 损害主题可解释性。

### Bag-of-words (BoW) 假设
- 丢弃词序。"Dog bites man" = "Man bites dog"。
- **DTM（文档-词矩阵）**：行=文档，列=词，值=计数。真实语料 99%+ 稀疏。
- 实用主义辩护：词的存在模式跨多文档已能捕捉主题。

### TF-IDF
- **直觉**：raw count 过度权重常见词（"the" 出现在所有文档，无区分度）。
- TF-IDF：词频 × log(文档总数 / 含该词的文档数)。
- 出现在所有文档的词 IDF = 0（被压成零）。
- **关键警告**：**不要把 TF-IDF 喂给 LDA**——LDA 期望离散计数。**用 TF-IDF 筛词汇，然后传过滤后的 raw count 给 LDA**。

### n-grams
- "climate" + "change" 分开丢失短语含义。
- 把 "climate_change" 作为单 token 包含进 DTM。
- 代价：词汇暴增，需按频率严格过滤。

### Co-occurrence matrix
- V×V 对称矩阵，C_ij = 词 i, j 在窗口内共现次数。
- 信息丰富的"分布行为"表征——上下文相似的词有相似的行。
- 用作 **LSA**（共现 SVD）、**GloVe**（共现的对数分解）的输入。
- **分布假设**："you shall know a word by the company it keeps"——基础理论。

### 维度问题驱动需求
DTM 50,000 维稀疏；共现矩阵 50,000 × 50,000。维度灾难 + 存储成本。Word embedding 就是解决这个的低维稠密表示。

### Word embedding 目标
- 词汇映射到 ℝ^d（d 几百维）。
- 相似上下文的词在几何上靠近。
- 低维、稠密，支持 cosine 相似度、聚类、线性运算。
- **"Static"**：每词一个向量，不管上下文。

### word2vec：两个架构
- **CBOW（continuous bag-of-words）**：用上下文预测中心词。上下文向量取平均；softmax 在词汇上预测中心词。
- **Skip-gram**：用中心词预测每个上下文词（独立）。每次出现产生 2c 个训练样例（c = 窗口半径）。
- **Skip-gram 对稀有词更好**（CBOW 把稀有词淹没在上下文平均里）。
- 两个嵌入矩阵：input V（词作为中心/上下文）和 output U（被预测时）。习惯返回 V 或 V+U。

### Softmax 瓶颈 & negative sampling
- 完整 softmax 需要在整个词汇（百万级）上归一化 → 每次梯度步骤 O(V·d)，不可行。
- **Negative sampling (SGNS)**：把 softmax 换成 k 个二分类——对每个真 (中心, 上下文) 对，从噪声分布采 k 个"负样本"，让模型把真对打高分、负对打低分。
- 每次更新只接触 k+1 个向量。

### Noise distribution
- 不是均匀采样。常用：unigram 频率的 3/4 次幂。这个 3/4 是经验值，原始 word2vec 实现确定的。

### Subsampling frequent words
- 训练前以概率丢弃每个 token，丢弃概率随词频上升。
- 防止极常见词主导训练信号。

### Levy-Goldberg 结果
- SGNS 隐式分解 **shifted PMI** 矩阵（PMI = 共现的对数比的 log）。
- 在最优时，VU^T ≈ PMI − log k。
- **意义**：word2vec 是低秩矩阵分解的伪装——把它接回 Ch 2 的矩阵分解机器。

### GloVe
- 直接对共现矩阵的对数做加权最小二乘拟合。
- 加权函数 f(x) 下调稀有共现的影响，封顶常见共现（"the" 不能主导）。
- 比 SGNS 在大语料上**训练快**（每对词只处理一次，而非每次出现）。
- 嵌入质量在标准基准上相似。

### word2vec vs GloVe
| | SGNS | GloVe |
|---|---|---|
| 输入 | 流式语料 | 预计算共现 |
| 隐式矩阵 | shifted PMI | log X |
| 训练成本 | 线性于语料 | 线性于非零共现 |
| 稀有词 | skip-gram 好 | 稳健 |

### Analogies
- 经典：king − man + woman ≈ queen；Paris − France + Italy ≈ Rome。
- 两类：句法（walked, walking, ran, running）和语义（country, capital）。
- 出自分布结构：在相似上下文出现的词占据相似位置。

### Static embedding 的致命缺陷：**Polysemy**
- "bank"（河岸 vs 银行账户）只有一个向量——它是各义项加权平均（按语料频率）。
- 需要词义区分的任务（情感、消歧、细粒度分类）→ static 不够 → contextual embeddings（Ch 11）。

### 实际工作流
- 用 `word2vec`、`text2vec` 包训练，或用预训练向量（Google News、GloVe Wikipedia、fastText 多语言）。
- **可复现性要钉死**：语料、tokenizer、窗口、维度、负样本数、随机种子。

### 社科 text-as-data 两条警告
1. **每个建模选择是实质性选择**——tokenizer、stopword、最小频次、窗口、维度都改变结果。**全部报告**。
2. **验证不可少**——topic models、clusterings、embeddings 给出**假设**而非发现。和人工编码的子样本核对，是应用文献最常被跳过的步骤。

---

## Ch 10. Probabilistic topic models

### 大画面
- Word embedding 回答词级问题；topic model 回答**文档级**问题。
- 文档很少只关于一个东西——一篇碳税新闻 40% 气候 + 35% 政治 + 25% 财政。
- Topic = **词汇上的概率分布**，不是标签。"政治"主题给 senate、bill、vote 高概率。

### LDA 生成故事
1. 对每个主题 k：从 Dirichlet 抽一个词汇分布 φ_k。
2. 对每个文档 d：
   - 从 Dirichlet 抽一个主题分布 θ_d。
   - 对每个词位置：从 θ_d 抽主题；从对应 φ_k 抽词。

| 符号 | 含义 |
|---|---|
| K | 主题数（用户指定）|
| V | 词汇量 |
| θ_d | 文档-主题分布；`tidytext` 中叫 "gamma" |
| φ_k | 主题-词分布；`tidytext` 中叫 "beta" |
| α | θ 的 Dirichlet 浓度参数 |
| η | φ 的 Dirichlet 浓度参数 |

### Dirichlet 浓度参数的作用
- 小 α → 每文档集中在少数主题（稀疏）。
- 小 η → 每主题集中在少数词（稀疏）。
- 大值 → 平滑到均匀。
- **默认偏好小值**——支持"文档关于几个主题、主题由几个特征词刻画"的可解释情形。

### 推断（不需要会推导，知道存在两种）
- **Variational EM (VEM)**：参数化可处理的分布逼近真后验，最小化 KL。快、确定性。
- **Collapsed Gibbs sampling**：把 θ、φ 解析积分掉，只采样词级主题分配 z_dn。直觉很清楚——每次更新一个词的主题分配，概率正比于"该文档已经用这个主题多少 × 该主题已经用这个词多少"。两个力量平衡。

### LDA 的预处理决定一切
- **自定义 stopword 列表**：通用英文 stopword 不够。国会演讲会出现 "gentleman、yield、speaker"；学术摘要会出现 "paper、propose、novel"。
- **n-grams**：合并 "climate_change"、"United_States"。
- **Lemmatize > stem**。
- **TF-IDF 筛词汇**，然后传 raw count。**不要传 TF-IDF 进 LDA**。

### 选 K——本章最重要的话题
**Perplexity（困惑度）**：留出文档上的反向几何平均似然。数学上无可指责，**但是**：
- **Chang et al. 2009 "Reading Tea Leaves"** 用两个众包任务：
  - **Word intrusion**：给评分者看 5 个 topic top words + 1 个外来词，找入侵者。
  - **Topic intrusion**：给评分者看一篇文档 + 3 个高概率主题 + 1 个低概率主题，找入侵者。
- 结论：**perplexity 更低的模型在人类入侵任务上表现更差**。优化 perplexity 系统性损害可解释性。
- 启示：perplexity 测预测拟合，这不是"用于人类解读的模型"应该优化的标准。

**Coherence（连贯性）**：从主题 top words 和语料共现统计算单一分数。UMass、NPMI 是两种实现。**与入侵任务相关性远好于 perplexity**。

**Exclusivity（排他性）**：主题 top words 是否独有？通用词在多主题都出现说明该主题不有用。`stm` 包返回两者。

**Cardinality caveat**：coherence 在更大 K 模型上机械偏高（每主题 top words 少 → 共现比例自然高）。不要跨大幅不同的 K 直接比较 coherence 数值。

**Workable workflow**：
1. 钉死预处理 pipeline。
2. 扫 K（10, 20, 30, 40, 50）。
3. 画 coherence vs exclusivity，找 **Pareto frontier**。
4. 读候选模型每个主题的 top words，挑可解释性最好的。
5. 稳定性检查：±20% K 时实质结论是否仍然成立？不成立就报告为 K-依赖的。

LLM 现在可以低成本充当入侵任务的代理评分者。

### Structural Topic Model (STM)
**问题**：plain LDA 把文档当作可交换（顺序、元数据无关），但社科问题正是关于元数据（共和党 vs 民主党、年份、实验条件）。

**有缺陷的两步法**：先 LDA，再把 θ_d 回归到协变量。问题：θ_d 估计有不确定性，作为回归因变量时**系数被衰减**（errors-in-variables attenuation）。

**STM 解决方案**：把协变量直接嵌入生成模型。
- **Topic prevalence**：θ_d 的均值通过 logistic-normal 链接到协变量 X_d。控制"文档关于该主题的多少"。
- **Topic content**：φ_k 可以随协变量 U_d 变化。控制"该主题被如何谈论"——不同作者用不同词汇谈同主题。
- 用 VEM 拟合；`estimateEffect()` 给出协变量对主题流行度的影响及标准误。
- 用 `init.type = "Spectral"` 获得确定性、可复现的初始化。

### Biterm Topic Model (BTM)
**问题**：LDA 在短文本（tweets、headlines、单句开放回答）上失败——单文档 token 太少，无法支持 Dirichlet 先验工作。结果是噪声、重叠的主题。

**BTM 解决方案**：放弃文档级生成故事，把每个无序词对（"biterm"）作为基本单元，topic 是 biterm 上的分布。共现在**全语料**测度而非单文档，统计上稳定。文档主题在拟合后通过 biterm 主题分配聚合推断。

**经验法则**：平均文档长度 < ~50 token → 用 BTM 或 contextual embeddings；LDA 在短文本上**沉默失败**——给出貌似合理但不可靠的主题。

### Topic models vs Word embeddings
| | LDA/STM | word2vec/GloVe |
|---|---|---|
| 分析单元 | 文档 | 词 |
| 表示 | 计数（BoW）| 稠密向量 |
| 上下文窗口 | 整个文档 | 局部窗口 |
| Polysemy | 捕捉（词可载多主题）| 不捕捉 |
| 输出 | 文档主题混合 + 主题词分布 | 语义相似、类比 |

### 2026 社科工作流
1. **第一遍——STM 做结构推断**：含协变量。用 coherence + exclusivity + K 扫描选模型。读 top words 贴标签。`estimateEffect()` 估协变量效应。
2. **第二遍——BERTopic 做语义探索**（Ch 11）。
3. **比较**：BERTopic 合并 STM 分开的文档（或反过来）的地方往往是最有趣的实质性发现。
4. **验证**：读最低 coherence 主题——预处理问题在这里浮现；±20% K 稳定性；LLM-as-judge 入侵任务；预注册 K 选择标准。

---

## Ch 11. Contextual embeddings & modern topic models

### 大画面
Static embedding 给 "bank" 一个向量；contextual embedding 让 "bank" 在 "river bank" 和 "bank account" 里得到不同向量。这一改变带来了现代 NLP 的几乎所有突破。

### Attention：直觉
- BoW 每词贡献相等。
- 滑窗模型固定窗口。
- Attention：每个位置的输出是**整个序列**的加权平均，权重由序列本身计算。

### Query, Key, Value
- 每个 token 投影成三个向量：
  - **Query (q)**：位置 i "在找什么"。
  - **Key (k)**：位置 j "能提供什么"。
  - **Value (v)**：位置 j 实际"贡献什么"。
- 权重 a_ij 是 q_i 和 k_j 的相似度，softmax 归一化。
- 输出 = 各位置 value 的加权和。

### Self-attention & multi-head
- **Self-attention**：Q、K、V 都来自同一序列——每 token 的表示依赖整个序列，不只局部窗口。
- **Multi-head**：并行多个 attention "头"，各自学不同关系（句法、共指、语义相似）。输出拼接后投影回原维。

### Causal mask
- **Bidirectional**（BERT）：每位置 attend 整个序列。
- **Causal**（GPT）：mask 未来位置，每位置只看自己和之前。用于从左到右生成。

### Transformer block
1. Multi-head self-attention。
2. Residual connection + layer norm。
3. Position-wise feed-forward。
4. Residual + layer norm。

堆叠 12（BERT base）/ 24（BERT large）/ 更多。**Position embedding** 必加，否则 attention 对顺序无感。

### BERT 预训练任务
- **Masked Language Modelling (MLM)**：随机 mask 15% token，从两侧上下文预测——**双向表示**。
- **Next-Sentence Prediction (NSP)**：判断第二句是否真接第一句——后来证明贡献小，多数后继模型放弃。

### Sentence-BERT
- 直接平均 BERT token 向量做句子表示效果差。
- Sentence-BERT 用 siamese 架构在句子相似度数据上 fine-tune，得到固定大小的句嵌入——cosine 相似可比。
- 现在多供应商通过 API 提供（OpenAI、Voyage、Cohere、Google）。

### BERTopic 流程
1. **Embed**：sentence transformer 把每文档编码（如 MiniLM 384 维）。
2. **Reduce**：UMAP 压到 5–15 维。
3. **Cluster**：HDBSCAN 在低维空间聚类——自动给 noise 类别。
4. **Describe**：**c-TF-IDF**（class-based TF-IDF）——把每个簇的所有文档拼成一个"类文档"，得到该簇相对其他簇的特征词。

### BERTopic 优势 / 局限
- **优**：短文本表现好（BoW 不够时）；对术语密集文本和多义词更稳健（同词在不同上下文有不同向量）。
- **限**：c-TF-IDF 标签仍是单词，可能误导；HDBSCAN 的局限继承；**不直接支持协变量建模**——社科问题仍需 STM。

→ **双 pass workflow**：STM 做结构推断 + BERTopic 做语义探索，分歧 = 诊断信号。

### Foundation models
**定义**：单一大型网络在广语料预训练，可适配多下游任务。**Scale**是定义性特征。当前一代从几十亿到几千亿参数。

### Scaling laws
Kaplan、Hoffmann (Chinchilla)：测试损失是 model size、训练数据、计算的幂律函数。**对任何计算预算有最优模型大小/数据量分配**。早期大模型相对参数量训练不足；Chinchilla 修正后开源模型遵循。

### In-context learning
- 模型足够大后，能从 prompt 中的几个示例**学会新任务，无需梯度更新**。
- 机制尚不完全理解；与规模可靠相关是稳健发现。
- 社科意义：分类、抽取、摘要任务从 fine-tune 变成 prompt engineering。**验证不可商量**——看起来正确不等于正确。

### Few-shot vs zero-shot
- **Few-shot**：prompt 含若干工作示例。
- **Zero-shot**：只有任务描述。
- Few-shot 通常在格式重要的任务上更好；zero-shot 适合探索。

### Chain-of-thought (CoT)
- 在示例里包含**中间推理步骤**，不只是最终答案。
- 在需要多步推理的任务（算术、逻辑）上显著提升。
- **"Let's think step by step"** 是零样本 CoT 触发语。
- **Self-consistency**：采样多条推理路径，多数投票答案。
- **Tree-of-thoughts**：在分支推理路径上搜索。
- **重要警告**：CoT trace 与模型实际计算之间的关系**不保证忠实**——用 CoT 提升精度，但**不要把 trace 当作真实解释**。

### LLM 推理短板
擅长流利语言和模式补全，弱于多步算术、形式逻辑、长链中间状态。同模型能通过律考却算不对两位数乘法。三种应对：
1. CoT 脚手架（常能缩小差距）。
2. 把精确计算外包给工具（计算器、Python、定理证明器）——模型只编排。
3. 在精选推理语料上训练（最新最大模型 + RL）。

### Agents 和 tool use
LLM 能调用外部工具（搜索、Python、SQL、其他模型）→ agent。模型决定调用什么、解析结果、决定下一步。把标注任务（10,000 文档复杂 schema）从重劳动变成 prompt 工程。**仍然需要分层抽样的人工审查**。

### 可复现性硬要求
- **模型版本号**钉死（同名 "gpt-4o" 不同月份是不同 artifact）。
- **Temperature**：分类用 0；生成用更高。
- 提示词、随机种子记录。

---

## Ch 12. Autoencoders, VAEs, Adversarial AE

### 该章在书中的位置
- Ch 2/4 的线性方法（PCA、MDS、MF）：线性投影+内积重构。
- Ch 5 的流形方法：非线性嵌入但**没有重构映射**，不能嵌入新点。
- Autoencoder 填这个洞：神经网络学到**非线性嵌入+学到的可应用函数**。

### Plain Autoencoder
- **Encoder** f_φ：输入 → 低维潜表示 z（瓶颈）。
- **Decoder** g_θ：z → 重构。
- **训练目标**：重构损失（连续输入用 MSE；二元用 binary cross-entropy）。
- 瓶颈维度 L 是关键超参——太小重构差；太大学到平凡复制（潜表示无信息）。

### 关键事实：Linear AE = PCA
- 编码器+解码器都是单线性层、损失是 MSE 时，AE 优化的子空间**正是** PCA 的 top-L 主成分子空间。
- 轴可能不同（网络可选任何基），但**子空间和重构误差相同**。
- **意义**：
  1. 线性关系下深度学习不会比 PCA 神奇更多；PCA 更简单、快、好理解。
  2. **AE 比 PCA 的所有提升都来自非线性激活**。隐藏层和激活函数让网络能发现弯曲流形。

### Latent space 是有结构的
对 held-out 数据可视化瓶颈激活，通常显示可解释结构（数字按身份、客户按行为、句子按主题聚集）。潜在维度本身没有命名因子（任意旋转），但**几何**有信息。

### 正则化变体
- **Denoising AE**：输入加噪，解码器重构**干净**输入。强制网络把噪声输入投影到数据流形。学习稀缺时的标准预训练技巧。
- **Sparse AE**：在瓶颈激活上加 L1 惩罚。不同输入激活不同的少量单元 → 可解释的稀疏编码。计算神经科学中皮层表示模型。
- **Contractive AE**：惩罚 encoder Jacobian 的 Frobenius 范数 → 编码器对输入小变动局部不敏感。与 denoising 紧密相关，但解析地起作用。
- 三者不互斥；常组合 denoising + sparsity。

### Variational Autoencoder (VAE)
**关键改变**：编码器不再输出潜空间的单一点，而是**概率分布的参数**（高斯的 μ 和 σ）。从该分布采样得到 z，传给解码器。整个网络通过最大化数据 log-likelihood 的**下界**训练。

### VAE 是生成模型
训练后从先验抽 z，解码器产生**像训练数据的合成观测**。Plain AE 没有生成解释——潜空间不约束到任何特定分布，从中采样得到无意义结果。

### 生成模型设定
- z_n 从标准高斯先验抽。
- 给定 z，x 从 decoder 参数化的条件分布抽（连续用高斯，二元用 Bernoulli）。
- **边际似然不可解**——decoder 是非线性的。直接 MLE 不可行。

### Amortized variational inference
- 引入**编码器**近似真实后验。编码器输出每输入对应的近似分布参数。
- "Amortized"：**一套参数 φ** 通过网络定义每个输入的近似后验，而非每观测一个变分分布——经典 VI 相比的核心效率提升。

### ELBO（Evidence Lower Bound）
- log-likelihood 的下界，依赖 θ 和 φ。
- **Reconstruction term**：编码器给的潜采样下，解码器对观测打多高的概率。
- **Regularization term (KL)**：编码器分布与先验的 KL 散度。
- 两项**反向拉**：reconstruction 要 q 编码 x 信息；KL 要 q ≈ 先验。训练好的 VAE 是妥协。

### Reparameterization trick
**问题**：要对 φ 求 reconstruction term 的梯度，但采样在 φ 上（不可微）。

**技巧**：把 z 重写为 φ 的确定性函数 + 来自固定分布的随机数 ε。
- 随机性在 ε 里，**不依赖 φ**。
- 梯度通过确定性映射 μ_φ 和 σ_φ 流动。
- 这是让 VAE 可用 SGD 训练的技术创新。

### VAE 中的三个分布
易混点。Plain AE 没有分布；VAE 有：
1. **编码器** 输出潜变量分布（近似后验）。
2. **解码器** 输出输入空间分布（条件似然）。
3. **先验** 在潜空间上锚定几何。

### VAE 比 plain AE 多给三样
1. **概率嵌入**：每输入一个高斯分布。方差有信息——不确定的点高方差。
2. **生成模型**：从先验抽 z 解码 → 合成观测。两真实数据潜向量间的线性插值产生平滑序列（图像 VAE 经典演示）。
3. **良条件潜空间**：KL 正则让编码器输出靠近标准正态 → 防止信息藏在难采样的小角落。任何区域解码都给合理输入。

### VAE vs PPCA
PPCA = VAE 的线性极限（编码器解码器都线性，噪声各向同性）。ELBO 解析可处理，MLE 有闭式谱解。换成神经网络 → 表达力 ↑，但失去闭式解。

→ **VAE 是因子分析家族的非线性深度学习表亲**——识别只到旋转、common vs unique 方差权衡、先验作用，几乎所有 FA 的性质都有 VAE 对应。

### Adversarial Autoencoder (AAE)
- VAE 的 KL 正则换成**鉴别器网络**——区分先验样本和编码器样本。编码器训练成"骗过鉴别器"。
- 与 GAN 的 minimax 博弈相似。
- **优势**：先验自由——VAE 要 KL 可处理（高斯/高斯混合），AAE 允许**任何可采样的先验**（非高斯、多模、结构化离散）。
- 适合需要非高斯潜的实质问题。

### 半监督扩展
- 在连续潜旁加一个**类别潜变量**（class label）。
- 小标注集 + 大无标注集 → 模型学到分离 class 和 style 的表示。
- 标签稀缺、未标注丰富时的标准范式——这是当代社科常见情形。

---

## 贯穿全书的家族关系（核心 takeaway）

| 方法 | 与之关联 |
|---|---|
| **PCA** | 协方差矩阵的特征分解 |
| **Linear AE** | 神经网络伪装的 PCA |
| **PPCA** | PCA + 高斯潜变量模型 |
| **VAE** | PPCA 解码器换成非线性网络 |
| **Classical MDS** | PCA 的对偶（分解 Gram 矩阵）|
| **Factor analysis** | PPCA 的更灵活版本（分公共/唯一方差）|
| **IRT** | 类别观测的因子模型 |
| **LCA** | 离散潜变量的因子模型 |
| **LDA** | 文档上的混合模型，潜变量是主题分布 |
| **BERTopic** | LDA 架构 + contextual embeddings 替代 BoW |
| **k-means** | 各向同性噪声 + 硬化 responsibility 的 GMM |
| **GMM** | k-means 的软泛化（任意协方差）|
| **Spectral clustering** | 图拉普拉斯特征向量 → k-means |
| **Laplacian Eigenmaps** | 同样的特征向量本身作为嵌入 |
| **Matrix factorization recsys** | 稀疏矩阵的低秩近似 |
| **Spatial voting** | 议员×议案矩阵上的 MF（因子叫 ideal points）|

**一句话**：几乎所有方法 = 数据 = 低维潜结构 + 围绕它的变异。它们在"什么算低维"、"什么算结构"、"什么算变异"上不同。

---

## 考试日决策速查表

| 任务 | 默认工具 |
|---|---|
| 线性降维 | PCA |
| 可视化（非线性、大 N）| UMAP |
| 出样本嵌入 | KPCA 或 UMAP（保存模型）|
| 验证等距嵌入 | Isomap |
| 估内在维度 | MVU 特征值间隔 |
| 凸簇、可标准化 | k-means（`nstart` + scale）|
| 任意形状、单密度 | DBSCAN |
| 任意形状、变密度 | HDBSCAN |
| 图数据、K 已知 | Spectral |
| 连续 + 不确定性 | GMM（mclust + BIC）|
| 类别响应 | LCA（poLCA）|
| 长文档主题 | STM（带协变量）|
| 短文本主题 | BTM 或 BERTopic |
| 语义相似 | sentence-BERT cosine |
| 生成低维表示 | VAE |

---

## 高频考点（容易出考题的概念区分）

1. **Scale vs Index**：因果方向。Scale 项目应相关、用 α；Index 项目不必相关、α 不适用。
2. **Reliability vs Validity**：reliable 是 valid 的必要不充分条件。
3. **PCA vs FA**：描述性 vs 概率模型；总方差 vs 公共+唯一方差。
4. **EFA vs CFA**：发现 vs 验证；同样本同时跑 = chance capitalization。
5. **Kleinberg**：scale-invariance + richness + consistency 不可同时。
6. **k-means 失败模式**：非凸、不等大小、异常值——分别对应 DBSCAN/spectral、GMM、PAM。
7. **DBSCAN vs HDBSCAN**：单一密度 vs 变密度；ε 必选 vs 只 minPts。
8. **Hard vs Soft**：MAP = 硬化的 responsibility。
9. **Conditional independence 假设违反 → K 膨胀**。
10. **GMM ↔ k-means**：协方差极限。
11. **Perplexity 误导**：lower perplexity ≠ better topics；Chang 入侵任务。
12. **STM 的两步法 bias**：θ 估计不确定性导致回归系数被衰减。
13. **t-SNE 三大警告**：簇间距离、簇大小、全局结构都不可靠。
14. **UMAP 比 t-SNE 好**：显式排斥项 + LE 初始化 + 密度归一化 + OOS。
15. **Static embedding 致命缺陷**：polysemy（多义词共享单一向量）。
16. **CoT 警告**：trace 不一定是模型实际推理的忠实描述。
17. **Linear AE = PCA**：AE 的所有 PCA 之外的好处都来自非线性。
18. **VAE 三个分布**：encoder q、decoder p、prior。
19. **VAE vs PPCA**：PPCA 是 VAE 的线性极限。
20. **AAE vs VAE**：AAE 用鉴别器替代 KL，允许任何先验。

考试加油！
