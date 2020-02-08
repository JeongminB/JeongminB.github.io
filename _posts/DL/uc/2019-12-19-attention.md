---
title: "RNN, LSTM, seq2seq, Attention 훑어보기"
categories: [DL, DL-UC]
---

글의 주된 내용은 Attention이므로 RNN, LSTM, seq2seq에 대해서는 간단하게 다룹니다. Transformer에 대해서는 따로 다루겠습니다.

## ◆ RNN

흔히 쓰이는 신경망은 FF<sub>(feed forward)</sub> 방식입니다. 네트워크의 입력층에서 은닉층을 거쳐 출력층까지 인접한 레이어들이 연결되어 있고, Tensor<sub>(값, 정보)</sub> 는 입력에서 출력으로 향하는 방향으로만 전달됩니다.

그러나 데이터 중에서는 순서나 흐름이 중요한 것들이 있습니다. 음성이라든지, 주식 차트, 자연어가 대표적인 예시일 겁니다. 특히 자연어 분야에서 문장 속 단어가 담고 있는 semantic<sub>(의미)</sub> 은 일반적인 FF 신경망으로 학습하기 어렵습니다.

RNN<sub>(Recurrent Neural Network)</sub> 은 순환 신경망을 말합니다. 신경망에 입력이 순서대로 입력되고, 각 step 마다의 출력을 얻을 수 있습니다. 또한, 입력과 별개로 이전 step 에서의 state를 받게 됩니다. 이로써 sequence data의 흐름적 정보를 얻게 됩니다.

step의 출력이 다시 모델의 입력으로 들어가기 때문에 순환하는 구조와도 같으며, 보통 모델의 hidden state $h$ 라고 표현합니다.

<p>
<img src='/assets/res/dl/rnn.png' width='60%' class='center'/>
<span class='center'>colah.github.io</span>
</p>

RNN도 step을 따라 펼쳐서 보면 본질적으로는 일반 신경망과 동일합니다. 그림처럼 step 방향으로 unrolling해서 표현합니다. 당연히도 backpropagation을 수행할 수 있고, 특별히 RNN같은 경우는 BPTT<sub>(Backpropagation Through Time)</sub>라고 부릅니다.

<p>
<img src='/assets/res/dl/rnn2.jpeg' width='100%' class='center'/>
<span class='center'> Suleka Helmini (TDS)</span>
</p>

일반적인 RNN은 $t$ 시점에서 입력 $x_t$와 $h_{t-1}$에 대한 각각의 파라미터가 존재하여 선형 연산 후에 더해집니다. $h_{t-1}$는 output 출력을 위해 연산을 한 번 더 거치거나 $h_{t}$로 넘어가고, 이러한 과정을 반복합니다. 이때 각 step에서의 파라미터는 동일합니다. 즉, 그림의 unrolled unit은 계산의 순서가 다르고 내놓는 값이 다를 뿐 내부적으로는 실체가 동일한 네트워크입니다.

parameter sharing을 하는 이유는 조금만 고민해보면 답이 나옵니다. 전체 시퀀스에 대한 동일한 규칙을 적용할 수 있고, 길이가 다른 입력에 대해서도 일반화가 가능하며, input 길이에 맞춰 따라 파라미터가 늘어나거나 하지 않는다는 장점 등이 있습니다.

---

## ◆ LSTM

simple RNN의 단점이라면, output과 거기에 영향을 미치는 input의 step 격차가 크면 gradient vanishing, exploding 문제가 발생하기 쉽다는 것입니다. 순전파에서도 같은 파라미터가 계속 $h$에 곱해지면서 이전의 정보들은 점차 희미해질 것입니다.

<p>
<img src='/assets/res/dl/lstm.png' width='80%' class='center'/>
<span class='center'>colah.github.io</span>
</p>

그래서 제시된 모델이 LSTM<sub>(Long Short-Term Memory)</sub> 입니다. 여기에는 cell state $c$가 추가로 존재합니다. 또한 LSTM이나 GRU에는 gate라는 개념이 존재합니다. LSTM에는 Forget Gate, Input Gate, Output Gate가 존재하죠. 이러한 구조로 LSTM은 장기 의존 관계를 학습할 수 있게 됩니다. GRU에 대한 설명이나 LSTM 셀에서 일어나는 구체적인 연산은 생략하겠습니다.

---

## ◆ seq2seq

<p>
<img src='/assets/res/dl/seq2seq.png' width='100%' class='center'/>
<span class='center'>github.com/tensorlayer</span>
</p>

sequence to sequence는 말 그대로 시퀀스 데이터를 다른 시퀀스 데이터로 만드는 일을 합니다. 여기서 제시하는 모델로 단순한 chatbot이나 machine translation 모델을 구현할 수도 있습니다. seq2seq 모델은 위처럼 LSTM 등으로 이루어진 Encoder와 Decoder 구조로 나뉘는데, 입력으로 쓸 문장 따위를 토큰화하여 순서대로 입력하게 됩니다. 마지막 LSTM cell의 hidden state는 디코더의 초기 상태로 받게 됩니다.

