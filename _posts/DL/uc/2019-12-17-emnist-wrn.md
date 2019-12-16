---
title: "ResNet, WRN 훑어보기"
categories: [DL, DL-UC]
---

## ◆ ResNet 훑어보기

자세한 구조보다는 Residual Network에 쓰인 중요 개념만 다루고 가겠습니다.

먼저 ResNet보다 먼저 나온 VGGNet은 kernel size를 3x3으로 고정한 상태에서 층을 깊게 만드는 것이 kernel size를 크게하고 층을 얕게 만드는 것보다 성능이 낫다는 것을 보여주었습니다. 그러나 너무 깊은 모델에서는 성능이 오히려 떨어지는 모습을 보입니다. 모델의 overfitting과 관련 없이 층이 깊어지면서 성능이 떨어지는 현상을 <strong><font color='#FF7D33'>degradation</font></strong>  현상이라고 합니다.

<p>
<span class='center'>
<img src='/assets/res/dl/wrn1.png' width='85%' /></span>
<span class='center'>https://arxiv.org/pdf/1512.03385</span>
</p>

20층 짜리 모델을 먼저 학습시키고, extra layer를 삽입한 56층 모델을 구성하면 어떨까요? 추가되는 레이어를 identity mapping 하도록 세팅한다면 적어도 같은 error를 가지거나 성능이 개선되지 않을까 기대할 수 있겠으나.. 현실은 위와 같이 성능이 나빠졌습니다.

<p>
<span class='center'>
<img src='/assets/res/dl/res1.png' width='60%' /></span>
</p>

ResNet을 소개한 논문에서는 degradation 문제를 위와 같은 구조의 block으로 해결합니다.

$$ \mathcal H(\mathbf x) = \mathcal F(\mathbf x) + \mathbf x $$

만약 더해지는 두 값의 dimenstion이 일치하지 않는다면 identity $\mathbf x$에 linear projection을 통해서 일치시켜야 합니다. 우리가 원하는 어떤 mapping $\mathcal H(\mathbf x)$ 가 있다면, 실질적인 네트워크의 학습 대상은 다음과 같아집니다.

$$ \mathcal F(\mathbf x) = \mathcal H(\mathbf x) - \mathbf x $$

이처럼 desired underlying mapping 과 관측값 차에 대해서 학습하는 것입니다. 만약에 원하는 매핑 $\mathcal H(\mathbf x)$가 identity mapping이라면 단지 신경망은 0을 출력하도록 학습하면 됩니다. 아무래도 이러한 방식이 plain network에서 nonlinear layers에 $\mathbf x$를 입력해서 $\mathbf x$를 그대로 출력하도록 학습시키는 것보단 쉽지 않을까요?

shortcut을 통해 레이어를 건너뛰는 skip connection 방식은 순전파에서는 이전 레이어의 활성화 값을 재사용함으로써 RNN처럼 이전 값들의 유의미한 정보를 같이 고려하게 되는 효과를 줄 것으로 보이며,

$$ \mathbf y = \mathbf x + \mathcal F(\mathbf x), $$

$$ \begin{aligned}
\frac{\partial E}{\partial \mathbf x} &= \frac{\partial E}{\partial \mathbf y} \frac{\partial \mathbf y}{\partial \mathbf x} \\
&= \frac{\partial E}{\partial \mathbf y} (1 + \frac{\partial }{\partial \mathbf x} \mathcal F(\mathbf x))
\end{aligned} $$

덧셈 연산으로 연결되기 때문에 역전파에서 vanishing gradients 문제를 방지할 수 있을 것으로 보입니다.

<br>

<p>
<span class='center'>
<img src='/assets/res/dl/res2.png' width='100%' /></span>
</p>

ResNet을 구성하는 residual block도 다양한 구조로 실험해볼 수 있습니다. 논문에서는 activation과 normalization의 위치를 바꾸어가며 실험을 하였는데, BN ReLU 를 먼저 적용한 pre-activation 방식이 성능이 좋았습니다.

addition 이후에 ReLU를 거치게 되면 음의 값이 걸러지기 때문에 $\mathbf x$가 온전하게 전달되지 않습니다 [(a) 참고]. 특히, $\mathcal F(\mathbf x)$ 끝에 ReLU를 붙이게 되면 함수의 값 표현에 제약이 생긴 셈입니다 [(c) 참고]. 그래서 ReLU는 weight path로 뺍니다 [(d) 참고]. 연속된 (a)를 생각해보면 ReLU를 weight path로 뺀 것이 (d) 모양임을 알 수 있습니다.

BN이 shortcut 상에 놓이게 되면, 각 block 마다 변형된 정보를 넘기기 때문에 성능이 나빠집니다 [(b) 참고]. 그리고 addition 직전에 BN을 거치는 것은 $\mathbf x$가 합쳐지면서 다시 unnormalize 된 신호가 입력으로 들어가는 꼴이 됩니다 [(d) 참고]. 그래서 최종적으로 (e)와 같은 구조를 취하게 된 것입니다. 

---

## ◆ Wide ResNet 훑어보기

<strong><font color='#3367E5'>WRN</font></strong>은 Wide Residual Networks 를 말합니다. 

<p>
<span class='center'>
<img src='/assets/res/dl/res3.png' width='70%' /></span>
</p>

ResNet은 skip connection을 통해서 깊은 모델을 훈련시킬 수 있었는데, 50층 이상의 모델에서는 파라미터 수와 훈련 시간을 줄이기 위해 bottleneck 형태로 residual block을 바꾸었습니다. 1x1 크기의 kernel을 갖는 convolution layer는 차원의 축소 및 확장 (복원)을 담당하게 됩니다.

그러나 기존의 ResNet은 네트워크 구조 특성상 shortcut이 있기 때문에, 학습을 위해 gradient를 전파할 때 weight path로의 강제하는 능력이 떨어진다고 볼 수 있습니다. 그래서 층이 깊은 경우 useful representation을 학습하는 block은 몇 개 없거나, 많은 블록들이 적은 정보를 가지며 인접 블록과의 정보 공유가 거의 이루어지지 않을 수 있습니다.

즉, 깊은 ResNet은 <strong><font color='#FF7D33'>diminishing feature reuse</font></strong> (loss in information flow) 문제가 존재할 수 있습니다. *"Deep Networks with Stochastic Depth(2016)"* 논문에서는 dropout 방식처럼 무작위로 residual block을 비활성화 (즉, identity function과 같아짐) 시키는 방법으로 모델을 개선시켜 문제를 해소하기도 했습니다.

(작성중)

---

## References

Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun, *"Deep Residual Learning for Image Recognition"*, 2015

Sergey Zagoruyko, Nikos Komodakis, *"Wide Residual Networks"*, 2016

Gao Huang, Yu Sun, Zhuang Liu, Daniel Sedra, Kilian Weinberger, *"Deep Networks with Stochastic Depth"*, 2016