# 回帰分析：重要概念・公式

## OLS（最小二乗法）

!!! abstract "重回帰モデル"
    $$\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\varepsilon}, \quad \boldsymbol{\varepsilon} \sim N(\mathbf{0}, \sigma^2\mathbf{I})$$

!!! abstract "OLS推定量"
    $$\hat{\boldsymbol{\beta}} = (\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}$$

    性質（ガウス-マルコフの定理）: BLUE（最良線形不偏推定量）

!!! info "OLSの仮定（ガウス-マルコフ）"
    1. 線形性: $E[\mathbf{y}] = \mathbf{X}\boldsymbol{\beta}$
    2. 無相関性: $E[\varepsilon_i \varepsilon_j] = 0$（$i \neq j$）
    3. 等分散性: $\text{Var}(\varepsilon_i) = \sigma^2$（均一分散）
    4. $\mathbf{X}$ はフルランク（多重共線性なし）

---

## 決定係数

!!! abstract "定義"
    $$R^2 = 1 - \frac{SS_E}{SS_T} = \frac{SS_R}{SS_T}$$

    - $SS_T = \sum(y_i - \bar{y})^2$: 全平方和
    - $SS_R = \sum(\hat{y}_i - \bar{y})^2$: 回帰平方和
    - $SS_E = \sum(y_i - \hat{y}_i)^2$: 残差平方和

!!! abstract "自由度調整済み決定係数"
    $$\bar{R}^2 = 1 - \frac{SS_E/(n-p-1)}{SS_T/(n-1)} = 1 - (1-R^2)\frac{n-1}{n-p-1}$$

!!! warning "試験での注意点"
    $R^2$ は変数を増やすと常に増加（または不変）。変数選択には $\bar{R}^2$ や AIC を使う。

---

## 多重共線性

!!! abstract "VIF（分散拡大要因）"
    説明変数 $X_j$ の VIF:
    $$\text{VIF}_j = \frac{1}{1 - R_j^2}$$

    ここで $R_j^2$ は $X_j$ を他の説明変数で回帰したときの決定係数。

!!! warning "VIFの基準"
    - VIF < 5: 問題なし
    - VIF 5〜10: 注意
    - VIF > 10: 多重共線性の問題あり

---

## ロジスティック回帰

!!! abstract "モデル"
    二値応答変数 $Y \in \{0, 1\}$ に対して：
    $$\log\frac{p}{1-p} = \beta_0 + \beta_1 x_1 + \cdots + \beta_p x_p$$

    ここで $p = P(Y=1 \mid \mathbf{x})$、左辺を**ロジット**（対数オッズ）という。

!!! abstract "オッズ比"
    $x_j$ が 1 単位増えたときのオッズの変化率:
    $$\text{Odds Ratio} = e^{\beta_j}$$

!!! info "解釈"
    $\beta_j > 0$ → $x_j$ 増加でオッズ（ひいては確率）が増加
    $\beta_j < 0$ → $x_j$ 増加でオッズが減少

---

## モデル選択

!!! abstract "AICによる変数選択"
    $$\text{AIC} = -2\ell(\hat{\boldsymbol{\beta}}) + 2(p+1)$$

    $p$: 説明変数の数。AICが小さいモデルを選択。

!!! abstract "ステップワイズ法"
    - **前進法**: 変数を1つずつ追加
    - **後退法**: 変数を1つずつ削除
    - **変数増減法**: 追加と削除を組み合わせ

!!! warning "過学習への注意"
    訓練データへの当てはまりが良くても、未知データへの予測性能は別。
    交差検証（Cross-Validation）で予測性能を評価する。
