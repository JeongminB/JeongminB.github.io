---
title: "확률변수부터 기댓값, 분산, 표준편차까지"
categories: [Basics, Statistics]
---


일상에는 확정할 수 없는 문제들이 있습니다. coin flip의 결과가 head인지 tail인지 우리는 알 수 없습니다. 이와 같은 양을 수학적으로 다루기 위해서 확률에 대해서 배우게 됩니다. 블로그의 Statistics 항목에서는 확률과 통계와 관련된 내용이 올라옵니다.

---

### ◆ Random variable

**변수**(variable)는 간단히 '변할 수 있는 값'을 대표하는 기호와도 같습니다. **확률변수**(random variable)는 '확률적인 양'을 대표합니다. 예컨대 복권추첨 결과는 확률변수가 될 수 있습니다. 어떤 결과가 나올지는 알 수 없지만 특정 값이 자주 나오고, 잘 나오지 않는다는 것은 알 수 있습니다.

$$X(\omega) = x \;, \quad x \in \mathbb{R}$$

수학적으로 <strong><font color="#3367E5">확률변수</font></strong>(random variable)는 random experiment의 가능한 실현값(outcome)에 numerical value를 할당하는 함수와도 같습니다. 보통 확률변수는 대문자로 표기하고, 할당되는 값은 소문자로 표기하는 경우가 많습니다.

$$ \omega \in \Omega \quad \xrightarrow{X} \quad x \in \mathbb{R}$$

확률변수는 sample space $\Omega$를 정의역(domain)으로 갖습니다. 그리고 일반적으로 실수를 공역(range)으로 갖습니다.

---

### ◆ Sample space, Event

<strong><font color="#3367E5">표본공간</font></strong>은 관심 있는 세상(실험)에서 발생할 수 있는 '모든 현상(결과)들의 집합'입니다. <동전던지기를 2회 연달아 했을 때의 결과>를 알파벳으로 나타낸다면, sample space는 아래와 같이 discrete하게 정의됩니다:

$$\Omega=\{ \text{TT}, \text{HT}, \text{TH}, \text{HH} \}$$



그리고 표본공간 $\Omega$의 임의의 subset을 <strong><font color="#3367E5">사건</font></strong>(event) 혹은 사상(事象)이라고 말합니다. 사건 $A$가 <동전던지기 2회의 결과가 같은 경우>라면 다음과 같이 나타낼 수 있습니다:

$$A=\{ \text{TT}, \text{HH} \}$$

측도론에서 이야기하는 사건들의 집합 sigma-field $\mathcal{F}$에 대해서는 다루지 않겠습니다. 몰라요ㅠ

---

### ◆ Probability

**확률**은 **어떤 사건이 일어날 가능성을 나타내는 비율**이라고 말할 수 있을 것 같습니다. 아래는 우리가 잘 아는 확률의 공리를 간단히 나타낸 것입니다.

##### ◇ 1. Non-negativity

$\quad P(A) \ge 0\,, \quad\text{for every event}\,A$

##### ◇ 2. Normalization

$\quad P(\emptyset)=0, \; P(\Omega)=1$

##### ◇ 3. Additivity

$\quad P(A_1 \cup A_2)=P(A_1)+P(A_2)\,,\quad A_1 \cap A_2 = \emptyset$

기호로는 $P(\cdot)$ 혹은 $\text{Pr}(\cdot)$, $\text{Prob}(\cdot)$로 나타내기도 합니다. **확률측도**(probability measure)라고도 말합니다. 주목할 부분은 확률은 실수를 받는 것이 아닌 '사건이라는 집합을 받아 실수값'을 내놓는다는 점입니다. 이 이야기는 확률과 확률변수를 한 줄로 정리한 후 마치겠습니다.

* <strong><font color="#3367E5">확률</font></strong>은 표본의 집합인 사건을 '0이상 1이하의 실수(전체 경우에 대한 비율)'로 바꾸는 함수이다.
* <strong><font color="#3367E5">확률변수</font></strong>는 모든 표본을 각각 하나의 '실수'로 바꾸는, 표본공간 $\Omega$ 위에 정의된 함수이다.

---

### ◆ Probability distribution

공평한 주사위를 던진 결과가 확률변수 $X$라고 합시다. 확률변수의 실현값인 주사위 눈의 수와 $X$가 매핑하는 실수값을 일치시키겠습니다.

| **Outcome x** | **Probability P** |
|:---------:|:-------------:|
| 1   | 1/6    |
| 2   | 1/6    | 
| 3   | 1/6    | 
| 4   | 1/6    |
| 5   | 1/6    |
| 6   | 1/6    |

<div>

$P(X\!=\!4)$라고 한다면 '$X(\omega)=4$가 되는 사건의 확률'을 말합니다. 값은 1/6이네요. <strong><font color="#3367E5">확률분포</font></strong> (probability distribution)는 'random variable $X$가 특정 outcome을 가질 확률'을 나타냅니다. 좀 더 쉽게 말하면, 확률분포는 특정 사건들의 확률을 보여주는 정보라고 볼 수 있습니다. 위 테이블은 이산확률분포를 표로 정리한 것입니다.
<br><br>

<strong>이산확률변수</strong>가 가지는 확률분포는 이산확률분포이며 <strong>확률질량함수</strong>, PMF (probability mass function) $f_X(x)$로 표현할 수 있습니다. 이산확률분포가 가지는 확률값의 총합은 1이 됩니다.
<br><br>

