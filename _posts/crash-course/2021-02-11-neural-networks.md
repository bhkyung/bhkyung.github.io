---
title:  "신경망(Neural Networks)"
search: true
categories:
  - crash-course
toc: true
toc_label: "목차"
sidebar:
  title: "Machine Learning"
  nav: sidebar-sample
use_math: true

---

## 구조(Structure)

출처: [Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course/introduction-to-neural-networks/video-lecture?hl=en)

신경망은 특성 교차의보다 정교한 버전입니다. 본질적으로 신경망은 적절한 특성 교차를 학습합니다.

<div class="notice--success">
학습목표
<ul>
    <li>특히 다음과 같은 신경망에 대한 직관을 개발합니다. </li>
    <ul>
        <li>숨겨진 레이어 (hidden layers) </li>
        <li>활성화 함수 (activation function)</li>
    </ul>
</ul>
</div>  


[특성 교차(Feature Crosses) 단원](https://developers.google.com/machine-learning/crash-course/feature-crosses/video-lecture?hl=ko)을 회상해보면, 다음 분류 문제(classification problem)는 비선형이다.

![데카르트 그래프기존 x축은 'x1'로 표시됩니다. 기존 y축은 'x2'로 표시됩니다. 파란색 점은 북서쪽 및 남동쪽 사분면을 차지합니다. 노란색 점은 남서쪽 및 북동쪽 사분면을 차지합니다.](https://developers.google.com/machine-learning/crash-course/images/FeatureCrosses1.png?hl=ko)

**그림 1. 비선형 분류 문제**

'비선형'이라는 의미는 $b + w_1x_1 + w_2x_2$ 형태의 모델로 라벨을 정확하게 예측할 수 없다는 의미입니다. 다시 말해, '결정 표면(decision surface)'은 선이 아닙니다. 앞서 비선형 문제의 가능한 모델링 방식으로 [특성 교차](https://developers.google.com/machine-learning/crash-course/feature-crosses/video-lecture?hl=ko)를 살펴보았습니다.

다음 데이터 세트를 고려해 보겠습니다.

![데이터 세트에는 주황색 및 파란색 점이 다수 있습니다. 일관된 패턴을 결정하기는 어렵지만 주황색 점은 살짝 나선형을 형성하고 파란색 점은 다른 나선형을 형성합니다.](https://developers.google.com/machine-learning/crash-course/images/NonLinearSpiral.png?hl=ko)

**그림 2. 더 복잡한 비선형 분류 문제(nonlinear classification problem)**

그림 2의 데이터 세트는 선형 모델로는 해결할 수 없습니다.

신경망이 비선형 문제를 해결하는 데 어떻게 도움이 되는지 알아보기 위해, 선형 모델을 그래프로 나타내 보겠습니다.

![연속된 파란색 원 3개는 그 위에 있는 녹색 원과 화살표로 연결되어 있습니다.](https://developers.google.com/machine-learning/crash-course/images/linear_net.svg?hl=en)

**그림 3. 그래프로 나타낸 선형 모델**

각 파란색 원은 입력 특성(feature)을 나타내고, 녹색 원은 입력의 가중 합(weighted sum of the inputs)을 나타냅니다.

이 모델을 어떻게 변경하여 비선형 문제 해결 능력을 개선할 수 있을까요?

### 히든 레이어(Hidden Layers)

아래 그래프로 나타낸 모델에서, 중간값의 '히든 레이어'를 추가했습니다. 히든 레이어에서 각 노란색 노드는 파란색 입력 노드 값의 가중 합(a weighted sum)입니다. 출력은 노란색 노드의 가중 합(a weighted sum)입니다.

!['입력'이라고 지정된 연속된 파란색 원 3개는 '히든 레이어'라고 지정된 그 위의 노란색 원으로 이루어진 열과 화살표로 연결되어 있으며, 노란색 원은 상단에 '출력'이라고 지정된 녹색 원과 연결되어 있습니다.](https://developers.google.com/machine-learning/crash-course/images/1hidden.svg?hl=en)

**그림 4. 2-레이어 모델의 그래프**

위 모델은 선형일까요? 그렇습니다. 출력은 여전히 입력의 선형 조합(a linear combination)입니다.

아래 그래프로 나타낸 모델에서, 가중 합의 두 번째 히든 레이어를 추가했습니다.

!['입력'이라고 지정된 연속된 파란색 원 3개는 '히든 레이어 1'이라고 지정된 그 위의 노란색 원으로 이루어진 열과 화살표로 연결되어 있으며, 노란색 원은 그 위에 '히든 레이어 2'라고 지정된 또 다른 노란색으로 이루어진 열과 연결되어 있고, 이 노란색 원은 상단의 녹색 원과 연결되어 있습니다.](https://developers.google.com/machine-learning/crash-course/images/2hidden.svg?hl=en)

**그림 5. 3-레이어 모델의 그래프**

위 모델은 여전히 선형일까요? 그렇습니다. 출력을 입력의 함수(a function)로 표현하고 단순화하면, 입력의 또 다른 가중 합을 얻게 됩니다. 이 합계는 그림 2의 비선형 문제를 효과적으로 모델링하지 않습니다.

### 활성화 함수(Activation Functions)

비선형 문제를 모델링하기 위해, 비선형성을 직접 도입할 수 있습니다. 우리는 각 히든 레이어의 노드가 비선형 함수(a nonlinear function)를 통과하도록 할 수 있습니다.

아래 그래프로 나타낸 모델에서 히든 레이어 1의 각 노드 값이 비선형 함수로 변환된 후에 다음 레이어의 가중 합으로 전달되었습니다. 이 비선형 함수를 활성화 함수(Activation Functions)라고 합니다.

!['비선형 변환 레이어'라고 지정된 분홍색 원으로 이루어진 열이 히든 레이어 두 개 사이에 추가된 것을 제외하면 이전 그림과 동일합니다.](https://developers.google.com/machine-learning/crash-course/images/activation.svg?hl=en)

**그림 6. 3-레이어 모델의 그래프와 활성화 함수**

이제 활성화 함수를 추가하였으므로, 레이어를 추가하면 효과가 더 큽니다. 비선형성을 누적하면(stacking nonlinearities) 입력과 예측 출력 간의 매우 복잡한 관계를 모델링할 수 있습니다. 간단히 말해, 각 레이어는 원시 입력(raw inputs)에 적용되는 더 높은 수준의 복잡한 함수를 효과적으로 학습합니다. 함수의 작동 방식을 자세히 알아보려면 [Chris Olah의 훌륭한 블로그 게시물](http://colah.github.io/posts/2014-03-NN-Manifolds-Topology/)을 참조하세요.

#### 일반적인 활성화 함수

다음 **시그모이드** 활성화 함수는 가중 합을 0과 1 사이의 값으로 변환합니다.
$$
F(x) = \frac{1}{1 + e^{-x}}
$$
다음은 플롯(a plot)입니다.

![시그모이드 함수](https://developers.google.com/machine-learning/crash-course/images/sigmoid.svg?hl=en)

**그림 7. 시그모이드 활성화 함수**

다음 **정류 선형 유닛**(rectified linear unit) 활성화 함수(**ReLU**)는 시그모이드와 같은 평활 함수(a smooth function)보다 조금 더 효과적이지만, 훨씬 쉽게 계산할 수 있습니다.
$$
F(x)=max(0,x)
$$
ReLU의 우월성은 경험적 결과를 기반으로 하며, 이는 ReLU의 반응성(responsiveness) 범위가 더 유용하기 때문일 것입니다. 시그모이드의 반응성은 양쪽(both sides)에서 상대적으로 빨리 떨어집니다.

![ReLU 활성화 함수](https://developers.google.com/machine-learning/crash-course/images/relu.svg?hl=ko)

**그림 8. ReLU 활성화 함수**

사실 어떠한 수학 함수라도 활성화 함수의 역할을 할 수 있습니다. σ가 활성화 함수(ReLU, 시그모이드 등)를 나타낸다고 가정해 보세요. 결과적으로 네트워크의 노드 값은 다음 수식으로 나타냅니다.
$$
\sigma (w\cdot x + b)
$$
텐서플로우에서는 [다양한 활성화 함수](https://www.tensorflow.org/api_docs/python/nn.html?hl=en)를 바로 사용할 수 있습니다. 하지만 ReLU로 시작하시는 것이 좋습니다.

### 요약

이제 우리 모델에는 사람들이 '신경망'이라고 말하는 모든 표준 구성요소를 갖추고 있습니다:

- 뉴런과 유사한 노드 집합이 레이어로 구성되어 있습니다.
- 각 신경망 레이어와 하위 레이어와의 연결을 나타내는 가중치 집합(a set of weights). 하위 레이어는 또 다른 신경망 레이어(another neural network layer)이거나 유형이 다른 레이어(some other kind of layer)일 수도 있습니다.
- 편향 집합(a set of biases), 각 노드에 하나.
- 레이어에서 각 노드의 출력을 변환하는 활성화 함수. 레이어마다 활성화 함수가 다를 수 있습니다.

주의: 신경망은 특성 교차보다 효과적이지 않은 경우도 있지만, 대개 효과적인 유연한 대안을 제공합니다.
{: .notice--danger}

## [Playground 실습](https://developers.google.com/machine-learning/crash-course/introduction-to-neural-networks/playground-exercises?hl=en)

### 첫번째 신경망(A First Neural Network)

이 실습에서는 처음으로 신경망을 학습시켜 보게 됩니다. 신경망을 통해 명시적인 특성 교차를 사용하지 않고도 비선형 모델을 학습할 수 있습니다.

과제 **1:** 주어진 모델은 두 개의 입력 특성(input features)을 하나의 뉴런으로 결합합니다. 이 모델이 비선형성을 학습할 수 있을까요? 모델을 실행하여 추측을 확인해 보세요.

**과제 2:** 히든 레이어의 뉴런 수를 1개에서 2개로 늘려보고 선형 활성화에서 ReLU와 같은 비선형 활성화로 변경해 보세요. 비선형성을 학습하는 모델을 만들 수 있나요? 데이터를 효과적으로 모델링할 수 있나요?

**과제 3:** ReLU와 같은 비선형 활성화를 사용하여 히든 레이어의 뉴런 수를 2개에서 3개로 늘립니다. 데이터를 효과적으로 모델링 할 수 있나요? 모델 품질은 실행마다 어떻게 다른가요?

**과제 4:** 히든 레이어 및 레이어당 뉴런을 추가하거나 삭제하여 실험을 계속해 봅니다. 또한 자유롭게 학습률, 정규화 및 기타 학습 설정을 변경해 보세요. 0.177 이하의 테스트 손실을 얻기 위해, 사용할 수 있는 가장 작은 뉴런 및 레이어 수는 얼마인가요?

모델 크기를 늘리면 적합도가 향상되나요, 아니면 얼마나 빨리 수렴하나요? 이것이 좋은 모델로 수렴하는 빈도를 변경하나요? 예를 들어 다음 아키텍처를 시도해보십시오.

- 첫번째 히든레이어에 3개의 뉴런
- 두번째 히든레이어에 3개의 뉴런
- 세번째 히든레이어에 2개의 뉴런

  과제 1의 답
<div class="notice--primary" style="font-size: 70%; font-style: italic;">
    활성화가 <code>Linear</code>으로 설정되어 있으므로 이 모델은 어떠한 비선형성도 학습할 수 없습니다. 손실은 매우 높아, 이 모델은 데이터에 적합하지 않다(underfit)고 말합니다.
</div>
 과제 2의 답
<div class="notice--primary" style="font-size: 70%; font-style: italic;">
    비선형 활성화 함수는 비선형 모델을 학습할 수 있습니다. 하지만 뉴런이 2개인 1개의 히든 레이어는 데이터의 모든 비선형성을 반영할 수 없고, 노이즈가 없어도 손실이 매우 높습니다: 여전히 데이터에 적합하지 않습니다(underfit). 이 실습은 비결정적이므로(nondeterministic), 실행(run)시 마다 학습이 효과적일 수도 비효과적일 수도 있습니다. 최고의 모델은 당신이 예상하는 모양이 아닐 수도 있습니다.
</div>
 과제 3의 답
<div class="notice--primary" style="font-size: 70%; font-style: italic;">
    플레이 그라운드의 비 결정적 속성은 이 실습을 통해 빛을 발합니다. 3개의 뉴런이 있는 단일 히든레이어는 데이터세트(노이즈 없음)를 모델링하기에 충분하지만 모든 실행이 좋은 모델로 수렴되는 것은 아닙니다.<br><br>
    XOR 함수는 3개의 반면(3 half-planes) (ReLU 활성화)의 조합으로 표현 될 수 있기 때문에, 3개의 뉴런으로 충분합니다. 개별 뉴런의 출력을 보여주는, 뉴런 이미지를 보면 알 수 있습니다. 뉴런이 3개이고 ReLU가 활성화 된 좋은 모델에서는 $X_1$이 positive (또는 negative, 이것은 바뀔 수 있음)임을 감지하는, 거의 수직선인 이미지 1개, $X_2$를 감지하는 거의 수평선인 이미지 1 개, 상화작용을 감지하는 대각선 이미지 1 개가 있을 것입니다.<br><br> 
    그러나 모든 실행이 좋은 모델로 수렴되는 것은 아닙니다. 일부 실행은 2개의 뉴런이 있는 모델보다 좋지 않을 것입니다, 이러한 경우 중복 뉴런(duplicate neurons)을 볼 수 있습니다.
</div>
과제 4의 답
<div class="notice--primary" style="font-size: 70%; font-style: italic;">
    3개의 뉴런이 있는 단일 히든 레이어는 데이터를 모델링할 수는 있지만, 중복성이 없으므로 많은 실행에서 쉽게(effectively) 뉴런을 잃고 좋은 모델을 학습하지 못합니다. 뉴런이 3개 이상인 단일 레이어는 중복성이 더 많으므로 좋은 모델로 수렴할 가능성이 더 많습니다.<br><br>
    앞에서 보았듯이 2개의 뉴런만 있는 단일 히든 레이어는 데이터를 잘 모델링할 수 없습니다. 시도해 보면 출력 레이어의 모든 항목이 두 노드의 선으로만 구성된 모양임을 알 수 있습니다. 이 경우 더 깊은 네트워크가 첫 번째 히든 레이어만 있는 것보다 데이터 세트를 더 잘 모델링 할 수 있습니다: 두 번째 레이어의 개별 뉴런은 첫 번째 레이어의 뉴런을 결합하여 오른쪽 위 사분면과 같은 더 복잡한 모양을 모델링 할 수 있습니다. 두 번째 숨겨진 레이어를 추가하면 첫 번째 숨겨진 레이어보다 데이터 세트를 더 잘 모델링할 수 있지만, 두 번째 레이어가 모양을 만드는 키트의 일부가 되도록 더 많은 선을 첫 번째 레이어에 추가하는 것이 더 합리적일 수 있습니다.<br><br>    
    그러나 첫 번째 히든 레이어에 1개의 뉴런이 있는 모델은 깊이와 관계없이 좋은 모델을 학습 할 수 없습니다. 이는 첫 번째 레이어의 출력이 1차원(일반적으로 대각선)을 따라서만 달라지므로, 이 데이터 세트를 잘 모델링하기에 충분하지 않기 때문입니다. 이후 레이어는 아무리 복잡하더라도 이를 보완 할 수 없습니다: 입력 데이터의 정보가 복구 불가능하게 손실됩니다.<br><br>    
    이와 같은 간단한 문제를 해결하기 위해 소규모 네트워크를 구축하는 대신, 많은 뉴런을 포함하는 많은 레이어가 있다면 어떨까요? 글쎄, 우리가 본 것처럼 첫 번째 레이어는 다양한 선 기울기(line slopes)를 시도할 수 있습니다. 그리고 두 번째 레이어는 그것들을 다양한 모양으로 축적할 수 있고, 그 다음 레이어에도 다양한 모양을 만들 수 있습니다.<br><br>    
    모델이 다양한 은닉 뉴런을 통해 다양한 모양을 고려할 수 있으므로, 모델이 훈련 세트의 노이즈에 쉽게 과적합될 수 있는 충분한 공간을 만들어, 이러한 복잡한 모양을 만들어, 일반화된 사실이 아닌 훈련 데이터의 특징(foibles)과 일치시킬수 있습니다. 이 예제에서 더 큰 모델은 정확한 데이터 포인트와 일치하는 복잡한 경계를 가질 수 있습니다. 극단적인 경우, 대형 모델은 데이터 기억이라고하는 개별 노이즈 지점 주변의 섬을 학습 할 수 있습니다. 모델을 훨씬 더 크게 허용하면, 문제를 해결하기에 충분한 뉴런이 있는 단순한 모델보다 실제로 성능이 더 나쁘다는 것을 알 수 있습니다.
</div>

### 신경망 초기화 (Neural Net Initialization)

이 실습에서는 다시 XOR 데이터를 사용하는데, 학습용 신경망의 반복성과 초기화의 중요성을 살펴봅니다.

**과제 1:** 주어진 모델을 4~5회 실행합니다. 매번 시도하기 전에 **네트워크 초기화(Reset the network)** 버튼을 눌러  새롭게 무작위 초기화(random initialization)합니다. (**네트워크 초기화** 버튼은 재생 버튼 바로 왼쪽에 있는 원형의 초기화 화살표입니다.) 수렴을 보장하기 위해 매 시도마다 최소 500단계를 실행하도록 합니다. 각 모델 출력이 어떤 형태로 수렴하나요? 이 결과가 비볼록 최적화(non-convex optimization)에서 초기화의 역할은 어떤 의미가 있나요?

**과제 2:** 레이어 한 개와 추가 노드를 몇 개 더 추가하여 모델을 약간 더 복잡하게 만들어 보세요. 과제 1의 시도를 반복합니다. 결과에 안정성이 보강되나요?

 과제 1의 답
<div class="notice--primary" style="font-size: 70%; font-style: italic;">
    각 시도마다 학습된 모델의 형태가 달랐습니다. 테스트 손실 수렴 결과는 최저와 최고가 거의 2배까지 차이가 날 정도로 다양했습니다.
</div>
 과제 2의 답
<div class="notice--primary" style="font-size: 70%; font-style: italic;">
    레이어와 추가 노드를 추가하여 더 반복적인 결과를 얻었습니다. 매 시도마다 결과 모델은 거의 같은 형태였습니다. 또한 테스트 손실 수렴 결과는 매 시도마다 변화가 적었습니다.
</div>
### 나선형 신경망 (Neural Net Spiral)

이 데이터 세트는 노이즈가 있는 나선형입니다. 분명 선형 모델은 여기에서 실패하겠지만 직접 정의된 특성 교차(feature crosses)도 구성이 어려울 수 있습니다.

**과제 1:** $X_1$과 $X_2$만 사용하여 가능한 한 최고의 모델로 학습시켜 봅니다. 자유롭게 레이어와 뉴런을 추가 또는 삭제하고 학습률, 정규화율, 배치 크기와 같은 학습 설정을 변경해 보세요. 얻을 수 있는 최고의 테스트 손실은 얼마인가요? 모델 출력 표면은 얼마나 매끄러운가요?

**과제 2:** 신경망이라도 최고의 성능을 달성하기 위해서는 특성 추출(feature engineering)이 일부 필요합니다. 추가 교차 특성이나 $sin(X_1)$, $sin(X_2)$과 같은 기타 변환을 추가해 보세요. 더 나은 모델이 도출되나요? 모델 표면이 더 매끄러워지나요?

과제 1, 2의 답

[비디오 참조](https://developers.google.com/machine-learning/crash-course/introduction-to-neural-networks/playground-exercises?hl=ko#expandable-6)
