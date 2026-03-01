# 確率論：重要概念・公式

## 確率の公理（コルモゴロフの公理）

!!! abstract "定義"
    確率 $P$ は以下の3つの公理を満たす：

    1. **非負性**: $P(A) \geq 0$
    2. **規格化**: $P(\Omega) = 1$
    3. **加法性**: $A \cap B = \emptyset$ のとき $P(A \cup B) = P(A) + P(B)$

!!! info "導出される重要公式"
    - $P(\emptyset) = 0$
    - $P(A^c) = 1 - P(A)$
    - $P(A \cup B) = P(A) + P(B) - P(A \cap B)$（加法定理）

---

## 条件付き確率とベイズの定理

!!! abstract "条件付き確率の定義"
    $$P(A \mid B) = \frac{P(A \cap B)}{P(B)}, \quad P(B) > 0$$

!!! abstract "全確率の定理"
    $\{B_1, B_2, \ldots, B_n\}$ が $\Omega$ の分割のとき：
    $$P(A) = \sum_{i=1}^{n} P(A \mid B_i) P(B_i)$$

!!! abstract "ベイズの定理"
    $$P(B_i \mid A) = \frac{P(A \mid B_i) P(B_i)}{\sum_{j=1}^{n} P(A \mid B_j) P(B_j)}$$

!!! warning "試験での注意点"
    ベイズの定理では分母が「全確率の定理」になっていることを確認する。
    「事前確率」と「尤度」を混同しないこと。

---

## 確率変数・期待値・分散

!!! abstract "期待値"
    - 離散型: $E[X] = \sum_x x \cdot P(X=x)$
    - 連続型: $E[X] = \int_{-\infty}^{\infty} x f(x) \, dx$

!!! abstract "分散"
    $$\text{Var}(X) = E[(X - \mu)^2] = E[X^2] - (E[X])^2$$

!!! info "線形性と変換公式"
    - $E[aX + b] = aE[X] + b$
    - $\text{Var}(aX + b) = a^2 \text{Var}(X)$
    - $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) + 2\text{Cov}(X, Y)$

!!! info "共分散と相関係数"
    $$\text{Cov}(X, Y) = E[XY] - E[X]E[Y]$$
    $$\rho(X, Y) = \frac{\text{Cov}(X, Y)}{\sqrt{\text{Var}(X) \cdot \text{Var}(Y)}}$$

---

## 主要分布族

### 離散分布

| 分布 | パラメータ | 期待値 | 分散 |
|---|---|---|---|
| 二項分布 $B(n, p)$ | $n, p$ | $np$ | $np(1-p)$ |
| ポアソン分布 $Po(\lambda)$ | $\lambda > 0$ | $\lambda$ | $\lambda$ |
| 幾何分布 $Ge(p)$ | $0 < p \leq 1$ | $1/p$ | $(1-p)/p^2$ |
| 負の二項分布 | $r, p$ | $r(1-p)/p$ | $r(1-p)/p^2$ |
| 超幾何分布 | $N, K, n$ | $nK/N$ | $n\frac{K}{N}\frac{N-K}{N}\frac{N-n}{N-1}$ |

### 連続分布

| 分布 | パラメータ | 期待値 | 分散 |
|---|---|---|---|
| 正規分布 $N(\mu, \sigma^2)$ | $\mu, \sigma^2$ | $\mu$ | $\sigma^2$ |
| 一様分布 $U(a, b)$ | $a < b$ | $(a+b)/2$ | $(b-a)^2/12$ |
| 指数分布 $Exp(\lambda)$ | $\lambda > 0$ | $1/\lambda$ | $1/\lambda^2$ |
| ガンマ分布 $Ga(\alpha, \beta)$ | $\alpha, \beta > 0$ | $\alpha/\beta$ | $\alpha/\beta^2$ |
| ベータ分布 $Be(\alpha, \beta)$ | $\alpha, \beta > 0$ | $\alpha/(\alpha+\beta)$ | $\frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$ |
| カイ二乗分布 $\chi^2(n)$ | $n > 0$ | $n$ | $2n$ |
| $t$ 分布 $t(n)$ | $n > 0$ | $0$ ($n > 1$) | $n/(n-2)$ ($n > 2$) |
| $F$ 分布 $F(m, n)$ | $m, n > 0$ | $n/(n-2)$ ($n > 2$) | — |

