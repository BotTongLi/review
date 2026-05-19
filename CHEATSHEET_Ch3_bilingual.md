# Ch 3. Measurement, Similarity, Proximity（中英混合版）

考试：30 道选择题，40 分钟。
重点：**concept distinction**、**failure modes**、**decision rules**。

---

## 🔥 本章高频考点（先看这个）

1. **Scale vs index**：因果方向决定能不能用 **α**、**factor analysis**。
2. **Reliability vs validity**：**reliability** 是 **validity** 的
   **necessary but not sufficient condition**。
3. **PCA vs factor analysis**：descriptive vs probabilistic model；
   **total variance** vs **common + unique variance**。
4. **EFA + CFA 同样本** = **chance capitalization**。
5. **Cronbach's α 三个批评**：item 数量、**tau-equivalent**、
   不等于 **unidimensional**。
6. **DIF ≠ group mean difference**：是 **item mapping** 方式不同。
7. **Face validity** 是**最弱**的 validity 证据。
8. **Reflective vs formative**：删一项会不会改变 construct 定义？

---

## Stevens Measurement Levels

| Level | 允许操作 | 例子 |
|---|---|---|
| **Nominal** | 计数、mode | 性别、政党 |
| **Ordinal** | 排序、median | Likert、学历 |
| **Interval** | 减法、mean、SD | 摄氏温度、IQ |
| **Ratio** | 所有 arithmetic | 身高、reaction time |

⚠️ 在 **nominal** 上算 mean = **category error**；
**interval** 上算 geometric mean 无意义（零点 arbitrary）。

---

## Scale vs Index（最常考）

| | **Scale (reflective)** | **Index (formative)** |
|---|---|---|
| 因果 | **latent → items** | **items → construct** |
| Items 相关? | 必须相关 | 不必相关 |
| 删一项 | 不改变 construct | **改变** construct 定义 |
| 用 α / FA? | ✓ | **✗ 不适用** |
| 例 | 焦虑 scale | **SES**（社会经济地位）|

**判别问题**：construct 能在 items 不变时变化吗？
能 → **reflective**；不能 → **formative**。

---

## Classical Test Theory (CTT)

- **observed score = true score + error**
- **Reliability**：**true score variance** 占 **observed
  score variance** 的比例。
- **Reliability** 是 **validity** 的 **necessary but not
  sufficient condition**。
- 浴室秤永远多 10 磅 → **reliable** 但 **invalid**。
- 卷尺每次读数不同 → **unreliable** 也必然 **invalid**。

---

## Cronbach's α

- Internal consistency 最常用 coefficient。
- 阈值：**0.7 够 / 0.8 好 / 0.9 优秀**。

⚠️ **三个常见批评**（必考）：
1. **Item 数越多 α 越高**（机械效应）。
2. 假设 **tau-equivalent**（所有 items 等 loading）。
   Loading 不等时 α **低估** reliability。
3. **高 α ≠ unidimensional**。两个相关 factor 也能给高 α。

---

## McDonald's ω

- 从 **factor model** 直接算，比 α 稳健。
- **ω_t (total)**：所有 **common factors** 解释的方差比例。
  Tau-equivalent 时 ω_t = α；否则 ω_t **≥ α**。
- **ω_h (hierarchical)**：**bifactor model** 中
  **general factor** 解释的比例。
- **ω_h / ω_t 高** → 即使 multidimensional，总分仍可辩护。

---

## Reliability 类型

| Type | 测什么 |
|---|---|
| **Test-retest** | 时间稳定性 |
| **Parallel forms** | 等价版本一致 |
| **Internal consistency** | items 一致（α、ω）|
| **Inter-rater** | raters 一致（**κ**、**ICC**）|

---

## Validity（论证，不是 coefficient）

**五类 validity evidence**：
- **Content**：items 是否覆盖 construct
- **Internal structure**：factor structure 匹配理论
- **Relations to other variables**：convergent + discriminant
- **Response processes**：受访者是否如预期思考
- **Consequences** of testing

⚠️ **Face validity 是最弱的证据**，易被
**socially desirable responding** 污染。

---

## MTMM (Multitrait-Multimethod) Matrix

| 关系 | 应该是 |
|---|---|
| 同 trait 不同 method | **高**（convergent）|
| 不同 trait 同 method | 中等（method bias）|
| 不同 trait 不同 method | **低**（discriminant）|
| 同 trait 同 method | test-retest 对角 |

→ Convergent > discriminant 且 trait effect > method effect
就是 **construct validity** 的证据。

---

## DeVellis 八步量表开发

关键点（其他步骤略）：
- Item pool 要**冗余**
- 专家评审
- 每 item 至少 10 个受访者
- ⚠️ **独立样本验证**（最常被跳过的一步）

---

## PCA vs Factor Analysis ⭐

| | **PCA** | **Factor Analysis** |
|---|---|---|
| 性质 | descriptive | **probabilistic model** |
| 方差分解 | **total variance** | **common + unique** |
| Components/factors | 数据的精确线性组合 | latent 随机变量 |
| 用途 | 降维、composite score | 测试 latent causes |

---

## 决定 factor 数量

- **Scree plot**：找拐点（kink）
- **Kaiser** (**λ > 1**)：常**过度保留**
- **Parallel analysis**：与随机数据比 → **最稳妥**

---

## Factor Rotation

| | 类型 | 假设 |
|---|---|---|
| **Varimax** | orthogonal | factors 不相关 |
| **Oblimin / Promax** | **oblique** | factors 相关 |

→ 多数 psychological constructs 应该用 **oblique**。
→ 目标：**simple structure**（每 item 主载一个 factor）。

