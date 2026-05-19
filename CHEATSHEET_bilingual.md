# UML4SS Cheatsheet（中英混合版 · Ch 3–12）

考试：30 道选择题，40 分钟（≈80 秒/题）。
重点：**concept distinction**、**failure modes**、**decision rules**。

---

## 🔥 全书最高频考点（先扫一遍）

1. **Reflective scale vs formative index**：因果方向决定能否用
   **α**、**factor analysis**。
2. **Reliability ≠ validity**；reliability 是 validity 的
   **necessary but not sufficient** 条件。
3. **PCA vs factor analysis**：descriptive vs probabilistic；
   total vs common+unique variance。
4. **Kleinberg impossibility**：**scale-invariance**、
   **richness**、**consistency** 不可同时满足。
5. **k-means 失败模式** → 用 **DBSCAN / spectral**（非凸）、
   **GMM**（不等方差）、**PAM**（outlier）。
6. **DBSCAN vs HDBSCAN**：**single density** vs **variable density**。
7. **Conditional independence violation → K 膨胀**。
8. **t-SNE 三大警告**：簇间距离、簇大小、global structure 都不可靠。
9. **UMAP > t-SNE**：显式 **repulsion** + **LE init** + **OOS**。
10. **Static embedding 致命缺陷**：**polysemy**。
11. **Perplexity 误导**：lower perplexity ≠ better topics。
12. **STM 解决两步法 attenuation bias**。
13. **Linear AE = PCA**；非线性才有 PCA 之外的价值。
14. **VAE 三个分布**：encoder、decoder、prior。
15. **TF-IDF 不能喂 LDA**（LDA 需要 discrete count）。

---

# Ch 3. Measurement, Similarity, Proximity

## Stevens Measurement Levels
| Level | 允许操作 | 例 |
|---|---|---|
| **Nominal** | count、mode | 性别 |
| **Ordinal** | rank、median | Likert |
| **Interval** | mean、SD | 摄氏温度 |
| **Ratio** | 所有 arithmetic | 身高 |

⚠️ **Nominal** 上算 mean = **category error**。

## Scale vs Index ⭐
| | **Scale (reflective)** | **Index (formative)** |
|---|---|---|
| 因果 | latent → items | items → construct |
| Items 相关 | 必须 | 不必 |
| 删一项 | 不改 construct | **改变定义** |
| α / FA | ✓ | **✗** |
| 例 | 焦虑 scale | **SES** |

## CTT
- **observed = true score + error**
- **Reliability** = **true score variance** / **observed variance**
- 浴室秤永远多 10 磅 = **reliable** 但 **invalid**

## Cronbach's α
阈值：**0.7 / 0.8 / 0.9**。
⚠️ **三个批评**：
1. items 越多 α 越高
2. 假设 **tau-equivalent**（loading 不等时低估）
3. **高 α ≠ unidimensional**

## McDonald's ω
- **ω_t**：所有 common factors 解释的比例（≥ α）
- **ω_h**：**bifactor** 中 **general factor** 的比例
- ω_h / ω_t 高 → 多维但总分仍可辩护

## Reliability 类型
| Type | 测什么 |
|---|---|
| **Test-retest** | 时间稳定 |
| **Parallel forms** | 等价版本 |
| **Internal consistency** | items 一致（α、ω）|
| **Inter-rater** | raters 一致（**κ**、**ICC**）|

## Validity（论证）
五类证据：**Content**、**Internal structure**、
**Relations to other variables**、**Response processes**、
**Consequences**。

⚠️ **Face validity 是最弱**的证据，易被
**socially desirable responding** 污染。

## MTMM
| 关系 | 应该 |
|---|---|
| 同 trait 不同 method | **高**（convergent）|
| 不同 trait 不同 method | **低**（discriminant）|

## PCA vs Factor Analysis ⭐
| | **PCA** | **FA** |
|---|---|---|
| 性质 | descriptive | probabilistic model |
| 分解 | **total variance** | **common + unique** |
| 用途 | 降维 | 测试 latent causes |

## 决定 factor 数
**Scree plot** / **Kaiser**（λ>1，过度保留）/
**Parallel analysis**（最稳妥）。

## Rotation
- **Varimax**（orthogonal）：factors 不相关
- **Oblimin / Promax**（**oblique**）：factors 相关
- 目标：**simple structure**

