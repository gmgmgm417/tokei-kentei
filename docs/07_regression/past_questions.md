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
