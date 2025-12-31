


## Schrieffer-Wolff変換

いま, 無摂動ハミルトニアン$\hat{H}_0$と摂動$\hat{V}$からなる以下のハミルトニアン$\hat{H}_0$を考える:

$$
\begin{align}
 \hat{H}=\hat{H}_0+\hat{V},
\end{align}
$$

ただし$\hat{V}$は微小パラメータ$\epsilon$ ($\epsilon\ll 1$)の1次式で表せると仮定する. 
例えば$\hat{H}_0$は結合がないときの各qubitや共振器の自由ハミルトニアンであり, その固有値$E_n$や固有状態$\ket{n}$は既知であると仮定する. 
一方$\hat{V}$は$\hat{H}_0$の基底では対角成分を持たないと仮定する. 

ここで目指すのは, ユニタリ変換

$$
\begin{align}
 \hat{H}\rightarrow\hat{H}'={\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}}\quad(\hat{S}\text{は反エルミート演算子})
\end{align}
$$

によって, $O(\epsilon^3)$の項を除いて$\hat{H}_0$の基底で対角的となるような$\hat{S}$を探すことである. 
Baker--Campbell--Hausdorffの補助公式より,

$$
\begin{align}
 \hat{H}'= {\rm e}^{-\hat{S}}\hat{H}{\rm e}^{\hat{S}}
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

となる. 
$\hat{S}$として, 

$$
\begin{align}
 \hat{S}=-\sum_{m,n}\frac{\bra{m}{\hat{V}}\ket{n}}{E_m-E_n}\ket{m}\bra{n}
\end{align}
$$

と選べば, 1つ目の条件$\hat{V} + [\hat{H}_0,\hat{S}] = 0 $は満たされる.
確かに,

$$
\begin{align}
 &\hat{V} + [\hat{H}_0,\hat{S}]
=\hat{V} -\sum_{m,n}E_m\frac{\bra{m}{\hat{V}}\ket{n}}{E_m-E_n}\ket{m}\bra{n}
+ \sum_{m,n}E_n\frac{\bra{m}{\hat{V}}\ket{n}}{E_m-E_n}\ket{m}\bra{n}
=\hat{V} - \sum_{m,n}\ket{m}\bra{m}\hat{V}\ket{n}\bra{n} =0.
\end{align}
$$

2つ目の条件は必ずしも満たされるわけではないが, 回路QEDの領域で現れる$\hat{V}$ではこの条件が満たされる場合が多い. 
このようにして摂動つきハミルトニアンの近似的な対角化が行われ, 結果として

$$
\begin{align}
\hat{H}' = \hat{H}_0 + \frac{1}{2}[\hat{V},\hat{S}]+O(\epsilon^3)
\end{align} 
$$

が得られる. 

$\hat{H}'$の固有値, 固有状態をそれぞれ$E_n'$, $\ket{n}'$とする. 
固有方程式は$\hat{H}'\ket{n}'=E_n'\ket{n}'$であり, 両辺に左から${\rm e}^{\hat{S}}$をかけると,

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
 \ket{n}'={\rm e}^{-\hat{S}}\ket{n} = \left(1-\hat{S}\right)\ket{n}+O(\alpha^2).
\end{align}
$$

したがって, SW変換によって対角化できたからといって, 変換前の固有状態が時間発展で変化しないわけではないことに注意する必要がある. 


### 結合2量子系のハミルトニアンのSW変換

式~(\ref{eq:1})のSW変換を考える. 
摂動非対角項$\hat{V}$を計算基底で展開すると, 

$$
\begin{align}
\hat{V}
&=\hbar g(\hat{a}^\dag\hat{b}+{\rm H.c.})\nonumber\\
%
&=\hbar g
\sum_{jk}\sqrt{(j+1)(k+1)}\ket{j+1}\bra{j}\otimes\ket{k}\bra{k+1}
+{\rm H.c.}
\end{align}
$$

と表せる.
ここで$\hat{S}$を

