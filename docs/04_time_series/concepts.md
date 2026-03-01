# 時系列解析：重要概念・公式

## 定常性

!!! abstract "弱定常性（2次定常性）"
    時系列 $\{X_t\}$ が弱定常 $\Leftrightarrow$

    1. $E[X_t] = \mu$（一定）
    2. $\text{Var}(X_t) = \sigma^2$（一定）
    3. $\text{Cov}(X_t, X_{t+h}) = \gamma(h)$（$t$ に依存しない）

!!! abstract "自己共分散・自己相関"
    - 自己共分散: $\gamma(h) = \text{Cov}(X_t, X_{t+h})$
    - 自己相関関数（ACF）: $\rho(h) = \frac{\gamma(h)}{\gamma(0)}$

---

## AR・MA・ARMAモデル

!!! abstract "AR(p)モデル"
    $$X_t = \phi_1 X_{t-1} + \phi_2 X_{t-2} + \cdots + \phi_p X_{t-p} + \varepsilon_t$$

    - **定常条件**: 特性方程式 $1 - \phi_1 z - \cdots - \phi_p z^p = 0$ の根が全て単位円の外
    - AR(1)の定常条件: $|\phi_1| < 1$

!!! abstract "MA(q)モデル"
    $$X_t = \varepsilon_t + \theta_1\varepsilon_{t-1} + \cdots + \theta_q\varepsilon_{t-q}$$

    - MA過程は常に定常
    - **可逆条件**: AR(p)の定常条件と同様

!!! abstract "ARMA(p,q)モデル"
    $$X_t = \phi_1 X_{t-1} + \cdots + \phi_p X_{t-p} + \varepsilon_t + \theta_1\varepsilon_{t-1} + \cdots + \theta_q\varepsilon_{t-q}$$

### ACF・PACFによるモデル識別

| モデル | ACF | PACF |
|---|---|---|
| AR(p) | 指数減衰 or 減衰振動 | ラグ $p$ 以降カットオフ |
| MA(q) | ラグ $q$ 以降カットオフ | 指数減衰 or 減衰振動 |
| ARMA(p,q) | 指数減衰 or 減衰振動 | 指数減衰 or 減衰振動 |

!!! warning "試験での注意点"
    ACFが急にカットオフ → MAモデルの可能性
    PACFが急にカットオフ → ARモデルの可能性

---

## ARIMAモデル

!!! abstract "ARIMA(p,d,q)"
    $d$ 回差分をとると ARMA(p,q) になる非定常過程。

    $d=1$ の差分: $\nabla X_t = X_t - X_{t-1}$

!!! info "単位根検定（ADF検定）"
    帰無仮説: 単位根あり（非定常）
    対立仮説: 単位根なし（定常）

---

## モデル選択基準

!!! abstract "AIC・BIC"
    $$\text{AIC} = -2\ell + 2k, \quad \text{BIC} = -2\ell + k\log n$$

    $\ell$: 最大対数尤度、$k$: パラメータ数、$n$: サンプルサイズ

    値が小さいモデルを選択。BICはAICより大きいパラメータ数にペナルティ。
