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

## 外部駆動時の時間発展(途中)

超伝導qubitに共鳴する周波数のマイクロ波を照射することで, qubitの状態を励起または脱励起することができる. 超伝導qubitに対して周波数$\omega_{\rm d}$のマイクロ波駆動を行った場合のハミルトニアンは, 以下の形で表される(導出は超伝導電気回路の節を参照):

$$
\begin{align}
\hat{H}(t) = -\hbar\omega_{\rm q}\frac{\hat{Z}}{2} + \hbar\varOmega\cos(\omega_{\rm d}t+\phi)\hat{X}
\end{align}
$$

右辺第1項目の自由ハミルトニアンの項に加えて, 右辺第2項目にマイクロ波駆動時はPauli-Xを含む振動項が現れる. ここで$\varOmega$はマイクロ波の振幅をRabi周波数換算した量, $\phi$は駆動マイクロ波の位相である. 伝送線路におけるマイクロ波の振幅の単位は通常V (Volt)で表されるが, 回路QEDの文脈では, その振幅の共鳴マイクロ波がqubitに照射された際に生じるRabi振動の振動数(単位Hz)に換算された量$\varOmega$で扱われる. また右辺第2項目のPauli演算子を$\hat{X}$とするか$\hat{Y}$とするかには任意性があり, ここでは実験者が有する位相基準に対して位相差ゼロ$(\phi=0)$のマイクロ波を照射した際に$\hbar\varOmega\cos(\omega_{\rm d}t)\hat{X}$の駆動項が現れるとした. 

このハミルトニアンの時間依存性を消去して時間発展を直観的に捉えるために, ここでは駆動周波数$\omega_{\rm d}$の回転座標系に変換することを考える. つまり, 回転座標変換のユニタリ演算子

$$
\begin{align}
\hat{U}_{\rm r}(t) = 
\exp
\left(
    \frac{-{\rm i}\omega_{\rm d}t\hat{Z}}{2}
\right)
\end{align}
$$

を用いて, ハミルトニアンを以下のように変換する:

$$
\begin{align}
\hat{H}_{\rm r} 
&= \hat{U}_{\rm r}(t)\hat{H}\hat{U}_{\rm r}^\dag(t)
+{\rm i}\hbar
\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}(t) \cdot\hat{U}_{\rm r}^\dag(t)\nonumber\\
&= -\hbar(\omega_{\rm q}-\omega_{\rm d})\frac{\hat{Z}}{2} + \hbar\varOmega\cos(\omega_{\rm d}t+\phi)\hat{U}_{\rm r}(t)\hat{X}\hat{U}_{\rm r}^\dag(t)
\end{align} 
$$

ここで右辺第2項目における

$$
\begin{align}
\hat{U}_{\rm r}(t)\hat{X}\hat{U}_{\rm r}^\dag(t)
=
\exp
\left(
    \frac{-{\rm i}\omega_{\rm d}t\hat{Z}}{2}
\right)
\hat{X}
\exp
\left(
    \frac{{\rm i}\omega_{\rm d}t\hat{Z}}{2}
\right)
\end{align} 
$$

は, Baker-Campbell-Hausdorffの公式:

$$
\begin{align}
{\rm e}^{\hat{A}}\hat{B}{\rm e}^{-\hat{A}}
=
\hat{B} + [\hat{A},\hat{B}] + \frac{1}{2!}[\hat{A},[\hat{A},\hat{B}]] + \frac{1}{3!}[\hat{A}, [\hat{A},[\hat{A},\hat{B}]]]+ \cdots
\end{align} 
$$

を用いると解析的に解くことができる. つまり$k:=-{\rm i}\omega_{\rm d}t/2$とおいて, 