## Bifactor vs Hierarchical
- **Hierarchical**：second-order general factor（**mediated**）
- **Bifactor**：general + specific 并列 load on items

## EFA vs CFA ⭐
| | **EFA** | **CFA** |
|---|---|---|
| 结构 | 发现 | **强加** |
| Cross-loading | 允许 | fix to 0 |
| 输出 | loadings | + **CFI/TLI/RMSEA/SRMR** |

⚠️ EFA → CFA 须在**独立样本**上，否则 **chance capitalization**。

## IRT
- **2PL**：**difficulty (b)** + **discrimination (a)**
- **3PL**：+ **guessing (c)**（multiple choice）
- **Graded Response Model**：ordered polytomous

## Item Information
- Item 在 **b 附近**信息最大
- **Test information** = 各 item 之和
- **CAT** = adaptive testing

## DIF ⭐
- 同 θ 不同 group 对 item 反应不同
- ⚠️ **DIF ≠ group mean difference**——是 mapping 不同
- 含 DIF → 跨组比较 mean **misleading**

## CTT vs IRT
| | **CTT** | **IRT** |
|---|---|---|
| 难度 | sample-dependent | **sample-invariant** |
| SE | 常数 | 随 θ 变 |
| 样本 | 几百 | 500+ |

## Latent Variable 统一观点
| Indicators \ Latent | Continuous | Discrete |
|---|---|---|
| Continuous | **Factor Analysis** | **Latent Profile** |
| Categorical | **IRT** | **Latent Class** |

## Distance Metrics
| Metric | 用途 |
|---|---|
| **Euclidean** | default（先 standardize）|
| **Manhattan** | outlier-robust |
| **Mahalanobis** | covariance 校正 |
| **Cosine** | 忽略 magnitude；text 标准 |
| **Jaccard** | binary 集合 |
| **Gower** | 混合类型 |

---

# Ch 4. Recommender Systems & Spatial Models

## 推荐问题设置
- 用户 × 物品矩阵，99% 缺失
- **Explicit feedback**（评分）vs **Implicit feedback**（点击）
- Implicit **没有负样本**
- **MNAR**（missing not at random）：人爱评强观点

## Baseline 必先建
prediction = global mean + user bias + item bias
→ MF 提升应**相对 baseline** 报告。

## Matrix Factorization (MF) ⭐
- 每用户 / 物品 一个低维 vector，预测 = inner product + baseline
- 全观测时 = **truncated SVD**（Eckart-Young 最优低秩）
- 有缺失时**只在 observed 上**最小化误差 + regularization
- 对 P、Q **联合非凸**、分别凸 → **ALS**

## ALS vs SGD
- **ALS**：交替最小二乘，**可并行**，生产主力
- **SGD**：随机挑 observed 更新，超大规模适用

## Probabilistic MF
高斯似然 + 高斯先验，MAP = ridge MF。
推广到非高斯（**Bernoulli**、**Poisson**）。

## 变体
- **NMF**：非负 P、Q → 部件式、稀疏、可解释
- **Implicit feedback (HKV)**：confidence-weighted
- **BPR (Bayesian Personalized Ranking)**：优化**排序**，适合 top-k
- **Factorization Machines**：加 side info 和 interactions
- **Neural CF**：内积换 MLP，丧失 SVD 性质

## 评估
- 评分预测：**RMSE**、**MAE**
- Top-k：**Precision@k**、**Recall@k**、**NDCG**、**MAP**
- 必在 **held-out** 上评估

## Spatial Voting（孪生兄弟）
- 议员 × 议案，**ideal point** + bill 的 **yea/nay** 位置
- **Poole-Rosenthal**、**W-NOMINATE**
- **识别问题**：rotation/reflection 等价 → 锚定已知议员

## Recsys ↔ Spatial 对应
用户 ↔ 议员，物品 ↔ 议案，评分 ↔ 投票。
推荐优化 **prediction**；空间模型优化 **measurement**。

---

# Ch 5. Nonlinear Dimensionality Reduction

## Manifold Hypothesis
- 高维数据在**低维 manifold** 附近
- **Intrinsic dimension** ≪ ambient dimension
- 数字图像 784 维，内在 ~10–20 维

## Geodesic vs Euclidean
- Swiss roll 上：同弧两点 **geodesic 近** 但 **Euclidean 远**
- 几乎所有 manifold 方法都在替换 Euclidean

