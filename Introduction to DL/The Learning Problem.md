# The Learning Problem

## Main Topic
- 원하는 Function을 직접 알 수 없을때, Training Data로 Weight를 어떻게 찾을 수 있을까?

## Key Concepts Explanation
**1. 실제로 주어지는 것: Function이 아니라 Example들**
  - Image에서 고양이를 판단하는 Function이 아니라, Training Pair을 받음  
    * Image와 "고양이" Label, 다른 Image와 "고양이아님" Label  
  - Network는 제한된 Example에서 아직 보지 못한 Image에서도 작동할 관계를 찾아야함  
  => Training에서는 먼저 주어진 Example에서 Network Output과 Target이 얼마나 다른지를 측정,,  

**2. Rosenblatt's Perceptron Learning Rule: 틀린 Example-> Weight 수정**
  - 두 Class의 Label를 +1, -1로 두고, Bias를 Weight Vector에 포함하면, 잘못 판단한 Example에 다음  Update를 적용할 수 있음.  

$$
W\leftarrow W+\eta yX
$$

$X$: 현재 Example의 Input Vector, $y$: 현재 Example의 Label, $\eta$: Update 크기를 정하는 Learning Rate  
  - Positive Example을 Negative로 판단하면 해당 Example쪽으로 판단을 이동시키고, Negative Example을 Positive로 판단했다면 반대 방향으로 이동시킴  
  - Linearly Separable Data라면 유한한 Update 뒤에 모든 Training Example을 올바르게 판단할 수 있음!  
  => But 하나의 Linear Boundary로 나눌 수 없는 Data에서는 무한회귀

**3. MLP에서는 Hidden Neuron의 Target이 주어지지 않는다.**  
  - 고양이의 최종 Label은 알지만, 각각의 Hidden Neuron이 무엇을 출력해야 하는지는 모름  
  - 어떤 Neuron이 귀를 찾고, 어떤 Neuron이 털을 찾고, 어떤 Neuron이 눈을 찾도록 만들지 직접 정하기는 어려움
  - 따라서 Perceptron Learning Rule을 직접 Hidden Neuron에 그대로 적용할 수 없음.  
  => 대신 질문 Change, "이 Weight를 조금 바꾸면 최종 Loss가 어떻게 달라지는가?"

**4. Threshold와 단순한 Error Count는 작은 개선을 알려주지 못한다**
  - 틀린 판단에서, Weight를 조금 수정해도 최종 판단이 여전히 틀리면 Error Count는 그대로  
  -> But 내부적으로는 올바른 판단에 가까워졌을수도?  
  - Threshold Output과 Error Count는 이런 작은 변화를 보여주기 어려움, 많은 영역에서 Derivative가 0이고, 판단이 바뀌는 지점에서는 불연속  
  - 해결하기 위해 다음 2개를 바꿈
    * Activation을 작은 변화에 반응하는 형태로 바꿈
    * 평가 기준을 조금 나아진 정도도 보여주는 Loss로 만듬

**5. Sigmoid 함수: 중간 정도의 판단 표현**
  - 
$$
\sigma(z)=\frac{1}{1+e^{-z}}
$$

  Sigmoid Output은 0이나 1이 아닌, 그 사이의 값을 출력
  - 같은 틀린 판단이라도 0.1->0.4로 변하면, Target이 1인 경우 더 가까워졌다는 것을 확인할 수 있음
  - Binary Classfication에서는 이를 $P(Y=1\mid X)$에 대한 Estimate로 해석
