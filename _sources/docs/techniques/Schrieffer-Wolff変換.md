# Schrieffer-Wolff変換


いま, 無摂動ハミルトニアン$\hat{H}_0$と摂動$\hat{V}$からなる以下のハミルトニアン$\hat{H}_0$を考える:

$$
\begin{align}
 \hat{H}=\hat{H}_0+\hat{V},
\end{align}
$$

ただし$\hat{V}$は$\hat{H}_0$に比べて微小パラメータ$\epsilon$ ($\epsilon\ll 1$)の1次のオーダで小さいと仮定する. つまり

$$
\begin{align}
\frac{\|\hat{V}\|}{\|\hat{H}_0\|}=O(\epsilon).
\end{align}
$$

例えば$\hat{H}_0$は結合がないときの各qubitや共振器の自由ハミルトニアンであり, その固有値$E_n$や固有状態$\ket{n}$は既知であると仮定する. 一方$\hat{V}$は$\hat{H}_0$の基底では対角成分を持たないと仮定する. 

ここで目指すのは, ユニタリ演算子${\rm e}^{-\hat{S}}$を用いた相互作用描像への変換:

$$
\begin{align}
 \hat{H}\rightarrow\hat{H}'
 &={\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}}+{\rm i}\hbar\frac{\rm d}{{\rm d}t}{\rm e}^{-\hat{S}}\cdot({\rm e}^{-\hat{S}})^\dagger\nonumber\\
 &={\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}}-{\rm i}\hbar\dot{\hat{S}}
 \quad(\hat{S}\text{は反エルミート演算子})
\end{align}
$$

によって, $\hat{H}'$が$O(\epsilon^3)$の項を除いて$\hat{H}_0$の基底で対角的となるような$\hat{S}$を探すことである. ただし$\hat{S}$は$O(\epsilon)$のオーダの大きさであると仮定する. また右辺第2項目は, $\hat{V}$が時間無依存である場合は0となる. 

Baker-Campbell-Hausdorffの補助公式より,

$$
\begin{align}
 (\text{右辺第1項目})
&= {\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}} \nonumber\\
&= \hat{H} + [\hat{H},\hat{S}] + \frac{1}{2}[[\hat{H},\hat{S}],\hat{S}]+O(\epsilon^3)\nonumber\\
&=\hat{H}_0 +\underbrace{\hat{V} + [\hat{H}_0,\hat{S}]}_{\epsilon\text{の1次項}}
+ \underbrace{[\hat{V},\hat{S}]+\frac{1}{2}[[\hat{H}_0,\hat{S}],\hat{S}]}_{\epsilon\text{の2次項}}+O(\epsilon^3)
\end{align}
$$

と表せるため, 求める$\hat{S}$の必要十分条件は

$$
\begin{align}
 \hat{V} + [\hat{H}_0,\hat{S}] = 0 \quad\text{かつ}\quad
[\hat{V},\hat{S}]+\frac{1}{2}[[\hat{H}_0,\hat{S}],\hat{S}] \text{が対角的}
\end{align}
$$

となる. $\hat{S}$として, 

$$
\begin{align}
 \hat{S}=-\sum_{m,n}\frac{\bra{m}{\hat{V}}\ket{n}}{E_m-E_n}\ket{m}\bra{n}
\end{align}
$$

と選べば, 1つ目の条件$\hat{V} + [\hat{H}_0,\hat{S}] = 0 $は満たされる.

2つ目の条件は必ずしも満たされるわけではなく, 一般には$(n, n+2)$成分と$(n+2, n)$成分に$O(\epsilon^2)$のオーダの要素を持つ. これらの要素に対してさらに高次のSW変換を行うことで, $(n, n+3)$成分と$(n+3, n)$成分に$O(\epsilon^3)$のオーダの要素として押しやることができる. このようにして摂動つきハミルトニアンの近似的な対角化が行われ, 結果として

$$
\begin{align}
\hat{H}' = \hat{H}_0 + \frac{1}{2}[\hat{V},\hat{S}]+O(\epsilon^3) 
-{\rm i}\hbar\dot{\hat{S}}
\end{align} 
$$

が得られる. 