## 七种方法一览
| 方法 | 保留 | **OOS** |
|---|---|---|
| **Isomap** | graph 最短路径 | ✗ |
| **LLE** | local linear weights | ✗ |
| **Laplacian Eigenmaps** | 邻居 + 热核权重 | ✗ |
| **Kernel PCA** | kernel inner product | **✓** |
| **MVU** | 局部距离精确 | ✗ |
| **t-SNE** | neighborhood prob | ✗ |
| **UMAP** | density-normalized fuzzy graph | **✓** |

⭐ 只有 **KPCA** 和 **UMAP** 原生 OOS。

## Isomap
3 步：k-NN graph → all-pairs shortest path（Dijkstra）→ MDS。
- 只有 **k** 一个超参
- k 太小 → graph 断；k 太大 → 短路穿过卷层

## LLE
保留 **local linear reconstruction weights**。
旋转、平移、缩放不变。

## Laplacian Eigenmaps
- 强连接的点在 embedding 中**保持靠近**
- 解 = graph Laplacian 最小非零 eigenvalues
- ⭐ **UMAP 的 init 就是 LE**

## Kernel PCA
- 用 kernel 把数据隐式映射到高维特征空间做 PCA
- 常用：linear、polynomial、**RBF (Gaussian)**
- ✓ **原生 OOS**
- ⚠️ **pre-image problem** 病态 → 不是 generative

## MVU
- **SDP**（半正定规划）
- ⭐ **eigenvalue gap** 直接显示 **intrinsic dimension**
- 实际很少用：SDP 太贵，~2000 点上限

## t-SNE ⭐
- 高维 + 低维都建邻居概率，最小化 **KL divergence**
- **Perplexity**：邻居数；default **30**
- 低维用 **Student-t**（重尾）→ 解 **crowding problem**

⚠️ **t-SNE 三大警告**：
1. **簇间距离没有意义**
2. **簇大小没有意义**
3. **Global structure 丢失**

## UMAP ⭐
比 t-SNE 好的关键差异：
- **Density-normalized** 高维 metric
- 损失函数有**显式 repulsion**
- **LE init**（暖启动）
- ✓ **支持 OOS**
- 超参：**n_neighbors**、**min_dist**

## t-SNE vs UMAP
| | **t-SNE** | **UMAP** |
|---|---|---|
| Init | random | **LE** |
| 显式 repulsion | ✗ | **✓** |
| Global structure | 丢失 | 部分保留 |
| OOS | ✗ | **✓** |

## 决策树
1. 先试 **PCA**
2. 大规模可视化 → **UMAP**
3. 生产 OOS → **KPCA** 或 **UMAP**
4. 估 intrinsic dim → **MVU**

---

# Ch 6. Hard Clustering — Partitioning & Hierarchical

## 三个难点
1. 没有 **ground truth**
2. **算法 = 假设**（不同算法对"簇"假设不同）
3. **Curse of dimensionality**：高维中 max/min 距离趋同
   → 标准应对：**先降维再聚类**

## Kleinberg Impossibility ⭐
聚类不可同时满足：
1. **Scale-invariance**
2. **Richness**
3. **Consistency**

→ **k-means** 违反 consistency；
**single-linkage HAC** 违反 richness。

## k-means
- 目标：**WCSS** 最小化
- **Lloyd's algorithm**：assign → update → repeat
- **几何**：**Voronoi cells**，**直线边界** → 非凸形状失败

## k-means 必知
- ⚠️ **初始化敏感**：用 `nstart = 25+` 或 **k-means++**
- ⚠️ **永远先 scale！** 否则被最大方差特征支配

## k-means 失败模式 ⭐
| 失败原因 | 应对 |
|---|---|
| **非凸形状** | DBSCAN / spectral |
| 簇大小/方差差异巨大 | GMM (full covariance) |
| Outliers | PAM (k-medoids) |

## k-medoids (PAM)
- 质心 = **真实数据点**（medoid）
- 支持**任意 dissimilarity**（Gower、edit distance）
- 大 N 用 **CLARA**

## HAC (Hierarchical Agglomerative Clustering)
- 每点单簇 → 合并最相似 → 重复
- 输出 **dendrogram**
- **Deterministic**（无随机、无 init）
- ⚠️ Dendrogram **只有高度有意义**，横向位置无关

