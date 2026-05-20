# UML4SS Cheatsheet（按主题组织 · 选择题专用）

考试：30 道 MC，40 分钟（≈80 秒/题）。
看到题先用 **Decision Guide** 定位方法族，再翻对应 block。

---

## 🔥 全书最高频陷阱（先扫一遍 30 秒）

1. **Reliability** 是 **validity** 的 *necessary but not sufficient*。
2. **PCA ≠ Factor Analysis**：descriptive vs probabilistic model。
3. **EFA + CFA 同样本** = **chance capitalization**。
4. **Kleinberg impossibility**：**scale-invariance / richness /
   consistency** 不可同时。
5. **k-means 必须先 scale**；只能产生**直线** Voronoi 边界。
6. **DBSCAN** = single density；**HDBSCAN** = variable density。
7. **BIC 方向陷阱**：**mclust BIC 越高越好**，**poLCA BIC 越低越好**。
8. **Conditional independence 违反 → K 膨胀**（不是模型崩溃）。
9. **t-SNE** 三大警告：簇间距离 / 簇大小 / global structure 都不可靠。
10. **UMAP > t-SNE**：显式 repulsion + LE init + **OOS** 支持。
11. **TF-IDF 不能喂 LDA**（LDA 要 discrete count）。
12. **Static embedding** 致命缺陷：**polysemy**。
13. **Perplexity 越低 ≠ topic 越好**（Reading Tea Leaves）。
14. **Linear AE ≈ PCA**；非线性激活才有额外价值。
15. **Plain AE latent space 不规整** → 不能 sample 生成；
    **VAE / AAE** 才能。

---

## 1️⃣ Decision Guide（题目类型 → 方法族）

| 题目里看到 / 问什么 | 优先想到 |
|---|---|
| 把很多变量压成少数**连续维度** | **PCA / MDS** |
| 测量 **latent construct** | **Factor Analysis / IRT** |
| 想要**硬分组**（每点一类） | **k-means / k-medoids / HAC** |
| **非凸 / 非圆形** cluster | **DBSCAN / HDBSCAN / Spectral** |
| 每点**属于每类的概率** | **GMM / LCA** |
| 文本**主题** | **LDA / STM / BERTopic** |
| **curved manifold** 上降维 | **Isomap / LLE / LE / UMAP** |
| **out-of-sample** 嵌入 | **Kernel PCA / UMAP**（其他都不支持）|
| **neural representation / 生成** | **AE / VAE / AAE** |
| user × item 评分矩阵 | **Matrix Factorization (ALS / SGD)** |
| 议员 × 议案投票 | **Spatial voting / Ideal point**（同上）|

⭐ 看到题先回答："这题属于上面哪一行？"

---

## 2️⃣ PCA / MDS / Factor Analysis

### 核心方法对比

| 方法 | 核心逻辑 | 关键词 |
|---|---|---|
| **PCA** | 找最大 **projected variance** 方向 ≡ 最小 **reconstruction error** | eigenvectors, loadings, scores |
| **Classical MDS** | 从 pairwise **distances** 还原低维坐标 | double-centering, **Gram matrix** |
| **Metric MDS** | 保留**距离大小** | **stress** |
| **Non-metric MDS** | 只保留**距离排序** | rank order, monotonic |
| **Factor Analysis** | **latent factor** 引起 item responses | common variance, **uniqueness** |

### PCA ⭐ 必记
- 两个**等价定义**：max projected variance ≡ min reconstruction error
- Components 是数据的**精确线性组合**（不是 latent 变量）
- 分**total variance**（不区分 common / unique）
- **Scree plot** 找拐点；**Kaiser**（λ>1）常 over-retain；
  **parallel analysis** 最稳妥

### PCA vs FA ⭐⭐ 选择题金矿
| | **PCA** | **Factor Analysis** |
|---|---|---|
| 性质 | descriptive | **probabilistic model** |
| 方差分解 | **total** | **common + unique** |
| 成分本质 | 数据的精确线性组合 | latent 随机变量 |
| 用途 | data reduction, composite | **测量** latent causes |

→ "PCA is not factor analysis" 是固定考点。

### Classical MDS ↔ PCA
**Classical MDS = PCA 的 dual**——
PCA 分解 covariance；Classical MDS 分解 centered **Gram matrix**。
输入是距离时用 MDS，输入是坐标时用 PCA，**结果等价**。

