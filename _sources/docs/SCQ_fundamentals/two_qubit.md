# 2 qubit

## 結合2 qubit系

2qubit周波数が同じときと, 十分離れている時の2通りを説明する.  

Schrieffer-Wolff変換は軽く気持ちを説明する. 
qubit系での計算では常在ZZは出てこないが, 軽く言及する.  
SW変換の気持ちを説明する. 

## CZゲート

周波数可変型の場合. 

## 交差共鳴ゲート

クロストークは出てこない.  
CNOTゲートの作り方. 







いいね、その“別ルート”の骨子は合っています。ここでは、完全に行列（3準位×3準位）に落として、どこで $\cos(\phi_0-\phi_1)$ や $\alpha_i$・4本の分母が出るのかを、計算の手触りが残る形で丁寧に辿ります。結論は最後に再掲します。

⸻

A) 準備：3準位Duffing＋回転枠＋RWA

各トランズモン $i\in\{0,1\}$ を $|0\rangle,|1\rangle,|2\rangle$ に切り詰め、回転枠（$\omega_d$）＋RWA に移します。
	•	数演算子 $n_i=a_i^\dag a_i$（行列表現：$a=|0\rangle\langle1|+\sqrt2\,|1\rangle\langle2|$）。
	•	$\Delta_{i,d}=\omega_i-\omega_d, \beta_i=\Omega_i e^{i\phi_i}$。

$$
\begin{aligned}
H_0 &= \sum_i\Big(\Delta_{i,d}\,n_i+\tfrac{\alpha_i}{2}n_i(n_i-1)\Big),\\
H_J &= J\,(a_0+a_0^\dag)(a_1+a_1^\dag),\\
H_d &= \sum_i \tfrac12\big(\beta_i a_i^\dag+\beta_i^\ast a_i\big).
\end{aligned}
$$

⸻

B) 第1段：駆動をSWで消去 → 対角（縦）ACシュタルク

「$[H_0,S_\Omega]=-H_d$ を満たす」反エルミート生成子を取ると
$S_\Omega = -\sum_i \frac12\big(\beta_i\Lambda_i-\beta_i^\ast\Lambda_i^\dag\big),
\quad
\Lambda_i=\frac{|1\rangle\!\langle0|}{\Delta_{i,d}}+\frac{\sqrt2\,|2\rangle\!\langle1|}{\Delta_{i,d}+\alpha_i}$.
（$[H_0,\Lambda_i]=a_i^\dag$ に注意。）

