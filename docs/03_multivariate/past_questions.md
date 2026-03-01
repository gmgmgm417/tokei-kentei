# 多変量解析：過去問

## 問題 M1-001 (応用) ：主成分分析の解釈

> **出典**: 統計検定準1級 類題

相関行列の固有値が $\lambda_1 = 2.4$、$\lambda_2 = 1.8$、$\lambda_3 = 0.5$、$\lambda_4 = 0.3$（$p=4$）のとき、
第2主成分までの累積寄与率を求めよ。

??? success "解答・解説を見る"

    **正解**: 84%

    ### 計算過程

    累積寄与率 $= \frac{\lambda_1 + \lambda_2}{\lambda_1 + \lambda_2 + \lambda_3 + \lambda_4} = \frac{2.4 + 1.8}{2.4 + 1.8 + 0.5 + 0.3} = \frac{4.2}{5.0} = 0.84 = 84\%$

    !!! tip "試験対策"
        相関行列を使った PCA では固有値の合計 $= p$（変数の数）になる。
        第1主成分だけで $\lambda_1/p = 2.4/4 = 60\%$ の寄与率。

---

## 問題 M1-002 (基礎) ：PCAの性質

> **出典**: 統計検定準1級 類題

主成分分析について正しいものを選べ。

1. 主成分間は互いに無相関である
2. 各主成分の分散は対応する固有値に等しい
3. 変数の単位が異なる場合でも分散共分散行列でPCAを行うべきである
4. 全主成分の分散の和は元のデータの全分散の和に等しい

??? success "解答・解説を見る"

    **正解**: 1, 2, 4（3は誤り）

    - (1) ○: 主成分は互いに直交し、無相関
    - (2) ○: $\text{Var}(Z_j) = \lambda_j$
    - (3) ✗: 単位が異なる場合は**相関行列**（標準化）でPCAを行う
    - (4) ○: トレース不変 $\sum \lambda_j = \text{tr}(\boldsymbol{\Sigma}) = \sum \text{Var}(X_j)$

    !!! warning "よくある間違い"
        単位が異なる変数（例: 身長[cm]と体重[kg]）を分散共分散行列でPCAすると、
        単位の大きな変数が支配的になる。必ず相関行列を使う。

---

## 問題 M1-003 (応用) ：多変量正規分布の線形変換・条件付き分布

> **出典**: 統計検定準1級 2021年6月 第3問（表現を改変）

確率ベクトル $(X, Y, Z)^\top$ が以下の3変量正規分布に従うとする：

$$\begin{pmatrix}X\\Y\\Z\end{pmatrix} \sim N\!\left(\begin{pmatrix}1\\2\\3\end{pmatrix},\ \begin{pmatrix}2&0&1\\0&3&2\\1&2&4\end{pmatrix}\right)$$

**(1)** $(X+Y,\ Y-Z)^\top$ が従う2変量正規分布を次の①〜⑤から選べ。

① $N\!\left(\begin{pmatrix}3\\1\end{pmatrix}, \begin{pmatrix}5&0\\0&3\end{pmatrix}\right)$　　② $N\!\left(\begin{pmatrix}3\\1\end{pmatrix}, \begin{pmatrix}4&0\\0&2\end{pmatrix}\right)$

③ $N\!\left(\begin{pmatrix}3\\1\end{pmatrix}, \begin{pmatrix}5&4\\4&3\end{pmatrix}\right)$　　④ $N\!\left(\begin{pmatrix}3\\-1\end{pmatrix}, \begin{pmatrix}4&0\\0&2\end{pmatrix}\right)$

⑤ $N\!\left(\begin{pmatrix}3\\-1\end{pmatrix}, \begin{pmatrix}5&0\\0&3\end{pmatrix}\right)$

**(2)** $X=x$、$Y=y$ を与えたときの $Z$ の条件付き分布を①〜⑤から選べ。

① $N(3,\ 15/4)$　　② $N(x+2y-2,\ 15/4)$　　③ $N\!\left(\dfrac{x}{2}+\dfrac{2y}{3}+\dfrac{7}{6},\ \dfrac{13}{6}\right)$