$$
\begin{align}
\hat{S}&=-\sum_{klmn}\frac{\bra{kl}{\hat{V}}\ket{mn}}{E_{kl}-E_{mn}}\ket{kl}\bra{mn}\nonumber\\
%
&=-g\sum_{jk}\frac{\sqrt{(j+1)(k+1)}}{\varDelta_{ab}+\alpha_a j - \alpha_b k}
\left(\ket{j+1}\bra{j}\otimes\ket{k}\bra{k+1}
-{\rm H.c.}\right)
\end{align}
$$

(ただし$\varDelta_{ab}:=\omega_a-\omega_b$)と選ぶと, 

$$
\begin{align}		
[\hat{V},\hat{S}]
&=\hbar g^2\sum_{jk}
\frac{\sqrt{(j+1)(k+1)}}{\varDelta_{ab}+\alpha_a j-\alpha_b k}
\Big[
\sqrt{j(k+2)}
\left(\ket{j+1}\bra{j-1}\otimes\ket{k}\bra{k+2}+{\rm H.c.}\right)
\nonumber\\
&\hspace{5cm}
-\sqrt{(j+2)k}
\left(\ket{j+2}\bra{j}\otimes\ket{k-1}\bra{k+1}+{\rm H.c.}\right)
\nonumber\\
&\hspace{2cm}
+2\sqrt{(j+1)(k+1)}
\left(\ket{j+1}\bra{j+1}\otimes\ket{k}\bra{k}
-\ket{j}\bra{j}\otimes\ket{k+1}\bra{k+1}\right)
\Big]
\end{align}
$$

となる.
この$\hat{S}$を用いてSW変換を行うと,   

$$
\begin{align}
\hat{H}'&=\hat{H}_0+\frac{1}{2}[\hat{V},\hat{S}]
+O\left[\varDelta_{ab}\left(\frac{g}{\varDelta_{ab}}\right)^3\right]\nonumber\\
%
&\approx
\sum_{j}\hbar\omega_a^{(j)}\ket{j}\bra{j}\otimes\hat{1}
+\sum_{k}\hbar\omega_b^{(k)}\hat{1}\otimes\ket{k}\bra{k}\nonumber\\
&\qquad
+\hbar g^2\sum_{jk}
\frac{(j+1)(k+1)}{\varDelta_{ab}+\alpha_a j-\alpha_b k}
\left(\ket{j+1}\bra{j+1}\otimes\ket{k}\bra{k}
-\ket{j}\bra{j}\otimes\ket{k+1}\bra{k+1}\right)
\nonumber\
%
&\qquad
+\frac{\hbar g^2}{2}\sum_{jk}
\frac{\sqrt{(j+1)(k+1)}}{\varDelta_{ab}+\alpha_a j-\alpha_b k}
\Big[
\sqrt{j(k+2)}
\left(\ket{j+1}\bra{j-1}\otimes\ket{k}\bra{k+2}+{\rm H.c.}\right)
\nonumber\\
&\hspace{6cm}
-\sqrt{(j+2)k}
\left(\ket{j+2}\bra{j}\otimes\ket{k-1}\bra{k+1}+{\rm H.c.}\right)
\Big]
\end{align}
$$

となる. 
第4項目以降に非対角項が残っており, この一般形のハミルトニアンを対角化するにはさらに高次のSW変換を行っていく必要がある. 
ただし次節で取り上げるような2準位系, 調和振動子の場合はこの非対角項は0となるため, この時点で対角化が完了している. 

## 結合2量子系のハミルトニアンのSW変換の具体例

### 2つの2準位系の場合

2準位系を考える場合は, $\{\ket{0},\ket{1}\}$で張られる空間成分だけを抜き出せば良い.
その場合,