$$
\begin{align}
{\rm e}^{k\hat{Z}}
\hat{X}
{\rm e}^{-k\hat{Z}}
&=
\hat{X} + k[\hat{Z},\hat{X}] + \frac{k^2}{2!}[\hat{Z},[\hat{Z},\hat{X}]] + \frac{k^3}{3!}[\hat{Z}, [\hat{Z},[\hat{Z},\hat{X}]]] + \cdots\nonumber\\
&=
\hat{X} + {\rm i}2k\hat{Y} + \frac{(2k)^2}{2!}\hat{X} + {\rm i}\frac{(2k)^3}{3!}\hat{Y} + \cdots\nonumber\\
&=
\left(
1 + \frac{(2k)^2}{2!} + \cdots
\right)\hat{X}
+ {\rm i}
\left(
2k + \frac{(2k)^3}{3!} + \cdots
\right)\hat{Y}\nonumber\\
&=
\left(
1 - \frac{(\omega_{\rm d}t)^2}{2!} + \cdots
\right)\hat{X}
+ 
\left(
\omega_{\rm d}t - \frac{(\omega_{\rm d}t)^3}{3!} + \cdots
\right)\hat{Y}\nonumber\\
&=
\cos(\omega_{\rm d}t)\hat{X} + \sin(\omega_{\rm d}t)\hat{Y}
\end{align} 
$$

となる. 

このようにして座標変換して得られた右辺第2項目

$$
\begin{align}
\hbar\varOmega\cos(\omega_{\rm d}t+\phi)
\left[
    \cos(\omega_{\rm d}t)\hat{X} + \sin(\omega_{\rm d}t)\hat{Y}
\right]
\end{align} 
$$

に対して, さらに以下のように回転波近似を行うことで時間依存項を消去する(回転波近似についての詳細は以下の項を参照). 
まずcosとsinを指数関数で展開する:

$$
\begin{align}
&\hbar\varOmega\cos(\omega_{\rm d}t+\phi)
\left[
    \cos(\omega_{\rm d}t)\hat{X} + \sin(\omega_{\rm d}t)\hat{Y}
\right]\nonumber\\
& = 
\hbar\varOmega
\frac{
    {\rm e}^{{\rm i}(\omega_{\rm d}t+\phi)} + 
    {\rm e}^{{\rm -i}(\omega_{\rm d}t+\phi)}
    }{2}
\left(
    \frac{
    {\rm e}^{{\rm i}\omega_{\rm d}t} + 
    {\rm e}^{{\rm -i}\omega_{\rm d}t}
    }{2}\hat{X} 
    + 
    \frac{
    {\rm e}^{{\rm i}\omega_{\rm d}t} - 
    {\rm e}^{{\rm -i}\omega_{\rm d}t}
    }{2{\rm i}}
    \hat{Y}
\right)\nonumber\\
& = 
\hbar\varOmega
\left(
    \frac{
    {\rm e}^{{\rm i}(2\omega_{\rm d}t+\phi)} + 
    {\rm e}^{{\rm i}\phi} +
    {\rm e}^{{\rm -i}\phi} + 
    {\rm e}^{{\rm -i}(2\omega_{\rm d}t+\phi)}
    }{4}\hat{X} 
    + 
    \frac{
    {\rm e}^{{\rm i}(2\omega_{\rm d}t+\phi)} - 
    {\rm e}^{{\rm i}\phi} +
    {\rm e}^{{\rm -i}\phi} - 
    {\rm e}^{{\rm -i}(2\omega_{\rm d}t+\phi)}
    }{4{\rm i}}
    \hat{Y}
\right)
\end{align} 
$$

ここで現れる角周波数$\pm 2\omega_{\rm d}$の振動項は, ハミルトニアンの他の項と同じオーダかそれ以下のノルムを持ち, 振動周波数($\sim$数GHz)の逆数(振動周期; $\sim$数100ps)は今注目している時間発展の時間スケール($\sim$数µs)に比べて非常に小さい. この時, この高速振動項は時間発展にはほとんど影響せず, 近似的に無視しても良い. これを回転波近似という. したがって上の式は近似的に

$$
\begin{align}
&\hbar\varOmega\cos(\omega_{\rm d}t+\phi)
\left[
    \cos(\omega_{\rm d}t)\hat{X} + \sin(\omega_{\rm d}t)\hat{Y}
\right]\nonumber\\
& \approx
\hbar\varOmega
\left(
    \frac{
    {\rm e}^{{\rm i}\phi} + {\rm e}^{{\rm -i}\phi}
    }{4}\hat{X} 
    + 
    \frac{
    - {\rm e}^{{\rm i}\phi} +{\rm e}^{{\rm -i}\phi} 
    }{4{\rm i}}
    \hat{Y}
\right)\nonumber\\
& =
\hbar\varOmega
\left(
    \cos\phi
    \frac{\hat{X}}{2}
    -
    \sin\phi
    \frac{\hat{Y}}{2}
\right)
\end{align} 
$$

