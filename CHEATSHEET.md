# UML4SS Cheatsheet — Chapters 3–12

Exam review covering measurement, recsys/spatial, manifold learning, clustering (hard, density, soft), text, topic models, contextual embeddings, autoencoders.

---

## Ch 3. Measurement, similarity, proximity

### Levels of measurement (Stevens)
| Level | Admits | OK statistics |
|---|---|---|
| Nominal | equality | mode, count |
| Ordinal | order | median, rank corr |
| Interval | subtraction, no true 0 | mean, SD, Pearson |
| Ratio | true zero | all arithmetic |

### Scales vs. indices
- **Scale (reflective):** latent construct → items. Items correlate. Use α/ω, factor analysis.
- **Index (formative):** items → construct (e.g., SES). Items need NOT correlate. α and factor analysis inappropriate.

### Classical Test Theory (CTT)
- Model: $X = T + e$, with $E[e]=0$, $\mathrm{Cor}(T,e)=0$, errors uncorrelated.
- $\mathrm{Var}(X) = \mathrm{Var}(T) + \mathrm{Var}(e)$.
- **Reliability:** $\rho_{XX'} = \mathrm{Var}(T)/\mathrm{Var}(X) \in [0,1]$.

### Reliability coefficients
- **Cronbach's α:** $\alpha = \frac{k}{k-1}\left(1 - \frac{\sum\sigma_i^2}{\sigma_T^2}\right)$. Thresholds 0.7 / 0.8 / 0.9.
  - Critiques: grows with k; assumes tau-equivalence (equal loadings); high α ≠ unidimensional.
- **McDonald's ω:**
  - $\omega_t$: total reliability from factor model; $\omega_t \geq \alpha$.
  - $\omega_h$: variance explained by general factor in bifactor model. High $\omega_h/\omega_t$ → defensible total score.
- Other: test-retest, parallel forms, inter-rater (Cohen's κ for categorical, ICC for continuous).

### Validity
- Reliable ≠ valid (heavy bathroom scale). Valid requires reliable.
- 5 sources: content, internal structure, relations to other variables, response processes, consequences.
- **MTMM matrix:** convergent (same trait, diff method) high; discriminant (diff trait, diff method) low.
- Face validity = weakest evidence.

### DeVellis 8-step scale development
1. Define construct precisely. 2. Generate redundant item pool. 3. Choose response format. 4. Expert review. 5. Development sample (≥10/item). 6. Exploratory analysis. 7. Refine. 8. **Confirm on independent sample** (most often skipped).

### Factor analysis
- Model: $\mathbf{x} = \boldsymbol{\Lambda}\mathbf{f} + \boldsymbol{\epsilon}$, $\mathbf{f}\sim N(0,\Phi)$, $\epsilon\sim N(0,\Psi)$ diagonal.
- $\Sigma_{xx} = \Lambda\Phi\Lambda^\top + \Psi$.
- **PCA vs FA:** PCA partitions *total* variance (descriptive, exact); FA partitions common + unique (probabilistic model).
- Extraction: ML (gives SEs, χ²), Principal Axis (robust), Minres (no distributional assumption).
- **Choosing # factors:** scree plot, Kaiser (λ>1, over-retains), **parallel analysis** (most defensible).
- **Rotation:** varimax (orthogonal); oblimin/promax (oblique, allows factor correlation).
- **Bifactor:** general + specific factors, all orthogonal. **Hierarchical:** general factor mediated through first-order.
- **EFA → CFA discipline:** EFA on sample A, CFA on sample B. CFA fit: CFI>0.95, TLI>0.95, RMSEA<0.06, SRMR<0.08.

### Item Response Theory (IRT)
- **2PL:** $\Pr(x_{ij}=1|\theta_i) = \frac{1}{1+\exp(-a_j(\theta_i - b_j))}$
  - $b_j$ = difficulty (θ at 50% endorsement); $a_j$ = discrimination (slope).
- **3PL:** adds guessing $c_j$; $\Pr = c_j + (1-c_j)\cdot[\text{2PL}]$.
- **Graded Response Model (Samejima):** $K-1$ thresholds per item for ordered categorical.
- **Item info:** $I_j(\theta) = a_j^2 p_j(\theta)(1-p_j(\theta))$. Test info = sum. SE(θ) = 1/√I(θ).
- **DIF:** same θ, different groups → different P(endorse). Detect via Mantel-Haenszel, lordif.

### CTT vs IRT
| | CTT | IRT |
|---|---|---|
| Score | total X | latent θ |
| Difficulty | sample-dependent | sample-invariant |
| SE | constant | varies with θ |
| Sample size | modest | 500+ |

### Unified latent-variable view
| Indicators \ Latent | Continuous | Discrete |
|---|---|---|
| Continuous | Factor analysis | Latent profile |
| Categorical | IRT | Latent class |

### Distances
- **Euclidean** $\sqrt{\sum(x_d-y_d)^2}$ — default, standardize first.
- **Manhattan** $\sum|x_d-y_d|$ — robust to outliers.
- **Mahalanobis** $\sqrt{(x-y)^\top\Sigma^{-1}(x-y)}$ — corrects for covariance. = Euclidean on ZCA-whitened data.
- **Cosine** — magnitude-invariant; standard for text.
- **Jaccard** = |A∩B|/|A∪B| — binary similarity. **Hamming** counts mismatches.
- **Gower's coefficient** — mixed types (continuous/ordinal/nominal); `cluster::daisy`.

---

## Ch 4. Recommender systems & spatial models

### Rating matrix
- $R \in \mathbb{R}^{N\times M}$, mostly missing. Explicit (ratings) vs implicit (clicks/views) feedback.
- Implicit has no negatives; data are MNAR (people rate strong opinions).

### Baseline
$\hat{R}_{ij} = \mu + b_i + b_j$ (global + user bias + item bias). Accounts for most explainable variance on Netflix; report MF gains *relative to this*.

### Matrix factorization
- Model: $\hat{R}_{ij} = \mu + b_i + b_j + \mathbf{p}_i^\top \mathbf{q}_j$, with $K$ = 10–200.
- Equivalent to truncated SVD (Eckart-Young) when fully observed.
- **Objective (missing-aware):**
$$\min \sum_{(i,j)\in\mathcal{O}}(R_{ij} - \hat{R}_{ij})^2 + \lambda(\|P\|_F^2 + \|Q\|_F^2 + \|b\|^2)$$
- Non-convex jointly, convex in P|Q and Q|P → **Alternating Least Squares (ALS)**.

### SGD update
$\mathbf{p}_i \leftarrow \mathbf{p}_i + \eta(e_{ij}\mathbf{q}_j - \lambda\mathbf{p}_i)$; similarly for $\mathbf{q}_j$. Scales linearly in observed entries.

### Probabilistic MF
Gaussian likelihood + Gaussian priors. MAP = ridge MF with $\lambda = \sigma^2/\sigma_P^2$. Gives uncertainty + non-Gaussian extensions.

### Variants
- **NMF:** non-negative P,Q. Parts-based, sparse, interpretable. Topic-like decomposition of TF-IDF.
- **Implicit feedback (Hu-Koren-Volinsky):** confidence-weighted; all unobserved pairs contribute.
- **BPR (Bayesian Personalized Ranking):** $\Pr(i>_u j) = \sigma(\mathbf{p}_u^\top(\mathbf{q}_i - \mathbf{q}_j))$. For top-k recommendation.
- **Factorization Machines:** include side info; all pairwise feature interactions.
- **Neural CF (NeuMF):** replaces bilinear with MLP; loses SVD guarantees.
- **Bandit-based:** Thompson sampling/UCB for exploration vs exploitation.

### Evaluation
- Rating prediction: RMSE, MAE.
- Top-k: Precision@k, Recall@k, NDCG, MAP.

### Spatial voting (Poole-Rosenthal)
- Legislator has ideal point $\mathbf{x}_i$; bill has yea $\mathbf{y}_j$ and nay $\mathbf{n}_j$ locations.
- $\Pr(\text{yea}) = \Phi(\|\mathbf{x}_i - \mathbf{n}_j\|^2 - \|\mathbf{x}_i - \mathbf{y}_j\|^2)$.
- Identification: fix rotation/reflection by anchoring known liberals/conservatives.
- W-NOMINATE in `pscl`; dynamic ideal points (Martin-Quinn for SCOTUS).

### Recsys ↔ spatial mapping
Users=legislators, items=bills, rating=vote, $\mathbf{p}_i$=ideal point, $\mathbf{q}_j$=(yea,nay), link=identity/logit→probit.

---

## Ch 5. Nonlinear dimensionality reduction

### Manifold hypothesis
Data live near low-dim manifold in high-dim ambient space. Intrinsic dim = # degrees of freedom (rotation angle, etc.).

### Seven methods overview
| Method | Preserves | Solves | Out-of-sample |
|---|---|---|---|
| Isomap | geodesic dist | classical MDS on geodesic Gram | No |
| LLE | local linear recon weights | sparse eigenproblem | No |
| Laplacian Eigenmaps | heat-kernel neighbour graph | generalized eigenproblem on L | No |
| Kernel PCA | kernel inner products | eigendecomp of centered K | **Yes** |
| MVU | local distances + max variance | SDP + MDS | No |
| t-SNE | neighbourhood probabilities | gradient descent on KL | No |
| UMAP | density-normalized fuzzy graph | SGD + neg sampling | **Yes (saved model)** |

### Isomap
1. Build k-NN graph (Euclidean edges). 2. All-pairs shortest paths (Dijkstra) = geodesic. 3. Classical MDS on $D_G$.
- $K_G = -\frac{1}{2}C_N D_G^{(2)} C_N$, embed via top eigenvectors.
- **k too small** → graph fragments; **k too large** → short-circuit edges across folds.
- Cost: $O(N^3)$.

### LLE
1. Per point: solve $\min\|x_i - \sum_j W_{ij}x_j\|^2$ s.t. $\sum W_{ij}=1$.
2. Embed: minimize $\mathrm{tr}(Z^\top M Z)$ with $M=(I-W)^\top(I-W)$; take bottom non-trivial eigenvectors.
- Preserves local affine structure (rotation/translation/scale invariant).
- Less robust than LE on curved manifolds.

### Laplacian Eigenmaps
- Heat kernel weights: $W_{ij}=\exp(-\|x_i-x_j\|^2/t)$ on k-NN graph.
- Graph Laplacian $L = D - W$. Solve $Lv = \lambda Dv$.
- Discard $\lambda_1=0$ (constant); use $v_2,\ldots,v_{L+1}$.
- Used as **warm start for UMAP**.

### Kernel PCA
- Kernel trick: $k(x,y) = \phi(x)^\top\phi(y)$ without materializing $\phi$.
- Common kernels: linear, polynomial $(x^\top y + c)^d$, **RBF** $\exp(-\sigma\|x-y\|^2)$.
- Center kernel: $\tilde{K} = C_N K C_N$. Eigendecompose; embed = $V_L \Lambda_L^{1/2}$.
- **Out-of-sample:** project new $k^*$ onto eigenvectors.
- **Pre-image problem** ill-posed → not generative.

### MVU
- SDP: maximize $\mathrm{tr}(K)$ s.t. $K\succeq 0$, centered, neighbour distances pinned to original.
- Trace = variance; eigenvalue gap reveals intrinsic dimension automatically.
- Cost $O(N^{3.5})$ → rarely used in practice; ceiling ~2000 points.

### t-SNE
- High-D: $p_{j|i} = \frac{\exp(-\|x_i-x_j\|^2/2\sigma_i^2)}{\sum_k \exp(\cdot)}$. $\sigma_i$ chosen so entropy matches **perplexity** target.
- Symmetrize: $P_{ij} = (p_{j|i}+p_{i|j})/2N$.
- Low-D (Student-t, 1 df): $q_{ij} \propto (1+\|z_i-z_j\|^2)^{-1}$. Heavy tail fixes **crowding problem**.
- Loss: $\mathrm{KL}(P\|Q) = \sum P_{ij}\log(P_{ij}/q_{ij})$.
- Early exaggeration: multiply P by 4–12 for first ~100 iter.
- **Perplexity:** default 30; low (5–10) = local; high (50–100) = larger neighbourhoods.
- Cost: $O(N^2)$ exact, $O(N\log N)$ Barnes-Hut.

**t-SNE warnings:** inter-cluster distances NOT meaningful; cluster sizes NOT meaningful; global structure lost.

### UMAP
- High-D: density-normalized exponential $p_{j|i}=\exp(-(d(x_i,x_j)-\rho_i)_+/\sigma_i)$, with $\rho_i$ = nearest-neighbour distance. $\sum_j p_{j|i} = \log_2 K$.
- Symmetrize fuzzy union: $P_{ij} = p_{j|i}+p_{i|j} - p_{j|i}p_{i|j}$.
- Low-D: $q_{ij} = (1 + a\|z_i-z_j\|^{2b})^{-1}$; (a,b) fit from `min_dist`.
- **Fuzzy cross-entropy** (KL + explicit repulsion):
$C = \sum [P\log(P/q) + (1-P)\log((1-P)/(1-q))]$.
- Init via Laplacian Eigenmap; SGD with negative sampling. Cost $O(NK)$/epoch.
- Hyperparams: `n_neighbors` (15 default; local↔global) and `min_dist` (0.1; cluster compactness).
- **Has out-of-sample (saved model).**

### t-SNE vs UMAP
| | t-SNE | UMAP |
|---|---|---|
| Low-D kernel | Cauchy | parametric (a,b) |
| Cost | KL | fuzzy cross-entropy + repulsion |
| Init | random | Laplacian eigenmap |
| Global structure | lost | partially preserved |
| OOS | No | Yes |

### Decision rule
1. Try PCA first. 2. Visualization at scale → UMAP. 3. Production OOS → KPCA or UMAP. 4. Local geometry, small N → LE or LLE. 5. Verify isometry / find intrinsic dim → Isomap or MVU.

---

## Ch 6. Hard clustering — partitioning & hierarchical

### Three difficulties
1. No ground truth. 2. Algorithm = embedded assumption. 3. **Curse of dimensionality:** $(\max - \min)/\min \to 0$ as $D\to\infty$ → reduce dim before clustering.

### Kleinberg's impossibility theorem
No clustering function satisfies all three: **scale-invariance, richness, consistency**.
- k-means violates consistency. Single-linkage HAC violates richness.

### k-means
- **Objective (WCSS):** $J = \sum_k \sum_{n:C(n)=k}\|x_n - \mu_k\|^2$.
- Equivalent pairwise form: $J = \sum_k \frac{1}{|C_k|}\sum_{n,m\in C_k}\frac{1}{2}\|x_n-x_m\|^2$.
- **Lloyd's algorithm:** assign to nearest centroid → update centroid = cluster mean → repeat. Local minimum, finite convergence.
- **Voronoi cells:** linear hyperplane boundaries (perpendicular bisectors). Fails on non-convex shapes.
- **Always scale before k-means!** (Euclidean dominated by largest-variance feature.)
- **Initialization:** `nstart=25+` random starts; **k-means++**: pick next centroid with prob ∝ squared distance to nearest already-chosen. Worst-case $O(\log K)$ from optimum.
- Fails when: non-convex shapes, very unequal sizes/variances, outliers (pulled centroid).
- Pipeline: UMAP → k-means in low-dim space.

### k-medoids (PAM)
- Min $\sum_k \sum_{n:C(n)=k} d(x_n, m_k)$, with medoid $m_k$ a real observation.
- **BUILD** phase (greedy seeding) + **SWAP** phase (try replacing each medoid). Cost $O(K(N-K)^2)$/iter.
- Works with ANY dissimilarity (Manhattan, Gower, edit distance). Medoid = interpretable example.
- **CLARA**: PAM on random subsamples for large N.

### Hierarchical Agglomerative Clustering (HAC)
- Algorithm: start each point alone → merge closest pair → repeat. Output = dendrogram.
- **Deterministic.** Cost: $O(N^2)$ memory, $O(N^2\log N)$–$O(N^3)$ time. Use `fastcluster` for large N.
- **Read dendrogram:** only height matters; horizontal position is arbitrary. Large vertical gap suggests natural cut.

### Linkage criteria
| Name | Definition | Behaviour |
|---|---|---|
| Single | $\min d$ | chains; thin clusters; noise-sensitive |
| Complete | $\max d$ | compact, equal-diameter |
| Average (UPGMA) | mean d | compromise |
| **Ward** | $\frac{n_i n_j}{n_i+n_j}\|\bar x_i - \bar x_j\|^2$ | compact, equal-size; minimizes WCSS increase (k-means analogue) |

Use `method="ward.D2"` in R (NOT `ward.D`).

### Choosing K
- **Elbow:** WCSS vs K, look for kink.
- **Silhouette:** $s(i) = \frac{b(i)-a(i)}{\max(a,b)} \in [-1,1]$. a=mean dist within cluster; b=mean dist to nearest other. Pick K maximizing mean silhouette.
- **Calinski-Harabasz:** $\mathrm{CH}(K) = \frac{B_K/(K-1)}{W_K/(N-K)}$; higher better; favours equal-size spherical.
- **Gap statistic** (Tibshirani): $\mathrm{Gap}(K) = E^*[\log W_K] - \log W_K$ vs random reference data. Pick smallest K with Gap(K) ≥ Gap(K+1) − s_{K+1}.
- No metric replaces domain knowledge; rings have no natural K.

### External validation (when labels known)
- **ARI (Adjusted Rand Index):** pair agreements corrected for chance; 1=perfect, 0=random.
- **NMI:** normalized mutual information, [0,1].
- **Fowlkes-Mallows:** geometric mean of pairwise precision/recall.
- **V-measure:** harmonic mean of homogeneity + completeness.

### Cluster stability
- `fpc::clusterboot`: bootstrap, Jaccard overlap per cluster.
- Hennig: >0.85 highly stable; 0.6–0.75 moderate; <0.6 artifact.

---

## Ch 7. Density-based & spectral clustering

### DBSCAN
Hyperparams: ε (radius), minPts.
- **Core point:** ≥minPts neighbours in ε-ball.
- **Border:** in ε-neighbourhood of core but not core itself.
- **Noise:** neither.
- **Density-reachable** (transitive through cores); **density-connected** (via common third).
- Cluster = maximal density-connected set.
- Algorithm: walk through points, expand from cores; recursion stops at borders.

**Tuning:**
- minPts ≥ D+1 (rule of thumb), 4–5 standard for low-D.
- **k-distance plot:** sort minPts-th NN distances, find elbow → ε.
- Cost $O(N\log N)$ with kd-tree.

**Strengths:** arbitrary shapes, explicit noise, no K needed.
**Weaknesses:** ε hard in high-D (distance concentration); requires single density; border-point assignment depends on visit order.

### HDBSCAN
Removes ε.
- **Core distance:** $d_{\text{core}}(p) = d(p, p_{\text{minPts}})$.
- **Mutual reachability distance:** $d_{\text{mreach}}(p,q) = \max(d_{\text{core}}(p), d_{\text{core}}(q), d(p,q))$.
- MST on mreach graph → cut edges by decreasing weight → hierarchy.
- **Condensed tree:** keep only splits ≥ minPts on each side.
- **Cluster stability** = integrated persistence in $1/\lambda = \varepsilon$ units. Flat extraction selects clusters where stability > sum of children's.
- **Handles variable density** that defeats DBSCAN.
- Soft membership probabilities available.

### Spectral clustering (Ng-Jordan-Weiss)
1. Build similarity graph (k-NN or full Gaussian $W_{ij}=\exp(-\|x_i-x_j\|^2/2\sigma^2)$).
2. Degree matrix $D_{ii}=\sum_j W_{ij}$.
3. Normalized Laplacian: $L_{\text{sym}} = I - D^{-1/2}WD^{-1/2}$.
4. Eigenvectors $v_1,\ldots,v_K$ of K smallest eigenvalues.
5. Stack columns of N×K matrix V; row-normalize to unit norm.
6. k-means on rows of V.

**Why it works:** disconnected components → λ=0 with multiplicity K, eigenvectors = indicator. Almost-disconnected → small λ, approximate indicators.

**Hyperparams:** K + graph params (k or σ).
**Strengths:** non-convex shapes, spectral-gap diagnostic for K.
**Weaknesses:** $O(N^3)$ eigendecomp (sparse helps), sensitive to graph choice, inherits k-means' sensitivity.

### When to use what
| | DBSCAN | HDBSCAN | Spectral |
|---|---|---|---|
| Variable density | No | **Yes** | Partially |
| Explicit noise | Yes | Yes | No |
| Scales to N>10k | Yes | Yes | Slower |
| Requires K | No | No | **Yes** |

---

## Ch 8. Soft clustering & finite mixtures

### Soft assignment
$r_{ik} = \Pr(z_i=k|x_i) \in [0,1]$, $\sum_k r_{ik}=1$. **Responsibility.** Hard = MAP $\hat z_i = \arg\max_k r_{ik}$.

### Conditional independence note
Given the latent class, observed features assumed independent. Default in LCA, LDA, diagonal-cov GMM.
- When the assumption holds: clean components.
- When violated: algorithm **inflates K** to absorb within-component covariation.
- Diagnostic: bivariate residuals.

### Gaussian Mixture Model
$p(x) = \sum_k \pi_k \mathcal{N}(x|\mu_k, \Sigma_k)$, $\sum\pi_k=1$.

**Responsibility (Bayes):**
$$r_{ik} = \frac{\pi_k \mathcal{N}(x_i|\mu_k,\Sigma_k)}{\sum_j \pi_j \mathcal{N}(x_i|\mu_j,\Sigma_j)}$$

**EM algorithm:**
- **E:** compute $r_{ik}^{(t)}$ from current params.
- **M:** treat r as soft counts; $N_k = \sum_i r_{ik}$, $\pi_k = N_k/N$, $\mu_k = \frac{1}{N_k}\sum_i r_{ik}x_i$, $\Sigma_k = \frac{1}{N_k}\sum_i r_{ik}(x_i-\mu_k)(x_i-\mu_k)^\top$.
- Log-lik monotone non-decreasing; local max; multiple starts.
- **k-means = GMM limit:** $\Sigma_k \to \sigma^2 I$, $\sigma\to 0$.

**Covariance shapes:** spherical (σ²I), diagonal (uncorrelated within), full. `mclust` parameterizes $\Sigma_k = \lambda_k D_k A_k D_k^\top$, 14 models.

**Model selection:** BIC. In `mclust`: BIC = $2\ell - p\log N$ (higher better).

### GMM vs k-means
| | k-means | GMM |
|---|---|---|
| Assignment | hard | soft |
| Shape | spherical equal | elliptical, parameterized |
| Uncertainty | none | full $r_{ik}$ |
| Selection | elbow, silhouette | BIC |

### Latent Class Analysis (LCA)
Categorical analogue of GMM. Under local independence:
$$\Pr(x_i) = \sum_k \pi_k \prod_j \Pr(x_{ij}|z_i=k)$$
- Parameters: $\pi_k$, $\rho_{jkr} = \Pr(x_{ij}=r|z_i=k)$.
- EM: E-step posterior class; M-step weighted item probabilities.
- BIC for K (lower better in `poLCA`).
- **Bivariate residual** diagnostic; multiple starts essential.
- Extension: covariates on class membership via multinomial logit.

### LDA preview (soft-clustering view)
- Documents = soft cluster over K topics ($\theta_d$); topics = distributions over vocab ($\phi_k$).
- Bag-of-words = conditional independence at token level. Full treatment Ch 10.

### Summary table
| | GMM | LCA | LDA |
|---|---|---|---|
| Data | continuous | categorical | text/counts |
| Soft | $r_{ik}$ | $r_{ik}$ | $\theta_d$ |
| Component | MVN | product of categoricals | Dirichlet over words |
| Inference | EM | EM | VEM or Gibbs |
| Selection | BIC | BIC | perplexity, coherence |

### Extensions
- **Mixture of factor analyzers:** GMM with low-rank component covariance.
- **Latent profile analysis:** LCA with continuous indicators.
- **Structural topic model:** LDA with covariates.

---

## Ch 9. Text — BoW to word embeddings

### Pipeline
1. **Tokenize:** whitespace/rule-based (treebank), or subword (BPE, WordPiece) for modern LMs.
2. **Normalize:** lowercase; remove stopwords (custom!); **lemmatize > stem** (Porter stemmer over-conflates; lemmatize uses dictionary).
3. **Document-Term Matrix (DTM):** rows=docs, cols=vocab, values=counts. >99% sparse typically.

### Bag-of-words
Order discarded. "Dog bites man" = "Man bites dog". Defended pragmatically.

### TF-IDF
$$\text{tf-idf}_{t,d} = \text{tf}_{t,d}\cdot \log\frac{D}{|\{d:t\in d\}|}$$
- Common words IDF → 0. Rare words get highest weight.
- **Never feed TF-IDF into LDA** (needs counts). Use TF-IDF to filter vocabulary first.

### N-grams
Include "climate_change" as token to recover phrase meaning. Inflates vocabulary; filter by frequency.

### Co-occurrence matrix
$C_{ij}$ = count of i,j within window. Symmetric V×V. Input to LSA, GloVe. **Distributional hypothesis:** similar context → similar meaning.

### Word embeddings goal
Map vocab → $\mathbb{R}^d$ (d~hundreds). Dense, cosine-similar for similar meaning. **Static**: one vector per word (polysemy ignored).

### word2vec
Two architectures:
- **CBOW:** predict centre from average of context. $\Pr(w|\text{context}) = \frac{\exp(u_w^\top \bar v)}{\sum_{w'}\exp(u_{w'}^\top \bar v)}$.
- **Skip-gram:** predict each context word from centre. Better for rare words.

Two matrices: input V (centre or context) and output U (predicted). Conventional embedding = V; sometimes V+U.

### Negative sampling (SGNS)
Replace full softmax with k binary classifications:
$$\log\sigma(u_{w_j}^\top v_w) + \sum_{n=1}^k E_{w_n\sim P_n}[\log\sigma(-u_{w_n}^\top v_w)]$$
- Noise distribution $P_n(w) \propto \text{count}(w)^{3/4}$.
- Subsample frequent words: discard with prob $1 - \sqrt{t/f(w)}$, $t\approx 10^{-5}$.
- Typical k: 5–20 small corpus, 2–5 large.

### Levy-Goldberg result
SGNS implicitly factorizes shifted PMI:
$$VU^\top \approx \mathrm{PMI}(w,c) - \log k, \quad \mathrm{PMI} = \log\frac{P(w,c)}{P(w)P(c)}$$
→ Word2vec = low-rank matrix factorization.

### GloVe
$$J = \sum_{w,c} f(X_{wc})(v_w^\top u_c + b_w + b_c - \log X_{wc})^2$$
- $f(x) = (x/x_{\max})^\alpha$ if x<x_max else 1; $x_{\max}=100$, $\alpha=0.75$.
- Faster than SGNS on large corpora.

### word2vec vs GloVe
| | SGNS | GloVe |
|---|---|---|
| Input | streaming corpus | pre-computed co-occurrence |
| Implicit matrix | shifted PMI | log X |
| Rare words | skip-gram good | robust |

### Analogies
king − man + woman ≈ queen (syntactic + semantic).

### Fatal flaw: polysemy
*bank* (river vs financial) = single vector = average over senses. Solved by contextual embeddings (Ch 11).

---

## Ch 10. Probabilistic topic models

### Generative LDA
For each topic k: $\phi_k \sim \text{Dir}(\eta)$ over V-vocab simplex.
For each document d:
- $\theta_d \sim \text{Dir}(\alpha)$ over K-topic simplex.
- For each word position n: $z_{dn} \sim \text{Cat}(\theta_d)$; $w_{dn} \sim \text{Cat}(\phi_{z_{dn}})$.

| Symbol | Meaning |
|---|---|
| K | # topics (user) |
| V | vocab size |
| $\theta_d$ | doc-topic, "gamma" in `tidytext` |
| $\phi_k$ | topic-word, "beta" |
| $\alpha,\eta$ | Dirichlet concentration; small → sparse |

### Inference
- **Variational EM** (VEM): fast, deterministic.
- **Collapsed Gibbs sampling:** integrate out $\theta,\phi$ analytically. Conditional:
$$\Pr(z_{dn}=k|\cdot) \propto \underbrace{(n_{d,k}^{-dn}+\alpha)}_{\text{doc uses topic?}}\cdot \underbrace{\frac{n_{k,w}^{-dn}+\eta}{n_{k,\cdot}^{-dn}+V\eta}}_{\text{topic uses word?}}$$

### Preprocessing
- **Custom stopwords**: domain-specific (e.g., procedural words in congressional speech).
- N-grams collapse phrases.
- **Lemmatize, don't stem** (Schofield: stemming degrades interpretability).
- TF-IDF to filter vocab → then feed raw counts.

### Choosing K
- **Perplexity:** $\exp(-\log p(w)/N)$. Lower predicts better, but **Chang et al. (Reading Tea Leaves):** lower perplexity → worse human interpretability.
- **Coherence (UMass, NPMI):** correlates with intrusion-task accuracy.
- **Exclusivity:** top words unique to this topic.
- **Cardinality caveat:** coherence biased toward larger K.

**Word intrusion:** show 5 top words + 1 random → identify intruder.
**Topic intrusion:** show doc + 3 top topics + 1 low → identify intruder.

**Workflow:** fix preprocessing → sweep K (10,20,30,40,50) → Pareto frontier coherence×exclusivity → inspect labels → check stability at ±20% K.

### Structural Topic Model (STM)
LDA + document covariates.
- **Topic prevalence** $\theta_d$: logistic-normal mean depends on covariates $X_d$.
- **Topic content** $\phi_k$: can vary by covariate $U_d$.
- Avoids two-step LDA-then-regress attenuation bias.
- Use `init.type="Spectral"` for reproducibility.
- `estimateEffect()` for covariate effects with SE.

### BTM (Biterm Topic Model)
For short text (<50 tokens/doc): drop document-level story, model topics over unordered word pairs ("biterms") in entire corpus. Document topics inferred post-hoc.

### LDA vs word embeddings
| | LDA/STM | word2vec/GloVe |
|---|---|---|
| Unit | document | word |
| Context | document | local window |
| Polysemy | captured (loads on multiple topics) | not captured |

### 2026 workflow
1. STM with covariates (structural inference).
2. BERTopic on same corpus (semantic exploration).
3. Compare; disagreements = interesting cases.
4. Validate with human-coded subsamples or LLM-judged intrusion.

---

## Ch 11. Contextual embeddings & modern topic models

### Attention — weighted sum
$y_i = \sum_j a_{ij} x_j$, $\sum_j a_{ij}=1$, weights from sequence.

### Query/Key/Value
$q_i = W_Q x_i$, $k_i = W_K x_i$, $v_i = W_V x_i$. Q = what i looks for; K = what j offers; V = j's contribution.

### Scaled dot-product attention
$$a_{ij} = \frac{\exp(q_i^\top k_j/\sqrt{d_k})}{\sum_\ell \exp(q_i^\top k_\ell/\sqrt{d_k})}$$
$$\text{Attention}(Q,K,V) = \text{softmax}(QK^\top/\sqrt{d_k})V$$
- $\sqrt{d_k}$ scaling for gradient stability.

### Self-attention vs multi-head
- **Self-attention:** Q,K,V from same input.
- **Multi-head:** h parallel heads each dim d/h; concat then project. Different heads learn different relationships (syntax, coref, semantics).

### Masking
- **Bidirectional** (BERT): attend everywhere.
- **Causal** (GPT): mask future positions (set to −∞ pre-softmax) for left-to-right generation.

### Transformer block
1. Multi-head self-attention. 2. Residual + layer norm. 3. Position-wise FFN. 4. Residual + layer norm.

Stack 12 (BERT base) / 24 (BERT large) / many more. Input = token embeddings + position embeddings (attention is order-blind otherwise).

### BERT pretraining
- **Masked Language Modelling (MLM):** mask 15% of tokens, predict from context. → bidirectional representations.
- **Next-Sentence Prediction (NSP):** binary; mostly dropped in successors.

### Sentence-BERT
BERT's pooled vectors compare poorly. Sentence-BERT fine-tunes with siamese architecture on similarity data → fixed-size sentence vector, cosine-comparable.

Commercial: OpenAI `text-embedding-3-*`, Voyage `voyage-3/4`, Cohere, Google.

### BERTopic pipeline
1. **Embed** with sentence transformer (e.g., MiniLM 384-dim).
2. **Reduce** via UMAP to 5–15 dims.
3. **Cluster** with HDBSCAN.
4. **Describe** with **c-TF-IDF** (class-based TF-IDF): treat each cluster's concatenated docs as one "class document"; distinctive words per cluster.

**Strengths:** better on short text, polysemy-aware (different vectors per occurrence).
**Limits:** c-TF-IDF labels are single words (lossy); HDBSCAN limits; no covariate model → still use STM for hypothesis testing.

### Foundation models
- Scaling laws (Kaplan, Chinchilla): test loss = power law in params, data, compute. Optimal allocation matters.
- **In-context learning:** new task from prompt examples, no gradient updates. Emerges with scale.
- **Few-shot** (with examples) vs **zero-shot** (just description).
- **Chain-of-thought (CoT):** include reasoning steps in examples. Improves multi-step tasks. "Let's think step by step" zero-shot variant. **Self-consistency** = majority vote over sampled CoTs.
- LLM CoT trace ≠ faithful explanation; improves accuracy not interpretability.
- **Reasoning deficit:** weak at arithmetic, formal logic. Remedies: CoT, tool use (calculator/Python), training on reasoning corpora.
- **Agents:** LLM + tool calls (search, code execution, DB).

### Reproducibility for LLMs
Pin model **version**, **temperature** (=0 for classification), random seed. APIs drift between months.

---

## Ch 12. Autoencoders, VAEs, AAEs

### Plain autoencoder
- Encoder $f_\phi: \mathbb{R}^D \to \mathbb{R}^L$ ($L\ll D$). Decoder $g_\theta: \mathbb{R}^L \to \mathbb{R}^D$.
- **Reconstruction loss:** $\mathcal{L}_{\text{rec}} = \frac{1}{N}\sum_n \|x_n - g_\theta(f_\phi(x_n))\|^2$.
- Binary inputs → per-pixel BCE.
- Bottleneck L = hyperparameter (too small → poor recon; too large → trivial copy).

### Linear AE = PCA
Linear encoder + decoder + MSE → optimum spans same L-dim subspace as top-L PCs. Axes may differ (any basis of subspace). **All gains over PCA come from non-linear activations.**

### Regularized variants
- **Denoising AE:** corrupt input, reconstruct clean. → robust representation.
- **Sparse AE:** $\ell_1$ penalty on bottleneck activations. Different inputs activate different units.
- **Contractive AE:** penalize Frobenius norm of encoder Jacobian. Local invariance.

### Variational Autoencoder (VAE)
Generative model:
$$z_n \sim N(0, I_L), \quad x_n | z_n \sim p_\theta(x|z_n)$$

Decoder $p_\theta(x|z)$ usually Gaussian (continuous) or Bernoulli (binary).

**Marginal likelihood intractable** → variational approximation.

### Amortized inference
Encoder outputs Gaussian over latent:
$$q_\phi(z|x_n) = N(z; \mu_\phi(x_n), \Sigma_\phi(x_n))$$
$\Sigma$ usually diagonal. **Amortized:** single $\phi$ defines posterior approx for every input.

### ELBO
$$\mathcal{L}(\theta,\phi;x_n) = \underbrace{E_{q_\phi(z|x_n)}[\log p_\theta(x_n|z)]}_{\text{reconstruction}} - \underbrace{D_{KL}(q_\phi(z|x_n)\|p(z))}_{\text{regularization}}$$
Lower bound on $\log p_\theta(x_n)$; tight when $q_\phi = p_\theta(z|x)$.

Two forces: reconstruction wants $q$ to encode info; KL wants $q$ ≈ prior.

### Reparameterization trick
Cannot backprop through sampling. Rewrite:
$$z = \mu_\phi(x) + \sigma_\phi(x) \odot \varepsilon, \quad \varepsilon \sim N(0,I)$$
Randomness in $\varepsilon$ (no params); gradient flows through $\mu,\sigma$.

### KL closed form (Gaussian q, standard normal prior)
$$D_{KL} = -\frac{1}{2}\sum_{j=1}^L (1 + \log \sigma_{\phi,j}^2 - \mu_{\phi,j}^2 - \sigma_{\phi,j}^2)$$

### Three distributions in a VAE
1. Encoder's $q_\phi(z|x)$ over latent.
2. Decoder's $p_\theta(x|z)$ over input.
3. Prior $p(z)$ on latent.

### VAE vs plain AE
VAE adds: probabilistic embedding (variance per input), generative model (sample z from prior → decode), well-conditioned latent space (KL keeps it Gaussian-like).

### VAE vs Probabilistic PCA
PPCA = VAE with linear encoder/decoder and isotropic noise. Closed-form MLE. Replace linear with NN → VAE expressiveness; no closed-form, train via ELBO.

### Adversarial Autoencoder (AAE)
Replace KL with discriminator network that distinguishes encoder samples from prior samples; encoder trained to fool discriminator (minimax). **Benefit:** any prior with samples (non-Gaussian, multimodal, structured discrete).

### Semi-supervised AE/VAE
Append categorical latent (class label). Small labelled + large unlabelled → disentangle class from style.

---

## Through-line — the family

| Method | Lineage |
|---|---|
| PCA | covariance eigendecomp |
| Linear AE | = PCA in NN clothes |
| PPCA | PCA + Gaussian latent model |
| VAE | PPCA with non-linear decoder |
| Classical MDS | PCA in the dual (Gram) |
| Factor analysis | PPCA + separate unique variance |
| IRT | Factor model for binary indicators |
| LCA | Factor model with discrete latent |
| LDA | Mixture model for documents |
| BERTopic | LDA architecture with contextual embeddings |
| k-means | GMM with isotropic noise, hardened r |
| GMM | soft k-means with covariance |
| Spectral clustering | LE eigenvectors → k-means |
| Laplacian Eigenmaps | same eigenvectors as embedding |
| Matrix-factorization recsys | low-rank approx of sparse matrix |
| Spatial voting | MF on legislator-bill matrix |

**One picture:** every method = low-dim latent structure + variation around it. They differ in what's low-dim, what's structure, what's variation.

---

## Quick-reference: key formulas

| Concept | Formula |
|---|---|
| Reliability | $\rho = \mathrm{Var}(T)/\mathrm{Var}(X)$ |
| Cronbach α | $\frac{k}{k-1}(1 - \sum\sigma_i^2/\sigma_T^2)$ |
| 2PL IRT | $P = 1/(1+e^{-a(\theta-b)})$ |
| MF rating | $\hat R_{ij} = \mu+b_i+b_j+p_i^\top q_j$ |
| Geodesic Gram | $K_G = -\tfrac{1}{2}C_N D_G^{(2)} C_N$ |
| t-SNE q | $q_{ij}\propto (1+\|z_i-z_j\|^2)^{-1}$ |
| WCSS | $\sum_k\sum_{n\in C_k}\|x_n-\mu_k\|^2$ |
| Silhouette | $(b-a)/\max(a,b)$ |
| Mreach dist | $\max(d_{\text{core}}(p), d_{\text{core}}(q), d(p,q))$ |
| Norm Laplacian | $L_{\text{sym}}=I-D^{-1/2}WD^{-1/2}$ |
| GMM responsibility | $\pi_k\mathcal{N}(x|\mu_k,\Sigma_k)/\sum_j\pi_j\mathcal{N}(\cdot)$ |
| TF-IDF | $\text{tf}\cdot\log(D/df)$ |
| SGNS implicit | $VU^\top\approx\mathrm{PMI}-\log k$ |
| LDA Gibbs | $\propto(n_{d,k}+\alpha)\cdot\frac{n_{k,w}+\eta}{n_{k,\cdot}+V\eta}$ |
| Attention | $\text{softmax}(QK^\top/\sqrt{d_k})V$ |
| ELBO | $E_q[\log p(x\|z)] - D_{KL}(q\|p)$ |
| Reparam | $z=\mu+\sigma\odot\varepsilon$ |
| KL Gaussian | $-\tfrac{1}{2}\sum(1+\log\sigma_j^2-\mu_j^2-\sigma_j^2)$ |

---

## Exam-day decision rules

| Task | Default tool |
|---|---|
| Reduce dim, linear | PCA |
| Reduce dim, non-linear, viz | UMAP |
| OOS embedding | KPCA or UMAP (saved) |
| Verify isometry | Isomap |
| Find intrinsic dim | MVU eigenvalue gap |
| Convex clusters, scale ok | k-means (with `nstart`, scaling) |
| Non-convex, single density | DBSCAN |
| Non-convex, variable density | HDBSCAN |
| Graph data, K known | Spectral |
| Continuous + uncertainty | GMM (mclust BIC) |
| Categorical responses | LCA (poLCA) |
| Topics in long docs | STM (with covariates) |
| Topics in short text | BTM or BERTopic |
| Semantic similarity | sentence-BERT cosine |
| Generative low-dim | VAE |

Good luck on the exam.
