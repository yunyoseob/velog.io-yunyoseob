오늘 포스팅할 2번째 **키워드로 공부하는 데이터 분석**의 키워드는 Gradient Vanishing입니다.

퍼셉트론이란 입력층과 출력층으로만 구성된 최초의 인공신경망을 의미합니다.

![](https://images.velog.io/images/yunyoseob/post/6b718ffa-2e99-46c2-9048-50fa1b6c6fa9/image.png)

- 사진출처 : [딥러닝을 이용한 자연어 처리 입문 : 퍼셉트론](https://wikidocs.net/24958)

> **심층 신경망은 은닉층이 2개 이상인 신경망을 의미합니다.**

Feed Forward Neural Network(순방향신경망)은 입력데이터가 입력층, 은닉층, 출력층 순서로 전파되어 판별 함수 값으로 변환되는 신경망이며, Back Propagation(역전파)는 역방향으로 가중치 갱신을 통해 오차를 최소화시키도록 학습시키는 알고리즘입니다.

> **Feed Forward Neural Network & Back Propagation**

![](https://images.velog.io/images/yunyoseob/post/e9e6fc26-6e9d-4d9c-8516-2466473d7901/image.png)

- 사진 출처 : [Research Gate](https://www.researchgate.net/figure/Feed-forward-back-propagation-mechanism-in-artificial-neural-network_fig1_336707258)

오늘 다룰 Gradient Vanishing(기울기 소실) 문제는 Back Propagation에서 계산 결과와 정답과의 오차를 통해 가중치를 수정하는데, 입력층으로 갈수록 기울기가 작아져 가중치들이 업데이트 되지 않아 최적의 모델을 찾을 수 없는 문제입니다.

# Gradient Vanishing Problem : Sigmoid

Gradient Vanishg 문제는 신경망의 활성함수의 도함수 값이 계속 곱해지다 보면 가중치에 따른 결과값의 기울기가 0이 되어 버려서, Gradient Descent(경사하강법)을 이용할 수 없게 되는 문제입니다.

- **Gradient Descent에 대한 내용은 [이전 포스팅](https://velog.io/@yunyoseob/Gradient-Descent-%EA%B2%BD%EC%82%AC%ED%95%98%EA%B0%95%EB%B2%95)에 있습니다.**

> **예시로, 딥러닝에서 activation function을 시그모이드 함수로 설정했다고 할 때, Gradient Vanishing Problem은 다음과 같습니다.**

![](https://images.velog.io/images/yunyoseob/post/1f809fcd-0121-461e-bc13-bc073fe234ef/image.png)

딥러닝의 Back Propagation에서 수많은 weight 들을 업데이트 하기위해, Chain rule(미분 연쇄 법칙)을 이용할 때, sigmoid 함수는 0과 1 사이의 값을 출력하므로, 해당 과정에서 미분 결과값이 소실되어 버리는 문제가 발생합니다. (결과 값이 0으로 수렴)

![](https://images.velog.io/images/yunyoseob/post/1af88f40-c995-4b10-82ff-28c03dd969eb/image.png)

즉, 다음과 같은 식이 있을 때, 

![](https://images.velog.io/images/yunyoseob/post/09cd818a-795e-4893-b365-886e442c0ae3/image.png)

Gradient 항이 사라져 버리는 문제가 발생한다는 의미입니다.


- sigmoid 함수 미분 과정 참고 글 : [답을 찾아가는 과정 : 딥러닝 - 활성화 함수 종류 및 비교](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=handuelly&logNo=221824080339)

# Gradient Vanishing Problem Solving

> **Activation Function : ReLU**

딥러닝에서는 기울기 소실 문제를 해결하기 위해, ReLU(Rectified Linear Unit, 경사함수)를 도입하기도 합니다. 

![](https://images.velog.io/images/yunyoseob/post/7afc54ba-9a63-438a-a945-c553f0ab3775/image.png)

ReLU의 경우, 0보다 작은 값은 0으로 반환하고, 0보다 큰 값이 나올 경우, 그대로 반환하여 Sigmoid 함수를 Activation Function으로 설정했을 때, 발생하는 Gradient Vanishing Problem을 보완할 수 있습니다.

- 그렇기 때문에 딥러닝에서 이진분류 문제를 다룰 때, 보통 hidden layer의 activation function을 ReLU로 설정하고 마지막 output layer에서만 sigmoid 함수를 쓰는 경우가 많습니다.


> **Activation Function : Leaky ReLU**

ReLU 함수의 경우, max(0,x)에서 0으로 결과값이 도출된다면, 이후에 학습이 이루어지지 않는다는 한계가 있습니다. (이후 출력값이 모두 0이 되기 때문입니다.)

![](https://images.velog.io/images/yunyoseob/post/c5059f6b-5ea8-415f-b3e2-c5c458557585/image.png)

LeakyReLU는 max(0,x)에서 0대신 아주 작은 값을 x에 곱해주어, 0으로 결과값이 도출될 때 문제점을 보완한 함수입니다.

> **Batch Normalization(배치 정규화)**

배치 정규화는 배치 단위로 입력에 대해 평균을 0으로 만들고, 정규화를 합니다. 

![](https://images.velog.io/images/yunyoseob/post/8429ec53-d603-4db8-b1e2-499afedad977/image.png)

- 배치 정규화 과정 : [딥러닝을 이용한 자연어 처리 입문 : 기울기 소실과 폭주](https://wikidocs.net/61375)

배치 정규화는 각 층의 입력값의 평균과 표준편차를 다시 맞추어 주어, 입력값이 쏠리는 것을 막아, 가중치 초기화에 훨씬 덜 민감해지고, 기울기 소실 문제도 개선할 수 있는 방법입니다.


> **Resnet(Residual Network)**

이미지 분류 문제에 주로 사용되는 Convolutional Neural Network에서 발생하는 Gradient Vanishing 문제를 보완하기 위한 모델로는 Resnet이 있습니다. 

![](https://images.velog.io/images/yunyoseob/post/145a1e6f-c559-49a2-9698-dac04687139b/image.png)

- 사진 출처 : [Paper Review : ResNet](https://medium.com/humanscape-tech/paper-review-resnet-e768afd296bc)

Resnet 모델의 경우, 이전 Layer의 Feature Map을 다음 Layer의 Feature Map에 더해줍니다. 이를 Skip Connection이라고 합니다.  Resnet의 경우, 딥러닝에서 Layer가 깊어지면서 발생하는 Gradient Vanishing 문제를 Skip Connection을 통해 최소 gradient가 1이상 값을 갖게 하여, Gradient Vanishing 문제를 해결한 방법입니다.


**이상으로 키워드로 공부하는 데이터 분석의 두 번째 키워드인 Gradient Vanishing 포스트를 마치도록 하겠습니다. 😊** 
