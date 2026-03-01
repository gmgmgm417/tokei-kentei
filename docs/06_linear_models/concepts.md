# 線形モデル：重要概念・公式

## 一元配置分散分析（One-way ANOVA）

!!! abstract "モデル"
    $$Y_{ij} = \mu + \alpha_i + \varepsilon_{ij}, \quad \varepsilon_{ij} \overset{i.i.d.}{\sim} N(0, \sigma^2)$$

    $i = 1, \ldots, a$（水準数）、$j = 1, \ldots, n_i$（繰り返し数）

    制約条件: $\sum_{i=1}^a \alpha_i = 0$ または $\alpha_1 = 0$

!!! abstract "平方和の分解"
    $$SS_T = SS_A + SS_E$$

    - $SS_T = \sum_{i,j}(Y_{ij} - \bar{Y})^2$（総平方和）
    - $SS_A = \sum_i n_i(\bar{Y}_{i\cdot} - \bar{Y})^2$（群間平方和）
    - $SS_E = \sum_{i,j}(Y_{ij} - \bar{Y}_{i\cdot})^2$（群内平方和）

### ANOVA表

| 変動要因 | 平方和 | 自由度 | 平均平方 | $F$ 値 |
|---|---|---|---|---|
| 群間（処理） | $SS_A$ | $a-1$ | $MS_A = SS_A/(a-1)$ | $F = MS_A/MS_E$ |
| 群内（誤差） | $SS_E$ | $N-a$ | $MS_E = SS_E/(N-a)$ | |
| 全体 | $SS_T$ | $N-1$ | | |

$F \sim F(a-1, N-a)$ のもとで帰無仮説 $H_0: \alpha_1 = \cdots = \alpha_a = 0$ を検定。

!!! warning "試験での注意点"
    自由度の計算が頻出。群間の自由度 = $a-1$、群内の自由度 = $N-a$（$N$ は総データ数）

---

## 二元配置分散分析

!!! abstract "交互作用なしモデル"
    $$Y_{ij} = \mu + \alpha_i + \beta_j + \varepsilon_{ij}$$

    $i = 1, \ldots, a$、$j = 1, \ldots, b$

!!! abstract "交互作用ありモデル"
    $$Y_{ijk} = \mu + \alpha_i + \beta_j + (\alpha\beta)_{ij} + \varepsilon_{ijk}$$

### ANOVA表（交互作用あり）

| 変動要因 | 平方和 | 自由度 |
|---|---|---|
| 因子A | $SS_A$ | $a-1$ |
| 因子B | $SS_B$ | $b-1$ |
| 交互作用AB | $SS_{AB}$ | $(a-1)(b-1)$ |
| 誤差 | $SS_E$ | $ab(n-1)$ |
| 全体 | $SS_T$ | $abn-1$ |

!!! warning "交互作用の解釈"
    交互作用が有意 → 因子Aの効果が因子Bの水準によって異なる。
    交互作用が有意な場合、主効果の解釈は注意が必要。

---

## 多重比較

!!! abstract "多重比較の必要性"
    ANOVA で有意差があった後、どの群間に差があるかを検定。
    複数の検定を行うと第1種の過誤率が膨らむ（多重性の問題）。

| 方法 | 特徴 |
|---|---|
| ボンフェローニ法 | 有意水準を比較回数で割る。保守的 |
| テューキー法 | 全対比較向き。均衡データ向き |
| ダネット法 | コントロール群との比較向き |
| シェフェ法 | 任意の対比検定に使える。保守的 |