---

## 3️⃣ Measurement / Reliability / Validity / IRT

### Scale vs Index ⭐
| | **Scale (reflective)** | **Index (formative)** |
|---|---|---|
| 因果 | latent → items | items → construct |
| Items 相关 | 必须 | **不必** |
| 删一项 | 不改 construct | **改变定义** |
| 能用 α / FA? | ✓ | **✗ 不适用** |
| 例 | 焦虑 scale | **SES** |

**判别**：construct 能在 items 不变时变化吗？能 → reflective。

### Reliability vs Validity ⭐
- **Reliability**：true score variance / observed variance
- **Validity**：是否真的测到 construct
- **Reliability 是 validity 的 necessary but not sufficient**
- Reliable but invalid ✓（浴室秤永远多 10 磅）
- Valid but unreliable ✗（**不可能**）

### Cronbach's α
阈值：**0.7 / 0.8 / 0.9**。
⚠️ **三个批评**：
1. items 越多 α 越高
2. 假设 **tau-equivalent**；loading 不等 → **低估**
3. 高 α **≠ unidimensional**

### McDonald's ω
- **ω_t**：所有 common factor 解释的比例（≥ α）
- **ω_h**：**bifactor** 中 general factor 的比例
- 适合 **congeneric model**（loading 不等的更现实情形）

### Validity 五类证据
**Content / Internal structure / Relations to other vars /
Response processes / Consequences**。

⚠️ **Face validity 最弱**，易被 social desirability 污染。

### IRT
| 参数 | 含义 |
|---|---|
| **difficulty (b)** | 50% 认可的 θ 水平 |
| **discrimination (a)** | ICC 斜率 |
| **guessing (c)** | 3PL 加，multiple choice 用 |

- **Graded Response Model**：ordered polytomous
- **CAT**：按当前 θ 选题
- **DIF ≠ group mean difference** ⭐——是 item 映射方式不同

### EFA vs CFA ⭐
| | **EFA** | **CFA** |
|---|---|---|
| 结构 | 发现 | **强加** |
| Cross-loading | 允许 | fix to 0 |
| 输出 | loadings | + **CFI / TLI / RMSEA / SRMR** |

⚠️ 同样本依次做 = **chance capitalization**，必须独立样本。

### Bifactor vs Hierarchical
- **Hierarchical**：general factor **mediated through** first-order
- **Bifactor**：general + specific **parallel** load on items

### Latent Variable 统一观点
| Indicators \ Latent | Continuous | Discrete |
|---|---|---|
| Continuous | **Factor Analysis** | **Latent Profile** |
| Categorical | **IRT** | **Latent Class** |

---

## 4️⃣ Clustering 大表（核心 · 占最多空间）

### Hard Clustering 方法对比 ⭐
| 方法 | 输入 / 目标 | 优 | 缺 / 陷阱 |
|---|---|---|---|
| **k-means** | numeric features, hard | fast, simple | 需指定 K；**spherical** 簇；**对 scale / outlier / init 敏感** |
| **k-medoids (PAM)** | 任意 distance | medoid 是真实点；**outlier-robust**；支持 Gower 等 | 慢；大 N 用 **CLARA** |
| **HAC** | distance matrix | **dendrogram**，无需先定 K | greedy；linkage 敏感 |
| ↳ **Single linkage** | nearest neighbor | 可捕异形 | **chaining problem** |
| ↳ **Complete linkage** | farthest neighbor | 紧凑 | 易拆大簇 |
| ↳ **Average (UPGMA)** | mean dist | 折中 | — |
| ↳ **Ward** | min Δ WCSS | 紧凑等大；k-means 层次版 | Euclidean 假设 |
| **DBSCAN** | density region | 任意形状；**显式 noise** | **ε 敏感**；**单一密度** |
| **HDBSCAN** | density hierarchy | **变密度**；**无 ε** | 仍需调 minPts |
| **Spectral** | graph connectivity | 非凸；谱间隔诊断 K | 依赖图构造；O(N³) |

### k-means 必记
- 目标 = 最小化 **WCSS (Within-Cluster Sum of Squares)**
- **Lloyd's algorithm**：assign → update → repeat
- **Voronoi cells** → 直线边界 → 非凸形状必败
- ⚠️ **必须先 scale！** 否则被最大方差特征主导
- **k-means++** 智能初始化（按到最近已选质心的距离概率选种子）