と表すことができ, 時間依存項を消去することができる. 


### 回転波近似について補足

回転波近似が成立する理由を直観的に説明する. 今, 以下のように同じオーダのノルムを持つ時間無依存項$\hat{H}_0$と周波数$\omega$の振動項$\hat{H}_1{\rm e}^{{\rm i}\omega t}$からなるハミルトニアン$\hat{H}(t)$を考える:

$$
\begin{align}
\hat{H}(t) = \hat{H}_0 + \hat{H}_1{\rm e}^{{\rm i}\omega t}.
\end{align}
$$

この時間依存ハミルトニアンによる時間発展を, 小さな時間区分$\Delta t$ごとに分割して以下のように表す:

$$
\begin{align}
\hat{U}(0, N\Delta t)
=
\hat{U}((N-1)\Delta t, N\Delta t)\cdots
\hat{U}(0\Delta t, 1\Delta t),
\end{align}
$$

ただし$\hat{U}(t_{\rm start}, t_{\rm end})$は$t_{\rm start}$から$t_{\rm end}$における上記$H(t)$による時間発展ユニタリ演算子である. それぞれのユニタリ要素は, 

$$
\begin{align}
\hat{U}(m\Delta t, (m+1)\Delta t)
&\approx
\exp\left(
\frac{-{\rm i}\hat{H}(n\Delta t)\Delta t}{\hbar}
\right)\nonumber\\
&=1 + \frac{-{\rm i}\hat{H}(n\Delta t)\Delta t}{\hbar} + O\left[(\|\hat{H}\|\Delta t)^2\right]
\end{align}
$$

と表せるので, 全体としては, 

$$
\begin{align}
\hat{U}(0, N\Delta t)
&=\left(
    1 + \frac{-{\rm i}\hat{H}((N-1)\Delta t)\Delta t}{\hbar}
\right)
\cdots
\left(
    1 + \frac{-{\rm i}\hat{H}(0\Delta t)\Delta t}{\hbar}
\right)
+ O\left[(\|\hat{H}\|\Delta t)^2\right]\nonumber\\
&=
1 + \frac{-{\rm i}\sum_{m=0}^{N-1}\hat{H}(m\Delta t)\Delta t}{\hbar}
+ O\left[(\|\hat{H}\|\Delta t)^2\right]
\end{align}
$$

と表せる. この時, $\sum_{m=0}^{N-1}\hat{H}(m\Delta t)$において高速振動項$\hat{H}_1{\rm e}^{{\rm i}\omega t}$は平均化されるため, 十分小さくなり無視することができる. これが回転波近似の直観的な考え方である. 

なお, 上の計算で回転波近似後の駆動ハミルトニアン

$$
\begin{align}
\hbar\varOmega
\left(
    \cos\phi
    \frac{\hat{X}}{2}
    -
    \sin\phi
    \frac{\hat{Y}}{2}
\right)
\end{align} 
$$

を逆回転座標変換して実験室フレームに戻すと, 

$$
\begin{align}
\hbar\varOmega
\left[
    \cos(\omega_{\rm d}t+\phi)
    \frac{\hat{X}}{2}
    -
    \sin(\omega_{\rm d}t+\phi)
    \frac{\hat{Y}}{2}
\right]
\end{align} 
$$

となる. これは駆動電場のかかる方向がX軸方向だけの振動ではなく, XY平面を回転している描像となる. これが回転波近似の名前の由来である. 

### Rabi振動

$\omega_{\rm d}$の回転座標系に乗り, 回転波近似を行った後の全体のハミルトニアンは以下のように表せる:

$$
\begin{align}
\hat{H} = -\hbar(\omega_{\rm q}-\omega_{\rm d})\frac{\hat{Z}}{2} + 
\hbar\varOmega
\left(
    \cos\phi
    \frac{\hat{X}}{2}
    -
    \sin\phi
    \frac{\hat{Y}}{2}
\right).
\end{align}
$$

