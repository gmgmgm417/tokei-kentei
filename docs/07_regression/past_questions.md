# 回帰分析：過去問

## 問題 R1-001 (基礎) ：OLS推定量の性質

> **出典**: 統計検定準1級 類題

単純回帰 $Y_i = \beta_0 + \beta_1 x_i + \varepsilon_i$ のOLS推定量 $\hat{\beta}_1$ を求めよ。

??? success "解答・解説を見る"

    **正解**:

    $$\hat{\beta}_1 = \frac{\sum_{i=1}^n (x_i - \bar{x})(Y_i - \bar{Y})}{\sum_{i=1}^n (x_i - \bar{x})^2} = \frac{S_{xy}}{S_{xx}}$$

    ### 導出

    残差平方和 $Q = \sum(Y_i - \beta_0 - \beta_1 x_i)^2$ を最小化。

    正規方程式:
    $$\frac{\partial Q}{\partial \beta_0} = -2\sum(Y_i - \hat{\beta}_0 - \hat{\beta}_1 x_i) = 0$$

    $$\frac{\partial Q}{\partial \beta_1} = -2\sum x_i(Y_i - \hat{\beta}_0 - \hat{\beta}_1 x_i) = 0$$

    1式目から $\hat{\beta}_0 = \bar{Y} - \hat{\beta}_1\bar{x}$

    2式目に代入して整理すると $\hat{\beta}_1 = S_{xy}/S_{xx}$

    !!! tip "不偏性の確認"
        $E[\hat{\beta}_1] = \beta_1$（不偏推定量であることを示せる）

---

## 問題 R1-002 (応用) ：多重共線性の影響

> **出典**: 統計検定準1級 類題

多重共線性が存在するとき、OLS推定量に生じる問題を説明せよ。

??? success "解答・解説を見る"

    **問題点**:

    1. **推定量の分散が大きくなる**: $\text{Var}(\hat{\beta}_j) = \sigma^2 (\mathbf{X}^\top\mathbf{X})^{-1}_{jj}$ で、共線性が強いと $(\mathbf{X}^\top\mathbf{X})$ の行列式が 0 に近づき逆行列が不安定になる

    2. **係数の解釈が困難**: 各変数の独立した効果を分離できない

    3. **推定値の不安定性**: データの小さな変化で推定値が大きく変動

    ただし、**予測目的のみ**なら多重共線性があっても予測精度への影響は小さい場合がある。

    !!! tip "対処法"
        - VIF を確認し、高い変数を除外
        - リッジ回帰（L2正則化）を使用
        - 主成分回帰（PCAで次元削減後に回帰）

---

## 問題 R1-003 (応用) ：原点通過回帰・尤度比検定

> **出典**: 統計検定準1級 類題（表現を改変）

$n$ 次元確率変数 $\mathbf{Y} = (Y_1, \ldots, Y_n)^\top$ が $E(\mathbf{Y}) = b\mathbf{x}$、$V(\mathbf{Y}) = \sigma^2 I_n$ の線形モデルに従うとする。$\mathbf{x} = (x_1, \ldots, x_n)^\top$ は既知の定数ベクトル（各 $x_i \neq 0$）、$b$ と $\sigma^2 (> 0)$ は未知母数。また $\tilde{\mathbf{x}} = (\bar{x}, \ldots, \bar{x})^\top$（$\bar{x} = \frac{1}{n}\sum x_i$）とする。

$n = 6$、$\mathbf{x} = (1.1,\ 1.2,\ 1.9,\ 2.7,\ 2.8,\ 3.0)^\top$、$\mathbf{y} = (0.1,\ 2.7,\ 3.3,\ 8.0,\ 6.2,\ 7.1)^\top$ のとき、$\mathbf{x}^\top\mathbf{x} = 30.39$、$\mathbf{x}^\top\mathbf{y} = 69.88$、$\mathbf{y}^\top\mathbf{y} = 171.04$ とする。

**(1)** $(\mathbf{y} - b\mathbf{x})^\top(\mathbf{y} - b\mathbf{x})$ を最小にする $b$ の値として最も適切なものを選べ。

① 1.0　　② 1.9　　③ 2.3　　④ 3.6　　⑤ 4.1

**(2)** (1) の最小二乗推定量の実現値を $\hat{b}$ とする。残差平方和 $(\mathbf{y} - \hat{b}\mathbf{x})^\top(\mathbf{y} - \hat{b}\mathbf{x})$ に適切な数をかけて得られる $\sigma^2$ の不偏推定量の実現値として最も適切なものを選べ。

① 1.3　　② 1.8　　③ 2.1　　④ 4.7　　⑤ 6.8

**(3)** $b$ の最小二乗推定量に関する次の (A)(B) の正誤として正しいものを選べ。

**(A)** 最小二乗推定量は不偏性をもつが、他にも不偏性をもつ推定量が存在する。$n$ 次元列ベクトル $\mathbf{c}$ に対して $\mathbf{c}^\top\mathbf{Y}$ という形の推定量を考えると、$\mathbf{c}^\top\mathbf{x} = 1$ のとき、かつそのときに限って、$\mathbf{c}^\top\mathbf{Y}$ は不偏性をもつ。

**(B)** 最小二乗推定量の分散より小さい分散をもつ不偏推定量が存在することはない。

① (A)(B) 両方正しい　　② (A) 正しく (B) 誤り　　③ (B) 正しく (A) 誤り　　④ 両方誤り

**(4)** $H_0: b = 0$ vs $H_1: b \neq 0$ の尤度比検定（正規分布を仮定、有意水準5%）において、尤度比統計量の変形で得られる検定統計量 ア と棄却域の下限 イ の組み合わせとして正しいものを選べ。

