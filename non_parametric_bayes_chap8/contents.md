class: center, middle

# ノンパラメトリックベイズ 
## 点過程と統計的機械学習の数理
### Chapter 8. 測度論の基礎

---

### 測度論的確率論の動機(1/2)

確率を扱う上で大きく2つの理論的枠組みがある。

* 古典的確率論
    * 大抵の統計の本はこっち
* 測度論的確率論
    * 数学の確率論の本はこっち
    * 無限回の試行に対する理論的な解析を与える

次の例は測度論的確率論に対する一つのモチベーションを与える。

#### 例
以下を満たすような$(\Omega, \mathcal{F}, P), A, F\_{\alpha} \in \mathcal{F} (\alpha \in A)$が存在する。
$(\Omega, \mathcal{F}, P)$は確率空間とし、$A$は添え字集合で

$$
\forall \alpha \in A, P(F\_{\alpha}) = 1
$$

だが、

$$
P(\bigcap\_{\alpha \in A} F\_{\alpha}) = 0.
$$

---

### 測度論的確率論の動機(2/2)

実際、コイン投げの無限回試行を考えると 裏表のあるコインを投げ、表の場合は$H$とし、裏の場合は$T$で表すとする。
$(\Omega, \mathcal{F}, P)$を次のように作る。
$\Omega = [0, 1]$として、$\omega \in \Omega$について、$\omega$の2進展開を$0.\omega\_{1}\omega\_{2}\ldots$とかく。
ここで、$\omega\_{k} \in \\{0, 1\\}$はである。
$0$を$H$とし、$1$を$T$とすると、$\omega$は無限回のコイン投げの1回の試行に対応する。
ここで、$\mathcal{F}$を次で定義する。

$$
\mathcal{F} := \sigma(\\{ \omega \in \Omega \mid \omega\_{n} = W \\}\_{n \in \mathbb{N}, W \in \\{H, T \\}}).
$$

更に$P$を$[0, 1]$上のルベーグ測度とする。
$A := \\{\alpha:\mathbb{N} \rightarrow \mathbb{N} \mid \alpha(1) < \alpha(2) < \ldots \\}$で

$$
\forall \alpha \in A, 
F\_{\alpha} 
:= \left\\{ \omega \mid \frac{\\{k \le n \mid \omega\_{\alpha(k)} = H\\}}{n} \rightarrow \frac{1}{2} \right\\} \in \mathcal{F},
$$

とおけばよい。

---

### 測度論の動機(1/3)