④ $N\!\left(\dfrac{x}{2}+\dfrac{2y}{3}+\dfrac{7}{6},\ \dfrac{15}{4}\right)$　　⑤ $N(x+2y-2,\ 13/6)$

??? success "解答・解説を見る"

    **(1) 正解：⑤**

    ### 線形変換の公式

    $\mathbf{W} = A\mathbf{X}$ のとき、$\mathbf{W} \sim N(A\boldsymbol{\mu},\ A\boldsymbol{\Sigma}A^\top)$

    変換行列：$A = \begin{pmatrix}1&1&0\\0&1&-1\end{pmatrix}$

    **平均の計算**：
    $$A\boldsymbol{\mu} = \begin{pmatrix}1&1&0\\0&1&-1\end{pmatrix}\begin{pmatrix}1\\2\\3\end{pmatrix} = \begin{pmatrix}3\\-1\end{pmatrix}$$

    **分散共分散行列の計算**：
    $$A\boldsymbol{\Sigma} = \begin{pmatrix}1&1&0\\0&1&-1\end{pmatrix}\begin{pmatrix}2&0&1\\0&3&2\\1&2&4\end{pmatrix} = \begin{pmatrix}2&3&3\\-1&1&-2\end{pmatrix}$$

    $$A\boldsymbol{\Sigma}A^\top = \begin{pmatrix}2&3&3\\-1&1&-2\end{pmatrix}\begin{pmatrix}1&0\\1&1\\0&-1\end{pmatrix} = \begin{pmatrix}5&0\\0&3\end{pmatrix}$$

    よって $(X+Y, Y-Z)^\top \sim N\!\left(\begin{pmatrix}3\\-1\end{pmatrix}, \begin{pmatrix}5&0\\0&3\end{pmatrix}\right)$ → **⑤**

    !!! tip "計算のコツ"
        $A\boldsymbol{\Sigma}A^\top$ は2段階で計算。まず $A\boldsymbol{\Sigma}$（2×3行列）を求め、次に右から $A^\top$（3×2行列）をかける。

    ---

    **(2) 正解：③**

    ### 条件付き正規分布の公式

    $\mathbf{X}_1 = (X,Y)^\top$、$X_2 = Z$ と分割すると：

    $$\boldsymbol{\Sigma}_{11} = \begin{pmatrix}2&0\\0&3\end{pmatrix},\quad \boldsymbol{\Sigma}_{12} = \begin{pmatrix}1\\2\end{pmatrix},\quad \Sigma_{22} = 4$$

    $$\boldsymbol{\Sigma}_{11}^{-1} = \begin{pmatrix}1/2&0\\0&1/3\end{pmatrix}$$

    **条件付き平均**：
    $$\mu_{Z|x,y} = 3 + (1,\ 2)\begin{pmatrix}1/2&0\\0&1/3\end{pmatrix}\begin{pmatrix}x-1\\y-2\end{pmatrix}$$
    $$= 3 + \frac{1}{2}(x-1) + \frac{2}{3}(y-2) = \frac{x}{2} + \frac{2y}{3} + \frac{7}{6}$$

    **条件付き分散**：
    $$\sigma^2_{Z|x,y} = 4 - (1,\ 2)\begin{pmatrix}1/2&0\\0&1/3\end{pmatrix}\begin{pmatrix}1\\2\end{pmatrix} = 4 - \left(\frac{1}{2}+\frac{4}{3}\right) = 4 - \frac{11}{6} = \frac{13}{6}$$

    よって $Z \mid X=x, Y=y \sim N\!\left(\dfrac{x}{2}+\dfrac{2y}{3}+\dfrac{7}{6},\ \dfrac{13}{6}\right)$ → **③**

    !!! tip "試験対策"
        条件付き正規分布の分散は $x, y$ の値に依存しない（定数）。
        公式: $\sigma^2_{2|1} = \Sigma_{22} - \boldsymbol{\Sigma}_{21}\boldsymbol{\Sigma}_{11}^{-1}\boldsymbol{\Sigma}_{12}$

    !!! warning "よくある間違い"
        $\boldsymbol{\Sigma}_{12}$ は列ベクトル（$p_2 \times p_1$）、$\boldsymbol{\Sigma}_{21}$ は行ベクトルの向きに注意。
