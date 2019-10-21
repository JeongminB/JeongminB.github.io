---
title: "베르누이 분포, 이항 분포, (작성중)"
categories: [Basics, Statistics]
---

## ◆ Bernoulli distribution

<div>

먼저, Bernoulli distribution에 대해서 알아봅시다. 베르누이 분포는 '동전 한 번 던지기'를 떠올리면 쉽습니다. 확률변수 $X$가 동전 던지기 결과가 head인 경우 $x=1$, tail인 경우 $x=0$이라고 합시다.

$$ \Omega=\{\text{Head}, \text{Tail}\} $$

$$X(\omega) = 
\begin{cases} 
1   & \text{if }\omega=\text{Head}, \\
0 & \text{if }\omega=\text{Tail}
\end{cases}$$

그 다음 결과가 Head일 확률을 $p$라고 하고, Tail일 확률을 $(1-p)$라고 합시다. outcomes이 둘 뿐이라 이렇게 표기하는 것이 가능합니다.

$$\begin{aligned}
&P(X=1) = p \\
&P(X=0) = 1-p
\end{aligned}$$

그렇다면, 다음과 같이 확률변수 $X$가 '$x=1$일 때 확률이 $p$인 <strong><font color="#3367E5">베르누이 분포</font></strong>를 따른다'고 표기할 수 있습니다.

$$ X\sim\text{B}(1, p) $$

베르누이 분포는 결과가 두 가지이며, 결과의 확률이 일정하고 각 시행이 독립적인 확률변수의 분포를 말합니다. 
</div>

---

## ◆ Binomial distribution

<div>

$$ X\sim\text{B}(n, p) $$

<strong><font color="#3367E5">이항 분포</font></strong>는 베르누이 분포의 '$n$번 반복'이라고 생각하면 쉽습니다. 즉, 베르누이 시행 횟수 $n$이 1이면 베르누이 분포와 동일합니다. '동전 $n$번 던지기'로 이해하면 쉽습니다. 이때, 각 시행은 독립적이고 확률 $p$는 일정합니다 (동일분포).
<br><br>

각각의 시행을 독립적인 확률변수 $X_1, X_2, \cdots , X_n$로 본다면 이들을 '독립 동일 분포'를 따른다고 말할 수도 있습니다. 약자로 <strong><font color='#FF7D33'>i.i.d.</font></strong> (independent and identically distributed)라고 씁니다. 그리고 이 독립적인 분포들을 모두 더한 $X=X_1+X_2+\cdots +X_n$가 이항분포가 됩니다.
<br><br>

간단한 예로 앞면이 나올 확률이 $p$인 동전을 5번 던진다고 합시다. 이것의 결과가 확률변수 $X$라고 한다면, $X$는 이항분포 $B(5,p)$를 따릅니다. 그리고 나온 앞면의 횟수를 outcome $k=\sum_{i=1}^5 X_i$ 라고 합시다. 예시에서 $k$는 0부터 5까지의 범위에서 값을 가지며 모든 확률을 더하면 1이 될 것입니다. 분포로 그려보면 어떠한 모양이 나오겠죠.

이들 중 하나인 앞면이 3개가 나올 확률, $P(X=3)$ 를 구한다고 합시다.

$$\begin{aligned}
&\text{TTHHH THTHH THHTH THHHT} \\
&\text{HTTHH HTHTH HTHHT} \\
&\text{HHTTH HHTHT} \\
&\text{HHHTT}
\end{aligned}$$

위와 같이 가능한 모든 조합을 고려합니다 ($_{5}\mathrm{C}_{3}=10$). 동전 5개를 던져서 앞면에 3개일 확률은 앞면의 확률이 $p$일 때, $p^3(1-p)^{5-3}$입니다. 확률은 다음과 같습니다:

$$ P(X=3) = _{5}\!\!\mathrm{C}_{3} \;p^3(1-p)^{5-3}, \quad X\sim B(5,p)$$

식을 좀 더 일반화 한다면 아래와 같을 것입니다.

$$ P(X=k) = _{n}\!\!\mathrm{C}_{k} \;p^k(1-p)^{n-k}, \quad X\sim B(n,p)$$

</div>

### ◇ Binomial coefficient

<div>
이항분포 $B(n,p)$에서 '$n$번 시행 중 $k$번 확률 $p$에 해당하는 결과나 나온 경우' $P(X=k)$를 계산하는 과정에서, 각 독립시행 결과의 <strong><font color="#3367E5">조합</font></strong>(combination)이 계수가 되었습니다. 이는 각 독립시행의 순서를 따지지 않기 때문입니다. 해서, <strong><font color="#3367E5">이항 계수</font></strong>라고 부르며 아래와 같이 표기하기도 합니다.

$${n\choose k} = _{n}\!\!\mathrm{C}_{k} = \frac{_{n}\mathrm{P}_{k}}{k!} 
= \frac{n!}{k! \,(n-k)!}$$

각 시행의 순서가 구분되는 경우 <strong><font color='#FF7D33'>순열</font></strong>(permutation) $_{n}\mathrm{P}_{k}$를 통해서 경우의 수를 계산합니다.
</div>
<br><br>

(작성중)