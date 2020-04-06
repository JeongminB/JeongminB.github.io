---
title: "orthogonal basis function"
categories: [Basics, B-UC]
---

Fourier transform 들어가기 전에 Fourier series 들어가기 전에 뭐 좀 알아봅시다 (?) 

이전 글: <a href="/basics/b-uc/euler/
">Taylor series, Euler’s formula</a>

---

## ◆ vector space

선형대수학에서 말하는 <strong><font color='#FF7D33'>vector</font></strong>는 그냥 vector space의 원소를 말합니다. 벡터공간이 성립하려면 벡터들과 스칼라 사이에서 여러 조건을 만족해야 합니다.

덧셈에 대한 항등원 (영벡터), 덧셈에 대한 역원이 존재해야 하고, 벡터 간 교환법칙과 결합법칙이 성립해야 하며, 스칼라와 벡터 사이에 분배법칙과 결합법칙이 성립하면 됩니다. 우리에게 익숙한 2차원 3차원 직교좌표계에서 다루는 벡터를 떠올리면 쉽게 알 수 있습니다. (간단히 말해, 선형조합 연산에 닫혀있음)

$$ a \hat{\mathbf i} + b \hat{\mathbf j} $$

우리는 <strong>임의의 벡터를 그 벡터 공간의 basis vector (기저벡터) 들의 linear combination (선형조합) 으로 나타낼 수 있습니다</strong>. 그리고 이들의 가능한 모든 조합의 집합을 span (기저의 확장공간?) 이라고 말합니다.

<p>
<img src='/assets/res/etc/f8.png' width='60%' class='center'/>
</p>

$$ \vec{\mathbf v} = a \hat{\mathbf i} + b \hat{\mathbf j} + c \hat{\mathbf k} $$

일반적인 n-dimensional Euclidean space에서 n개의 기저벡터들의 span이 n차원 공간이 되려면 각각의 기저벡터들은 <strong><font color='#FF7D33'>linearly independent</font></strong> (선형독립) 이어야 합니다. 그렇다면 벡터를 basis와 scalar 사이의 선형조합으로 표현하는 방법이 유일해집니다. (선형독립 판별은 여기서 다루지 않습니다)

linearly dependent하면 n개의 기저의 선형조합이 n차원 공간 전체로 확장될 수 없고 subspace를 이루며 이는 redundant한 기저벡터가 존재한다는 의미입니다.

---

## ◆ orthogonal basis

벡터들이 <strong><font color='#3367E5'>orthogonal</font></strong> 하다는 것은 직교 (直交) 한다, 수직 (perpendicular) 을 이룬다는 것을 의미합니다. 유클리드 공간에서 벡터의 직교 여부를 판단하는 법은 내적 (dot product) 을 구해보는 것입니다.

$$ \begin{aligned} \mathbf a\cdot \mathbf b &= \|\mathbf a\| \|\mathbf b\| \cos\theta, \\
\mathbf a^T\mathbf b &= a_1 b_1 + a_2b_2 + \cdots + a_nb_n \end{aligned} $$

기하학적으로는 벡터 하나를 투영시켜서 이들의 길이를 곱하는 것이므로, <strong>두 벡터가 직교인 경우 내적은 0</strong>이 됩니다.

+) 여담으로, 첫 번째 정의에서 우변에 $\cos \theta$만 남겨놓으면 두 벡터의 cosine similarity가 됩니다.

$$ \mathbf u_i \cdot \mathbf u_i = |\mathbf u_i|^2 = 1, \quad i=1,2,3 $$

$\hat{\mathbf i}, \hat{\mathbf j}, \hat{\mathbf k}$ 대신, 벡터 공간의 기저를 $\mathbf u_i$라고 하겠습니다. 이들의 크기가 모두 1인 unit vector이고 서로 직교한다면, <strong><font color='#3367E5'>orthonormal</font></strong> (정규직교) 하다고 말합니다.

