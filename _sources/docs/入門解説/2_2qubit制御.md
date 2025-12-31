# 2 qubit制御

超伝導qubit系における2 qubit制御は, 弱く結合した2つのqubit系のダイナミクスで理解できる. 
ここでは, まず結合2 qubit系の基本的なハミルトニアンを整理し, その上で, 周波数可変qubitの場合に用いられるiSWAPゲートとCZゲートの実現方法, および周波数固定qubitの場合に用いられる交差共鳴（CR）ゲートの実現方法をそれぞれ説明する.

## 結合2 qubit系

弱く結合した2つのqubit Q0, Q1からなる複合系のハミルトニアンは以下の形で表される:

$$
\begin{align}
\hat{H}
&= 
-\hbar\omega_0\frac{\hat{Z}_0}{2}
-\hbar\omega_1\frac{\hat{Z}_1}{2}
+ \hbar g \left(\hat{\sigma}_0^\dagger \hat{\sigma}_1 + \hat{\sigma}_0 \hat{\sigma}_1^\dagger\right)
\end{align}
$$

ここで$\hat{\sigma}_i$はqubit-$i$に対する消滅演算子であり, 行列表示では$\hat{\sigma}_i=\begin{bmatrix}
0&1\\
0&0\\
\end{bmatrix}$と表される.  
ハミルトニアンを行列表示すると, 

$$
\begin{align}
\hat{H}
&= 
-\frac{\hbar\omega_0}{2}
\begin{bmatrix}
1&0\\
0&-1\\
\end{bmatrix}
\otimes
\begin{bmatrix}
1&0\\
0&1\\
\end{bmatrix}
-\frac{\hbar\omega_1}{2}
\begin{bmatrix}
1&0\\
0&1\\
\end{bmatrix}
\otimes
\begin{bmatrix}
1&0\\
0&-1\\
\end{bmatrix}
                 \nonumber\\
&\qquad
+ \hbar g \left(
    \begin{bmatrix}
0&0\\
1&0\\
\end{bmatrix}
\otimes
\begin{bmatrix}
0&1\\
0&0\\
\end{bmatrix}
+
\begin{bmatrix}
0&1\\
0&0\\
\end{bmatrix}
\otimes
\begin{bmatrix}
0&0\\
1&0\\
\end{bmatrix}
\right)
\nonumber\\
&=
-\frac{\hbar\omega_0}{2}
\begin{bmatrix}
1&0&0&0\\
0&1&0&0\\
0&0&-1&0\\
0&0&0&-1\\
\end{bmatrix}
-\frac{\hbar\omega_1}{2}
\begin{bmatrix}
1&0&0&0\\
0&-1&0&0\\
0&0&1&0\\
0&0&0&-1\\
\end{bmatrix}
+\hbar g
\begin{bmatrix}
0&0&0&0\\
0&0&1&0\\
0&1&0&0\\
0&0&0&0\\
\end{bmatrix}
     \nonumber\\
&=
\hbar
\begin{bmatrix}
\frac{-\omega_0-\omega_1}{2} &0&0&0\\
0& \frac{-\omega_0+\omega_1}{2} & g &0\\
0& g & \frac{\omega_0-\omega_1}{2} &0\\
0&0&0& \frac{\omega_0+\omega_1}{2}\\
\end{bmatrix}
\end{align}
$$

と表せる. 
以下では, この系を2つのqubit周波数の相対関係によって2つの極限に分けて考える.


### 2 qubit周波数が十分離れている場合： $|\omega_0 - \omega_1| \gg g$

このとき, 非対角項は対角項に比べ十分小さいため, 非対角項（結合項）は摂動的に扱える. 
数学的には**Schrieffer–Wolff（SW）変換**という基底変換により, 非対角成分を対角成分に繰り込み, $g$の1次のオーダまでで近似的に対角化できる. 

SWの詳しい理論は別の節で解説するとして, ここではSWの概要のみを述べる. 
SW変換では, ハミルトニアンの対角成分を無摂動ハミルトニアン$\hat{H}_0$, 非対角成分(結合項)を$O(g)$のオーダの摂動ハミルトニアン$\hat{V}$とし, 