디코더에는 문장의 시작과 끝을 알리는 `<sos>`, `<eos>` 같은 특별한 토큰이 쓰입니다. 인코더로부터 받은 은닉 상태와 `<sos>`를 받으면 디코더는 스스로 `<eos>`를 반환할 때까지 어떤 출력을 내놓게 됩니다. 인코더와 달리 디코더는 이전에 출력한 단어가 다시 입력으로 들어가는 것에 주목합시다.

seq2seq를 훈련할 때에는 인코더에 입력을 넣어 얻은 context vector와 디코더를 훈련시킬 정답 시퀀스를 넣어줘야 합니다. 위 예시에서는 각 스텝마다 `<start> | Yes, | What's | up?`를 넣어주고 각 스텝마다 `Yes, | What's | up? | <end>`를 내놓도록 학습을 시킵니다. 실제로 사용할 때는 context vector와 `<start>`만을 디코더 입력으로 넣으며 이전 step에서의 단어를 다시 입력으로 받도록 모델을 수정하면 됩니다.

또한 신경망이 토큰을 처리할 수 있도록 문자(열) 형태에서 벡터로 바꾸는 작업을 해줍니다. 일반적으로 신경망은 숫자로 이루어진 데이터만 처리하기 때문입니다. 대부분의 단어는 연속적인 관계를 가지지 않고 categorical하기 때문에 one-hot vector로 단어를 표현할 수 있을텐데, 이 방법은 몇 가지 문제가 있습니다.

일단 corpus가 커질수록 입력 벡터가 커집니다. 벡터는 모두 같은 크기를 가지고 같은 거리만큼 떨어져 있으며, 단 하나의 차원을 제외하고 모두 0이란 값을 가집니다 (sparse함). 단어 사이에 어떠한 정보나 연관성도 담지 못하고 크기만 커질 뿐입니다.

<p>
<img src='/assets/res/dl/word2vec.png' width='80%' class='center'/>
<span class='center'>ResearchGate</span>
</p>

그래서 비교적 저차원 단어 벡터를 얻기 위한 word embedding 작업을 거치게 됩니다. embedding layer를 LSTM 앞에 연결한다든지, 사전 훈련된 word2vec 같은 unsupervised model을 이용하는 방법이 있겠습니다. 한 가지 유의할 부분은, 프레임워크에서 제공하는 **embedding layer를 쓰는 경우, 모델 훈련에서 쓰이는 loss function 값을 최소화하기 위한 벡터 표현을 얻을 뿐이지 word2vec과 같은 semantics 학습이 보장되는 건 아닙니다.**

---

## ◆ Attention

seq2seq 모델은 인코더에서 context vector를 만들어서 decoder로 넘깁니다. 이 vector의 크기는 고정되어 있고 인코더의 마지막 스텝까지 와서야 얻을 수 있습니다. 입력 시퀀스가 아주 길다면 정보의 손실이 일어날 수밖에 없고, 학습을 위한 gradient 전파 역시 LSTM을 쓴다 하더라도 소실되는 것을 피할 수는 없을 것입니다.

그래서 기존의 seq2seq 모델에 Attention이라는 새로운 구조를 도입합니다. LSTM 같은 경우 hidden state와 cell state가 있고 이를 인코더가 context vector로 디코더한테 넘겨주는데, 이것만 보고 긴 시퀀스 데이터를 처리하는 건 힘드니, 인코더의 hidden state를 모두 모아두었다가 디코더의 각 step에서 이들을 보면서 참고하겠다는 것입니다.

기계 번역을 예로 들어보겠습니다.

* **(1) `ちょっと` `静かに` `しなさい`。→ `조용히` `좀` `해라`.**
* ちょっと (좀), 静かに (조용히), しなさい (해, 해라, 하렴)

인코더에는 `ちょっと`, `静かに`, `しなさい`가 순서대로 들어갑니다. 각각의 hidden state를 $h_1$, $h_2$, $h_3$ 라고 하겠습니다. 디코더를 학습시킬 때 먼저 인코더의 state를 물려받고 `<sos>`를 넣어 `조용히`가 나오도록 (step $t_1$), `조용히`를 넣어 `좀`이 나오도록(step $t_2$), `좀`을 넣어 `해라`가 나오게(step $t_3$), `해라`를 넣어 `<eos>`가 나오게 학습을 시킵니다 (step $t_4$).

Attention이 도입된다면, 올바른 번역을 위해서 $t_1$에서는 $h_2$를 (`조용히`라는 의미 포함), $t_2$에서는 $h_1$을 (`좀`이라는 의미 포함), $t_3$에서는 $h_3$을 (`해라`라는 의미 포함) 참고해야 할 겁니다. 저는 맨 처음에 이해가 안 갔습니다. 신경망에다 각 단어의 의미를 알려주는 것도 아니고, 두 언어간 대응 관계를 알려주는 것도 아닌데, 번역을 위해서 자신이 참고해야할 state를 신경망이 어떻게 학습하는가? 이게 제 의문이었습니다.