## Linkage
| | 倾向 |
|---|---|
| **Single** | **chaining**；细长簇；噪声敏感 |
| **Complete** | 紧凑等径 |
| **Average** | 折中 |
| **Ward** | 紧凑等大；k-means 的层次版 |

⚠️ R 用 `ward.D2`，不用 `ward.D`。

## 选 K
- **Elbow**：WCSS vs K
- **Silhouette**：cohesion vs separation，[-1, 1]
- **Calinski-Harabasz**：between/within；偏向等大球形
- **Gap statistic**：与随机参考比，**最有原则**

⚠️ 环上均匀分布 → **没有自然 K**。

## 外部验证
- **ARI**（adjusted Rand index）—— **最常报告**
- **NMI**
- **V-measure** = homogeneity + completeness

## Cluster Stability
**Bootstrap** + Jaccard 重叠。
>0.85 高稳定；<0.6 可能是 artifact。

---

# Ch 7. Density-based & Spectral Clustering

## 为什么需要
Ch 6 假设簇是**凸团**。半月、同心圆 → k-means 切错。

## DBSCAN ⭐
两个超参：**ε**（半径）、**minPts**。

三类点：
- **Core**：ε 内 ≥ minPts
- **Border**：在某 core 邻域里
- **Noise**：都不是

**Density-reachable** 通过 core 链传递。
**簇** = maximal density-connected set。

## DBSCAN 调参
- **minPts** ≥ D+1，低维用 4–5
- **ε**：**k-distance plot** 找肘部

## DBSCAN 优劣
✓ 不需 K；任意形状；显式 **noise**；快
✗ ε 在中等维度难选；**单一密度**；border 分配依赖访问顺序

## HDBSCAN ⭐
**核心改进**：去掉 ε，处理**变密度**。

- **Mutual reachability distance**：拉远稀疏区
- 在 mreach 图上构 **MST** → 层次
- **Cluster stability**（持续面积）
- 只有 **minPts** 一个超参

## Spectral Clustering
**思路**：聚类 = graph cut。

6 步：
1. 构 similarity graph（**k-NN** 或 **Gaussian**）
2. 算 degree matrix
3. **Normalized graph Laplacian**
4. 取最小 K 个 eigenvalues 的 eigenvectors
5. 行归一化
6. **k-means on rows**

## 三方法对比 ⭐
| | **DBSCAN** | **HDBSCAN** | **Spectral** |
|---|---|---|---|
| 超参 | ε, minPts | 只 minPts | K + graph |
| 任意形状 | ✓ | ✓ | ✓ |
| **变密度** | ✗ | **✓** | 部分 |
| 显式 noise | ✓ | ✓ | ✗ |

---

# Ch 8. Soft Clustering & Finite Mixtures

## Hard vs Soft
- Hard：每点一个簇标签
- Soft：**responsibility**（簇成员概率分布）
- Hard = **MAP** of responsibility

## 共同骨架：EM
- **E step**：算 responsibility
- **M step**：用 responsibility 做软计数更新参数

## Conditional Independence ⭐
**给定 latent class，observed features 条件独立**。
- LCA、LDA、**diagonal-covariance GMM** 的默认假设
- 身高-鞋码例子：合并相关高，分组相关近零
- ⚠️ **假设违反 → 算法把单簇拆成多簇 → K 膨胀**

## Gaussian Mixture Model (GMM)
- 每组件 = **Multivariate Gaussian**
- **Responsibility** = posterior P(component | data)
- 多起点必备
- **k-means = GMM 极限**（各向同性协方差 → 0）

## 协方差形状
| | 含义 |
|---|---|
| **Spherical** | σ²I |
| **Diagonal** | 组内不相关 |
| **Full** | 任意相关结构 |

## GMM vs k-means ⭐
| | **k-means** | **GMM** |
|---|---|---|
| 分配 | hard | soft |
| 簇形 | 等径球 | 椭圆 |
| 不确定性 | 无 | 完整后验 |
| 选 K | elbow | **BIC** |

## Latent Class Analysis (LCA)
- GMM 的**类别变量**版本
- **Local independence** = 条件独立
- 选 K 用 **BIC**

## Local Independence 失败诊断
- **Bivariate residual**：观测 vs 拟合频数
- 失败时 BIC 偏好**更大 K**

## 三方法总结
| | **GMM** | **LCA** | **LDA** |
|---|---|---|---|
| 数据 | continuous | categorical | text |
| 软分配 | r_ik | r_ik | θ_d |
| 推断 | EM | EM | **VEM / Gibbs** |
| 选 K | BIC | BIC | coherence |