### k-means 失败模式（选哪个替代）⭐
| 失败原因 | 替代 |
|---|---|
| **非凸形状** | DBSCAN / HDBSCAN / Spectral |
| 簇**大小 / 方差**差异巨大 | **GMM** (full covariance) |
| **Outliers** | **k-medoids (PAM)** |
| 高维 | 先 **UMAP** 再 k-means |

### DBSCAN 概念
| 类型 | 定义 |
|---|---|
| **Core point** | ε 邻域内 ≥ minPts |
| **Border point** | 在某 core 的邻域内，自己不是 core |
| **Noise point** | 都不是 |
| **Density-reachable** | 通过 core 链传递 |

调参：**minPts** ≈ D+1（低维 4–5）；**ε** 看 **k-distance plot** 肘部。

### Kleinberg Impossibility ⭐
**三性质不可同时满足**：
1. **Scale-invariance**
2. **Richness**
3. **Consistency**

→ k-means 违反 consistency；single-linkage HAC 违反 richness。
**意义**：算法选择是**实质性选择**，没有"最好"算法。

---

## 5️⃣ Clustering Evaluation（高低方向表）⭐ 陷阱金矿

| 指标 | 看什么 | 方向 |
|---|---|---|
| **WCSS** | cluster 内距离 | 越**低**越好（但 K 大自然降）|
| **Elbow** | WCSS 拐点 | 找肘部 |
| **Silhouette** | cohesion vs separation | 越**高**越好（[-1, 1]）|
| **Calinski-Harabasz** | between / within 方差比 | 越**高**越好 |
| **Gap statistic** | 与随机数据对比 | 用 **SE 规则**找最小 K |
| **BIC in mclust** | penalized likelihood | ⚠️ **越高越好**（正向 BIC）|
| **BIC in poLCA** | standard BIC | ⚠️ **越低越好** |

⚠️ **mclust 用 positive BIC formulation**，方向**和 poLCA 相反**！
选择题超爱出这道。

### External Validation（有标签时）
- **ARI (Adjusted Rand Index)**——**最常报告**
- **NMI** = normalized mutual information
- **V-measure** = homogeneity + completeness 调和均值

### Cluster Stability
**Bootstrap** + Jaccard。
>0.85 高稳定；<0.6 可能是 artifact。

---

## 6️⃣ Soft Clustering / Mixture Models

### 三方法对比 ⭐
| 方法 | 数据类型 | latent 是什么 | 输出 | 拟合 |
|---|---|---|---|---|
| **GMM** | continuous | Gaussian component | **responsibilities** | **EM** |
| **LCA** | categorical | latent class | posterior class prob | **EM** |
| **LDA** | count / text | topic mixture | **β + γ** | **Gibbs / VEM** |

### 必记句子
- Soft clustering 给**概率**，不给固定 label
- **GMM = k-means 的 probabilistic version**，簇可 elliptical
- **LCA 假设 local independence**（给定 class，items 独立）
- **LDA = document 的 soft clustering**：一篇文章同时属多 topic

### GMM 协方差形状
| | 含义 |
|---|---|
| **Spherical** | σ²I（= k-means 极限）|
| **Diagonal** | 组内不相关 |
| **Full** | 任意椭圆 |

### Conditional Independence 违反 ⭐⭐
**关键陷阱**：当 conditional independence 假设被违反时，
算法**不会崩溃**——它会**把单簇拆成多簇**来吸收组内相关。
→ 你看到的 K **被人为放大**。

**诊断**：**Bivariate residual**（item 对 observed vs fitted 频数）。

### GMM vs k-means
| | **k-means** | **GMM** |
|---|---|---|
| 分配 | hard | soft |
| 簇形 | 等径球 | 椭圆 |
| 不确定性 | 无 | 完整后验 |
| 选 K | elbow / silhouette | **BIC** |

---

## 7️⃣ Manifold Learning（按"保存什么"组织）

### Manifold Hypothesis
高维数据在**低维 manifold** 附近。
**Intrinsic dimension** ≪ ambient dimension。
Euclidean 距离在**curved manifold** 上是错的。