---

## 重要な分布の関係

!!! info "分布間の関係"
    - $X_1, \ldots, X_n \overset{i.i.d.}{\sim} N(0,1)$ のとき:
        - $\sum X_i^2 \sim \chi^2(n)$
        - $\frac{X_1}{\sqrt{\chi^2(n)/n}} \sim t(n)$
        - $\frac{\chi^2(m)/m}{\chi^2(n)/n} \sim F(m, n)$
    - $t^2(n) \sim F(1, n)$
    - $\chi^2(n) = Ga(n/2, 1/2)$（ガンマ分布の特殊形）

!!! warning "試験での注意点"
    $F$ 分布の自由度の順番（分子・分母）を必ず確認する。
    $F(m,n)$ と $F(n,m)$ は逆数の関係：$F_{1-\alpha}(m,n) = 1/F_{\alpha}(n,m)$

---

## モーメント母関数（積率母関数）

!!! abstract "定義"
    $$M_X(t) = E[e^{tX}]$$

!!! info "重要な性質"
    - $E[X^k] = M_X^{(k)}(0)$ （$k$ 次モーメント）
    - 独立な $X, Y$ のとき: $M_{X+Y}(t) = M_X(t) \cdot M_Y(t)$
    - $M_X(t)$ が一致すれば分布が一致（一意性）

!!! example "主要分布のMGF"
    | 分布 | $M_X(t)$ |
    |---|---|
    | $N(\mu, \sigma^2)$ | $\exp\!\left(\mu t + \frac{\sigma^2 t^2}{2}\right)$ |
    | $Po(\lambda)$ | $\exp(\lambda(e^t - 1))$ |
    | $B(n,p)$ | $(1 - p + pe^t)^n$ |
    | $Exp(\lambda)$ | $\frac{\lambda}{\lambda - t}$ ($t < \lambda$) |
    | $Ga(\alpha, \beta)$ | $\left(\frac{\beta}{\beta - t}\right)^\alpha$ ($t < \beta$) |

---

## 大数の法則・中心極限定理

!!! abstract "大数の弱法則（WLLN）"
    $X_1, X_2, \ldots$ が $i.i.d.$、$E[X_i] = \mu$、$\text{Var}(X_i) < \infty$ のとき：
    $$\bar{X}_n \xrightarrow{P} \mu \quad (n \to \infty)$$

!!! abstract "中心極限定理（CLT）"
    $X_1, X_2, \ldots$ が $i.i.d.$、$E[X_i] = \mu$、$\text{Var}(X_i) = \sigma^2 < \infty$ のとき：
    $$\frac{\sqrt{n}(\bar{X}_n - \mu)}{\sigma} \xrightarrow{d} N(0, 1)$$

!!! warning "試験での注意点"
    CLTは正規分布でなくても適用できる。
    「標本平均の分布」が正規に近似されるのが CLT の主張。

---

## 確率不等式

!!! abstract "マルコフの不等式"
    $X \geq 0$、$a > 0$ のとき：
    $$P(X \geq a) \leq \frac{E[X]}{a}$$

!!! abstract "チェビシェフの不等式"
    $k > 0$ のとき：
    $$P(|X - \mu| \geq k\sigma) \leq \frac{1}{k^2}$$

!!! tip "試験での活用"
    確率の上界を求める問題でよく登場する。
    チェビシェフは「平均から $k$ 標準偏差以上離れる確率」の上界。