---

# Ch 9. Text — Bag-of-Words to Word Embeddings

## 预处理流水线
1. **Tokenize**：whitespace / subword（**BPE**、**WordPiece**）
2. **Normalize**：lowercase、去标点
3. **Stemming** vs **Lemmatization**：
   - Stemming 砍后缀，**过度合并**
   - **Lemmatization > stemming**（首选）

## Bag-of-Words (BoW)
- 丢弃词序："Dog bites man" = "Man bites dog"
- **DTM** 99%+ 稀疏

## TF-IDF ⭐
- raw count 偏重常见词；TF-IDF 下调
- 全文档都出现的词 → IDF = 0
- ⚠️ **TF-IDF 不能喂 LDA**（LDA 需要 discrete count）
- TF-IDF 用来**筛词汇**，然后传 raw count

## n-grams
合并 "climate_change"、"United_States" 为单 token。

## Co-occurrence Matrix
V×V，窗口内共现次数。
**Distributional hypothesis**：上下文相似 → 含义相似。

## Word2vec 两个架构
| | **CBOW** | **Skip-gram** |
|---|---|---|
| 任务 | 用 context 预测 center | 用 center 预测 context |
| 稀有词 | 弱 | **好** |

## Negative Sampling (SGNS)
完整 softmax 不可行（百万词汇）→
把 softmax 换成 **k 个二分类**（k+1 个向量/更新）。

## Levy-Goldberg 结果 ⭐
**SGNS 隐式分解 shifted PMI 矩阵**。
→ word2vec = 矩阵分解的伪装。

## GloVe
对 **log co-occurrence** 直接做加权最小二乘。
比 SGNS 在大语料**训练快**。

## word2vec vs GloVe
| | **SGNS** | **GloVe** |
|---|---|---|
| 输入 | 流式语料 | 预计算共现 |
| 稀有词 | skip-gram 好 | 稳健 |

## Analogies
king − man + woman ≈ queen。

## Static Embedding 致命缺陷 ⭐
**Polysemy**：bank（河岸 vs 银行）只有一个向量。
→ 需 **contextual embeddings**（Ch 11）。

## 社科警告
- 每个建模选择是**实质性选择**
- 输出是**假设**而非发现 → 必须 validate

---

# Ch 10. Probabilistic Topic Models

## 大画面
- Word embedding 答词级；**topic model 答文档级**
- **Topic** = 词汇上的**概率分布**，不是标签

## LDA 生成故事
1. 每 topic 抽 word distribution **φ_k**
2. 每 document：
   - 抽 topic distribution **θ_d**
   - 每词位置：抽 topic → 抽 word

| 符号 | 含义 |
|---|---|
| **K** | topic 数 |
| **θ_d** | 文档-主题（tidytext "gamma"）|
| **φ_k** | 主题-词（tidytext "beta"）|
| **α, η** | Dirichlet concentration |

## 推断（不需会推）
- **Variational EM (VEM)**：快、确定性
- **Collapsed Gibbs sampling**：积分掉 θ、φ

## 预处理决定一切
- **自定义 stopword**（domain-specific）
- **n-grams** 合并短语
- **Lemmatize > stem**
- **TF-IDF 筛词汇** → 传 raw count

## 选 K ⭐ —— 本章最重要

**Perplexity 的陷阱**：
- 数学上无可指责
- ⚠️ **Chang et al. "Reading Tea Leaves"**：
  perplexity **更低** 的模型在 **word intrusion** /
  **topic intrusion** 任务上**更差**
- 优化 perplexity **系统性损害** interpretability

**两个 intrusion task**：
- **Word intrusion**：5 top words + 1 外来词
- **Topic intrusion**：文档 + 3 高 prob topics + 1 低

**Coherence**（**UMass**、**NPMI**）+ **Exclusivity**
是更好的选择标准。

⚠️ **Cardinality caveat**：coherence 在大 K 上**机械偏高**。

## Structural Topic Model (STM) ⭐
**两步法 bug**：先 LDA 再回归 θ_d
→ θ_d **estimation uncertainty** → 系数 **attenuation**

**STM 解决**：协变量**直接嵌入** generative model。
- **Topic prevalence**：主题多少 ~ 协变量
- **Topic content**：怎样谈 ~ 协变量