$$
\begin{align}
 \hat{H}\rightarrow\hat{H}'={\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}}
\end{align}
$$

と変換する. 
ここで$\hat{S}$は以下で定義する反エルミート演算子:

$$
\begin{align}
 \hat{S}:=-\sum_{m,n}\frac{\bra{m}{\hat{V}}\ket{n}}{E_m-E_n}\ket{m}\bra{n}
 =\frac{g}{\omega_0-\omega_1}(\ket{01}\bra{10} - \ket{10}\bra{01})
\end{align}
$$

である.
ここで$E_m$, $E_n$はそれぞれ無摂動ハミルトニアン$\hat{H}_0$の$m$, $n$番目の固有値（固有エネルギー）, $\ket{m}$, $\ket{n}$はそれぞれそれらの固有値に属する固有ベクトル（固有状態）である. 
この変換により, ハミルトニアンは以下のように変換される（計算の詳細は省略）:

$$
\begin{align}
\hat{H}' &= \hat{H}_0 + \frac{1}{2}[\hat{V},\hat{S}]+O(g^3)\nonumber\\
&= 
-\hbar\left(\omega_0 + \frac{g^2}{\omega_0-\omega_1}\right)\frac{\hat{Z}_0}{2}
-\hbar\left(\omega_1 - \frac{g^2}{\omega_0-\omega_1}\right)\frac{\hat{Z}_1}{2}
+O(g^3)
\end{align} 
$$

このように, SW変換によって少しだけ基底をずらすことによって, その基底では$O(g)$のオーダでは非対角成分が消え, 互いに結合がない2つのqubitが独立に振る舞うように見ることができる. 
その代わりに各qubitの共鳴周波数はそれぞれ$\pm g^2/(\omega_0-\omega_1)$だけシフトする（**ラムシフト**）. 
なお, qubitではなく実際のトランズモンのように3準位以上ある量子系の結合の場合には, ラムシフトだけでなく, $\ket{11}$状態に対応する固有エネルギーだけ弱くシフトする**常在ZZ相互作用**も存在するが, ここでの説明は省略する. 


### 2 qubit周波数が同じ（または近い）場合： $|\omega_0 - \omega_1| \sim g$

このとき, 非対角項は対角項と同じオーダの大きさであるため, SW変換を行うことはできない. 
全体のハミルトニアンのうち, $\ket{01}$, $\ket{10}$の成分だけを取り出すと

$$
\begin{align}
\hat{H}_{\ket{01},\ket{10}}
&=
\hbar
\begin{bmatrix}
\frac{-\omega_0+\omega_1}{2} & g\\
g & \frac{\omega_0-\omega_1}{2}\\
\end{bmatrix}
=
\hbar\frac{-\omega_0+\omega_1}{2}\hat{Z} + \hbar g\hat{X}
\end{align}
$$

となり, パウリZとパウリXの線型結合で表される. 
したがって$|10\rangle$と$|01\rangle$は時間発展に伴って混成するため, これを利用して2 qubitゲートを構成することができる（後述）.


## iSWAPゲート（周波数可変型）

周波数可変型トランズモンでは, 磁束バイアスによりqubit周波数を変化させることができる. 
アイドル時（2 qubitゲートをかけない時）は, 2 qubitの周波数を大きく離すことで, 互いに結合がない2つのqubitとして独立に振る舞う. 
以下では周波数可変型qubitにおける2 qubitゲートの例として, **iSWAPゲート**および**√iSWAPゲート**を説明する. 

iSWAPゲートおよび√iSWAPゲートを実現する際には, 2つのqubitの周波数が等しくなるように周波数を移動させる: $\omega_0 = \omega_1 =: \omega_{\rm q}$.
この時, 全体のハミルトニアンは