$$
\begin{align}
\hat{H}'
&=\hbar\omega_a\ket{1}\bra{1}\otimes\hat{1}
+\hbar\omega_b\hat{1}\otimes\ket{1}\bra{1}
+\frac{\hbar g^2}{\varDelta_{ab}}(\ket{1}\bra{1}\otimes\ket{0}\bra{0}-\ket{0}\bra{0}\otimes\ket{1}\bra{1})\nonumber\\
&\qquad
+2\hbar g^2\frac{\alpha_a+\alpha_b}{(\varDelta_{ab}+\alpha_a)(\varDelta_{ab}-\alpha_b)}\ket{1}\bra{1}\otimes\ket{1}\bra{1}\nonumber\\
%
&=\hbar\left({\omega}_a+\frac{g^2}{\varDelta_{ab}}\right)\hat{a}^\dag\hat{a}
+\hbar\left({\omega}_b-\frac{g^2}{\varDelta_{ab}}\right)\hat{b}^\dag\hat{b}
+
2\hbar \xi
\hat{a}^\dag\hat{a}
\hat{b}^\dag\hat{b}\nonumber\\
%
&=\hbar\left({\omega}_a+\frac{g^2}{\varDelta_{ab}}\right)\ket{10}\bra{10}
+\hbar\left({\omega}_b-\frac{g^2}{\varDelta_{ab}}\right)\ket{01}\bra{01}
+
\hbar(\omega_a+\omega_b+2\xi)\ket{11}\bra{11}\\
%
\xi&:=
g^2\left(\frac{1}{\varDelta_{ab}-\alpha_b} - \frac{1}{\varDelta_{ab}+\alpha_a}\right)
=g^2\frac{\alpha_a+\alpha_b}{(\varDelta_{ab}+\alpha_a)(\varDelta_{ab}-\alpha_b)}
\end{align}
$$

と表せる. 
ただし$\hat{a},\hat{b}=\ket{0}\bra{1}$, $\hat{a}^\dag\hat{a},\hat{b}^\dag\hat{b}=\ket{1}\bra{1}$を用いた. 
このように計算基底や生成消滅演算子で表した形式ではエネルギー準位の高さが理解しやすく, 基底エネルギーに対して$\ket{10}$のエネルギーは$\omega_a$から$+g^2/\varDelta_{ab}$, $\ket{01}$のエネルギーは$\omega_b$から$-g^2/\varDelta_{ab}$, 
$\ket{11}$のエネルギーは$\omega_a + \omega_b$から$2\xi$だけずれることがわかる\footnote{
$2\xi$の形は, ge遷移-ef遷移, ef遷移-ge遷移の相互作用によるラムシフトが同時に起きていると考えると理解しやすい:

$$
\begin{align}
2\xi = \frac{(\sqrt{2}g)^2}{\omega_a-(\omega_b+\alpha_b)} - \frac{(\sqrt{2}g)^2}{(\omega_a+\alpha_a)-\omega_b}.
\end{align}
$$

$\sqrt{2}$の因子は昇降演算子の係数により現れる値である. 
}.


またパウリ演算子を用いて表すと, $\ket{1}\bra{1}=(\hat{1}-\hat{Z})/2$を代入して定数項を除くと,

$$
\begin{align}
\hat{H}'
&=
-\hbar\left({\omega}_a+\frac{g^2}{\varDelta_{ab}}+\xi\right)\frac{\hat{Z}\otimes\hat{1}}{2}
-\hbar\left({\omega}_b-\frac{g^2}{\varDelta_{ab}}+\xi\right)\frac{\hat{1}\otimes\hat{Z}}{2}
+\hbar\xi\frac{\hat{Z}\otimes\hat{Z}}{2}\nonumber\\
%
&=
\hbar\left(-\frac{\omega_a+\omega_b}{2}-\frac{\xi}{2}\right)\ket{00}\bra{00}
+\hbar\left(-\frac{\omega_a-\omega_b}{2}-\frac{g^2}{\varDelta_{ab}}-\frac{\xi}{2}\right)\ket{01}\bra{01}\nonumber\\
&\quad
+\hbar\left(\frac{\omega_a-\omega_b}{2}+\frac{g^2}{\varDelta_{ab}}-\frac{\xi}{2}\right)\ket{10}\bra{10}
+\hbar\left(\frac{\omega_a+\omega_b}{2}+2\xi-\frac{\xi}{2}\right)\ket{11}\bra{11}
\end{align}
$$