$$ \begin{aligned}
\mathbf u_1 \cdot \mathbf u_1 = 1,\quad \mathbf u_2 \cdot \mathbf u_2 = 1,\quad \mathbf u_3 \cdot \mathbf u_3 = 1 \\
\mathbf u_1 \cdot \mathbf u_2 = 0,\quad \mathbf u_1 \cdot \mathbf u_3 = 0,\quad \mathbf u_2 \cdot \mathbf u_3 = 0
\end{aligned} $$

기저들이 정규직교하는 기저라면, 같은 기저 벡터끼리의 내적은 1이 되고, 다른 기저 벡터끼리의 내적은 0이 됩니다. 물론 기저들은 서로 선형독립이구요. 이 성질을 이용하면, 우리는 임의의 벡터를 직교 벡터들의 선형조합으로 분해하는 것이 가능합니다. 방법은 다음과 같습니다.


$$ \mathbf x = \sum_i \left\langle \mathbf x, \mathbf u_i \right\rangle \mathbf u_i = \left\langle \mathbf x, \mathbf u_1 \right\rangle \mathbf u_1 + \left\langle \mathbf x, \mathbf u_2 \right\rangle \mathbf u_2 + \left\langle \mathbf x, \mathbf u_3 \right\rangle \mathbf u_3 $$

<div>

<strong>각 기저벡터와 벡터 $x$와의 내적은 그 기저가 놓인 선 위로의 projection 이고, 이는 해당 벡터를 기저로 표현하기 위한 scalar 값이 됩니다</strong>. 만약에 기저가 orthogonal 하다면 scalar를 $\|\mathbf u_i\|^2$로 나누어줘야 합니다 (잘 기억하세요~).
</div>

---

## ◆ L2 inner product of functions

$$ \int_a^b |f(x)|^2dx <\infty $$

Hilbert space 중 하나인 $L^2$ space에서 함수 $f(x)$는 위 조건을 만족합니다. 이 공간을 이루는 원소는 $L^2$ function, 혹은 다른 말로 square-integrable function 입니다. 연속함수도 염언히 더하거나 곱할 수 있고 scalar 연산에도 자유롭기 때문에 vector space에 해당합니다.

당분간 시간에 대한 신호만 다룰 건데, 시구간 $[a, b]$ 사이에서 두 함수의 내적은 다음과 같이 정의합니다.

$$ \left\langle f, g \right\rangle = \int_{t_1}^{t_2} f(t) g^*(t)dt $$

복소수 영역까지 다룰 것이기 때문에 conjugate를 취합니다. 위에서 다뤘던 '벡터 성분별 곱의 합'으로 구하는 내적의 정의를 떠올리면 둘을 어렵지 않게 연관지을 수 있습니다. 그리고 다음과 같이 동일한 함수 사이에서 내적을 하면 <strong><font color='#FF7D33'>신호의 에너지</font></strong>가 나옵니다.

$$ E = \left\langle f, f \right\rangle = \int_{t_1}^{t_2} f(t)f^*(t) dt = \int_{t_1}^{t_2} |f(t)|^2 dt $$

이 에너지는 실제 물리적인 에너지를 의미하는 건 아니고, 신호를 정량적으로 표현하여 비교할 수 있도록 해줄 뿐입니다. 에너지를 적분 구간으로 나누어 평균 에너지를 구하면 그것이 신호의 전력 (power, 역시나 신호 관점의 전력) 이고, square root를 취해주면 실효값 (Root Mean Square) 인데 주로 다룰 내용은 아니라 넘어가겠습니다.

$$ \left\langle u_i(t), u_j(t) \right\rangle = \begin{cases}0  & \text{if } i\neq j \\ E_{u_i} & \text{if } i=j
\end{cases} $$

함수의 내적이 정의된 공간에서, 만약에 위처럼 직교하는 함수의 집합이 있다면, 그리고 그것을 기저함수로 둔다면 함수의 신호를 기저함수의 선형조합으로 나타낼 수 있지 않을까요?

<p>
<img src='/assets/res/etc/f7.png' width='80%' class='center'/>
</p>

