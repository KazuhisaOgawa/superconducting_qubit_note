# 1 qubit

## ハミルトニアン

量子系の時間発展を適切に制御するためには, その系のハミルトニアンを正確に同定・設計できることが重要である. これは量子系の時間発展はSchr&ouml;dinger方程式:

$$
\begin{align}
{\rm i}\hbar\frac{\rm d}{{\rm d}t}\ket{\psi(t)}
=\hat{H}\ket{\psi(t)}
\end{align}
$$

に従うため, ハミルトニアン$\hat{H}$がその時間発展を特徴づけているからである. 

ハミルトニアンはその系のエネルギーを表す物理量演算子である. エネルギーが$E_0$と$E_1$ ($E_0<E_1$)である2準位系(qubit系)のハミルトニアンは, 

$$
\begin{align}
\hat{H} = E_0|0\rangle\langle0| + E_1|1\rangle\langle1|
\end{align}
$$

と表せる. 恒等演算子$\hat{I}=\begin{bmatrix} 1&0\\0&1\\ \end{bmatrix}$, Pauli-Z演算子$\hat{Z}=\begin{bmatrix} 1&0\\0&-1\\ \end{bmatrix}$を用いると, 

$$
\begin{align}
\hat{H} = \frac{E_0+E_1}{2}\hat{I} + \frac{E_0-E_1}{2}\hat{Z}
\end{align}
$$

となる. ここで$\hat{I}$に比例する項はエネルギーの基準値に対応する項であり, Schr&ouml;dinger方程式の解としては量子状態全体にかかる全体位相というゲージ自由度に現れる. この量は観測には現れず, 実際に観測に現れるのは準位間のエネルギー差に対応する周波数である. したがって$\hat{I}$に比例する項は無視し, $\omega_{\rm q}:=(E_1-E_0)/\hbar>0$とすると, ハミルトニアンは

$$
\begin{align}
\hat{H} = -\hbar\omega_{\rm q}\frac{\hat{Z}}{2}
\end{align}
$$

と表せる. これが外部駆動がない時の1 qubitのハミルトニアンである. 

## 回転座標変換