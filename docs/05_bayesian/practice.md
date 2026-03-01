# ベイズ統計：練習問題

## 予想問題 B-001：ポアソン-ガンマモデル

**難易度**: ★★★☆☆
**頻出度**: 高

単位時間に発生するイベント数 $X \sim Po(\lambda)$ とする。$\lambda$ の事前分布を $Ga(\alpha, \beta)$ とする。
$n$ 回観測で $\sum_{i=1}^n x_i = s$ を得たとき、事後分布とベイズ推定量を求めよ。

??? hint "ヒント"
    ポアソン尤度にガンマ事前分布は共役。
    $Ga(\alpha, \beta)$ の事後更新: $Ga(\alpha + s, \beta + n)$

??? success "解答・解説"

    **事後分布**: $\lambda \mid \mathbf{x} \sim Ga(\alpha + s, \beta + n)$

    ガンマ-ポアソン共役更新:
    $$Ga(\alpha, \beta) \to Ga(\alpha + \sum x_i, \beta + n) = Ga(\alpha + s, \beta + n)$$

    **ベイズ推定量**（事後期待値）:
    $$\hat{\lambda}_{Bayes} = \frac{\alpha + s}{\beta + n}$$

    !!! info "MLEとの比較"
        MLE: $\hat{\lambda}_{MLE} = s/n = \bar{x}$

        ベイズ推定量は $n \to \infty$ で MLE に収束する。

---

## 予想問題 B-002：MAP推定とリッジ回帰の対応

**難易度**: ★★★★☆
**頻出度**: 中

正規線形回帰モデル $y_i = \boldsymbol{\beta}^\top\mathbf{x}_i + \varepsilon_i$（$\varepsilon_i \sim N(0, \sigma^2)$）において、
$\boldsymbol{\beta}$ の事前分布を $N(\mathbf{0}, \tau^2 I)$ としたとき、MAP推定量がリッジ回帰推定量に一致することを示せ。

??? success "解答・解説"

    ### 計算過程

    事後分布の対数:
    $$\log p(\boldsymbol{\beta} \mid \mathbf{y}) \propto -\frac{1}{2\sigma^2}\sum(y_i - \boldsymbol{\beta}^\top\mathbf{x}_i)^2 - \frac{1}{2\tau^2}\|\boldsymbol{\beta}\|^2$$

    MAP推定（最大化 = 以下を最小化）:
    $$\hat{\boldsymbol{\beta}}_{MAP} = \arg\min_{\boldsymbol{\beta}} \left[\sum(y_i - \boldsymbol{\beta}^\top\mathbf{x}_i)^2 + \frac{\sigma^2}{\tau^2}\|\boldsymbol{\beta}\|^2\right]$$

    $\lambda = \sigma^2/\tau^2$ とおくと、これはリッジ回帰の目的関数 $\text{RSS} + \lambda\|\boldsymbol{\beta}\|^2$ に一致。

    !!! tip "正則化のベイズ解釈"
        - リッジ回帰（L2正則化） ↔ 正規事前分布のMAP推定
        - LASSO（L1正則化） ↔ ラプラス事前分布のMAP推定