① ア: $\dfrac{5\mathbf{x}^\top\mathbf{x}(\hat{b})^2}{(\mathbf{Y}-\hat{b}\mathbf{x})^\top(\mathbf{Y}-\hat{b}\mathbf{x})}$、イ: 6.61

② ア: $\dfrac{5\mathbf{x}^\top\mathbf{x}(\hat{b})^2}{(\mathbf{Y}-\hat{b}\mathbf{x})^\top(\mathbf{Y}-\hat{b}\mathbf{x})}$、イ: 2.02

③ ア: $\dfrac{5(\mathbf{x}-\tilde{\mathbf{x}})^\top(\mathbf{x}-\tilde{\mathbf{x}})(\hat{b})^2}{(\mathbf{Y}-\hat{b}\mathbf{x})^\top(\mathbf{Y}-\hat{b}\mathbf{x})}$、イ: 2.02

④ ア: $\dfrac{6(\mathbf{x}-\tilde{\mathbf{x}})^\top(\mathbf{x}-\tilde{\mathbf{x}})(\hat{b})^2}{(\mathbf{Y}-\hat{b}\mathbf{x})^\top(\mathbf{Y}-\hat{b}\mathbf{x})}$、イ: 6.61

??? success "解答・解説を見る"

    **(1) 正解：③ 2.3**

    ### 最小二乗推定量（原点通過回帰）

    残差平方和を $b$ で微分してゼロとおく：

    $$\frac{d}{db}(\mathbf{y} - b\mathbf{x})^\top(\mathbf{y} - b\mathbf{x}) = -2\mathbf{x}^\top(\mathbf{y} - b\mathbf{x}) = 0$$

    $$\hat{b} = \frac{\mathbf{x}^\top\mathbf{y}}{\mathbf{x}^\top\mathbf{x}} = \frac{69.88}{30.39} \approx 2.30$$

    !!! tip "原点通過回帰の特徴"
        切片なし（原点通過）モデルなので $\hat{b} = x^\top y / x^\top x$（切片ありは $S_{xy}/S_{xx}$）。

    ---

    **(2) 正解：③ 2.1**

    ### 不偏分散推定

    残差平方和 (RSS)：

    $$RSS = \mathbf{y}^\top\mathbf{y} - \frac{(\mathbf{x}^\top\mathbf{y})^2}{\mathbf{x}^\top\mathbf{x}} = 171.04 - \frac{(69.88)^2}{30.39} = 171.04 - 160.69 \approx 10.35$$

    推定パラメータが $b$ のみ（1個）なので残差自由度 $= n - 1 = 5$。

    $$\hat{\sigma}^2 = \frac{RSS}{n-1} = \frac{10.35}{5} \approx 2.07$$

    !!! warning "自由度に注意"
        原点通過回帰は切片がないため、自由度は $n-1$（切片ありは $n-2$）。

    ---

    **(3) 正解：①（A・B 両方正しい）**

    **(A) の検証**：

    $$E[\mathbf{c}^\top\mathbf{Y}] = \mathbf{c}^\top E[\mathbf{Y}] = \mathbf{c}^\top(b\mathbf{x}) = b(\mathbf{c}^\top\mathbf{x})$$

    これが任意の $b$ に対して $b$ に等しいのは $\mathbf{c}^\top\mathbf{x} = 1$ のとき、かつそのときに限る。→ (A) 正しい

    **(B) の検証**（ガウス-マルコフの定理）：

    $\hat{b} = \mathbf{x}^\top\mathbf{Y}/\mathbf{x}^\top\mathbf{x}$ は BLUE（最良線形不偏推定量）。$\text{Var}(\hat{b}) = \sigma^2/\mathbf{x}^\top\mathbf{x}$ はクラメール-ラオ下界に等しく、すべての不偏推定量の中で最小分散を達成する。→ (B) 正しい

    !!! tip "ガウス-マルコフの定理"
        線形モデルで $E(\boldsymbol{\varepsilon})=0$、$V(\boldsymbol{\varepsilon})=\sigma^2 I$ が成立すれば、OLS は BLUE（最良線形不偏推定量）。

    ---

    **(4) 正解：①**

    ### 尤度比統計量の変形

    $\mathbf{Y}$ が6次元正規分布に従うとして対数尤度比を計算すると：

    $$\Lambda = \left(\frac{\mathbf{y}^\top\mathbf{y}}{RSS}\right)^{n/2} = \left(\frac{\mathbf{y}^\top\mathbf{y}}{\mathbf{y}^\top\mathbf{y} - \hat{b}^2\mathbf{x}^\top\mathbf{x}}\right)^{n/2}$$

    $\Lambda$ が大きい ⟺ $\hat{b}^2\mathbf{x}^\top\mathbf{x}/RSS$ が大きい。これに $(n-1) = 5$ を乗じると：

    $$F = \frac{5\mathbf{x}^\top\mathbf{x}(\hat{b})^2}{(\mathbf{Y}-\hat{b}\mathbf{x})^\top(\mathbf{Y}-\hat{b}\mathbf{x})} \sim F(1,\ n-1) = F(1,\ 5) \quad (H_0 \text{下で})$$

    有意水準5% の棄却域：$F \geq F_{0.05}(1, 5) = 6.61$

    !!! tip "尤度比検定とF検定の対応"
        尤度比統計量を変形すると $F$ 統計量（自由度 $(1, n-1)$）になる。$t^2 = F$ の関係から $t(n-1)$ 検定と等価。

    !!! warning "なぜ $\tilde{\mathbf{x}}$ ではなく $\mathbf{x}$ を使うか"
        原点通過モデルでは「切片がゼロ」を検定するのではなく「傾き $b$ がゼロ」を検定するため、$\tilde{\mathbf{x}}$（平均ベクトル）ではなく $\mathbf{x}$ をそのまま使う。
