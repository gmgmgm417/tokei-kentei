# 統計的推測：過去問

!!! note "利用方法"
    問題を読んで解答を考えてから、「解答・解説を見る」をタップしてください。

---

## 問題 I1-001 (基礎) ：最尤推定

> **出典**: 統計検定準1級 類題

$X_1, \ldots, X_n \overset{i.i.d.}{\sim} Po(\lambda)$ のとき、$\lambda$ の最尤推定量を求めよ。

??? success "解答・解説を見る"

    **正解**: $\hat{\lambda}_{MLE} = \bar{X}$

    ### 計算過程

    ポアソン分布の確率関数: $P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}$

    尤度関数:
    $$L(\lambda) = \prod_{i=1}^n \frac{\lambda^{x_i} e^{-\lambda}}{x_i!}$$

    対数尤度:
    $$\ell(\lambda) = \sum_{i=1}^n x_i \log\lambda - n\lambda - \sum_{i=1}^n \log(x_i!)$$

    尤度方程式:
    $$\frac{d\ell}{d\lambda} = \frac{\sum x_i}{\lambda} - n = 0$$

    $$\hat{\lambda}_{MLE} = \frac{\sum x_i}{n} = \bar{X}$$

    !!! tip "試験対策"
        ポアソン分布の MLE は標本平均。これはモーメント推定量とも一致する。
        2階微分 $d^2\ell/d\lambda^2 = -\sum x_i/\lambda^2 < 0$ なので最大点であることを確認。

---

## 問題 I1-002 (応用) ：不偏推定量

> **出典**: 統計検定準1級 類題

$X_1, \ldots, X_n \overset{i.i.d.}{\sim} Exp(\lambda)$ のとき、$1/\lambda$ の不偏推定量を求めよ。また、その推定量の分散を求めよ。

??? success "解答・解説を見る"

    **正解**: $\bar{X} = \frac{1}{n}\sum X_i$（不偏）、分散 $= \frac{1}{n\lambda^2}$

    ### 計算過程

    指数分布 $Exp(\lambda)$ の期待値: $E[X] = 1/\lambda$

    よって $E[\bar{X}] = 1/\lambda$（不偏）

    $\text{Var}(X) = 1/\lambda^2$ より:
    $$\text{Var}(\bar{X}) = \frac{\text{Var}(X)}{n} = \frac{1}{n\lambda^2}$$

    !!! tip "クラメール-ラオ下界との比較"
        指数分布のフィッシャー情報量 $I(\lambda) = 1/\lambda^2$

        CR下界: $\frac{1}{nI(\lambda)} \cdot \left(\frac{d(1/\lambda)}{d\lambda}\right)^2 = \frac{\lambda^2}{n} \cdot \frac{1}{\lambda^4} = \frac{1}{n\lambda^2}$

        $\bar{X}$ はCR下界を達成しているので UMVUE。

---

## 問題 I1-003 (基礎) ：区間推定

> **出典**: 統計検定準1級 類題

$n = 25$ の標本から $\bar{X} = 10$、$S = 4$ を得た。$\mu$ の95%信頼区間を求めよ。（$t_{0.025}(24) = 2.064$ を使用）

??? success "解答・解説を見る"

    **正解**: $(10 - 1.6512, \; 10 + 1.6512) = (8.349, \; 11.651)$

    ### 計算過程

    $\sigma^2$ 未知の場合の信頼区間:
    $$\bar{X} \pm t_{\alpha/2}(n-1) \cdot \frac{S}{\sqrt{n}}$$

    $\bar{X} = 10$、$S = 4$、$n = 25$、$t_{0.025}(24) = 2.064$

    $$10 \pm 2.064 \times \frac{4}{\sqrt{25}} = 10 \pm 2.064 \times 0.8 = 10 \pm 1.6512$$

    !!! warning "よくある間違い"
        母分散が未知のとき $z$ 分布ではなく $t$ 分布を使う（$n$ が小さいとき特に重要）。
        自由度は $n-1 = 24$（$n$ ではない）。

---

## 問題 I1-004 (応用) ：指数分布の分散の最尤推定・漸近分散

> **出典**: 統計検定準1級 類題（表現を改変）

$n$ 台の機器の稼働時間 $X_1, \ldots, X_n$ が、互いに独立に平均 $\lambda$ の指数分布に従うとする。確率密度関数は：
$$f(x) = \frac{1}{\lambda}e^{-x/\lambda}, \quad x \geq 0$$

(1) $X_i$ の分散 $\theta = V(X_i)$ を $\lambda$ の関数として表せ。

(2) (1) の分散 $\theta$ の最尤推定量 $\hat{\theta}$ を求めよ。

(3) (2) の最尤推定量の漸近分散 $\displaystyle\lim_{n \to \infty} V\!\left(\sqrt{n}(\hat{\theta} - \theta)\right)$ を $\lambda$ の関数として表せ。

??? success "解答・解説を見る"

    **(1)** $\theta = \lambda^2$

    平均 $\lambda$ の指数分布では $E[X] = \lambda$、$E[X^2] = 2\lambda^2$ なので：
    $$\theta = V(X) = E[X^2] - (E[X])^2 = 2\lambda^2 - \lambda^2 = \lambda^2$$

    ---

    **(2)** $\hat{\theta} = \bar{X}^2$

    まず $\lambda$ の MLE を求める。対数尤度：
    $$\ell(\lambda) = -n\log\lambda - \frac{1}{\lambda}\sum_{i=1}^n x_i$$

    尤度方程式：
    $$\frac{d\ell}{d\lambda} = -\frac{n}{\lambda} + \frac{\sum x_i}{\lambda^2} = 0 \implies \hat{\lambda} = \bar{X}$$

    MLE の不変性より：
    $$\hat{\theta} = \hat{\lambda}^2 = \bar{X}^2$$

    ---

    **(3)** $4\lambda^4$

    フィッシャー情報量を求める：
    $$\frac{\partial^2 \log f}{\partial \lambda^2} = \frac{1}{\lambda^2} - \frac{2x}{\lambda^3}$$

    $$I(\lambda) = -E\!\left[\frac{\partial^2 \log f}{\partial \lambda^2}\right] = -\frac{1}{\lambda^2} + \frac{2\lambda}{\lambda^3} = \frac{1}{\lambda^2}$$

    $\theta = g(\lambda) = \lambda^2$、$g'(\lambda) = 2\lambda$ としてデルタ法を適用：
    $$\lim_{n\to\infty} V\!\left(\sqrt{n}(\hat{\theta}-\theta)\right) = \frac{(g'(\lambda))^2}{I(\lambda)} = \frac{(2\lambda)^2}{1/\lambda^2} = 4\lambda^2 \cdot \lambda^2 = \mathbf{4\lambda^4}$$

    !!! tip "デルタ法の公式"
        $\sqrt{n}(g(\hat{\lambda}) - g(\lambda)) \xrightarrow{d} N\!\left(0, \dfrac{(g'(\lambda))^2}{I(\lambda)}\right)$

    !!! warning "よくある間違い"
        $\hat{\theta} = \bar{X}^2$ は**不偏推定量ではない**（$E[\bar{X}^2] = \lambda^2 + \lambda^2/n \neq \lambda^2$）。
        ただし一致推定量（$n \to \infty$ で真値に収束）ではある。