## Biterm Topic Model (BTM)
**短文本**（<50 token/doc）LDA 沉默失败 → BTM。
基本单元 = **biterm**（无序词对）。

## Topic Models vs Word Embeddings
| | **LDA / STM** | **word2vec / GloVe** |
|---|---|---|
| 单元 | document | word |
| 上下文 | 整个文档 | 局部窗口 |
| Polysemy | 捕捉 | **不捕捉** |

---

# Ch 11. Contextual Embeddings & Modern Topic Models

## 大画面
Static："bank" 一个向量。
**Contextual**："bank" 在不同句子得不同向量。

## Attention 直觉
每位置输出 = **整个序列**的加权平均，
权重由序列本身计算。

## Query / Key / Value
- **Query (Q)**：位置 i "在找什么"
- **Key (K)**：位置 j "能提供什么"
- **Value (V)**：j 实际"贡献什么"
- 权重 = Q 与 K 的相似度

## Self-attention & Multi-head
- **Self-attention**：Q、K、V 都来自同一序列
- **Multi-head**：并行多个头学不同关系
  （syntax、coreference、semantic）

## Causal Mask
| | 用于 |
|---|---|
| **Bidirectional** | **BERT**（看整序列）|
| **Causal** | **GPT**（只看之前，用于生成）|

## Transformer Block
1. Multi-head self-attention
2. **Residual** + **layer norm**
3. Position-wise FFN
4. Residual + layer norm

⚠️ 必加 **position embedding**，否则 attention 对顺序无感。

## BERT 预训练
- **Masked Language Modelling (MLM)**：mask 15% token 预测
- **Next-Sentence Prediction (NSP)**：贡献小，后继多放弃

## Sentence-BERT
直接平均 BERT token 向量效果差。
Sentence-BERT 用 **siamese** 架构 fine-tune，
得到固定大小句嵌入，**cosine 可比**。

## BERTopic 流程 ⭐
1. **Embed**：sentence transformer
2. **Reduce**：UMAP 到 5–15 维
3. **Cluster**：HDBSCAN，自动 noise 类
4. **Describe**：**c-TF-IDF**（class-based TF-IDF）

## BERTopic 优劣
✓ 短文本好；多义词稳健
✗ c-TF-IDF 标签仍是单词
✗ **不直接支持协变量** → 社科仍需 **STM**

→ **双 pass workflow**：STM 结构推断 + BERTopic 语义探索。

## Foundation Models
- **Scale** 是定义性特征
- **Scaling laws**（Kaplan、Chinchilla）：power law

## In-context Learning
- 大模型从 prompt 几个示例**学新任务，无需梯度更新**
- ⚠️ **验证不可商量**：看起来正确 ≠ 正确

## Few-shot vs Zero-shot
- **Few-shot**：含示例
- **Zero-shot**：只有任务描述

## Chain-of-Thought (CoT)
- 在示例里含**中间推理步骤**
- 多步推理任务上显著提升
- ⚠️ **CoT trace 不一定忠实**——
  提升精度但**别当真实解释**

## Agents
LLM + tool calls = agent。
标注任务从重劳动变成 prompt 工程，**仍需人工抽查**。

## 可复现性
钉死**模型版本**、**temperature**（分类用 0）、种子。

---

# Ch 12. Autoencoders, VAEs, AAE

## 该章位置
- Ch 2/4 线性：投影 + 内积重构
- Ch 5 流形：非线性嵌入但**无重构映射**
- **Autoencoder 填洞**：非线性嵌入 + 学到的函数

## Plain Autoencoder
- **Encoder**：输入 → 低维 **latent**
- **Decoder**：latent → 重构
- 目标：**reconstruction loss**
- **Bottleneck dim L**：太小重构差；太大平凡复制

## 关键事实：Linear AE = PCA ⭐
- 线性 encoder + decoder + MSE
  → AE 优化的**子空间 = top-L PC 子空间**
- 轴可能不同（任意基），**子空间相同**

**意义**：AE 比 PCA 的所有提升**都来自非线性激活**。

## 正则化变体
| 变体 | 做什么 |
|---|---|
| **Denoising AE** | 加噪输入，重构干净 |
| **Sparse AE** | L1 惩罚 bottleneck |
| **Contractive AE** | 惩罚 encoder Jacobian |

