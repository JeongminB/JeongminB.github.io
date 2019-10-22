---
title: "베르누이 분포, 이항 분포, 이항 분포의 기댓값과 분산"
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

간단한 예로 앞면이 나올 확률이 $p$인 동전을 5번 던진다고 합시다. 이것의 결과가 확률변수 $X$라고 한다면, $X$는 이항분포 $\text{B}(5,p)$를 따릅니다. 그리고 나온 앞면의 횟수를 outcome $k=\sum_{i=1}^5 X_i$ 라고 합시다. 예시에서 $k$는 0부터 5까지의 범위에서 값을 가지며 모든 확률을 더하면 1이 될 것입니다. 분포로 그려보면 어떠한 모양이 나오겠죠.

이들 중 하나인 앞면이 3개가 나올 확률, $P(X=3)$ 를 구한다고 합시다.

$$\begin{aligned}
&\text{TTHHH THTHH THHTH THHHT} \\
&\text{HTTHH HTHTH HTHHT} \\
&\text{HHTTH HHTHT} \\
&\text{HHHTT}
\end{aligned}$$

위와 같이 가능한 모든 조합을 고려합니다 ($_{5}\mathrm{C}_{3}=10$). 동전 5개를 던져서 앞면에 3개일 확률은 앞면의 확률이 $p$일 때, $p^3(1-p)^{5-3}$입니다. 확률은 다음과 같습니다:

$$ P(X=3) = {}_{5}\mathrm{C}_{3} \;p^3(1-p)^{5-3}, \quad X\sim B(5,p)$$

식을 좀 더 일반화 한다면 아래와 같을 것입니다.

$$ P(X=k) = {}_{n}\mathrm{C}_{k} \;p^k(1-p)^{n-k}, \quad X\sim B(n,p)$$

</div>

### ◇ Binomial coefficient

<div>

각 시행의 순서가 구분되는 경우 <strong><font color='#FF7D33'>순열</font></strong>(permutation) $_{n}\mathrm{P}_{k}$를 통해서 경우의 수를 계산합니다. $n$명에서 $k$명을 뽑아 줄세우기를 하는 경우의 수가 대표적인 순열의 예시입니다. 첫 번째 사람을 뽑는 경우의 수가 $n$, 두 번째가 $(n-1)$, $k$번째는 $(n-k+1)$이므로, factorial로 나타내면 $\frac{n!}{(n-k)!}$가 됩니다.

$$ {}_{n}\mathrm{C}_{k} = \frac{_{n}\mathrm{P}_{k}}{k!}
= \frac{n!}{k! \,(n-k)!}$$

반면에, <strong><font color='#FF7D33'>조합</font></strong>(combination) $_{n}\mathrm{C}_{k}$는 시행의 순서를 따지지 않습니다. 줄세우기 예시로 따지면 $k$명의 순서를 구분하지 않기 때문에 순열에서 다시 $k$명을 줄세우는 경우의 수 $k!$만큼 나눠줍니다.
<br><br>

이항분포 $\text{B}(n,p)$에서 '$n$번 시행 중 $k$번만큼 확률 $p$에 해당하는 결과나 나온 경우' $P(X=k)$를 계산하는 과정에서, 각 독립시행 결과의 <strong>조합</strong>(combination)이 계수가 되었습니다. 시행 결과의 순서를 따지지 않고 발생 횟수만 따지기 때문입니다. 따라서, <strong><font color="#3367E5">이항 계수</font></strong>라고도 부르며 아래와 같이 표기하기도 합니다.

$${n\choose k} = {}_{n}\mathrm{C}_{k} = \frac{_{n}\mathrm{P}_{k}}{k!} 
= \frac{n!}{k! \,(n-k)!}$$
</div>

---

## ◆ 이항분포의 기댓값, 분산

<div>

$$ \mu = E[X] = \sum_i x_i \,p(x_i) $$

위는 통계에서 말하는 평균, 기댓값의 정의였습니다. 우리는 이항분포를 따르는 확률변수가 시행의 발생 횟수 $k$를 값으로 가지는 것을 알고, 특정 값의 확률 $P(X=k)$를 알고 있으니 대입을 해봅시다.

$$E[X] = \sum_{k=0}^n k \,{}_{n}\mathrm{C}_{k} \;p^k(1-p)^{n-k}$$

식을 정리해봅시다. $k$가 0인 경우 값이 0이므로 summation을 $k=1$로 바꿔도 같습니다.

$$\begin{aligned}
&= \sum_{k=1}^n \color{blue}{k} \,\frac{n!}{\color{blue}{k!} \,(n-k)!} \;p^k(1-p)^{n-k} \\
&= \sum_{k=1}^n \frac{\color{blue}{n} (n-1)!}{(k-1)! \,(n-k)!} \;\color{blue}{p} \,p^{k-1}(1-p)^{n-k} \\
&= np \sum_{k=1}^n {}_{n-1}\mathrm{C}_{k-1} \; \,p^{k-1}(1-p)^{n-k}
\end{aligned}$$

위와 같이 정리하면 summation 부분이 이항분포 $\text{B}(n\!-\! 1,p)$를 따르는 확률변수의 모든 case들의 확률을 더한 결과가 됩니다. $k\!-\!1=k^\prime$, $n\!-\!1=n^\prime$ 으로 치환하면 좀 더 알아보기 쉽습니다.

$$\begin{aligned}
E[X]  &= np \sum_{k^\prime=0}^{n^\prime} {}_{n^\prime}\mathrm{C}_{k^\prime}  \,p^{k^\prime}(1-p)^{n^\prime-k^\prime} \\
&= np
\end{aligned}$$

고로, <strong>이항분포를 따르는 확률변수의 기댓값</strong>은 <strong><font color='#FF7D33'>$np$</font></strong> 임을 알 수 있습니다. 참고로 <strong>분산</strong>은 <strong><font color='#FF7D33'>$np(1-p)$</font></strong> 가 나옵니다. 이항분포를 직접 그래프로 확인해봅시다.
<br><br>

<p>
<span class='center'><img src='/assets/res/statistics/stat-2-img1.png' width='45%' /> &nbsp; <img src='/assets/res/statistics/stat-2-img2.png' width='45%' /></span>
<span class='center'>출처: en.wikipedia.org</span>
</p>

왼쪽은 이항분포를 따르는 확률변수의 PMF (probability mass function), 오른쪽은 CDF (cumulative distribution function)입니다. 확률질량함수를 보면 분포의 기댓값이 $np$ 라는 것을 눈으로도 확인할 수 있습니다.
<br><br>

<p>
<span class='center'>
<img src='/assets/res/statistics/stat-2-img3.png' width='50%' /></span>
<span class='center'>출처: google 계산기</span>
</p>

분산은 유도 대신 직관적으로 이해하고자 합니다. 이항분포를 따르는 확률변수의 분산 크기는 위와 같은 그래프 형태를 따릅니다. 보다시피, 분산은 $p=0.5$에서 가장 크고 0이나 1에 가까울 때 작습니다. 이는 시행 결과의 random성이 작을수록 샘플들이 분산되지 않고 (한 쪽 끝으로) 모일 것이므로 이야기가 들어맞습니다.
<br><br>

분산이 시행횟수에 비례하는 것은 PMF 그래프에서 <font color="blue">◆</font> $\text{B}(20,0.5)$와 <font color="red">●</font> $\text{B}(40,0.5)$를 참고하여 직관적으로만 이해합시다. 그리고 표준편차는 당연히 $\sigma = \sqrt{np(1-p)}$가 됩니다. 
</div>
<br><br>

(작성중?)