と表せる. 
パウリ演算子を用いた形式は, 全エネルギー準位の平均値を基準とした表記である.
B系が$\ket{0}$, $\ket{1}$の時, A系のge遷移周波数はそれぞれ$\omega_a+g^2/\varDelta_{ab}$, $\omega_a+g^2/\varDelta_{ab}+2\xi$と異なる値をとる. 
回転座標系を考える時はその平均値$\omega_a+g^2/\varDelta_{ab}+\xi$を回転周波数にとることが一般的である.  
この値は$\hat{Z}\otimes\hat{1}/2$の係数と等しいため, 回転座標変換により$\hat{Z}\otimes\hat{1}/2$の項はすっきり消える($\hat{1}\otimes\hat{Z}/2$の項についても同様). 







### 外部駆動項がある場合のSW変換

2つの量子系のうち, 一方(A系)が外部から駆動されているハミルトニアンに対するSW変換を考える. 
この駆動項はSW変換でも対角化されないため, この項の影響により2つの量子系を外部制御によりエンタングルさせることができる. 
外部駆動項は以下の形で表せる.
文献によっては$\hat{a}+\hat{a}^\dag$ではなく$-{\rm i}(\hat{a}-\hat{a}^\dag)$の形を用いている場合があるが, これは$\ket{j}\rightarrow(-{\rm i})^j\ket{j}$とゲージ変換することにより本稿の形にすることができるため, 物理的に等価な議論である.

$$
\begin{align}
 \hat{H}\sub{d}
&=
\hbar\varOmega\cos(\omega\sub{d}t)(\hat{a}+\hat{a}^\dag)\otimes\hat{1}\nonumber\\
%
&=
\hbar\varOmega\cos(\omega\sub{d}t)
\sum_i\sqrt{i+1}(\ket{i}\bra{i+1}\otimes\ket{i+1}\bra{i})\otimes\hat{1}.
\end{align}
$$

SW変換の$\hat{S}$は上で用いた式~(\ref{eq:4})を用いる:

$$
\begin{align}
\hat{S}
&=-g\sum_{jk}\frac{\sqrt{(j+1)(k+1)}}{\varDelta_{ab}+\alpha_a j - \alpha_b k}
\left(\ket{j+1}\bra{j}\otimes\ket{k}\bra{k+1}
-{\rm H.c.}\right).
\end{align}
$$

SW変換後の駆動項は以下のように表される:

$$
\begin{align}
 \hat{H}\sub{d}'= {\rm e}^{-\hat{S}}\hat{H}\sub{d}{\rm e}^{\hat{S}}
&= \hat{H}\sub{d} + [\hat{H}\sub{d},\hat{S}] + \frac{1}{2}[[\hat{H}\sub{d},\hat{S}],\hat{S}]+O(\epsilon^3).
\end{align}
$$

以下, 各項の具体的な形を導出する. 
簡単のため, ここでは量子系は2準位系または調和振動子であることを仮定する. 
この仮定により, $\hat{S}$の$1/(\varDelta_{ab}+\alpha_a j-\alpha_b k)$が$j,k$に依存しなくなり総和の外に出せるため, 計算結果が比較的シンプルになる. 
この仮定の下での計算結果を以下に示す:

$$
\begin{align}
 [\hat{H}\sub{d},\hat{S}]
&=
-\hbar g\varOmega\cos(\omega\sub{d}t)
\sum_{jk}\frac{(j+1)\sqrt{k+1}}{\varDelta_{ab}+\alpha_a j-\alpha_b k}\nonumber\\
&\qquad\times(\ket{j}\bra{j}-\ket{j+1}\bra{j+1})\otimes
(\ket{k}\bra{k+1}+\ket{k+1}\bra{k}),\\
%
[[\hat{H}\sub{d},\hat{S}],\hat{S}]&=0.
\end{align}
$$

### 外部駆動項がある場合のSW変換の具体例

#### 2つの2準位系の場合

$$
\begin{align}
 \hat{H}\sub{d}'
=
\hbar\varOmega\cos(\omega\sub{d}t)
\left[
\hat{X}\otimes\hat{1}
-\frac{g}{\varDelta_{ab}+\alpha_a}\hat{1}\otimes\hat{X}
-\frac{g\alpha_a}{\varDelta_{ab}(\varDelta_{ab}+\alpha_a)}\hat{Z}\otimes\hat{X}
\right].
\end{align}
$$

この項は交差共鳴ゲートをもたらす. 












