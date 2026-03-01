# ベイズ統計：重要概念・公式

## ベイズの定理と基本枠組み

!!! abstract "ベイズ更新"
    $$\underbrace{p(\theta \mid x)}_{\text{事後分布}} \propto \underbrace{p(x \mid \theta)}_{\text{尤度}} \times \underbrace{p(\theta)}_{\text{事前分布}}$$

!!! info "頻度論との比較"
    | | 頻度論 | ベイズ |
    |---|---|---|
    | パラメータ | 固定した未知定数 | 確率変数 |
    | 不確実性 | 反復試行の頻度 | 信念の度合い |
    | 区間推定 | 信頼区間（手続きの保証） | 信用区間（事後確率の保証） |

---

## 共役事前分布

!!! abstract "共役性の定義"
    事後分布が事前分布と同じ分布族に属するとき、その事前分布を**共役事前分布**という。

### 主要な共役ペア

| 尤度 | 共役事前分布 | 事後分布 |
|---|---|---|
| $B(n, \theta)$ | $Be(\alpha, \beta)$ | $Be(\alpha + x, \beta + n - x)$ |
| $Po(\lambda)$ | $Ga(\alpha, \beta)$ | $Ga(\alpha + \sum x_i, \beta + n)$ |
| $N(\mu, \sigma^2)$（$\sigma^2$既知） | $N(\mu_0, \tau^2)$ | $N\!\left(\frac{\frac{\mu_0}{\tau^2}+\frac{n\bar{x}}{\sigma^2}}{\frac{1}{\tau^2}+\frac{n}{\sigma^2}}, \frac{1}{\frac{1}{\tau^2}+\frac{n}{\sigma^2}}\right)$ |
| $Exp(\lambda)$ | $Ga(\alpha, \beta)$ | $Ga(\alpha + n, \beta + \sum x_i)$ |

!!! example "ベータ-二項モデルの例"
    コインの表の確率 $\theta$ を推定。$Be(1,1)$（一様）を事前分布として、$n=10$ 回中 $x=7$ 回表が出たとき：
    $$\theta \mid x \sim Be(1+7, 1+3) = Be(8, 4)$$
    事後期待値: $\frac{8}{8+4} = \frac{2}{3}$（MLE の $7/10 = 0.7$ に近似）

---

## ベイズ推定量

!!! abstract "事後期待値（EAP推定）"
    $$\hat{\theta}_{Bayes} = E[\theta \mid x]$$

    二乗損失関数のもとでの最適推定量。

!!! abstract "MAP推定（事後最頻値）"
    事後分布を最大化するパラメータ：
    $$\hat{\theta}_{MAP} = \arg\max_\theta p(\theta \mid x)$$

!!! warning "頻度論のMLE vs ベイズのMAP"
    - MAP推定は事前分布が一様分布のとき MLE と一致
    - 事前分布が正規分布のときのMAP推定 = リッジ回帰（L2正則化）に対応

---

## 信用区間（信用可能区間）

!!! abstract "定義"
    事後分布のもとで $\theta$ が区間内に入る確率が $1-\alpha$ である区間：
    $$P(\theta \in [a, b] \mid x) = 1 - \alpha$$

!!! warning "信頼区間との違い"
    - **信頼区間**: 「この手続きで 95% の割合で $\theta$ を含む区間を作れる」
    - **信用区間**: 「$\theta$ がこの区間内にある確率が 95%」（より直感的）