2次の有効ハミルトニアンは
$H_{\rm eff}
= e^{S_\Omega}(H_0+H_J+H_d)e^{-S_\Omega}
\simeq H_0+H_J+\underbrace{\tfrac12[S_\Omega,H_d]}_{\text{各ビットのACシュタルク}}
	•	\underbrace{\tfrac12[S_\Omega,[S_\Omega,H_J]]}_{\color{#C00}{\Omega^2J\;\text{項(ZZの源)}}}
+\cdots$ .

ここで、後で効いてくる交換子
$D_i\equiv[\Lambda_i,a_i]
= -\frac{|0\rangle\langle0|}{\Delta_{i,d}}
+\Big(\frac{1}{\Delta_{i,d}}-\frac{2}{\Delta_{i,d}+\alpha_i}\Big)|1\rangle\langle1|
+\frac{2}{\Delta_{i,d}+\alpha_i}|2\rangle\langle2|$
は完全に対角です。
$|0\rangle$ と $|1\rangle$ の差分
$\delta D_i\equiv\langle1|D_i|1\rangle-\langle0|D_i|0\rangle
=\frac{2}{\Delta_{i,d}}-\frac{2}{\Delta_{i,d}+\alpha_i}
=\frac{2\alpha_i}{\Delta_{i,d}(\Delta_{i,d}+\alpha_i)}$
\tag{★}
が後で Z 成分に写ります。ここで早くも「下枝 $\Delta_{i,d}$ と上枝 $\Delta_{i,d}+\alpha_i$ の直列」が現れています。

⸻

C) 第2段：交換結合 H_J の“二重ドレッシング” → ZZ

肝は
$\tfrac12[S_\Omega,[S_\Omega,H_J]]$.
$S_\Omega=S_{\Omega,0}+S_{\Omega,1}$ と分け、$H_J=J(a_0+a_0^\dag)(a_1+a_1^\dag)$ に対して (0を1回)(1を1回) のクロス項だけを拾います（同じビットで2回は1体項や定数に落ちる）：

1回目の交換で
$[S_{\Omega,0},a_0] = -\tfrac12(\beta_0 D_0-\beta_0^\ast D_0)$,
$[S_{\Omega,1},a_1] = -\tfrac12(\beta_1 D_1-\beta_1^\ast D_1)$
（$D_i$ は実対角なので $\dagger$ を省略可）。

さらにもう一度別ビットで交換すると、
$\tfrac12[S_\Omega,[S_\Omega,H_J]]
\;\Rightarrow\;
\frac{J}{2}\,\big(\beta_0\beta_1^\ast+\beta_0^\ast\beta_1\big)\;
\frac{D_0^{(01)}D_1^{(01)}}{4}
\;+\;(\text{1体項と定数})$.
ここで $D_i^{(01)}$ は $|0\rangle,|1\rangle$ 部分へ射影した $D_i$。
$\beta_0\beta_1^\ast+\beta_0^\ast\beta_1=2\Omega_0\Omega_1\cos(\phi_0-\phi_1)$ なので位相差の実部が効きます（$\cos(\phi_0-\phi_1)$ の由来）。

次に、二体系の $|00\rangle,|01\rangle,|10\rangle,|11\rangle$ の対角要素から $Z\otimes Z$ の係数だけを抽出する組合せ
$f_{11}+f_{00}-f_{10}-f_{01}$
を取ると、「各ビットで $|1\rangle$ と $|0\rangle$ の差」すなわち $\delta D_0\delta D_1$ が出ます。式(★)を代入して
$\delta D_0\,\delta D_1
=\frac{4\,\alpha_0\alpha_1}{\Delta_{0,d}\Delta_{1,d}(\Delta_{0,d}+\alpha_0)(\Delta_{1,d}+\alpha_1)}$.
係数の数え上げは
	•	交換順序（0→1, 1→0）で $\times2$
	•	実部取り（$\beta_0\beta_1^\ast+\text{c.c.}$）で $\times2$
	•	ただし前因子の $\tfrac12$ と、$S_\Omega$ 内の $\tfrac12$ が2回で $\div 4$
→ 全体として $\times2$ が残ります。

よって $\Omega^2J$ 次の ZZ 係数 は
$\boxed{
\tilde\nu_{ZZ}^{(\text{siZZle})}
=\frac{2J\,\alpha_0\alpha_1\,\Omega_0\Omega_1\cos(\phi_0-\phi_1)}
{\Delta_{0,d}\Delta_{1,d}(\Delta_{0,d}+\alpha_0)(\Delta_{1,d}+\alpha_1)}
}$.

⸻

D) 静的ZZを足して最終式

静的な（駆動なしの）2体分散相互作用は J^2 の2次摂動から出て
\nu_{ZZ,\rm s}
= -\frac{2J^2(\alpha_0+\alpha_1)}{(\alpha_1-\Delta_{01})(\alpha_0+\Delta_{01})},
\qquad \Delta_{01}=\omega_0-\omega_1,
（標準結果）なので、合成すれば
\boxed{
\tilde\nu_{ZZ}
= \nu_{ZZ,\mathrm{s}}
+\frac{2J\,\alpha_0\alpha_1\,\Omega_0\Omega_1\cos(\phi_0-\phi_1)}
{\Delta_{0,d}\Delta_{1,d}(\Delta_{0,d}+\alpha_0)(\Delta_{1,d}+\alpha_1)} }.

⸻

物理チェック（妥当性）
	•	\alpha_i\!\to\!0（線形振動子）で \tilde\nu_{ZZ}^{(\text{siZZle})}\to 0（ZZは消える）
	•	\phi_0-\phi_1=\pi で最小振幅で静的ZZを打ち消せる（符号反転）
	•	4本の分母は「二系×二枝」の仮想遷移の直列

⸻

必要なら、この導出を9×9の行列での数値対角化と比較して（弱駆動・大デチューニングでの一致、強駆動でのずれ）をその場で検算するミニコードも用意できます。パラメータ（\omega_{0,1},\alpha_{0,1},J,\omega_d,\Omega_{0,1},\phi_{0,1}）を教えてください。