### 七方法对比 ⭐
| 方法 | 保存什么 | 关键词 | **OOS** |
|---|---|---|---|
| **Isomap** | global **geodesic** distance | k-NN graph + Dijkstra + MDS | ✗ |
| **LLE** | local linear reconstruction weights | same weights in low-D | ✗ |
| **Laplacian Eigenmaps** | graph neighbors stay close | graph Laplacian eigenvectors | ✗ |
| **Kernel PCA** | nonlinear via kernel | kernel trick；RBF | **✓** |
| **MVU** | 局部距离精确 | SDP；intrinsic dim from eigenvalue gap | ✗ |
| **t-SNE** | local neighbor **probabilities** | KL；Student-t；perplexity | ✗ |
| **UMAP** | **density-normalized** fuzzy graph | LE init；显式 repulsion | **✓** |

→ 只有 **KPCA** 和 **UMAP** 原生 OOS。

### Isomap 流程必记
**3 步**：k-NN graph → all-pairs shortest path (Dijkstra) → Classical MDS。
- k 太小 → graph 断
- k 太大 → **短路**穿过卷层

### t-SNE 三大警告 ⭐⭐
1. **簇间距离没有意义**
2. **簇大小没有意义**
3. **Global structure 丢失**

→ "好的可视化" ≠ "可信的距离测量"。

### UMAP 比 t-SNE 好在哪 ⭐
- **Density-normalized** 高维 metric
- 损失函数有**显式 repulsion**（t-SNE 没有）
- **LE init**（不是 random）
- **支持 OOS**

### Kernel PCA
- 用 kernel 在隐式高维空间做 PCA
- 常用：linear / polynomial / **RBF (Gaussian)**
- ⚠️ **Pre-image problem 病态** → 不是 generative

---

## 8️⃣ Text Models（三层：classical → static → contextual）

### 第一层：预处理
| 步骤 | 必记 |
|---|---|
| **Tokenization** | whitespace / **BPE / WordPiece** |
| **Normalization** | lowercase, 去标点 |
| **Stemming** | 砍后缀；**粗糙、过度合并** |
| **Lemmatization** | 用词典；**精准但贵**；首选 |

### 第二层：Bag-of-Words
| 概念 | 必记 |
|---|---|
| **DTM (Document-Term Matrix)** | 99% 稀疏 |
| **TF-IDF** | 下调常见词；⚠️ **不能喂 LDA** |
| **n-grams** | 合并 "climate_change" |
| **Co-occurrence matrix** | V×V，**distributional hypothesis** |

⚠️ BoW 丢弃词序："Dog bites man" = "Man bites dog"。

### 第三层：Static Embeddings
| 方法 | 任务 | 关键 |
|---|---|---|
| **CBOW** | context 预测 center | 稀有词弱 |
| **Skip-gram** | center 预测 context | 稀有词**好** |
| **GloVe** | log co-occurrence 加权最小二乘 | 训练快 |

**Negative sampling (SGNS)**：把 softmax 换成 k 个二分类。
**Levy-Goldberg**：SGNS = 隐式分解 **shifted PMI** 矩阵。

### Static embedding 致命缺陷 ⭐
**Polysemy**：bank（河岸 vs 银行）只有一个向量
→ 各义项的加权平均 → 需 contextual embeddings。

### 第四层：Contextual Embeddings
| 方法 | 关键 |
|---|---|
| **BERT** | **bidirectional**；**MLM** 预训练 |
| **GPT** | **causal**；生成 |
| **Sentence-BERT** | siamese fine-tune；cosine 可比 |

### Attention 机制
| 部件 | 角色 |
|---|---|
| **Query (Q)** | 位置 i "在找什么" |
| **Key (K)** | 位置 j "能提供什么" |
| **Value (V)** | j 实际"贡献什么" |

- **Self-attention**：Q/K/V 都来自同一序列
- **Multi-head**：并行多头学不同关系
- 必加 **position embedding**

---

## 9️⃣ Topic Modeling 专门小表

### LDA 概念
| 符号 | 含义 |
|---|---|
| **β** | topic-word distribution（哪些词定义 topic）|
| **γ** | document-topic distribution（每篇属各 topic 多少）|
| **α** | 控 **document-topic sparsity**（小 → 文档稀疏）|
| **η** | 控 **topic-word sparsity**（小 → 主题稀疏）|

### 生成故事
1. 每 topic 抽 word distribution **β_k**
2. 每 document 抽 topic distribution **γ_d**
3. 每词位置：先抽 topic，再抽 word