## Variational Autoencoder (VAE) ⭐
**关键改变**：encoder 输出**概率分布参数**，不是单点。
从该分布采样 z 传给 decoder。
最大化 log-likelihood 的**下界（ELBO）**。

## VAE 是生成模型
从 **prior** 抽 z → decode → 合成观测。
Plain AE **没有**生成解释。

## ELBO 两项拉锯
- **Reconstruction term**：要 q 编码 x 信息
- **KL term**：要 q ≈ prior
- 训练好的 VAE 是妥协

## Reparameterization Trick
**问题**：采样在 φ 上 → 不可微。
**技巧**：z = μ_φ + σ_φ ⊙ ε，ε 从固定分布。
→ 让 VAE 可用 **SGD** 训练的技术创新。

## VAE 三个分布 ⭐（易混点）
1. **Encoder** 输出 latent 分布（**approximate posterior**）
2. **Decoder** 输出输入空间分布（**conditional likelihood**）
3. **Prior** 在 latent 上锚定几何

## VAE 比 plain AE 多三样
1. **概率嵌入**（方差 = 不确定性）
2. **生成模型**（从 prior 抽 → 合成）
3. **良条件 latent space**（KL 让接近标准正态）

## VAE vs PPCA ⭐
**PPCA = VAE 的线性极限**。
换非线性 decoder → 表达力↑，失去闭式解。
→ VAE 是 factor analysis 家族的**非线性深度学习表亲**。

## Adversarial Autoencoder (AAE)
- KL 正则换成 **discriminator network**
- ✓ **任何可采样 prior**（非高斯、多模、离散）

## 半监督扩展
连续 latent + **categorical latent**（class label）。
小标注 + 大无标注 → 分离 class vs style。

---

# 贯穿全书的家族关系

| 方法 | 与之关联 |
|---|---|
| **PCA** | covariance 特征分解 |
| **Linear AE** | 神经网络伪装的 PCA |
| **PPCA** | PCA + Gaussian latent |
| **VAE** | PPCA + 非线性 decoder |
| **Classical MDS** | PCA 的 dual |
| **Factor Analysis** | 更灵活的 PPCA |
| **IRT** | categorical 观测的 factor model |
| **LCA** | 离散 latent 的 factor model |
| **LDA** | document 上的 mixture |
| **BERTopic** | LDA 架构 + contextual embed |
| **k-means** | isotropic 硬化的 GMM |
| **GMM** | k-means 的软泛化 |
| **Spectral clustering** | LE eigenvectors + k-means |
| **MF recsys** | 稀疏矩阵低秩近似 |
| **Spatial voting** | 投票矩阵上的 MF |

**一句话**：所有方法 = **低维 latent 结构 + 围绕它的变异**。

---

# 🎯 考试日决策速查

| 任务 | 默认工具 |
|---|---|
| 线性降维 | **PCA** |
| 非线性可视化 | **UMAP** |
| 出样本嵌入 | **KPCA** 或 **UMAP** |
| 凸簇 | **k-means**（先 scale）|
| 任意形状、单密度 | **DBSCAN** |
| 任意形状、变密度 | **HDBSCAN** |
| 图数据 | **Spectral** |
| 连续 + 不确定性 | **GMM** + BIC |
| Categorical responses | **LCA** |
| 长文档主题 | **STM**（含协变量）|
| 短文本主题 | **BTM** 或 **BERTopic** |
| 语义相似 | **sentence-BERT cosine** |
| 生成低维表示 | **VAE** |

---

# 🎯 易混淆 ABCD 选项辨析（针对选择题陷阱）

### Ch 3 测量

**1. α vs ω**
- α 假设 **tau-equivalence** → 载荷不等时**低估**
- α 不是 unidimensionality 测试
- ω 从 factor model 算 → 更稳健

**2. Reflective vs Formative**
- Reflective：latent → items；删一项**不改** construct
- Formative：items → construct；删一项**改变定义**；**不能用 α**

**3. Reliability vs Validity**
- Reliable but invalid ✓ 可能
- Valid but unreliable ✗ **不可能**

**4. EFA vs CFA**
- EFA：cross-loading 允许
- CFA：分析者**指定**结构，给 fit indices
- 同样本依次做 = **chance capitalization**

**5. PCA vs FA**
- PCA：descriptive、total variance、components 是数据精确组合
- FA：probabilistic、common+unique、factors 是 latent