$\hat{H}'$の固有値, 固有状態をそれぞれ$E_n'$, $\ket{n}'$とし, $\hat{V}$は時間無依存(つまり$\dot{\hat{S}}=0$)とする. 固有方程式は$\hat{H}'\ket{n}'=E_n'\ket{n}'$であり, 両辺に左から${\rm e}^{\hat{S}}$をかけると,

$$
\begin{align}
 {\rm e}^{\hat{S}}\hat{H}'\ket{n}'=E_n'{\rm e}^{\hat{S}}\ket{n}'
\ \Leftrightarrow\ 
\hat{H}\left({\rm e}^{\hat{S}}\ket{n}'\right)
=E_n'\left({\rm e}^{\hat{S}}\ket{n}'\right),
\end{align}
$$

つまり, SW変換後も固有値は変わらず$E_n'=E_n$であるが, 固有状態は少し変化する:

$$
\begin{align}
 \ket{n}'={\rm e}^{-\hat{S}}\ket{n} = \left(1-\hat{S}\right)\ket{n}+O(\epsilon^2).
\end{align}
$$

したがって, SW変換によって対角化できたからといって, 変換前の固有状態が時間発展で変化しないわけではないことに注意する必要がある. 

## 具体例

今, 複素振幅$\varOmega(t)\in\mathbb{C}$で駆動されているトランズモンを考える. 駆動周波数$\omega_{\rm d}$の回転座標系ではハミルトニアンは以下のように表される($\hbar=1$とした):

$$
\begin{align}
\hat{H}
&= 
\varDelta_{\rm qd}\hat{a}^\dagger\hat{a} 
+ 
\frac{\alpha}{2}\hat{a}^{\dagger 2}\hat{a}^2
+
\frac{\varOmega}{2}\hat{a}
+\frac{\varOmega^*}{2}\hat{a}^\dagger,
\end{align} 
$$

ただし$\varDelta_{\rm qd}:=\omega_{\rm q}-\omega_{\rm d}$とする. 3準位系の部分空間のみに着目し, 行列で表すと, 

$$
\begin{align}
\hat{H}
&= 
\begin{bmatrix}
0&&\\
&\varDelta_{\rm qd}&\\
&&2\varDelta_{\rm qd}+\alpha\\
\end{bmatrix}
+
\frac{1}{2}
\begin{bmatrix}
&\varOmega&\\
\varOmega^*&&\sqrt{2}\varOmega\\
&\sqrt{2}\varOmega^*&\\
\end{bmatrix}
\end{align}
$$

と表せる. $\hat{S}$として

$$
\begin{align}
\hat{S}
&= 
\frac{1}{2}
\begin{bmatrix}
&\frac{\varOmega}{\varDelta_{\rm qd}}&\\
-\frac{\varOmega^*}{\varDelta_{\rm qd}}&&\frac{\sqrt{2}\varOmega}{\varDelta_{\rm qd}+\alpha}\\
&-\frac{\sqrt{2}\varOmega^*}{\varDelta_{\rm qd}+\alpha}&\\
\end{bmatrix}
\end{align}
$$

を用いてSW変換を行うと, 

$$
\begin{align}
\hat{H}'
&= 
\begin{bmatrix}
-\frac{|\varOmega|^2}{4\varDelta_{\rm qd}}&&\\
&\varDelta_{\rm qd}+\frac{|\varOmega|^2}{4\varDelta_{\rm qd}}-\frac{|\varOmega|^2}{2(\varDelta_{\rm qd}+\alpha)}&\\
&&2\varDelta_{\rm qd}+\alpha+\frac{|\varOmega|^2}{2(\varDelta_{\rm qd}+\alpha)}\\
\end{bmatrix}
-
\frac{\rm i}{2}
\begin{bmatrix}
&\frac{\dot{\varOmega}}{\varDelta_{\rm qd}}&\\
-\frac{\dot{\varOmega}^*}{\varDelta_{\rm qd}}&&\frac{\sqrt{2}\dot{\varOmega}}{\varDelta_{\rm qd}+\alpha}\\
&-\frac{\sqrt{2}\dot{\varOmega}^*}{\varDelta_{\rm qd}+\alpha}&\\
\end{bmatrix}\nonumber\\
&\quad+
\frac{\sqrt{2}}{8}
\left(
\frac{1}{\varDelta_{\rm qd}+\alpha} - \frac{1}{\varDelta_{\rm qd}}
\right)
\begin{bmatrix}
&&\varOmega^{2}\\
&0&\\
\varOmega^{*2}&&\\
\end{bmatrix}
\end{align}
$$