* **(1) `ちょっと` `静かに` `しなさい`。→ `조용히` `좀` `해라`.**
* **(2) `ちょっと` `しなさい`。→ `좀` `해라`.**
* **(3) `静かに` `しなさい`。→ `조용히` `해라`.**
* **(4) `おとなしく` `しなさい`。→ `얌전히` `있어라`.**

사실 대규모 말뭉치에서 학습한다는 사실을 떠올리면 금방 받아들일 수 있습니다. 일반적인 seq2seq 모델을 생각해봅시다. (1)~(3)를 보면 `しなさい`가 마지막으로 입력된 인코더의 context vector만 받고, `<sos>`를 받아 서로 다른 단어를 처음에 출력해야 합니다. 올바르게 번역이 되었다면, 인코더에 특정 단어를 넣었을 때 나오는 state vector 정보를 context vector 속에서 인지했다는 것입니다. 즉, 단어 간 alignment를 학습한 셈입니다.

Attention에서는 각각의 hidden state vector를 직접 참고할 수 있으니 정확도와 품질이 seq2seq보다 낫습니다. 어쨌든 번역되는 단어에 대응되는 벡터를 찾을 수 있어야 하는데, 여러 구현법이 있겠습니다만 큰 틀은 다음과 같습니다.

* 인코더의 hidden states와 디코더의 hidden state 사이의 score 계산
* softmax를 통해 합이 1이 되도록 정규화 (attention weights)
* attention weights와 hidden states로 weighted sum 계산 (context vector)
* 디코더의 hidden state와 context vector를 같이 고려해 output 생성

<p>
<img src='/assets/res/dl/attention1.jpg' width='60%' class='center'/>
<span class='center'>https://arxiv.org/abs/1508.04025v5</span>
</p>

score는 각 단어의 중요도와도 같습니다. 벡터 간 cosine이나, $\mathbf h_t^{\mathsf T} \mathbf W \bar {\mathbf h}_s$ 처럼 <a href="/dl-uc/bilinear/">bilinear</a> 연산을 통해 학습하는 일반적인 방법도 있지만 (Luong's style), 가장 간단한 방법은 두 벡터간 내적이 아닌가 싶습니다.

$$ \mathrm {score}(\mathbf h_t, \bar {\mathbf h}_s) = {\mathbf h_t}^{\mathsf T}  \bar {\mathbf h}_s $$

신경망은 주목해야 할 입력의 $\mathbf h_s$와 $\mathbf h_t$ 사이의 score를 높이는 hidden state vector 출력을 학습하게 됩니다.

`[max_len, h_size]` shape의 $\bar {\mathbf h}_s$와 `[1, h_size]` shape의 $\mathbf h_t$를 내적하면 참고하는 hidden state vector의 개수만큼 score를 얻게 됩니다. (인코더 output에 해당하는 $\bar {\mathbf h}_s$의 shape은 입력 시퀀스 최대 길이로 고정되어 있음)

$$ a_{ts} = \frac{\exp (\mathrm {score}(\mathbf h_t, \bar {\mathbf h}_s))}{\sum_{s^\prime=1}^S \exp (\mathrm {score}(\mathbf h_t, \bar {\mathbf h}_s))} $$

얻은 score들을 softmax 함수를 거쳐서 합이 1이 되도록 정규화하면 attention weights $a_{ts}$를 얻습니다. 각 hidden state vector에 적용될 가중치를 구했으니 번역에 필요한 맥락이 담긴 context vector $\mathbf c_t = \sum_s a_{ts} \mathbf h_s$를 구할 수 있습니다. 중요한 벡터의 성분이 많이 들어있고, 중요하지 않은 벡터는 거의 포함되지 않을 것입니다.

context vector $\mathbf c_t$와 디코더의 step $t$에서의 $\mathbf h_t$가 있으므로 이제는 신경망을 통해서 단어를 유추시키면 됩니다. 여기에도 여러가지 방법이 가능합니다. 둘을 concat해서 출력 단어를 내놓도록 신경망을 학습시키면 되겠습니다.

추가로, seq2seq의 성능을 올리기 위해 LSTM layer를 쌓거나, ResNet처럼 skip connection을 도입하거나, 입력의 순서를 뒤집어서 문장을 거꾸로 훑어 만들어낸 hidden state를 같이 고려하는 Bidirectional LSTM 구조를 도입할 수 있습니다.

---

## 참고할만한 링크

https://aikorea.org/blog/rnn-tutorial-3/ : BPTT, Vanishing Gradient

http://colah.github.io/posts/2015-08-Understanding-LSTMs/

https://towardsdatascience.com/sequence-models-by-andrew-ng-11-lessons-learned-c62fb1d3485b

https://www.quora.com/What-is-the-embedding-layer-in-LSTM-long-short-term-memory

https://stats.stackexchange.com/questions/324992/how-the-embedding-layer-is-trained-in-keras-embedding-layer

https://9bow.github.io/PyTorch-tutorials-kr-0.3.1/intermediate/seq2seq_translation_tutorial.html