$$
\begin{align}
\hat{H}
&= 
-\hbar\omega_{\rm q}\frac{\hat{Z}_0}{2}
-\hbar\omega_{\rm q}\frac{\hat{Z}_1}{2}
+ \hbar g \left(\hat{\sigma}_0^\dagger \hat{\sigma}_1 + \hat{\sigma}_0 \hat{\sigma}_1^\dagger\right)
=
\hbar
\begin{bmatrix}
-\omega_{\rm q} &0&0&0\\
0& 0 & g &0\\
0& g & 0 &0\\
0&0&0& \omega_{\rm q}\\
\end{bmatrix}
\end{align}
$$

となる. 
ここで2 qubitに対して周波数$\omega_{\rm q}$の回転座標変換を行い, Z回転が見えないフレームに乗ることを考える. 
具体的には, 

$$
\begin{align}
\hat{U}_{\rm r}(t) := 
\exp
\left(
    \frac{-{\rm i}\omega_{\rm q}t\hat{Z}_0}{2}
\right)
\exp
\left(
    \frac{-{\rm i}\omega_{\rm q}t\hat{Z}_1}{2}
\right)
\end{align}
$$

というユニタリ演算子を用いて, ハミルトニアンを

$$
\begin{align}
\hat{H} \longrightarrow \hat{H}_{\rm r}
=
\hat{U}_{\rm r}(t)\hat{H}\hat{U}_{\rm r}^\dagger(t)
+{\rm i}\hbar
\frac{\rm d}{{\rm d}t}\hat{U}_{\rm r}(t) \cdot\hat{U}_{\rm r}^\dagger(t)
\end{align} 
$$

と変換すると, $\hat{Z}_0$, $\hat{Z}_1$を含む項は打ち消されて0となり, 生成・消滅演算子$\hat{\sigma}$, $\hat{\sigma}^\dagger$は

$$
\begin{align}
\hat{\sigma} &\rightarrow 
\exp
\left(
    \frac{-{\rm i}\omega_{\rm q}t\hat{Z}}{2}
\right)
\hat{\sigma}
\exp
\left(
    \frac{{\rm i}\omega_{\rm q}t\hat{Z}}{2}
\right)
={\rm e}^{-{\rm i}\omega_{\rm r}t}\hat{\sigma},
\\
\hat{\sigma}^\dagger &\rightarrow 
\exp
\left(
    \frac{-{\rm i}\omega_{\rm q}t\hat{Z}}{2}
\right)
\hat{\sigma}^\dagger
\exp
\left(
    \frac{{\rm i}\omega_{\rm q}t\hat{Z}}{2}
\right)
={\rm e}^{{\rm i}\omega_{\rm r}t}\hat{\sigma}^\dagger
\end{align}
$$

と変換されるため, 

$$
\begin{align}
\hat{H}_{\rm r}
&= 
\hbar g \left(\hat{\sigma}_0^\dagger \hat{\sigma}_1 + \hat{\sigma}_0 \hat{\sigma}_1^\dagger\right)
=
\hbar
\begin{bmatrix}
0 &0&0&0\\
0& 0 & g &0\\
0& g & 0 &0\\
0&0&0& 0\\
\end{bmatrix}
=
\hbar
\left[
\begin{array}{c|c|c}
0 & 0 & 0 \\
\hline
0 & g\hat{X} & 0 \\
\hline
0 & 0 & 0 \\
\end{array}
\right]
\end{align}
$$

となる. 
最右辺はハミルトニアンをブロック対角化された行列と見た場合であり, $\ket{01}$, $\ket{10}$が張る部分空間では$\hbar g\hat{X}$というパウリX演算子が残る. 
このハミルトニアンにおけるユニタリ時間発展演算子$\hat{U}(t)$は, 以下のように計算できる:

$$
\begin{align}
\hat{U}(t) 
&=
\exp\left(\frac{-{\rm i}\hat{H}_{\rm r}t}{\hbar}\right)
=
\left[
\begin{array}{c|c|c}
1 & 0 & 0 \\
\hline
0 & \exp\left(-{\rm i}gt\hat{X}\right) & 0 \\
\hline
0 & 0 & 1 \\
\end{array}
\right]
=
\begin{bmatrix}
1&0&0&0\\
0&\cos(gt) & -{\rm i}\sin(gt) &0\\
0&-{\rm i}\sin(gt) & \cos(gt) &0\\
0&0&0&1\\
\end{bmatrix}.
\end{align}
$$