### 推断
- **Variational EM**：快、确定
- **Collapsed Gibbs**：积分掉 β、γ

### 选 K 的陷阱 ⭐⭐
| 指标 | 评价 |
|---|---|
| **Perplexity** | ⚠️ 数学好，**人评更差**（Chang "Reading Tea Leaves"）|
| **Coherence** (UMass, NPMI) | ✓ 与人评相关 |
| **Exclusivity** | ✓ top word 是否独有 |

⚠️ 选择题超爱问："为什么 perplexity 不好？"
答：**lower perplexity ≠ better interpretability**。

⚠️ **Cardinality caveat**：coherence 在大 K 上**机械偏高**。

### 入侵任务
- **Word intrusion**：5 top words + 1 外来词
- **Topic intrusion**：文档 + 3 高 prob topic + 1 低

### STM (Structural Topic Model) ⭐
**解决**：两步法（先 LDA 再回归 γ）的 **attenuation bias**。
- γ 估计有不确定性 → 作回归 y 系数被衰减
- STM 把协变量**直接嵌入** generative model
- **Topic prevalence**：主题多少 ~ 协变量
- **Topic content**：怎样谈 ~ 协变量

### BTM (Biterm Topic Model)
短文本（< 50 token/doc）→ LDA **沉默失败**。
BTM 基本单元 = **biterm**（全语料无序词对）。

### BERTopic 流程
**Embed (Sentence-BERT) → UMAP → HDBSCAN → c-TF-IDF**。
- ✓ 短文本好；多义词稳健
- ✗ **不直接支持协变量** → 社科仍需 STM

### Topic Models vs Word Embeddings
| | LDA / STM | word2vec |
|---|---|---|
| 单元 | document | word |
| 上下文 | 整个文档 | 局部窗口 |
| **Polysemy** | 捕捉 | **不捕捉** |

---

## 🔟 Autoencoder / VAE / AAE

### AE 家族对比 ⭐
| 方法 | latent space | 训练目标 | 能生成? |
|---|---|---|---|
| **Plain AE** | deterministic bottleneck | reconstruction | ✗ |
| **Linear AE** | linear bottleneck | reconstruction | ≈ **PCA** |
| **Denoising AE** | robust features | noise → clean | ✗ |
| **Sparse AE** | few units active | reconstruction + **L1** | ✗ |
| **VAE** | **stochastic** distribution | reconstruction + **KL** | **✓** |
| **AAE** | latent matched to prior by discriminator | recon + **adversarial** | **✓** |

### Linear AE = PCA ⭐⭐
- 线性 encoder + decoder + MSE
  → 优化的**子空间 = top-L PC 子空间**
- 轴可能不同（任意基），**子空间相同**

**意义**：AE 比 PCA 多的好处**全部来自非线性激活**。

### Plain AE 的局限
**Latent space 不规整、不连续** → 不能随便 sample 一个点生成。
→ 这是 **VAE / AAE 存在的理由**。

### VAE
**关键改变**：encoder 输出**概率分布参数**（μ, σ），不是单点。

**三个分布** ⭐（易混点）：
1. **Encoder**：approximate posterior q(z|x)
2. **Decoder**：conditional likelihood p(x|z)
3. **Prior** p(z)：在 latent 上锚定

**ELBO 两项拉锯**：
- **Reconstruction term**：让 q 编码 x 信息
- **KL term**：让 q ≈ prior

**Reparameterization trick**：把采样写成 μ + σ⊙ε（ε 从固定分布）
→ 让 VAE 可用 SGD 训练。

### VAE vs PPCA
**PPCA = VAE 的线性极限**。
换非线性 decoder → 表达力↑、失去闭式解。
→ VAE 是 factor analysis 家族的**非线性表亲**。

### AAE
- KL 正则换成 **discriminator network**
- ✓ **任何可采样 prior**（非高斯、多模、离散）

---

## 📐 贯穿全书的家族关系（一句话总结每个方法）