この章では、測度論における主主の概念の定義と確率論との対応を見る。
* 測度論の一つの目標は、積分論の理論的整理である。
    * 高校数学で扱っていた積分(リーマン積分)は理論的に扱いにくいものだった。
    * 測度を用いて積分(ルベーグ積分）を定義することで、理論的に扱いやすい積分得る。

具体的には次の極限操作が問題となる。
1. 被積分関数の極限の積分と被積分関数の積分の極限が一致するのはいつか？
2. 微分と積分の順序交換できるのはいつか？

---

### 測度論の動機(2/3)

1の例を見る為に、リーマン積分の定義を思い出してみる。
$a, b \in \mathbb{R}$、$f:\mathbb{R} \rightarrow \mathbb{R}$を$[a, b]$上有界な関数とする。
$\Delta\_{a}^{b} : a = x\_{0}  < x\_{1} < \ldots, < x\_{k} = b$を$[a, b]$の分割とし、$| \Delta\_{a}^{b} | := \max\_{1 \le i \le k}(x\_{i} - x\_{i-1})$とする。
分割$\Delta\_{a}^{b}$の区間$[x\_{i-1}, x\_{i}]$上のある点を$c\_{i}^{\Delta\_{a}^{b}} \in [x\_{i-1}, x\_{i}]$とかくと、$[a, b]$上の$f$のリーマン積分は、以下の極限が存在する時定義される。

$$
\int\_{a}^{b}f(x)\,dx 
:= \lim\_{|\Delta\_{a}^{b}| \rightarrow 0}f(c\_{i}^{\Delta\_{a}^{b}})(x\_{i} - x\_{i-1})
$$

更に、$f$の$\mathbb{R}$上の積分は次の広義積分として定義される。

$$
\int\_{-\infty}^{\infty}f(x)\,dx 
:= \lim\_{a \rightarrow -\infty, b \rightarrow \infty}\lim\_{|\Delta\_{a}^{b}| \rightarrow 0}f(c\_{i}^{\Delta\{a}^{b}})(x\_{i} - x\_{i-1})
$$

ここで、$g\_{n} \rightarrow g (n \rightarrow \infty)$なる$g\_{n} (\forall n \in \mathbb{N}), g$が存在したとする。
このとき、以下が成り立つのは？

$$
\lim\_{n \rightarrow \infty} \int\_{-\infty}^{\infty}g\_{n}(x)\,dx 
= \int\_{-\infty}^{\infty}g(x)\,dx 
$$

---

### 測度論の動機(3/3)
先ほどの例として次の問題がある。

####例
$\displaystyle G(t) := \int\_{0}^{\infty}\frac{\sin tx}{1 + x^{2}}\,dx $は$t$について連続である。

実際、ルベーグ積分の場合は、

$$
\left| \frac{\sin tx}{1 + x^{2}} \right| \le \frac{1}{1 + x^{2}}
$$

かつ、$\frac{1}{1 + x^{2}}$が$[0, \infty]$上可積分より、ルベーグの収束定理から$t \in [0, \infty]$について、

$$
t\_{n} \rightarrow t, \lim\_{n \rightarrow \infty} G(t\_{n}) = G(t),
$$

となって、$G$は連続である。

---

### 8.1 可測空間、測度空間、確率空間

積分は面積を測る道具であったを思い出す。
ここでは、面積を測るのに必要な道具立てを行い、面積が測れる集合(可測集合）とは何か、また面積を測る為の道具（測度）が満たすべき性質を示す。

####定義8.1 $\sigma$-加法族($\sigma$-algebra)、可測集合(measurable set)、可測空間(measurable space)
$\Omega$:集合、$\mathcal{F} \subseteq 2^{\Omega}$とする。 
$\mathcal{F}$が以下を満たすとき、$\Omega$上の$\sigma$-加法族($\sigma$-algebra or $\sigma$-field)という。
1. $\emptyset \in \mathcal{F}$
2. $A \in \mathcal{F} \Rightarrow A^{C} \in \mathcal{F}$
3. $A\_{n} \in \mathcal{F} \(\forall n \in \mathbb{N}\) \Rightarrow \cup\_{n=1}^{\infty} A\_{n} \in \mathcal{F}$

$\sigma$-加法族の元を可測集合(measurable set)と呼ぶ。
また、$(\Omega, \mathcal{F})$を可測空間(measurable sp.)と呼ぶ。

---

#### 定義8.2 測度(measure)、測度空間(measure space)、有限測度(finite measure)、$\sigma$-有限測度($\sigma$-finite measure)
$(\Omega, \mathcal{F})$を可測空間とする。
関数$\mu: \mathcal{F} \rightarrow \mathbb{R}_{\ge 0}$が次の条件を満たす時、$(\Omega, \mathcal{F})$上の測度(measure)という。
1. $\mu(A) \ge 0 \ (\forall A \in \mathcal{F})$
2. $\mu(\emptyset) = 0$
3. $A\_{n} \in \mathcal{F} (\forall n \in \mathbb{N}), A\_{n} \cap A\_{m} = \emptyset (n \neq m)$

$$
\Rightarrow \mu(\bigcup\_{n=1}^{\infty}A\_{n}) = \sum\_{n=1}^{\infty}\mu(A\_{n})
$$

#### Remark
測度$\mu$の定義で、$\mu$の値域が本とは異なる。
* 本の値域は$\bar{\mathbb{R}}$で、無限大を含む(上は含んでいない)。
    * この先の証明の煩雑さを省く為
* 本の値域は$\mathbb{R}$と負の値をとることを許すが、$0$以上に限定している。
    * 負の値をとることを許す場合は符号付き測度と呼ぶ場合が多い。
    * ルベーグ積分の定義には、負の値をとること自体は不要。
    * ルベーグ-スティルチェス積分の定義に必要となる。

---

#### 定義8.3 確率測度(propability measure)、確率空間(probability space)、標本空間(sample measure)、事象(event)、事象の族(family of events)
$(\Omega, \mathcal{F}, P)$を測度空間とする。
* $P(\Omega)=1$のとき、$(\Omega, \mathcal{F}, P)$を確率空間(prob. sp.)と呼ぶ。
* 確率空間上の$P$を確率測度(prob. measure)という。
* $\Omega$は標本空間(Sample sp.)と呼ぶ。
* $A \in \mathcal{F}$は事象(event)と呼ぶ。
* $\mathcal{F}$は事象の族(family of events)と呼ぶ。

#### コメント
事象は、確率が測れるような現象のこと。
確率が測れないものも存在する。

#### Remark
測度空間$(\Omega, \mathcal{F}, \mu)$において、$\mu$が有限測度であれば、$P(A):=\mu(A)/\mu(\Omega)$とすることで$(\Omega, \mathcal{F}, P)$は確率空間となる。

---

### 8.2 可測関数と確率変数
我々の目的は測度空間上の関数の積分（面積）を求めることであった。
その為に我々は次の2つの関数のクラスを定義する。
1. 測度で測れるような関数の全体
    * 可測関数
2. その可測関数に対して積分が定義できる関数の全体
    * 可積分関数

---

#### 定義8.4 可測関数(measurable function)
可測空間$(\Omega, \mathcal{F})$とする。
$f:\Omega \rightarrow \mathbb{R}$が、以下を満たす時$f$は$\mathcal{F}$-可測関数($\mathcal{F}$-measurable func.)という。

$$
\forall \alpha, \beta \in \mathbb{R}, \alpha < \beta, \\{ \omega \in \Omega \mid f(\omega) \in [\alpha, \beta) \\} \in \mathcal{F}
$$

または、単に可測関数、$f$は$\mathcal{F}$-可測、$f$は可測などという。

#### Remark
* $f$の値域は$\bar{\mathbb{R}}$の場合は上記の定義ではだめ。
    * $\bar{\mathbb{R}}$の位相をどういれているかにもよるが。
* $f$が可測であるということは次のようにも書ける。

$$
\forall \alpha, \beta \in \mathbb{R}, \alpha < \beta, f^{-1}([\alpha, \beta)) \in \mathcal{F}
$$

---

#### 定義8.5 確率変数(random variable)
$(\Omega, \mathcal{F}, P)$を確率空間とする。
$X:\Omega \rightarrow \mathbb{R}$が$\mathcal{F}$-可測であるとき、$X$を確率変数(r.v.)という。


#### 定義 ボレル集合族(borel family)、ボレル集合(borel set)
$(\Omega, \mathcal{O})$を位相空間とする。
以下で定義される$\mathcal{F} \subseteq 2^{\Omega}$をボレル集合族(borel family)という。

$$
\mathcal{F} := \sigma(\mathcal{O})
$$

ここで、$\sigma(\mathcal{O})$は$\mathcal{O}$を含む最小の$\sigma$-加法族である。
特に、$\Omega$のボレル集合族を$\mathcal{B}(\Omega)$とかく。
ボレル集合族の元をボレル集合(borel set)という。

---

####定義8.6 可測関数
$(S, \mathcal{O})$を位相空間、$(\Omega, \mathcal{F})$を可測空間とする。
関数$f:\Omega \rightarrow S$が任意のボレル集合$B \in \mathcal{B}(S)$に対して、以下を満たす時$\mathcal{F}$-可測関数という。

$$
f^{-1}(B) = \left\\{\omega \in \Omega \mid f(\omega) \in B \right\\} \in \mathcal{F}
$$

####定義8.7 確率変数
$(S, \mathcal{O})$を位相空間、$(\Omega, \mathcal{F}, P)$を確率空間とする。
関数$X:\Omega \rightarrow S$が任意のボレル集合$B \in \mathcal{B}(S)$に対して、以下を満たす時確率変数という。

$$
X^{-1}(B) = \left\\{\omega \in \Omega \mid X(\omega) \in B \right\\} \in \mathcal{F}
$$

---

### 8.3 単関数、非負値可測関数、単調収束定理
この節では、可測関数に対する積分を定義する。
可測関数に対する積分を次の手順を踏む。
1. 非負値単関数に対する積分を定義する。
2. 任意の非負値可測関数に対する積分を非負値単関数の積分の上限として定義する。
3. 可測関数を非負値と非正値部分に分け、積分を定義する。

上記の非負値単関数の積分による非負値可測関数の積分の近似は以下の2つ命題により直観的理解が与えられる。

1. 任意の非負値可測関数は非負値単関数で近似できることを示す。
2. 非負値可測関数に対する積分を単関数の積分の極限で定義する。

集合$A$の定義関数$1\_{A}$を以下で定義する。

$$
\begin{equation}
    1\_{A} := \begin{cases}
        1 \ \ x \in A, \\\\
        0 \ \ x \notin A
        \end{cases}
\end{equation}
$$

---

####定義8.4 非負値単関数(simple funciton)
$(\Omega, \mathcal{F}, \mu)$を測度空間とする。
$A\_{1}, \ldots, A\_{k} \in \mathcal{F}, A\_{i} \cap A\_{j} = \emptyset (i \neq j)$とし、$\Omega = \cup\_{i=1}^{k}A\_{i}$とする。
$a\_{1}, \ldots, a\_{k} \le 0$とする。
このとき、

$$
\begin{equation}
    \phi(\omega) := \sum\_{i=1}^{k}a\_{i}1\_{A\_{i}}(\omega),
\end{equation}
$$

を非負値単関数(simple func.)と定義する。
また、単関数$f$の積分を次で定義する。

$$
\begin{equation}
    \int\_{\Omega}\phi(\omega) \, d\mu(\omega)
    := \int\_{\Omega}\phi(\omega) \mu(d\omega) 
    := \sum\_{i=1}^{k}a\_{i} \mu(A\_{i})
\end{equation}
$$

---

####Remark
単関数は可測。
次の3つの命題により明らか。

####命題
$(S\_{i}, \mathcal{O\_{i}}) \ (i=1,2)$を位相空間、$(\Omega, \mathcal{F}, \mu)$を測度空間とし、$f:\Omega \rightarrow S\_{1}$を可測関数とする。
$g:S\_{1} \rightarrow S\_{2}$を連続関数とする。
このとき、$gf:\Omega \rightarrow S\_{2}$は可測関数。

####命題
$\mathbb{R}^{n}$上の和及び積は連続。

####命題
$(S, \mathcal{O})$を位相空間、$(\Omega, \mathcal{F}, \mu)$を測度空間とし、$f:\Omega \rightarrow S$を関数とする。
また、$\mathcal{A} \subset 2^{\Omega}, \sigma(\mathcal{A}) = \mathcal{B}(S)$とする。
このとき、以下は同値。
1. $f$が可測
2. $f$が以下を満たす。

$$
\forall A \in \mathcal{A}, f^{-1}(A) \in \mathcal{F}
$$

---

####Remark
非負値単関数の積分の定義は$\\{\alpha\_{i}\\}\_{i=1}^{k}$及び$A\_{i}$の取り方によらない。
実際$f$を非負値単関数とし、以下の二通りの表現を持つとする。

$$
f 
= \sum\_{i=1}^{k}\alpha\_{i}1\_{A\_{i}} 
= \sum\_{i=1}^{l}\beta\_{i}1\_{B\_{i}}.
$$

一般に非負値単関数$f, g$について、$f \le g$ (a.e.)であれば、$\int f \, d\mu \le \int g \, d\mu$である。
特に

$$
\sum\_{i=1}^{k}\alpha\_{i}1\_{A\_{i}} 
= \sum\_{i=1}^{l}\beta\_{i}1\_{B\_{i}}.
$$

より、

$$
\int \sum\_{i=1}^{k}\alpha\_{i}1\_{A\_{i}} \, \mu(d\omega)
= \int \sum\_{i=1}^{l}\beta\_{i}1\_{B\_{i}}\, \mu(d\omega).
$$

を得る。

---

####定義 非負値可測関数に対する積分
$(\Omega, \mathcal{F}, \mu)$を測度空間とし、$f$を非負値可測関数とする。
このとき$f$の積分を次で定義する。

$$
\int\_{\Omega} f(\omega) \,\mu(d\omega)
:= \sup\left\\{\int\_{\Omega} g(\omega) \,\mu(d\omega) \mid g \le f \, \mathrm{a.e.}, g:\mathrm{simple \, function} \right\\} \le \infty
$$


####定義 可測関数に対する積分
$(\Omega, \mathcal{F}, \mu)$を測度空間とし、$f$を可測関数とする。
ここで、$f^{+} := \max(f, 0)$, $f^{-} := \max(-f, 0)$とすると、 $f^{+}, f^{-}$は非負値可測関数で、$f = f^{+} - f^{-}$となる。
以下が定義可能な時、$f$の積分を以下で定める。

$$
\int\_{\Omega} f(\omega) \,\mu(d\omega)
:= \int\_{\Omega} f^{+}(\omega) \,\mu(d\omega) - \int\_{\Omega} f^{-}(\omega) \,\mu(d\omega)
$$

このとき、$f$は可積分という。

####Remark
非負値可測関数の積分は無限大を採りうることに注意。
次の2つの定理により、非負値可測関数の積分は単関数の列の積分で近似できることが分かる。

---

####定理8.9 単関数による近似定理
非負値可測関数$f:\Omega \rightarrow \mathbb{R}\_{\ge 0}$に対して、単関数の列$\\{\phi\_{n}\\}\_{n \in \mathbb{N}}$が存在して$\forall \omega \in \Omega$について、

$$
\begin{equation}
    \lim\_{n \rightarrow \infty}\phi\_{n}(\omega) := f(\omega),
\end{equation}
$$

かつ

$$
\begin{equation}
    0\le \phi\_{1}(\omega) \le \phi\_{\omega} \le \ldots.
\end{equation}
$$

[参考](image/001.jpg)

####定理8.10 単調収束定理
$f\_{n}:\Omega \rightarrow \mathbb{R}\_{\ge 0}\ (n \in \mathbb{N})$を非負値可測関数の列とし、$f:\Omega \rightarrow \mathbb{R}\_{\ge 0}$を非負値可測関数とする。
$f\_{n} \le f\_{n+1} \ (\forall n \in \mathbb{N})$, $\forall \omega \in \Omega, \lim\_{n \rightarrow \infty}f\_{n}(\omega) = f(\omega)$が成り立つとする。
このとき、

$$
\begin{equation}
    \lim\_{n \rightarrow \infty}\int\_{\Omega} f\_{n}(\omega) \mu(d\omega) 
    = \int\_{\Omega}f(\omega)\mu(d\omega) 
    = \int\_{\Omega}(\lim\_{n \rightarrow \infty} f\_{n})(\omega) \mu(d\omega)
\end{equation}
$$

---

### 8.4 確率変数の分布
$(\Omega, \mathcal{F}, P)$を確率空間とし、$X:\Omega \rightarrow S$を確率変数とする。
次で定義する$P\_{X}$を$X$の分布と呼ぶ。

$$
\begin{equation}
    P_{X}(B) 
    := P(\\{ \omega \in \Omega \mid X(\omega) \in B \\}) 
    = P(X^{-1}(B))
    \quad \forall B \in \mathcal{B}(S)
\end{equation}
$$

$P\_{X}$は$(\Omega, \mathcal{F})$上の確率測度である。
次で定義する$F\_{X}$を$X$の分布関数といい、$p\_{X}$を(存在すれば）密度関数という。

$$
F\_{X}(x) := P\_{X}([-\infty, x)) 
$$

$$
p\_{X}(x) := \frac{dF\_{X}(x)}{dx}
$$

####例
$X$が平均0分散1の1次元ガウス分布に従う。
$B = [-1, 2]$とすると、

$$
\begin{equation}
    P\_{X}([-1, 2]) 
    = \int\_{-1}^{2} \frac{1}{\sqrt{2\pi}} \exp\left( -\frac{x^{2}}{2} \right) \,dx
\end{equation}
$$

---

### 8.5 期待値
$X$を確率変数とする。
$X$の期待値を次で定義する。

$$
\mathbb{E}[X] := \int\_{\Omega}X(\omega)P(\,d\omega)
$$

また$\phi:\mathbb{R} \rightarrow S$をボレル可測関数とすると

$$
\begin{equation}
    \mathbb{E}[\phi(X)] = \int\_{\Omega}\phi(X(\omega)) P(\,d\omega)
\end{equation}
$$

#### 定理8.11 確率分布による期待値計算
$(\Omega, \mathcal{F}, P)$を確率空間とし、$X$を確率変数とする。
$\phi:\mathbb{R} \rightarrow S$をボレル可測関数とする。

$$
\begin{equation}
    \mathbb{E}[\phi(X)] 
    = \int\_{\Omega} \phi(X(\omega)) P(\,d\omega)
    = \int\_{S}\phi(x)P\_{X}(\,dx)
\end{equation}
$$

---

### 8.6 確率分布のラプラス変換
確率変数$X$のラプラス変換$m\_{X}:\mathbb{R} \rightarrow \mathbb{R}$を次て定義する。

$$
\begin{equation}
    m\_{X}(t) 
    := \mathbb{E}[e^{-tX}] 
    = 
    \begin{cases}
        \displaystyle \sum\_{x \in S}e^{-tx}P(\\{x\\}) \quad (\mathrm{離散値のとき}) \\\
        \displaystyle \int\_{S}e^{-tx}p(x) \,dx  \quad (\mathrm{密度関数が存在する時}) \\\
        \mathbb{E}[e^{-tX}] \quad (\mathrm{otherwise})
    \end{cases}
\end{equation}
$$

確率変数$X$が強度$\lambda$のポアソン分布に従うとき、

$$
\begin{equation}
    m\_{X}(t) 
    = \sum\_{n=0}^{\infty}e^{-tn}\frac{\lambda^{n}}{n!}e^{-\lambda}
    = e^{\lambda (e^{-t} - 1)}.
\end{equation}
$$

また、ガンマ分布の場合

$$
\begin{equation}
    m\_{X}(t) 
    = \left(\frac{b}{b+t}\right)^{a}
\end{equation}
$$

[参考](image/002.jpg)

---

ラプラス変換は確率分布のいくつかの性質を特徴づける。
確率論では、ラプラス変換より特性関数が利用されることが多い。

#### 定理
$X$を確率変数とし、 $\mathbb{E}[e^{-tX}] < \infty \, (\forall t \in \mathbb{R})$とする。
このとき、

$$
\mathbb{E}[X] = - \frac{dm\_{X}}{dt}(0).
$$

#### 定義
$\phi\_{X}(t) := \mathbb{E}[e^{-itX}]$を$X$の特性関数という。
ここで、$i = \sqrt{-1}$である。


---

### 8.7 確率1で成り立つ命題

$(\Omega, \mathcal{F}, P)$を確率空間とし、$X$を確率変数とする。

#### 定義
$\omega \in \Omega$について、成り立つ命題をprop.$(\omega)$とかく。
以下をが成り立つ時、prop.$(\omega)$が確率1で成り立つという。

$$
P(\\{\omega \in \Omega \mid \neg \mathrm{prop.}(\omega) \\}) = 0.
$$

また、prop.が*almost surely*で成り立つとも言い、prop. a.s.やprop. w.p.1などと書く。

#### 例
確率変数$X, Y$が確率1で等しいとは、

$$
P(\\{ \omega \in \Omega \mid X(\omega) \neq Y(\omega)\\}) = 0
$$

---

$X,Y$が確率1で等しいとする。
ある測度0集合$E$が存在して、

$$
\begin{align}
    \int\_{\Omega} X(\omega) P(d\omega)
    \nonumber & = \int\_{\Omega}X(\omega)P(d\omega) + \int\_{\Omega \setminus E}X(\omega)P(d\omega) \\\
    \nonumber & = \int\_{\Omega \setminus E}Y(\omega)P(d\omega) \\\
    \nonumber & = \int\_{\Omega \setminus E}Y(\omega)P(d\omega) + \int\_{\Omega \setminus E}Y(\omega)P(d\omega) \\\
    & = \int\_{\Omega}Y(\omega)P(d\omega) 
\end{align}
$$

---

### 8.8 ランダム測度
$(\Omega, \mathcal{F}, P)$を確率空間とし、$X$を確率変数とする。
$(S, \mathcal{B})$を可測空間とし、$M:\Omega \times \mathcal{B} \rightarrow [0, \infty]$を$(\Omega, S)$上の関数とする。

#### 定義
$M$が以下を満たす時、ランダム測度という。
* $\forall B \in \mathcal{B}$について、$M(\cdot, B): \Omega \rightarrow [0, \infty]$とすると$(\Omega, \mathcal{F}, P)$上の確率変数。
* $\forall \omega \in \Omega$について、$M(\omega, \cdot): \mathcal{B} \rightarrow [0, \infty]$が$(S, \mathcal{B})$上の測度。

#### 定義
$M$をランダム測度とし、$(S, \mathcal{B})$上の可測関数$f:S \rightarrow [0, \infty]$について、確率変数$Mf$を定義する。

$$
\begin{equation}
    Mf(\omega) := (Mf)(\omega) := \int\_{S}f(x)M(\omega, \,dx),  \forall \omega.
\end{equation}
$$

また、$\mathbb{R}$上の可測関数$\phi$について測度$\nu\_{\phi, M}$を以下で定義する。

$$
\begin{equation}
    \nu\_{\phi, M}(A)
    := \mathbb{E}[\phi(M(A))] 
    = \int\_{\Omega}\phi(M(\omega, A) P(\,d\omega), A \in \mathcal{B}.
\end{equation}
$$

---

#### Remark
$M(\cdot, A)$が確率変数なので、$M(\cdot, A)$の分布を$P\_{M\_{A}}$とすると定理8.11より、

$$
\begin{equation}
    \mathbb{E}[\phi(M(A))] 
    = \int\_{[0, \infty]} \phi(t)P\_{M\_{A}}(dt), \forall A \in \mathcal{B}
\end{equation}
$$

### 8.9 ランダム測度のラプラス汎関数
$(\Omega, \mathcal{F}, P)$を確率空間とし、可測空間$(S, \mathcal{B})$上の非負値可測関数$f:S \rightarrow [0, \infty]$について、

$$
\begin{equation}
    f \mapsto \mathbb{E}[e^{-Mf}] = \int\_{\Omega} e^{-\int\_{S}f(x) M(\omega, dx)} P(d\omega) \in [0, 1]
\end{equation}
$$

#### 定理8.12
$f\_{n}: S \rightarrow [0, \infty]\, (n \in \mathbb{N})$を非負値可測関数の列とし、$f:S \rightarrow [0, \infty]$を非負値可測関数とする。
$f\_{n} \le f\_{n+1} \forall n \in \mathbb{N},$ $\lim\_{n \rightarrow \infty}f\_{n}(x) = f(x)$のとき、

$$
\lim\_{n \rightarrow \infty} \mathbb{E}[e^{-Mf\_{n}}] = \mathbb{E}[e^{-Mf}]
$$

---

#### 定義
ランダム測度$M, N$が独立とは、
$\forall A \in \mathcal{B}$について、 $M(\cdot, A), N(\cdot, A)$が独立。


#### 定理8.13 
$M, N$をランダム測度とする。 
以下は同値。
1. $M, N$が独立
2. 任意の可測関数$f, g$について、$\mathbb{E}[e^{-(Mf + Ng)}] = \mathbb{E}[e^{-Mf}]\mathbb{E}[e^{-Ng}]$

#### 定理（有界収束定理)
$(\Omega, \mathcal{F}, P)$を有限測度空間とする。
$X\_{n} (\forall n \in \mathbb{N}), X$を可測関数とし、$\exists M \ge 0$ s.t. $X\_{n} \le M$とする。
$X\_{n} \rightarrow X$a.s.とすると

$$
\lim\_{n \rightarrow \infty} \mathbb{E}[X\_{n}] = \mathbb{E}[X].
$$