가능합니다. $L^2$ space 에서는 어떤 함수를 직교하는 기저함수의 선형조합으로 나타낼 수 있습니다. 물론 기저함수의 집합이 완전해야 하지만요. 위와 같은 경우는 기저 함수들이 직교하지만 (자신과의 내적 (=에너지) 은 1, 남과의 내적은 0), 보다 일반적인 신호를 표현할 수는 없겠죠.

---

## ◆ period, frequency

복소 지수함수 $e^{i\varphi}$를 기저함수로 쓰면 어떨까요? 여기서 주목할 점이 있는데 복소 지수함수는 각도 $\varphi$가 변함에 따라 단위원의 둘레를 회전하고 $2\pi$만큼 움직이면 제자리로 돌아오게 됩니다. 만약 시간에 대한 신호라면 다음과 같이 각속도 $\omega$ 를 따질 수 있습니다.

$$ \begin{aligned}
v &= \frac{s}{t} \; (m/s), \quad s = vt \; (m), \\
\omega &= \frac{\varphi}{t} \; (\text{rad}/s), \quad \varphi = \omega t \; (\text{rad}).
\end{aligned}$$

각속도는 회전한 각을 시간으로 나눈 값이라고 볼 수 있겠죠.. 각속도 $\omega$가 $\pi (\text{rad}/s)$라면, $2\pi$ (주기 $T$) 만큼 이동하는데 2초가 걸릴 겁니다. 즉, 각속도는 $\omega = 2\pi / T$ 라고 쓸 수도 있습니다.

$$ e^{i\varphi} = \cos \varphi + i\sin \varphi $$

오일러 공식에 따르면 $e^{i\varphi}$는 진동하는 cosine과 sine를 복소수로 결합?시킨 겁니다. 이 두 신호는 모두 진동하는 함수이고, '주파수'라는 개념을 따질 수 있죠. sine 파를 가지고 파형의 주기와 주파수를 생각해봅시다.

<p>
<img src='/assets/res/etc/f9.png' width='80%' class='center'/>
</p>

가장 작은 주기를 $T_0$라고 합시다. $x(t) = x(t+T)$를 만족하면 주기신호이기 때문에 $T_0, 2T_0, 3T_0, \cdots$ 이들도 모두 주기에 해당합니다. 앞으로 다루는 주기는 $T_0$와 같은 <strong><font color='#FF7D33'>기본 주기</font></strong> (fundamental period) 로 생각하겠습니다. 시간적 <strong>주기는 단위 사이클 당 걸린 시간</strong> (s)을 의미하고, 이것의 역수는 주파수 $f$가 됩니다 (1초당 몇 사이클 진행하는지).

$$ T = \frac{2\pi}{\omega} = \frac{1}{f} \quad (s), \quad \omega=\frac{2\pi}{T} = 2\pi f \quad (\text{rad}/s) $$

다시 정리해보면 위와 같습니다. $\omega$는 각속도, 각주파수, 각진동수 라는 용어를 혼용하곤 합니다. 정현파를 등속원운동으로 설명할 수 있어서 값이 같은 거지 의미적으로는 다르다고 생각합니다.

<br>

마침 주파수 $f$ 이야기가 나왔으니 convolution 글 마지막에서 언급했던 신호를 주파수 측면에서 다루는 이유를 간략히 알아봅시다.

<p>
<img src='/assets/res/etc/f10.png' width='60%' class='center'/>
</p>

위와 같은 정현파들의 선형조합인 신호가 있다고 합시다 (초록색). 시간 영역에서 파형을 표시하면 보기에도 복잡하지만 분석하기도 어렵습니다. 그런데 주파수 영역에서 보면 그냥 각각의 정현파들의 주파수와 크기를 표시하기만 하면 이 신호에 대한 모든 정보를 담게 되는 것입니다.

