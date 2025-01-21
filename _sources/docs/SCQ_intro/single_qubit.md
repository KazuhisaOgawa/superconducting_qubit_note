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

ハミルトニアンはその系のエネルギーを表す物理量演算子である. 下図のように, エネルギーが$E_0$と$E_1$ ($E_0<E_1$)である2準位系(qubit系)のハミルトニアンは, 

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


```{image} ../../figs/TLS.png
:width: 200px
:align: center
```


## 自由時間発展

このハミルトニアンにおける時間発展は, Schr&ouml;dinger方程式を解くことで求めることができる. 今はハミルトニアンが時間変化しないので, 以下のように簡単に求められる:

$$
\begin{align}
\ket{\psi(t)} &= \hat{U}(t)\ket{\psi(0)},\\
\hat{U}(t) &= \exp
\left(
    \frac{-{\rm i}\hat{H}t}{\hbar}
\right)
=
\exp
\left(
    \frac{{\rm i}\omega_{\rm q}t\hat{Z}}{2}
\right)
= \hat{R}_z(-\omega_{\rm q}t).
\end{align}
$$

これは静止系（実験室系）から見たBloch球上では, Z軸周りを角速度$-\omega_{\rm q}$で回転（XYZ軸が右手系配置の場合は左ネジ方向回転に対応）する描像となる. 典型的にqubitの共鳴周波数$\omega_{\rm q}$は数GHzであるのに対しコヒーレンス時間は数10 µsであるので, 注目する時間スケール内で高速に回転することになり, 時間発展を追いかけるには不都合である(下図左). 

外部駆動がない自由時間発展の際にqubitを静止した描像で捉えるためには, **回転座標変換**という手法が用いられる. これはBloch球回転と同じ角速度で回転するフレーム（回転座標系）に観測者が乗ることで, Bloch球が静止して見えるという考え方である(下図右). 数式としては, 状態ケット$\ket{\psi(t)}$（Z軸周り$-\omega_{\rm q}$回転している）に対して, 

$$
\begin{align}
\hat{U}_{\rm r}(t) := 
\exp
\left(
    \frac{-{\rm i}\omega_{\rm r}t\hat{Z}}{2}
\right)
\end{align}
$$

という変換を行った状態

$$
\begin{align}
\ket{\psi_{\rm r}(t)}:=\hat{U}_{\rm r}(t)\ket{\psi(t)} = 
\exp
\left(
    \frac{{\rm i}(\omega_{\rm q} - \omega_{\rm r})t\hat{Z}}{2}
\right)
\ket{\psi(0)}
\end{align}
$$

を考えることに対応する（相互作用描像と呼ばれる）. 特に$\omega_{\rm r}=\omega_{\rm q}$と選べば, 状態は静止して見える. 

回転座標系に乗った時の実効的なハミルトニアンの形を求めておく（qubitの回転を打ち消すような座標系に乗っているので, ハミルトニアンは0となるはずである）. 実験室系でのSchr&ouml;dinger方程式に$\hat{I} = \hat{U}_{\rm r}^\dagger(t)\hat{U}_{\rm r}(t)$を挿入して, 

$$
\begin{align}
&{\rm i}\hbar\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}^\dag(t)\hat{U}_{\rm r}(t)\ket{\psi(t)}
=\hat{H}\hat{U}_{\rm r}^\dag(t)\hat{U}_{\rm r}(t)\ket{\psi(t)} \\
%
\Leftrightarrow&
{\rm i}\hbar\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}^\dag(t)\ket{\psi_{\rm r}(t)}
=\hat{H}\hat{U}_{\rm r}^\dag(t)\ket{\psi_{\rm r}(t)} \\
%
\Leftrightarrow&
{\rm i}\hbar
\left\{
\left[\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}^\dag(t)\right]\ket{\psi_{\rm r}(t)}
+\hat{U}_{\rm r}^\dag(t)\left[\frac{\rm d}{{\rm d}t}\ket{\psi_{\rm r}(t)}\right]
\right\}
=\hat{H}\hat{U}_{\rm r}^\dag(t)\ket{\psi_{\rm r}(t)} \\
%
\Leftrightarrow&
{\rm i}\hbar
\hat{U}_{\rm r}^\dag(t)
\frac{\rm d}{{\rm d}t}\ket{\psi_{\rm r}(t)}
=
\left[
\hat{H}\hat{U}_{\rm r}^\dag(t)
-{\rm i}\hbar\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}^\dag(t)
\right]
\ket{\psi_{\rm r}(t)} \\
%
\Leftrightarrow&
{\rm i}\hbar
\frac{\rm d}{{\rm d}t}\ket{\psi_{\rm r}(t)}
=
\left[
\hat{U}_{\rm r}(t)\hat{H}\hat{U}_{\rm r}^\dag(t)
-{\rm i}\hbar
\hat{U}_{\rm r}(t) \frac{\rm d}{{\rm d}t} \hat{U}_{\rm r}^\dag(t)
\right]
\ket{\psi_{\rm r}(t)}, \\
\end{align}
$$

よって回転座標系における実効ハミルトニアン$\hat{H}_{\rm r}$は, 

$$
\begin{align}
\hat{H}_{\rm r} 
&= \hat{U}_{\rm r}(t)\hat{H}\hat{U}_{\rm r}^\dag(t)
-{\rm i}\hbar
\hat{U}_{\rm r}(t) \frac{\rm d}{{\rm d}t} \hat{U}_{\rm r}^\dag(t)\nonumber\\
&= \hat{U}_{\rm r}(t)\hat{H}\hat{U}_{\rm r}^\dag(t)
+{\rm i}\hbar
\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}(t) \cdot\hat{U}_{\rm r}^\dag(t)
\end{align} 
$$

と表せる. 今の場合は, 

$$
\begin{align}
\hat{U}_{\rm r}(t)\hat{H}\hat{U}_{\rm r}^\dag(t)
+{\rm i}\hbar
\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}(t) \cdot\hat{U}_{\rm r}^\dag(t)
= -\hbar\omega_{\rm q}\frac{\hat{Z}}{2}
+\hbar\omega_{\rm r}\frac{\hat{Z}}{2}
= -\hbar(\omega_{\rm q}-\omega_{\rm r})\frac{\hat{Z}}{2}
\end{align} 
$$

であり, 特に$\omega_{\rm r}=\omega_{\rm q}$の時は$\hat{H}_{\rm r}=0$となり, これは時間発展しない（状態は静止して見える）ことに対応する.

```{image} ../../figs/rotating_frame.png
:width: 600px
:align: center
```

## 外部駆動時の時間発展

超伝導qubitに共鳴する周波数のマイクロ波を照射することで, qubitの状態を励起または脱励起することができる. 
