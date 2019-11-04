---
title: "불편 추정량인 표본평균과 표본분산 (작성중)"
categories: [Basics, Statistics]
---

## ◆ Bias of an estimator

우리가 관심 있는 것이 모집단의 통계량인 모수 (parameter)인데 모집단이 너무 커서 이를 직접 구할 수 없는 경우, 표본들을 관찰해서 모수를 <strong>추정</strong> (estimation)을 하게 됩니다. 표본에서 구해지는 '표본평균', '표본분산'이라는 <strong>추정량</strong>을 통해서 (근사적인) 모수를 알고자 하는 것이죠.

<strong><font color="#3367E5">추정량</font></strong> $\hat \theta$(estimator)이란 관찰된 표본들로부터 모수 $\theta$(parameter)를 구하는 방법(rule), 함수, 혹은 단순히 모수를 추정하는 통계량을 말합니다. 추정량은 표본에 따라 값이 달라지기 때문에 <strong>확률변수</strong>입니다. 당연히 실제 모수와는 값의 차이가 있을 것이고, 모수를 잘 추정해야 좋은 추정량이라고 말할 수 있을 것입니다.

$$\begin{aligned}
\text{error: }& \hat \theta(x) - \theta \\
\text{bias: }& E(\hat \theta) - \theta
\end{aligned}$$

어떤 추정량이 바람직한가를 평가할 때 <strong><font color='#FF7D33'>편의</font></strong>(偏倚, bias)가 0인지를 따지기도 합니다. 편의는 추정량의 '기댓값'과 모수의 차이를 말합니다. 추정량 $\hat \theta$이 $E(\hat \theta) = \theta$을 만족할 때, 이러한 추정량을 <strong><font color="#3367E5">불편 추정량</font></strong> (unbiased estimator)이라고 말합니다.

불편 추정량의 예시로는 <strong>표본평균, 표본분산</strong> 등이 있습니다. 정리하면, <strong>표본평균의 기댓값은 확률변수의 기댓값과 같고, 표본분산의 기댓값은 확률변수의 분산과 같습니다.</strong> 아래에서는 표본평균과 표본분산의 정의와 이들이 실제로 불편 추정량인지을 증명해보겠습니다.

---

## ◆ 표본평균의 기댓값은 모집단 평균

$$ \mu = E[X] = \sum_i x_i \, \underbrace{p(x_i)}_{\text{PMF}} $$

확률변수 $X$의 기댓값을 $\mu$라고 합시다. $X$에서 샘플링한 $n$개의 표본에 대해서 구하는 표본평균은 아래와 같이 구할 수 있습니다. 여기에는 $n$개의 표본을 각각 독립독일분포인 확률분포로 가정하게 됩니다.

$$\bar X = \frac{1}{n} \sum_{i=1}^n X_i$$

이것의 기댓값은,

$$E[\bar X] = \frac{1}{n} \, E\left[ \sum_{i=1}^n X_i \right] = \frac{1}{n} \, E[X_1 + \cdots + X_n] $$

이며, <a href="/basics/statistics/statistics-1/#-properties-of-expectation">기댓값의 성질</a>에 의해서 '덧셈의 기댓값'은 '기댓값의 덧셈'으로 바꿀 수 있습니다. 각각의 확률변수 $X_1, \cdots, X_n$를 독립동일분포 i.i.d.라고 가정하면, 각각의 기댓값이 모두 동일하게 됩니다. 물론 $E[X_i]$는 확률변수 $X$의 기댓값 $\mu$와 같습니다.

$$ E[\bar X] = \frac{ E[X_1] + \cdots + E[X_n]}{n} = \frac{n\mu}{n} = \mu $$

고로 표본평균의 '기댓값'과 모수인 모집단 평균의 차이(bias)는 0으로, 위 정의를 따르는 표본평균이 불편 추정량임을 확인할 수 있습니다.

---

## ◆ 표본평균의 분산은 모집단 분산 / n

분산은 편차제곱에 대한 기댓값이므로, 표본평균의 분산은 다음과 같습니다.

