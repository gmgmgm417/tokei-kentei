# 公式チートシート

試験直前の最終確認用。全分野の重要公式を一覧にまとめています。

---

## 確率論

| 公式 | 式 |
|---|---|
| ベイズの定理 | $P(B_i\|A) = \frac{P(A\|B_i)P(B_i)}{\sum_j P(A\|B_j)P(B_j)}$ |
| 期待値と二乗 | $E[X^2] = \text{Var}(X) + (E[X])^2$ |
| 共分散 | $\text{Cov}(X,Y) = E[XY] - E[X]E[Y]$ |
| チェビシェフ | $P(\|X-\mu\| \geq k\sigma) \leq 1/k^2$ |
| MGF（正規） | $M_X(t) = \exp(\mu t + \sigma^2 t^2/2)$ |

---

## 主要分布のパラメータ

| 分布 | 平均 | 分散 | MGF |
|---|---|---|---|
| $N(\mu, \sigma^2)$ | $\mu$ | $\sigma^2$ | $e^{\mu t + \sigma^2 t^2/2}$ |
| $B(n,p)$ | $np$ | $np(1-p)$ | $(1-p+pe^t)^n$ |
| $Po(\lambda)$ | $\lambda$ | $\lambda$ | $e^{\lambda(e^t-1)}$ |
| $Exp(\lambda)$ | $1/\lambda$ | $1/\lambda^2$ | $\lambda/(\lambda-t)$ |
| $\chi^2(n)$ | $n$ | $2n$ | $(1-2t)^{-n/2}$ |
| $t(n)$ | $0$ ($n>1$) | $n/(n-2)$ ($n>2$) | — |

---

## 統計的推測

| 公式 | 式 |
|---|---|
| 標本平均の分布 | $\bar{X} \sim N(\mu, \sigma^2/n)$ |
| $t$ 統計量 | $T = \frac{\bar{X}-\mu}{S/\sqrt{n}} \sim t(n-1)$ |
| $\chi^2$ 統計量 | $\frac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$ |
| 不偏分散 | $S^2 = \frac{1}{n-1}\sum(X_i-\bar{X})^2$ |
| CR下界 | $\text{Var}(\hat{\theta}) \geq 1/(nI(\theta))$ |
| フィッシャー情報量 | $I(\theta) = -E[\partial^2 \log f/\partial\theta^2]$ |

---

## 回帰分析

| 公式 | 式 |
|---|---|
| OLS推定量 | $\hat{\boldsymbol{\beta}} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}$ |
| 単回帰傾き | $\hat{\beta}_1 = S_{xy}/S_{xx}$ |
| 決定係数 | $R^2 = 1 - SS_E/SS_T$ |
| 調整済み $R^2$ | $\bar{R}^2 = 1-(1-R^2)(n-1)/(n-p-1)$ |
| VIF | $\text{VIF}_j = 1/(1-R_j^2)$ |
| ロジット | $\log\frac{p}{1-p} = \mathbf{x}^\top\boldsymbol{\beta}$ |
| オッズ比 | $e^{\hat{\beta}_j}$ |

---

## 分散分析（ANOVA）

| 要因 | 平方和 | 自由度 | $F$ 値 |
|---|---|---|---|
| 一元配置：群間 | $SS_A$ | $a-1$ | $MS_A/MS_E$ |
| 一元配置：群内 | $SS_E$ | $N-a$ | |
| 二元配置：$A$ | $SS_A$ | $a-1$ | $MS_A/MS_E$ |
| 二元配置：$B$ | $SS_B$ | $b-1$ | $MS_B/MS_E$ |
| 二元配置：$AB$ | $SS_{AB}$ | $(a-1)(b-1)$ | $MS_{AB}/MS_E$ |

---

## ベイズ統計・共役分布

| 尤度 | 事前 | 事後 | 事後期待値 |
|---|---|---|---|
| $B(n,\theta)$ | $Be(\alpha,\beta)$ | $Be(\alpha+x, \beta+n-x)$ | $(\alpha+x)/(\alpha+\beta+n)$ |
| $Po(\lambda)$ | $Ga(\alpha,\beta)$ | $Ga(\alpha+\sum x_i, \beta+n)$ | $(\alpha+\sum x_i)/(\beta+n)$ |
| $N(\mu,\sigma^2)$ | $N(\mu_0,\tau^2)$ | $N(\mu_n, \sigma_n^2)$ | $\mu_n$ |

---

## 時系列

| モデル | ACF | PACF |
|---|---|---|
| AR($p$) | 指数減衰・振動 | ラグ $p$ 以降ゼロ |
| MA($q$) | ラグ $q$ 以降ゼロ | 指数減衰・振動 |
| ARMA($p$,$q$) | 指数減衰・振動 | 指数減衰・振動 |

AR(1)の定常条件: $|\phi_1| < 1$

AR(1)の分散: $\text{Var}(X_t) = \sigma^2/(1-\phi_1^2)$

---

## 多変量解析

| 公式 | 式 |
|---|---|
| 主成分の分散 | $\text{Var}(Z_j) = \lambda_j$（$\lambda_j$: 固有値） |
| 累積寄与率 | $\sum_{j=1}^k \lambda_j / \sum_{j=1}^p \lambda_j$ |
| マハラノビス距離 | $D^2 = (\mathbf{x}-\boldsymbol{\mu})^\top\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})$ |
| LDA判別関数 | $D(\mathbf{x}) = (\boldsymbol{\mu}_1-\boldsymbol{\mu}_2)^\top\boldsymbol{\Sigma}^{-1}\mathbf{x}$ |