となる. 

右辺第1項目ではac-Starkシフトによってエネルギー準位のシフトが生じている. 
右辺第2項目では駆動パルスの時間微分に比例する形で, $\epsilon$の1次の項が非対角成分に残っている. 立ち上がりが急激なパルスによって望まない0↔︎1や1↔︎2の遷移が生じるのはこのためである. 
右辺第3項目では(0,2)成分と(2,0)成分に$\epsilon$の2次の項が残っており, これは0↔︎2間のgf2光子遷移を表している. 

さらに(0,2), (2,0)成分を消去するためのSW変換を考える. (0,0), (0,2), (2,0), (2,2)成分の部分空間に着目し, 

$$
\begin{align}
\hat{H}_{02}
&= 
\begin{bmatrix}
-\frac{|\varOmega|^2}{4\varDelta_{\rm qd}}&\\
&2\varDelta_{\rm qd}+\alpha+\frac{|\varOmega|^2}{2(\varDelta_{\rm qd}+\alpha)}\\
\end{bmatrix}
+
\frac{\sqrt{2}}{8}
\left(
\frac{1}{\varDelta_{\rm qd}+\alpha} - \frac{1}{\varDelta_{\rm qd}}
\right)
\begin{bmatrix}
&\varOmega^{2}\\
\varOmega^{*2}&\\
\end{bmatrix}\nonumber\\
&=
\begin{bmatrix}
&\varOmega_{02}\\
\varOmega_{02}^*&\varDelta_{\rm 02}\\
\end{bmatrix}
-\frac{|\varOmega|^2}{4\varDelta_{\rm qd}}I\\
\varDelta_{\rm 02}
&:=
2\varDelta_{\rm qd}+\alpha+\frac{|\varOmega|^2}{2}
\left(
\frac{1}{\varDelta_{\rm qd}+\alpha}
+\frac{1}{2\varDelta_{\rm qd}}
\right)\\
\varOmega_{02}
&:=
\frac{\sqrt{2}}{8}
\left(
\frac{1}{\varDelta_{\rm qd}+\alpha} - \frac{1}{\varDelta_{\rm qd}}
\right)\varOmega^2
\end{align}
$$

からスタートする. $\hat{S}$行列は

$$
\begin{align}
\hat{S}_{02}
&=
\frac{1}{\varDelta_{02}}
\begin{bmatrix}
&\varOmega_{02}\\
\varOmega_{02}^*&\\
\end{bmatrix}
\end{align}
$$

であり, これを用いてSW変換を行うと, 

$$
\begin{align}
\hat{H}_{02}'
&=
\begin{bmatrix}
&\\
&\varDelta_{\rm 02}\\
\end{bmatrix}
-\frac{|\varOmega|^2}{4\varDelta_{\rm qd}}I
+
\frac{|\varOmega_{02}|^2}{2\varDelta_{02}}
\begin{bmatrix}
1&\\
&-1\\
\end{bmatrix}
-\frac{\rm i}{\varDelta_{02}}
\begin{bmatrix}
&\dot{\varOmega}_{02}\\
\dot{\varOmega}_{02}^*&\\
\end{bmatrix}
\end{align}
$$

となる. やはり駆動振幅の時間変化が早いと, (0,2), (2,0)成分にある振幅の時間微分項のために遷移が生じる. 駆動振幅の時間変化が遅くこの項の影響が無視できる場合は, この座標系で見たときに0↔︎1遷移も1↔︎2遷移も生じないことになる. 

ただし実際に観測にかかるのは, SW変換前の座標系の状態である. したがってSW変換が有用であるための条件として, 
- $O(\epsilon^2)$が十分無視できる
- 駆動振幅の時間微分項が0, または十分小さく無視できる, または駆動振幅の変調によりキャンセルできる(DRAG)

が満たされていないといけないことに留意する必要がある. 