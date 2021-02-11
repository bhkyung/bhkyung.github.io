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

출처: [Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course/introduction-to-neural-networks/video-lecture?hl=en)

신경망은 특성 교차의보다 정교한 버전입니다. 본질적으로 신경망은 적절한 특성 교차를 학습합니다.

학습 목표 
{: .notice--success}
- 특히 다음과 같은 신경망에 대한 직관을 개발합니다. 
{: .notice--success}
  - 숨겨진 레이어 (hidden layers) 
  {: .notice--success}
  - 활성화 함수 (activation function) 
  {: .notice--success}

## [구조(Structure)]

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