위처럼 예쁜 모양의 파형 말고 마구잡이로 생긴 일반적인 신호도 정현파들로 분해시켜서 주파수 도메인으로 변환해주는 것이 가능한데, 그게 바로 푸리에 변환입니다. 푸리에 급수나 푸리에 변환이 어떤 함수로 수렴할 '충분' 조건이 있지만 (Dirichlet Condition) 공학적인 활용 측면에서는 굳이 신경쓰지 않아도 될 것 같고 저도 다루지 않겠습니다 (어려웡).

주파수 영역에서 신호를 보면 신호를 해석하는 새로운 관점을 얻게 됩니다. 이미지 쪽에서도 쓰일 수도 있고 특히 소리나 진동 형태의 데이터의 분석 및 처리에 유용합니다 (통신, 음악, 영상, 유지보수, LTI system의 주파수응답 (steady state) 해석 등 활용 범위가 넓음).

---

## ◆ complex exponential basis function

복소 지수함수 $e^{i\varphi}=e^{i\omega t}$ 를 기저함수로 쓰면 어떨까? 라는 내용으로 돌아와봅시다. 이러한 기저함수를 가지고 급수로 전개할 함수를 '주기함수'로 한정할 것입니다. (스포: 푸리에 급수 이야기임)

먼저 주기함수의 기본 주기를 $T_0$라고 합시다. 그러면 같은 주기를 갖는 복소 지수함수는? 기본 주파수가 $f_0$이고, $\omega=2\pi f$ 이므로, $e^{i2\pi f_0 t}$ 입니다. 다시 한 번 말하지만 복소 지수함수는 주파수를 갖는 sine과 cosine으로 이루어집니다.

푸리에 급수에서는 이 기본 주파수 $f_0$의 <strong><font color='#FF7D33'>n차 고조파</font></strong> (harmonics) 집합을 기저 함수로 사용합니다. $n$차 고조파의 주파수는 $nf_0$입니다 ($n$은 정수). 즉, $n$차 고조파를 갖는 복소 지수함수는 $e^{i2\pi nf_0t}$ 입니다. 표기가 복잡하기 때문에 $\omega_0 = 2\pi f_0$ 인 점을 이용해 $e^{in\omega_0 t}$ 라고 쓰기도 합니다.

$$ \left\langle e^{im\omega_0 t}, e^{in\omega_0 t} \right\rangle = \int_{T_0} e^{im\omega_0 t} (e^{in\omega_0 t})^* dt $$

그러면 정수 $m, n$에 대해서 이 직교함수 집합이 orthogonal basis인지 확인해봅시다. 테일러 급수는 주기가 $T_0$인 주기함수를 다루기 때문에, $T_0$ 만큼의 적분구간에 대해서 만족하면 나머지 전체 구간으로 이야기를 확장할 수 있습니다.

내적했을 때 $m=n$인 경우는 에너지 $E$의 값을 가지고, $m\neq n$이면 0이 나와야 합니다. orthonormal basis ($E=1$) 가 아니어도 <strong>기저성분과 신호의 내적을 E로 나눠주면</strong> 똑같이 급수로 분해할 수 있습니다.

$$ \begin{aligned}
\int_{T_0} &e^{im\omega_0 t} (e^{in\omega_0 t})^* dt \\
= &\int_{T_0} e^{im\omega_0 t} e^{-in\omega_0 t} dt \\
= &\int_{T_0} e^{i(m-n)\omega_0 t} dt \\
= &\begin{cases}0  & \text{if } m\neq n \\ T_0 & \text{if } m=n
\end{cases}
\end{aligned} $$

$m=n$이면 적분 안쪽이 1이니까 내적이 (에너지가) $T_0$가 됩니다. $m\neq n$인 경우는 해보시면 cosine 성분은 상쇄되어 없어지고, sine 성분은 적분 구간을 $[0, T_0]$ 이나 $[-{T_0 \over 2}, {T_0 \over 2}]$ 따위로 잡았을 때 $\pi$의 정수배가 되어 0이 됩니다. 이로써 정수배의 주파수를 갖는 복소 지수함수들은 서로 직교하는 것을 알 수 있습니다 (정현파들도 마찬가지).