特に$gt=\pi/2$, $\pi/4$と選んだ場合のユニタリ発展は**iSWAPゲート**, **√iSWAPゲート**と呼ばれる:

$$
\begin{align}
\hat{U}_{\rm iSWAP}
&:=
\hat{U}\left(t=\frac{\pi}{2g}\right) 
=
\begin{bmatrix}
1&0&0&0\\
0&0& -{\rm i} &0\\
0&-{\rm i} & 0&0\\
0&0&0&1\\
\end{bmatrix},\\
\hat{U}_{\sqrt{{\rm iSWAP}}}
&:=
\hat{U}\left(t=\frac{\pi}{4g}\right) 
=
\begin{bmatrix}
1&0&0&0\\
0&\frac{1}{\sqrt{2}}& -\frac{\rm i}{\sqrt{2}} &0\\
0&-\frac{{\rm i}}{\sqrt{2}} & \frac{1}{\sqrt{2}}&0\\
0&0&0&1\\
\end{bmatrix}
=
\sqrt{\hat{U}_{\rm iSWAP}}.
\end{align}
$$

これらは$\ket{01}$と$\ket{10}$のモードを混成するゲートであり, 例えば初期状態$\ket{01}$にある系に対して, 

$$
\begin{align}
\hat{U}_{\rm iSWAP}\ket{01}
&= -{\rm i}\ket{10}, \\
\hat{U}_{\sqrt{{\rm iSWAP}}}\ket{01}
&=\frac{\ket{01} -{\rm i}\ket{10}}{\sqrt{2}}
\end{align}
$$

という変換をもたらす. 
特に後者はセパラブルな状態から量子もつれ状態を直接生成できる. 
またいずれの2 qubitゲートについても, そのゲートと1 qubitゲートの組み合わせによりCNOTゲートが構成できる.
したがって, いずれの2 qubitゲートもそのゲートと1 qubitゲートがユニバーサルゲートセットを構成できるという点で重要である.  

なお, 実際の周波数可変トランズモン系の実験では, iSWAPゲートや√iSWAPゲートよりも, $|11\rangle$と$|02\rangle$（または $|20\rangle$）を混成させて実現するCZゲートを用いる方が主流である. 
ここではqubit系（2準位系）を仮定しているため, このCZゲートについては省略する. 


## 交差共鳴（Cross-Resonance, CR）ゲート（周波数固定型）

qubitの共鳴周波数が動かせない周波数固定型qubit系でも, マイクロ波駆動によって2 qubitゲートを実現することができる. 
以下ではマイクロ波駆動で実現できる2 qubitゲートの例として, **交差共鳴（CR）ゲート**を説明する.  

周波数固定型qubit系では, 2つのqubit間の共鳴周波数は結合定数$g$に比べて大きく離して設計されており, アイドル時（マイクロ波を無駆動時）は2つのqubitが独立に振る舞う. 
CRゲートを実現ためには, 一方のqubit（制御qubit, ここではQ0）に, 他方のqubit（標的qubit, ここではQ1）の共鳴周波数のマイクロ波を印加する. 
この時のハミルトニアンは以下で与えられる:

$$
\begin{align}
\hat{H}
&= 
-\hbar\omega_0\frac{\hat{Z}_0}{2}
-\hbar\omega_1\frac{\hat{Z}_1}{2}
+ \hbar g \left(\hat{\sigma}_0^\dagger \hat{\sigma}_1 + \hat{\sigma}_0 \hat{\sigma}_1^\dagger\right)
+
\hbar\varOmega_{\rm d}\cos(\omega_{\rm d} t)\hat{X}_0
\end{align}
$$

まずSW変換を行い, 結合項を対角成分に繰り込む. 
上の例と同じく, 

$$
\begin{align}
 \hat{S}:=-\sum_{m,n}\frac{\bra{m}{\hat{V}}\ket{n}}{E_m-E_n}\ket{m}\bra{n}
 =\frac{g}{\omega_0-\omega_1}(\ket{01}\bra{10} - \ket{10}\bra{01})