$$ V[\bar X] = E\left[(\bar X - \mu)^2\right]$$

이제 표본평균의 정의를 대입해서 식을 풀어봅시다.

$$\begin{aligned}
&= E\left[\left(\frac{1}{n}\sum_{i=1}^nX_i - \mu\right)^2\right] \\
&= E\left[\left(\frac{\sum_{i=1}^nX_i - n\mu}{n}\right)^2\right] \\
&= \frac{1}{n^2}\,E\left[\left(\sum_{i=1}^n (X_i - \mu)\right)^2\right] \\
&= \frac{1}{n^2}\,E\left[\big( (X_1-\mu) + \cdots + (X_n-\mu) \big)^2\right] 
\end{aligned}$$

전개해보면 $(X_1-\mu)^2 + \cdots + (X_n-\mu)^2$ 같은 제곱항들과 $(X_1-\mu)(X_2-\mu)+\cdots + (X_{n-1}-\mu)(X_n-\mu)$ 항들로 나뉩니다. 기댓값을 나눠서 써보겠습니다.

$$\begin{aligned}
&= \frac{1}{n^2}\,E\left[ (X_1-\mu)^2 + \cdots + (X_n-\mu)^2\right] + \frac{1}{n^2}\,E\left[ (X_1-\mu)(X_2-\mu)+\cdots \right]
\end{aligned}$$

뒤쪽의 기댓값을 먼저 살펴보면, $(X_1-\mu)$와 $(X_2-\mu)$는 '독립'이기 때문에 기댓값의 성질에 의해 '기댓값의 곱셈'으로 분리할 수 있습니다. $E(X_1 - \mu)$는 다시 기댓값의 선형성 (linearity)에 의해 $E(X_1) - E(\mu)$으로 나눌 수 있습니다. 전자는 확률변수의 기댓값과 같으므로 $\mu$, 후자는 상수에 대한 기댓값이니 $\mu$가 그대로 나옵니다. 고로 0이 됩니다. 이처럼 제곱항을 제외하면 모두 0이 되기 때문에 다음과 같이 정리됩니다.

$$\begin{aligned}
&= \frac{1}{n^2}\,E\left[ (X_1-\mu)^2 + \cdots + (X_n-\mu)^2\right] \\
&= \frac{1}{n^2} (n \sigma^2) \\
&= \frac{\sigma^2}{n}
\end{aligned}$$

고로 표본평균의 분산은 모집단 분산을 $n$으로 나눈 것과 같습니다. 마지막으로 표본평균의 기댓값과 분산을 정리해봅시다.

$$\begin{aligned}
E[\bar X] &= \mu \\
V[\bar X] &= \frac{\sigma^2}{n}
\end{aligned}$$

앞서 말한 대로, 표본평균은 샘플에 따라 달라지는 랜덤한 값(확률변수)입니다. 그래서 표본평균의 기댓값은 모집단의 평균과 같으나, 분산은 0이 아닙니다.

그런데 확률변수에서의 샘플 추출이 복원추출이라고 보기 때문에 $n$을 얼마든지 늘릴 수 있습니다. $n$이 무한히 커진다면 분산은 확률적으로 0에 가까워집니다. 이는 '$n$이 무한히 커지면 표본평균이 모평균으로 수렴'한다는 이야기입니다. 이를 <strong><font color='#FF7D33'>큰 수의 법칙</font></strong> (law of large numbers)이라고 합니다.

---

## ◆ 표본분산의 기댓값은 모집단 분산

$$ \sigma^2 = V[X] = \sum_i (x_i - \mu)^2 p(x_i) = \frac{\sum_{i=1}^n (x_i - \mu)^2}{n}$$

확률변수 $X$의 분산, 모집단의 분산은 위와 같습니다. 그러나 표본분산은 표본평균과 다르게 아래와 같이 편차제곱합을 표본의 수 $n$이 아닌, '$n-1$'로 나누어줘야 불편 추정량이 됩니다.