まず, $\cos\phi\hat{X}-\sin\phi\hat{Y}$は, XY平面内のX軸から角度$-\phi$の方向のハミルトニアンであり, これを新たに$\hat{X}_{-\phi}$とおく. この時, ハミルトニアンは以下のように変形できる:

$$
\begin{align}
\hat{H} 
&= -\hbar(\omega_{\rm q}-\omega_{\rm d})\frac{\hat{Z}}{2} + 
\hbar\varOmega\frac{\hat{X}_{-\phi}}{2}\nonumber\\
&= \frac{\hbar\sqrt{(\omega_{\rm q}-\omega_{\rm d})^2 + \varOmega^2}}{2}
\left(
\frac{-(\omega_{\rm q}-\omega_{\rm d})}{\sqrt{(\omega_{\rm q}-\omega_{\rm d})^2 + \varOmega^2}}\hat{Z}
+
\frac{\varOmega}{\sqrt{(\omega_{\rm q}-\omega_{\rm d})^2 + \varOmega^2}}
\hat{X}_{-\phi}
\right)
\end{align}
$$

いま, 

$$
\begin{align}
\varOmega_{\rm Rabi}&:= \sqrt{(\omega_{\rm q}-\omega_{\rm d})^2 + \varOmega^2}\\
\cos\theta &= 
\frac{-(\omega_{\rm q}-\omega_{\rm d})}{\sqrt{(\omega_{\rm q}-\omega_{\rm d})^2 + \varOmega^2}}\\
\sin\theta &=
\frac{\varOmega}{\sqrt{(\omega_{\rm q}-\omega_{\rm d})^2 + \varOmega^2}}
\end{align}
$$

とおくと, ハミルトニアン全体は

$$
\begin{align}
\hat{H} 
&= \frac{\hbar\varOmega_{\rm Rabi}}{2}
\left(
\cos\theta\hat{Z}
+
\sin\theta
\hat{X}_{-\phi}
\right)
\end{align}
$$

と表すことができる. このハミルトニアンの下での時間発展ユニタリ演算子

$$
\begin{align}
\hat{U}(t) 
&= \exp\left[-{\rm i}
\frac{\varOmega_{\rm Rabi}t}{2}
\left(
\cos\theta\hat{Z}
+
\sin\theta
\hat{X}_{-\phi}
\right)
\right]
\end{align}
$$

は, $\cos\theta\hat{Z}+\sin\theta\hat{X}_{-\phi}$の軸まわりに角速度$\varOmega_{\rm Rabi}$での回転と理解することができる. この回転をしている状態をZ測定して観測される振動はRabi振動, $\varOmega_{\rm Rabi}$はRabi周波数と呼ばれる. 

Rabi振動の挙動は駆動周波数$\omega_{\rm d}$のqubit周波数$\omega_{\rm q}$からの離調$\omega_{\rm q}-\omega_{\rm d}$に応じて大きく変化する. $|\omega_{\rm q}-\omega_{\rm d}|$が大きい時, 回転軸の角度を表す$\theta$は$0$または$\pi$に近づき(つまり回転軸はZ軸に近づき), Rabi周波数は大きくなる. つまり非共鳴駆動の場合は, Rabi振動としては振幅は小さく, 振動は早く見える. 一方$\omega_{\rm q}=\omega_{\rm d}$の共鳴駆動の場合, $\theta=\pi/2$となり(つまり回転軸はXY平面上にあり), Rabi周波数は最小値$\varOmega_{\rm Rabi}=\varOmega$となる. つまり共鳴駆動の場合は, Rabi振動としては振幅は最大($+1$から$-1$までの大円運動)に, 振動数は最小値となり駆動振幅$\varOmega$に等しくなる. 

この性質を用いて, qubitの共鳴周波数を求めることが可能である. つまり駆動周波数を掃引しながら, 各駆動周波数の場合のRabi振動を観測し, Rabi周波数が最小となる条件の駆動周波数を探索することで, 未知のqubit共鳴周波数を調べることが可能である. このようにして得られる振動パターンは山模様をしているのでChevronパターンと呼ばれる. 


## Virtual-Zゲート

測定はZ測定しかできない。
結局回路は, 


任意の1 qubitゲートがこれで実現できる. 
