# 統計的推測：重要概念・公式

## 点推定

### 推定量の性質

!!! abstract "不偏性"
    推定量 $\hat{\theta}$ が不偏推定量 $\Leftrightarrow$ $E[\hat{\theta}] = \theta$

    - 標本平均 $\bar{X}$ は $\mu$ の不偏推定量
    - 標本分散 $S^2 = \frac{1}{n-1}\sum(X_i - \bar{X})^2$ は $\sigma^2$ の不偏推定量
    - $\frac{1}{n}\sum(X_i - \bar{X})^2$ は**不偏ではない**（注意！）

!!! abstract "一致性"
    推定量 $\hat{\theta}_n$ が一致推定量 $\Leftrightarrow$ $\hat{\theta}_n \xrightarrow{P} \theta$ ($n \to \infty$)

!!! abstract "有効性（効率性）"
    不偏推定量の中で分散が最小のものを UMVUE（一様最小分散不偏推定量）という。

!!! warning "試験での注意点"
    不偏性と有効性は別の概念。不偏でも分散が大きければ有効ではない。
    $n-1$ か $n$ で割るかで不偏性が変わる。

---

## 最尤推定（MLE）

!!! abstract "最尤推定の定義"
    対数尤度関数 $\ell(\theta) = \log L(\theta) = \sum_{i=1}^n \log f(x_i; \theta)$ を最大化する $\hat{\theta}$ を最尤推定量という。

    **尤度方程式**:

    $$\frac{\partial \ell(\theta)}{\partial \theta} = 0$$

!!! example "正規分布のMLE"
    $X_1, \ldots, X_n \overset{i.i.d.}{\sim} N(\mu, \sigma^2)$ のとき：
    $$\hat{\mu}_{MLE} = \bar{X}, \quad \hat{\sigma}^2_{MLE} = \frac{1}{n}\sum_{i=1}^n (X_i - \bar{X})^2$$

    注意: $\hat{\sigma}^2_{MLE}$ は**不偏ではない**（不偏推定量は $S^2 = \frac{1}{n-1}\sum(X_i - \bar{X})^2$）

!!! info "MLEの漸近性質"
    正則な条件下で、MLEは漸近的に正規分布に従う：
    $$\sqrt{n}(\hat{\theta}_{MLE} - \theta) \xrightarrow{d} N\!\left(0, \frac{1}{I(\theta)}\right)$$
    ここで $I(\theta)$ はフィッシャー情報量。

---

## クラメール-ラオの下界

!!! abstract "フィッシャー情報量"
    $$I(\theta) = E\!\left[\left(\frac{\partial \log f(X;\theta)}{\partial \theta}\right)^2\right] = -E\!\left[\frac{\partial^2 \log f(X;\theta)}{\partial \theta^2}\right]$$

!!! abstract "クラメール-ラオの不等式"
    不偏推定量 $\hat{\theta}$ の分散について：
    $$\text{Var}(\hat{\theta}) \geq \frac{1}{nI(\theta)}$$

!!! tip "UMVUE の判定"
    クラメール-ラオ下界を達成する不偏推定量が存在すれば、それが UMVUE。

---

## 区間推定

!!! abstract "信頼区間の定義"
    $1-\alpha$ 信頼区間: $P(\hat{\theta}_L \leq \theta \leq \hat{\theta}_U) = 1 - \alpha$

    **重要**: 「$\theta$ が信頼区間内に入る確率」ではなく、「この手続きで作った区間が $\theta$ を含む確率が $1-\alpha$」

### 正規分布の区間推定

| 場合 | 検定統計量 | $\mu$ の $1-\alpha$ 信頼区間 |
|---|---|---|
| $\sigma^2$ 既知 | $Z = \frac{\bar{X}-\mu}{\sigma/\sqrt{n}} \sim N(0,1)$ | $\bar{X} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}$ |
| $\sigma^2$ 未知 | $T = \frac{\bar{X}-\mu}{S/\sqrt{n}} \sim t(n-1)$ | $\bar{X} \pm t_{\alpha/2}(n-1) \cdot \frac{S}{\sqrt{n}}$ |

---

## 仮説検定

!!! abstract "検定の枠組み"
    - **帰無仮説** $H_0$: 棄却したい仮説
    - **対立仮説** $H_1$: 採択したい仮説
    - **有意水準** $\alpha$: 第1種の過誤の確率の上限

!!! abstract "誤りの種類"
    | | $H_0$ が真 | $H_1$ が真 |
    |---|---|---|
    | $H_0$ を採択 | 正しい | **第2種の過誤**（$\beta$） |
    | $H_0$ を棄却 | **第1種の過誤**（$\alpha$） | 正しい |

    - **検出力** $= 1 - \beta = P(\text{棄却} \mid H_1)$

!!! warning "試験での注意点"
    「有意でない = $H_0$ が正しい」ではない。$H_0$ の棄却に失敗しただけ。
    $p$ 値は「$H_0$ のもとでこれ以上極端な結果が得られる確率」。

### ネイマン-ピアソンの補題

!!! abstract "最強力検定"
    単純仮説 $H_0: \theta = \theta_0$ vs $H_1: \theta = \theta_1$ のとき、
    尤度比検定が最強力検定（UMP）である：
    $$\text{棄却域} = \left\{x : \frac{L(\theta_1; x)}{L(\theta_0; x)} > k\right\}$$

### 主要な検定

| 検定 | 帰無仮説 | 検定統計量 | 分布 |
|---|---|---|---|
| 一標本 $t$ 検定 | $\mu = \mu_0$ | $T = \frac{\bar{X}-\mu_0}{S/\sqrt{n}}$ | $t(n-1)$ |
| 二標本 $t$ 検定（等分散） | $\mu_1 = \mu_2$ | $T = \frac{\bar{X}_1-\bar{X}_2}{S_p\sqrt{1/n_1+1/n_2}}$ | $t(n_1+n_2-2)$ |
| $\chi^2$ 検定（分散） | $\sigma^2 = \sigma_0^2$ | $\chi^2 = \frac{(n-1)S^2}{\sigma_0^2}$ | $\chi^2(n-1)$ |
| $F$ 検定（等分散） | $\sigma_1^2 = \sigma_2^2$ | $F = S_1^2/S_2^2$ | $F(n_1-1, n_2-1)$ |