| 方法 | 一句话 |
|---|---|
| **PCA** | covariance 特征分解 |
| **Linear AE** | 神经网络伪装的 PCA |
| **PPCA** | PCA + Gaussian latent |
| **VAE** | PPCA + 非线性 decoder |
| **Classical MDS** | PCA 的 dual |
| **Factor Analysis** | 更灵活的 PPCA（分 common/unique）|
| **IRT** | categorical 观测的 factor model |
| **LCA** | 离散 latent 的 factor model |
| **LDA** | document 上的 mixture model |
| **BERTopic** | LDA 架构 + contextual embedding |
| **k-means** | isotropic + 硬化 responsibility 的 GMM |
| **GMM** | k-means 的软泛化 |
| **Spectral** | LE eigenvectors + k-means |
| **MF recsys** | 稀疏矩阵低秩近似 |
| **Spatial voting** | 投票矩阵上的 MF |

**一句话**：所有方法 = **低维 latent 结构 + 围绕它的变异**。

---

## 🎯 易混淆 ABCD 辨析（备考最后一晚专门看）

### 测量
**1. α vs ω**：α 假 tau-equivalence → 不等时**低估**；ω 从 factor 算更稳健。
**2. Reflective vs Formative**：删一项变不变 construct？变 → formative。
**3. Reliability vs Validity**：reliable 但 invalid 可能；valid 但 unreliable **不可能**。
**4. EFA vs CFA**：同样本依次做 = **chance capitalization**。
**5. PCA vs FA**：descriptive vs probabilistic；total vs common+unique。
**6. Kaiser vs Parallel Analysis**：Kaiser 过度保留；parallel 最稳妥。
**7. Bifactor vs Hierarchical**：general factor parallel vs mediated。
**8. DIF**：**不是** group mean diff；是 item mapping 不同。

### 降维 / 流形
**9. PCA 双等价**：max projected variance ≡ min reconstruction error。
**10. Metric vs Non-metric MDS**：保 distance vs 保 rank。
**11. Isomap k 选择**：太小 graph 断；太大短路。
**12. KPCA**：**不是 generative**（pre-image 病态）。
**13. t-SNE 三大警告**：簇间距离 / 簇大小 / global 都不可靠。
**14. UMAP 比 t-SNE 好**：repulsion + LE init + OOS。
**15. 哪些方法支持 OOS**：只有 **KPCA** 和 **UMAP**。

### 聚类
**16. Kleinberg**：scale-inv / richness / consistency 不可同时。
**17. k-means scale**：**永远**先 scale。
**18. k-means 失败模式**：非凸 → DBSCAN；不等大 → GMM；outlier → PAM。
**19. Linkage**：single → chaining；Ward → 紧凑等大。
**20. DBSCAN vs HDBSCAN**：单密度 vs 变密度。
**21. Spectral 用哪个 Laplacian**：**normalized** graph Laplacian。

### 评估
**22. BIC 方向陷阱** ⭐：**mclust 高好；poLCA 低好**。
**23. Silhouette / CH**：都越高越好。
**24. ARI vs accuracy**：ARI 才正确（标签 permutation 不变）。

### 软聚类
**25. Conditional independence 违反**：**K 膨胀**（沉默失败）。
**26. GMM 协方差**：spherical = k-means 极限。
**27. GMM 选 K**：用 **BIC**（不是 elbow）。

### 文本
**28. TF-IDF 错误用法**：**不能喂 LDA**（LDA 要 count）。
**29. CBOW vs Skip-gram**：稀有词用 **Skip-gram**。
**30. Static embedding 缺陷**：**polysemy**。
**31. BoW**：丢词序；99% 稀疏。

### 主题
**32. Perplexity 陷阱** ⭐：lower ≠ better topics。
**33. 选 K 用什么**：**coherence + exclusivity**。
**34. STM 解决什么**：两步法 **attenuation bias**。
**35. 短文本主题**：LDA **沉默失败** → 用 **BTM / BERTopic**。
**36. BERTopic 不能做什么**：不直接支持协变量。

### Attention / Foundation Models
**37. BERT vs GPT**：bidirectional vs causal。
**38. CoT 警告**：trace **不保证忠实**；提升精度但别当解释。

### 自编码器
**39. Linear AE = ?**：**= PCA**（同子空间）。
**40. Plain AE 不能 sample**：latent 不规整。
**41. VAE 三个分布**：encoder（approx posterior）/ decoder / prior。
**42. VAE vs PPCA**：PPCA 是 VAE 的线性极限。
**43. Reparameterization trick**：让采样**可微**（VAE 可 SGD 训练）。
**44. AAE vs VAE**：discriminator 替 KL → 允许任何 prior。

考试加油！💪