\end{align}
$$

を用いて

$$
\begin{align}
 \hat{H}\rightarrow\hat{H}'={\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}}
\end{align}
$$

と変換する. 
非駆動項$\hat{H}_{\rm static}$については, 上の例と同様に

$$
\begin{align}
\hat{H}_{\rm static}' 
&= 
-\hbar\left(\omega_0 + \frac{g^2}{\omega_0-\omega_1}\right)\frac{\hat{Z}_0}{2}
-\hbar\left(\omega_1 - \frac{g^2}{\omega_0-\omega_1}\right)\frac{\hat{Z}_1}{2}
+O(g^3)
\end{align} 
$$

と変換される. 
駆動項$\hat{H}_{\rm drive}$については, 以下のように変換される:

$$
\begin{align}
 \hat{H}_{\rm drive}'
 &={\rm e}^{-\hat{S}}\hat{H}_{\rm drive}{\rm e}^{\hat{S}}\nonumber\\
 &=\hat{H}_{\rm drive} + [\hat{H}_{\rm drive}, \hat{S}] 
 + \frac{1}{2}[[\hat{H}_{\rm drive}, \hat{S}], \hat{S}]
 + O(g^3)\nonumber\\
 &=\hbar\varOmega_{\rm d}\cos(\omega_{\rm d} t)
 \left\{
 \hat{X}_0 + [\hat{X}_0, \hat{S}] 
 + \frac{1}{2}[[\hat{X}_0, \hat{S}], \hat{S}]
 + O(g^3)
 \right\}\nonumber\\
 &= \hbar\varOmega_{\rm d}\cos(\omega_{\rm d} t)
 \left\{
    \left(
        1-\frac{g^2}{2(\omega_0-\omega_1)^2}
    \right)
 \hat{X}_0 
 - \frac{g}{\omega_0-\omega_1}\hat{Z}_0\otimes\hat{X}_1 
 + O(g^3)
 \right\}.
\end{align}
$$

次にこのSW変換後のハミルトニアン$\hat{H}'=\hat{H}'_{\rm static} + \hat{H}'_{\rm drive}$に対して, それぞれのqubitの（SW変換後の）共鳴周波数$\omega_0':=\omega_0+\frac{g^2}{\omega_0-\omega_1}$, $\omega_1':=\omega_1-\frac{g^2}{\omega_0-\omega_1}$での回転座標変換を行い, Z回転が見えないフレームに乗ることを考える. 
駆動項$\hat{H}'_{\rm drive}$の駆動周波数は$\omega_1'$と選ぶ. 
変換後のハミルトニアン$\hat{H}'_{\rm r}$は以下のように表せる:

$$
\begin{align}
\hat{H}'_{\rm r} 
&= \hbar\varOmega_{\rm d}\cos(\omega'_1 t)
 \Bigg\{
    \left(
        1-\frac{g^2}{2(\omega_0-\omega_1)^2}
    \right)
 \left[\cos(\omega'_0 t)\hat{X}_0 + \sin(\omega'_0 t)\hat{Y}_0 \right]\nonumber\\ 
 & \hspace{3cm}
 - \frac{g}{\omega_0-\omega_1}\hat{Z}_0\otimes \left[\cos(\omega'_1 t)\hat{X}_1 + \sin(\omega'_1 t)\hat{Y}_1 \right]
 + O(g^3)
 \Bigg\}.
\end{align}
$$

さらにcosとsinを指数関数で展開し, ゼロ周波数成分以外（$2\omega'_0$, $2\omega'_1$, $\omega'_0-\omega'_1$）の項を回転波近似で無視すると, 

$$
\begin{align}
\hat{H}'_{\rm r} \approx
-\hbar\mu\hat{Z}_0\otimes\hat{X}_1
\qquad
\mu:=
-\frac{\varOmega_{\rm d} g}{2(\omega_0-\omega_1)}
\end{align}
$$

という形の実効ハミルトニアンが得られる.  

$\hat{H}'_{\rm r}$はブロック対角な形

$$
\begin{align}
\hat{H}'_{\rm r} \approx
-\hbar\mu
\left(
\ket{0}\bra{0}\otimes\hat{X}_1
-\ket{1}\bra{1}\otimes\hat{X}_1
\right)
=-\hbar\mu
\left[
\begin{array}{c|c}
\hat{X} & 0 \\
\hline
0 & -\hat{X} \\
\end{array}
\right]
\end{align}
$$

であるため, ユニタリ時間発展も以下のようなブロック対角な形で表せる:

$$
\begin{align}
\hat{U}(t) &= \exp\left(\frac{-{\rm i}\hat{H}'_{\rm r}t}{\hbar}\right)
\nonumber\\
&=
\ket{0}\bra{0}\otimes\exp\left(-{\rm i}\mu t\hat{X}\right)
+\ket{1}\bra{1}\otimes\exp\left({\rm i}\mu t\hat{X}\right)\nonumber\\
&=
\ket{0}\bra{0}\otimes\hat{R}_x\left(2\mu t\right)
+\ket{1}\bra{1}\otimes\hat{R}_x\left(-2\mu t\right)
\end{align}
$$

これはつまり, Q0（制御qubit）が$\ket{0}$の時にはQ1（標的qubit）はX軸回りに角速度$+2\mu$で回転し, $\ket{1}$の時にはQ1はX軸回りに角速度$-2\mu$で回転するという制御回転ゲートが実現できることを意味している. 
特に$2\mu t=\pi/2$と選んだ場合:

$$
\begin{align}
\hat{U}_{\rm ZX90}:=\hat{U}\left(\frac{\pi}{4\mu}\right) 
=
\ket{0}\bra{0}\otimes\hat{R}_x\left(\frac{\pi}{2}\right)
+\ket{1}\bra{1}\otimes\hat{R}_x\left(-\frac{\pi}{2}\right)
\end{align}
$$

これは**ZX<sub>90</sub>ゲート**と呼ばれ, セパラブルな状態から最大エンタングル状態を生成することができる.  

また, $\hat{H}'_{\rm r}$は以下の形でも表せる:

$$
\begin{align}
\hat{H}'_{\rm r} \approx
-\hbar\mu
\left(
\hat{Z}_0\otimes\ket{+}\bra{+}
-\hat{Z}_0\otimes\ket{-}\bra{-}
\right)
\end{align}
$$

したがってユニタリ時間発展も以下のようなブロック対角な形でも表せる:

$$
\begin{align}
\hat{U}(t) &= \exp\left(\frac{-{\rm i}\hat{H}'_{\rm r}t}{\hbar}\right)
\nonumber\\
&=
\hat{R}_z\left(2\mu t\right)\otimes\ket{+}\bra{+}
+\hat{R}_z\left(-2\mu t\right)\otimes\ket{-}\bra{-}.
\end{align}
$$

これはつまり, 制御qubitと標的qubitの役割を入れ替えて, Q1（制御qubit）が$\ket{+}$の時にはQ0（標的qubit）はZ軸回りに角速度$+2\mu$で回転し, $\ket{-}$の時にはQ0はZ軸回りに角速度$-2\mu$で回転するという制御回転ゲートが実現できることを意味している.  

ZX<sub>90</sub>ゲートは, 1 qubitゲートと組み合わせることで**CNOTゲート**が実現できる. 
具体的には以下の組み合わせでCNOTゲートが実現できる:

$$
\begin{align}
\hat{U}_{\rm ZX90}
\left[\hat{R}_z\left(-\frac{\pi}{2}\right)\otimes\hat{R}_x\left(-\frac{\pi}{2}\right)\right]
&=
\left[\hat{R}_z\left(-\frac{\pi}{2}\right)\otimes\hat{R}_x\left(-\frac{\pi}{2}\right)\right]
\hat{U}_{\rm ZX90} \nonumber\\
&=
\begin{bmatrix}
1&0&0&0\\
0&1&0&0\\
0&0&0&1\\
0&0&1&0\\
\end{bmatrix} \nonumber\\
&= \hat{U}_{\rm CNOT}.
\end{align}
$$





