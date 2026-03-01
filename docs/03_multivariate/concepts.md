# 多変量解析：重要概念・公式

## 多変量正規分布

!!! abstract "定義"
    $p$ 次元確率ベクトル $\mathbf{X}$ が平均 $\boldsymbol{\mu}$、分散共分散行列 $\boldsymbol{\Sigma}$ の多変量正規分布に従うとき：
    $$f(\mathbf{x}) = \frac{1}{(2\pi)^{p/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\!\left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^\top\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu})\right)$$

!!! info "重要な性質"
    - 周辺分布・条件付き分布も正規分布
    - 無相関 $\Leftrightarrow$ 独立（正規分布のとき）
    - マハラノビス距離: $D^2 = (\mathbf{x}-\boldsymbol{\mu})^\top\boldsymbol{\Sigma}^{-1}(\mathbf{x}-\boldsymbol{\mu}) \sim \chi^2(p)$

---

## 主成分分析（PCA）

!!! abstract "目的"
    $p$ 個の変数を、情報損失を最小にしながら少数の主成分に次元削減する。

!!! abstract "数学的定式化"
    分散共分散行列 $\boldsymbol{\Sigma}$ の固有値・固有ベクトル問題：
    $$\boldsymbol{\Sigma}\mathbf{a}_j = \lambda_j\mathbf{a}_j, \quad \lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_p \geq 0$$

    第 $j$ 主成分: $Z_j = \mathbf{a}_j^\top\mathbf{X}$

!!! info "主成分の性質"
    - $\text{Var}(Z_j) = \lambda_j$
    - 主成分は互いに無相関
    - 累積寄与率: $\frac{\sum_{j=1}^k \lambda_j}{\sum_{j=1}^p \lambda_j}$（通常70〜80%以上で選択）

!!! warning "試験での注意点"
    PCAは**相関行列**か**分散共分散行列**で行うかで結果が異なる。
    変数の単位が異なる場合は相関行列（標準化）を使う。
    固有値 = 主成分の分散、固有ベクトル = 主成分の係数。

---

## 因子分析

!!! abstract "モデル"
    観測変数 $\mathbf{X}$ を共通因子 $\mathbf{F}$ と独自因子 $\boldsymbol{\varepsilon}$ で表現：
    $$\mathbf{X} = \boldsymbol{\mu} + \boldsymbol{\Lambda}\mathbf{F} + \boldsymbol{\varepsilon}$$

    ここで $\boldsymbol{\Lambda}$: 因子負荷量行列

!!! warning "PCAと因子分析の違い"
    | | PCA | 因子分析 |
    |---|---|---|
    | 目的 | 次元削減 | 潜在構造の発見 |
    | 成分/因子数 | データと同数（その後削減） | 事前に仮定 |
    | 誤差項 | なし | 独自因子あり |
    | 回転 | 通常なし | バリマックス等で回転 |

---

## 判別分析

!!! abstract "線形判別分析（LDA）"
    2グループ間の判別関数：
    $$D(\mathbf{x}) = (\boldsymbol{\mu}_1 - \boldsymbol{\mu}_2)^\top\boldsymbol{\Sigma}^{-1}\mathbf{x}$$

    マハラノビス距離が小さいグループに分類。

!!! info "マハラノビス距離"
    $$D^2(\mathbf{x}, \boldsymbol{\mu}_k) = (\mathbf{x} - \boldsymbol{\mu}_k)^\top\boldsymbol{\Sigma}^{-1}(\mathbf{x} - \boldsymbol{\mu}_k)$$

---

## クラスター分析

!!! abstract "階層的クラスタリング"
    距離の定義：

    | 方法 | 距離 |
    |---|---|
    | 最短距離法 | $d(C_i, C_j) = \min_{x \in C_i, y \in C_j} d(x,y)$ |
    | 最長距離法 | $d(C_i, C_j) = \max_{x \in C_i, y \in C_j} d(x,y)$ |
    | 群平均法 | 全ペアの平均距離 |
    | ウォード法 | 誤差平方和の増加量を最小化 |

!!! warning "試験での注意点"
    各クラスタリング手法の特徴と、デンドログラムの読み方が問われる。
    ウォード法は「コンパクトで球形」なクラスターを作る傾向がある。