---

## Bifactor vs Hierarchical

| | 结构 |
|---|---|
| **Hierarchical** | first-order factors 上有 **second-order general factor**（mediated）|
| **Bifactor** | **general factor** 和 **specific factors** 并列 load 在 items 上 |

两者回答不同问题，**bifactor** 问 general factor 在 item 层
解释多少方差。

---

## EFA vs CFA ⭐

| | **EFA** | **CFA** |
|---|---|---|
| 性质 | exploratory | confirmatory |
| 结构 | 发现 | **强加** structure |
| Cross-loading | 允许 | 通常 fix 为 0 |
| 输出 | loadings | + fit indices（**CFI, TLI, RMSEA, SRMR**）|

⚠️ **标准流程**：EFA on sample A → CFA on **independent**
sample B。同样本同时做 = **chance capitalization**。

---

## Item Response Theory (IRT)

处理 binary / ordered categorical responses。

**2PL** 两个参数：
- **difficulty (b)**：受访者有 50% 概率认可 item 的 θ 水平
- **discrimination (a)**：**ICC** 斜率，区分能力

**3PL** = 2PL + **guessing parameter (c)**：multiple-choice
猜对的概率，**high-stakes testing** 常用。

**Graded Response Model (GRM)**：ordered polytomous
（Likert 风格），每 item 一个 a + (K-1) 个 thresholds。

---

## Item Information

- Item 在 **difficulty b 附近**提供最多 information。
- **Test information** = items 的信息之和。
- **SE(θ) = 1 / √I(θ)**——所以 reliability 随 θ 变化。
- **CAT (Computerized Adaptive Testing)**：按当前 θ 估计选题，
  用更少 items 达到目标精度。

---

## Differential Item Functioning (DIF) ⭐

- 同 θ 不同 group 对 item 认可概率**不同**。
- ⚠️ **DIF ≠ group mean difference**——是 item 映射到
  construct 的方式不同。
- 含 DIF 的 scale **跨组直接比较 mean 是 misleading 的**。
- 检测：**Mantel-Haenszel**、**lordif**、multi-group IRT。

---

## CTT vs IRT

| | **CTT** | **IRT** |
|---|---|---|
| 分数 | total score | latent **θ** |
| Difficulty | **sample-dependent** | **sample-invariant** |
| SE | 区间常数 | 随 θ 变化 |
| 样本量 | 几百 | **500+** |

---

## 统一的 Latent Variable 观点

| Indicators \ Latent | Continuous | Discrete |
|---|---|---|
| Continuous | **Factor analysis** | **Latent Profile Analysis** |
| Categorical | **IRT** | **Latent Class Analysis** |

→ 同一族模型，差别只在 indicator 和 latent 是连续还是离散。

---

## Distance Metrics

| Metric | 用途 / 性质 |
|---|---|
| **Euclidean** | default（先 standardize）|
| **Manhattan** | 对 outliers 稳健 |
| **Mahalanobis** | 用 covariance 校正特征相关 |
| **Cosine** | 忽略 magnitude；text 标准 |
| **Jaccard** | binary 集合 |
| **Gower** | 混合类型数据 |

---

## 🎯 易混淆 ABCD 选项辨析（针对选择题陷阱）

### 1. α vs ω
- α 假设 **tau-equivalence** → loading 不等时 **低估** reliability。
- α 不是 **unidimensionality** 测试 → 高 α 可来自相关的 multi-factor。
- ω 直接从 factor model 算 → 更稳健。

### 2. Reflective vs Formative
- Reflective：latent **引起** items → items 相关 → 删一项**不改**
  construct 定义。
- Formative：items **构成** construct → 不必相关 → 删一项**改变**
  定义 → **不能用 α**。

### 3. Reliability vs Validity
- Reliable but invalid：✓ 可能（浴室秤）
- Invalid but reliable：✓ 可能
- Valid but unreliable：✗ **不可能**——validity 需要 reliability。

### 4. EFA vs CFA
- EFA：所有 items 可 load 所有 factors（cross-loading 允许）。
- CFA：分析者**指定** loading 结构，给 fit indices。
- ⚠️ 同样本依次做 EFA → CFA = **chance capitalization**。

### 5. PCA vs FA
- PCA：descriptive，分 **total variance**，components 是数据的精确组合。
- FA：probabilistic，分 **common + unique**，factors 是 latent。

### 6. Parallel analysis vs Kaiser
- Kaiser（λ > 1）→ **over-retains**。
- Parallel analysis 比随机数据 → **最稳妥**。

### 7. Varimax vs Oblimin
- Varimax = **orthogonal**（factors 不相关）。
- Oblimin / Promax = **oblique**（factors 相关）。
- 多数 psychological constructs → oblique。

### 8. Bifactor vs Hierarchical
- Hierarchical：general factor **mediated through** first-order。
- Bifactor：general + specific **parallel**，items 同时 load 两者。

### 9. IRT 2PL vs 3PL
- 2PL：difficulty + discrimination。
- 3PL：+ **guessing parameter**，multiple-choice 用。

### 10. DIF
- 不是 group mean difference。
- 是同 θ 下不同 group 对 item 的反应不同。
- 含 DIF 的 scale → 跨组比较 mean **misleading**。

### 11. Face validity
- **最弱**的 validity 证据。
- 易被 socially desirable responding 污染。
- ⚠️ "looks like measures construct" 本身不算证据。

### 12. MTMM
- Convergent（同 trait 不同 method）→ 应**高**
- Discriminant（不同 trait 不同 method）→ 应**低**

考试加油！
