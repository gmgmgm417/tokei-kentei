# 多変量解析：練習問題

## 予想問題 M-001：因子分析とPCAの違い

**難易度**: ★★★☆☆
**頻出度**: 高

主成分分析と因子分析の違いについて説明し、それぞれがどのような目的に適しているか述べよ。

??? success "解答・解説"

    ### 主成分分析（PCA）
    - **目的**: データの次元削減・情報圧縮
    - **モデル**: 線形変換のみ（誤差項なし）
    - **成分**: データ全体の分散を最大化する方向を抽出
    - **適用場面**: 可視化、前処理（高次元データの削減）

    ### 因子分析
    - **目的**: 観測変数の背後にある潜在構造（共通因子）の発見
    - **モデル**: $\mathbf{X} = \boldsymbol{\Lambda}\mathbf{F} + \boldsymbol{\varepsilon}$（独自因子あり）
    - **因子**: 共通分散のみ説明（独自分散は除く）
    - **適用場面**: 心理テスト・アンケートの潜在因子抽出

    ### 使い分け
    | 問いの形 | 手法 |
    |---|---|
    | 「これらの変数をまとめたい」 | PCA |
    | 「背後に何個の因子があるか」 | 因子分析 |

---

## 予想問題 M-002：マハラノビス距離

**難易度**: ★★★★☆
**頻出度**: 中

$\boldsymbol{\Sigma} = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$、$\boldsymbol{\mu} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$ のとき、
点 $\mathbf{x} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ のマハラノビス距離 $D^2$ を求めよ。

??? hint "ヒント"
    $\boldsymbol{\Sigma}^{-1} = \frac{1}{|\boldsymbol{\Sigma}|}\begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}$

??? success "解答・解説"

    **正解**: $D^2 = 2/3$

    ### 計算過程

    $|\boldsymbol{\Sigma}| = 2 \times 2 - 1 \times 1 = 3$

    $$\boldsymbol{\Sigma}^{-1} = \frac{1}{3}\begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}$$

    $$D^2 = \mathbf{x}^\top\boldsymbol{\Sigma}^{-1}\mathbf{x} = (1, 1) \cdot \frac{1}{3}\begin{pmatrix} 2 & -1 \\ -1 & 2 \end{pmatrix}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

    $$= (1, 1) \cdot \frac{1}{3}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{3}(1 + 1) = \frac{2}{3}$$