**6. Parallel Analysis vs Kaiser**
- Kaiser（λ>1）→ **over-retains**
- Parallel analysis → 最稳妥

**7. Bifactor vs Hierarchical**
- Hierarchical：general factor **mediated** through first-order
- Bifactor：general + specific **parallel** load on items

**8. DIF**
- ⚠️ 不是 group mean difference
- 是同 θ 不同 group 反应不同
- 含 DIF → 跨组比较 mean **misleading**

### Ch 4 推荐

**9. Explicit vs Implicit Feedback**
- Implicit **没有负样本**
- 未点击 ≠ 不喜欢

**10. ALS vs SGD**
- ALS：可并行
- SGD：超大规模

**11. BPR vs MF**
- MF：评分预测（RMSE）
- BPR：**排序优化**（top-k）

### Ch 5 流形

**12. Isomap k 选择**
- k 太小 → graph 断
- k 太大 → **短路**穿过卷层

**13. KPCA pre-image**
- KPCA **不是 generative**
- pre-image 问题病态

**14. t-SNE 三大警告** ⚠️
- 簇间距离不可靠
- 簇大小不可靠
- Global structure 丢失

**15. UMAP vs t-SNE**
- UMAP 有**显式 repulsion**
- UMAP **LE init**（不是 random）
- UMAP 支持 **OOS**

### Ch 6–7 聚类

**16. Kleinberg**
- 三性质：scale-inv / richness / consistency
- **不可同时**

**17. k-means 何时用 scale?**
- ⚠️ **永远** scale，否则被最大方差特征主导

**18. k-means 失败模式**
| 失败 | 用什么 |
|---|---|
| 非凸 | DBSCAN / spectral |
| 不等大小 | GMM full cov |
| Outlier | PAM |

**19. Linkage 区别**
- Single → **chaining**
- Ward → 紧凑等大（k-means 层次版）

**20. DBSCAN vs HDBSCAN**
- DBSCAN：**单一密度**
- HDBSCAN：**变密度** + 无 ε

**21. Spectral 用什么 Laplacian?**
- **Normalized** graph Laplacian
- 最小 K 个 eigenvalues 的 eigenvectors

### Ch 8 软聚类

**22. Conditional Independence 违反**
- ⚠️ 算法**把单簇拆成多簇 → K 膨胀**
- 不是模型崩溃，是**沉默失败**

**23. GMM 协方差形状**
- Spherical → 等径球（= k-means）
- Diagonal → 组内不相关
- Full → 任意形状

**24. GMM 选 K**
- 用 **BIC**，不是 elbow / silhouette

### Ch 9 文本

**25. TF-IDF 错误用法**
- ⚠️ **不能喂 LDA**（LDA 要 discrete count）
- TF-IDF 用来**筛词汇**

**26. CBOW vs Skip-gram**
- 稀有词 → **Skip-gram** 好

**27. Static Embedding 缺陷**
- ⚠️ **Polysemy**：一词一向量，对多义词失败

### Ch 10 主题

**28. Perplexity 陷阱**
- ⚠️ Lower perplexity **≠** better topics
- 用 **coherence + exclusivity**

**29. STM 解决什么**
- ⚠️ 两步法的 **attenuation bias**
- 协变量直接进 generative model

**30. 短文本主题**
- LDA **沉默失败**
- 用 **BTM** 或 **BERTopic**

### Ch 11 现代文本

**31. BERT vs GPT 注意力**
- BERT：**bidirectional**
- GPT：**causal**

**32. BERTopic 不能做什么**
- ⚠️ **不直接支持协变量** → 仍需 STM

**33. CoT 警告**
- ⚠️ Trace **不保证忠实**
- 提升精度，但**别当真实解释**

### Ch 12 自编码器

**34. Linear AE = ?**
- ⚠️ = **PCA**（同子空间）
- 非线性才有额外价值

**35. VAE 三个分布**
- Encoder（approx posterior）
- Decoder（conditional likelihood）
- Prior

**36. VAE vs PPCA**
- **PPCA = VAE 的线性极限**
- 非线性 decoder → 失去闭式解

**37. Reparameterization Trick 解决什么**
- 让采样**可微**
- 让 VAE 可用 **SGD** 训练

**38. AAE vs VAE**
- AAE 用 **discriminator** 替代 KL
- → 允许**任何 prior**（非高斯、多模、离散）

考试加油！💪