<strong>연속확률변수</strong>가 가지는 확률분포는 연속확률분포이며 <strong>확률밀도함수</strong> PDF (probability density function)로 표현할 수 있습니다. 연속확률분포는 확률밀도함수의 총면적이 1이 됩니다. ( $\int f_X(x)dx=1$ )
</div>

---

### ◆ Expectation, Sample mean

확률변수의 확률분포 특성을 설명하기 위해 쓰는 대표적인 양 중 하나가 <strong><font color="#3367E5">기댓값</font></strong>(expectation)입니다.

$$ \mu_X = E[X] = \sum_i x_i \, \underbrace{p(x_i)}_{\text{PMF}} $$

$$ \mu_X = E[X] = \int x \, \underbrace{p(x)}_{\text{PDF}} \,dx $$

<strong>샘플의 실현값과 샘플이 발생할 확률을 곱해서 모두 더하면 기댓값</strong>이 나옵니다. 위에서 나온 공평한 주사위의 기댓값은 3.5입니다. 기댓값 표기에서 대괄호 $[\cdot]$ 는 <strong>functional</strong> (범함수)임을 나타내는 것입니다. function이 숫자를 받아서 숫자를 내놓는다면, functional은 함수를 받아서 숫자를 내놓는다고 생각합시다.

$$\bar x = \frac{1}{N} \sum_{i=1}^N x_i$$

<strong><font color="#3367E5">표본평균</font></strong>(sample mean)은 data points의 산술평균(arithmetic mean)을 구할 때 씁니다. $\mu$는 보통 표본공간 전체에서의 평균인 확률변수의 기댓값 의미하고 (=모평균, population mean), $\bar x$는 가지고 있는 샘플들의 평균, 데이터 포인터 평균을 표기할 때 씁니다.

만약 샘플의 수 $N$이 충분히 크다면 $\bar x$는 $\mu$에 가까워집니다 (Law of large numbers). 주사위 던지기 결과 하나의 값은 어떤 값이 나올지 알 수 없지만, 주사위를 많이 던져서 나온 수의 평균을 내면 3.5에 가까운 값이 나올 것입니다.

#### ◇ 기댓값의 성질

$$\begin{aligned}
&E[X+c] = E[X] + c \\
&E[cX] = c E[X] \\
&E[X+Y] = E[X] + E[Y] \\
&E[XY] = E[X]\,E[Y] \,, \quad \text{if } X \perp\!\!\!\perp Y
\end{aligned}$$

기댓값의 기본 성질입니다. 마지막은 $X$와 $Y$가 독립인 경우에만 성립하니 주의합시다.

---

### ◆ Variance, Standard deviation

확률변수 $X$의 기댓값 $E[X]=\mu$를 알아도 여러 형태의 확률분포가 있을 수 있습니다. 값 $x$가 기댓값 근처에서 주로 나올 수도 있고, 기댓값과의 차이가 클 수도 있습니다.

그래서 확률분포가 기댓값을 중심으로 모여있는지 퍼져있는지(spread)를 나타내는 분산을 정의합니다. 분산이 크다는 것은 기댓값의 신뢰도가 떨어진다고도 생각할 수 있을 것 같습니다.

<div>

랜덤한 값 확률변수 $X$와 기댓값 차이는 $X-\mu$입니다. 만약 떨어진 거리를 구하겠다면 $| X-\mu |$처럼 절댓값을 씌울 수 있을 것입니다. 그러나 여러 가지 계산 이슈 때문에 제곱 오차를 주로 씁니다. $(X-\mu)^2$는 여전히 랜덤한 값입니다. 이것의 기댓값 $E[(X-\mu)^2]$은 고정된 값으로, 이를 <strong><font color="#3367E5">분산</font></strong>(variance)이라 하며, 좀 더 풀어쓰면 아래와 같습니다:

$$ \sigma^2 = V[X] = \sum_i (x_i - \mu)^2 p(x_i) $$

$$ \sigma^2 = V[X] = \int (x - \mu)^2 p(x) \,dx $$

$$ \sigma = \sqrt{V[X]} $$

<strong><font color="#3367E5">표준편차</font></strong>(standard deviation)는 분산의 square root입니다. 분산의 계산 과정에 제곱이 있기 때문에, 분산과 실제 편차의 수준이 직관적으로 맞지 않습니다. 단위를 맞추기 위해서 제곱근을 거치게 됩니다.
</div>

#### ◇ 분산의 성질

$$\begin{aligned}
&V[X] \geq 0 \\
&V[X] = E[(X-\mu)^2] = E[X]^2 - \mu^2 \\
&V[aX + b] = a^2V[X] \\
&V[X+Y] = V[X]+V[Y] \,, \quad \text{if } X \perp\!\!\!\perp Y \\
&V[X+Y] = V[X]+V[Y] +2\text{Cov}(X,Y)\,, \quad \text{if } X \not\! \perp\!\!\!\perp Y
\end{aligned}$$

분산은 항상 양수이며, 상수항은 분산과 무관하고 상수배는 제곱의 형태를 띕니다. 덧셈의 분산을 분산의 덧셈으로 나누려면 두 확률변수가 독립이어야 한다는 점에 유의 바랍니다.