$$s^2 = \frac{\sum_{i=1}^n (X_i - \bar X)^2}{n-1} $$

이는 관측된 표본의 <strong><font color='#FF7D33'>자유도</font></strong> (degrees of freedom)에서도 연관성을 찾을 수 있습니다. 자유도는 쉽게 말해서 실질적으로 독립적인 변수들의 개수를 의미합니다. 표본평균은 $n$개의 값들이 자유로운 값을 가지고 거기서의 평균을 구하지만, 표본분산, 그리고 제곱근을 취한 표본 표준편차에서는 <strong>편차</strong> (deviation) $X_i - \bar X$의 성질 때문에 자유도가 $n-1$이 됩니다. '편차의 총 합은 0'이라는 성질이 있기 때문에 $n-1$개의 값이 정해지면 나머지 하나의 값은 dependent한 값이 되기 때문입니다.

실제로 위 정의의 표본분산 기댓값이 모분산과 일치하는지 확인해봅시다.


$$\begin{aligned}
E[s^2] &= \frac{1}{n-1} \, E\left[ \sum_{i=1}^n (X_i - \bar X)^2 \right] \\
&= \frac{1}{n-1} \, E\left[ \sum_{i=1}^n \big((X_i - \mu) + (\mu - \bar X)\big)^2 \right] \\
&= \frac{1}{n-1} \, E\left[ \sum_{i=1}^n \big((X_i - \mu)^2 + 2(X_i - \mu)(\mu - \bar X) + (\mu - \bar X)^2\big) \right]
\end{aligned}$$

이 다음 $\sum_{i=1}^n$을 각각의 항에 대해서 취해주면 아래와 같이 정리가 가능합니다.

$$\begin{aligned}
&= \frac{1}{n-1} \, E\left[ \sum_{i=1}^n (X_i - \mu)^2 + 2n(\bar X - \mu)(\mu - \bar X) + n(\mu - \bar X)^2 \right]
\end{aligned}$$

두 번째 항은 표본평균의 정의에 의해 $n\bar X = \sum_{i=1}^n X_i$이기 때문에 $n$으로 묶을 수 있습니다. 나머지 $\mu$나 $\bar X$로 이루어진 부분은 $i$에 대한 값이 아니므로 상수처럼 취급되어 단순히 $n$배가 된다는 점에 유의합시다. 두 번째 항과 세 번째 항의 부호를 바꾸어 아래와 같이 정리가 가능합니다.

$$\begin{aligned}
&= \frac{1}{n-1} \, E\left[ \sum_{i=1}^n (X_i - \mu)^2 - n(\bar X - \mu)^2 \right] \\
&= \frac{1}{n-1} \, \left( \sum_{i=1}^n E\left[ (X_i - \mu)^2\right] - n\, E\left[(\bar X - \mu)^2\right] \right)
\end{aligned}$$

각각의 항에 대한 기댓값을 생각해봅시다. 첫 번째 항은 기댓값의 성질에 의해 summation을 밖으로 뺄 수 있습니다. 동립동일분포인 '확률변수 $X$에 대한 분산'을 $n$번 더한 것과 같으므로 $n\sigma^2$입니다. 두 번째 항은 '표본평균 $\bar X$에 대한 분산'에 $n$을 곱한 것입니다. 이것의 값은 $\frac{\sigma^2}{n}$이므로 아래와 같이 정리할 수 있습니다.

$$\begin{aligned}
&= \frac{1}{n-1} \, \left( n\sigma^2 - n \frac{\sigma^2}{n} \right) \\
&= \sigma^2
\end{aligned}$$

고로 표본분산을 불편 추정량으로 만들어주기 위해서는 편차제곱합을 $n-1$로 나누어줘야 합니다.

---

## ◆ Bessel's correction

불편 추정량으로 만들어주기 위해서 $n-1$로 나눈다는 것을 수식적으로 증명했으니 받아들일 수는 있겠으나, 그래도 $n$으로 나누면 안 되는 좀 더 와닿는 이유가 필요할지도 모르겠습니다.

(작성중)