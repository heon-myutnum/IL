# Representation

## Main Topic
- Neural network는 어떤 Function을 표현할 수 있는가?
- Depth와 Width의 중요성?
=> Representation: 어떤 Weight를 사용해야 원하는 Input-output relationship을 만들 수 있을까?
  
## Key Concepts
**1. Neuron은 작은 판단 장치이다.**
 - Neuron의 기본 계산: z = sigma wx+b, y=f(z)  
 - x: input, w: weight, b: bias, f: 계산 결과를 output으로 바꾸는 activation function  
 -> 동일한 input, weight라도, threshold가 바꾸면 판단 방식이 달라짐
  
**2. 하나의 Perceptron-> AND, OR: O, but XOR: X**
 - Perceptron은 Linear Classifier이므로, XOR를 표현할 수 없음 -> Hidden Layer 사용!
  
**3. Boolean Function -> Disjunctive Normal Form**
 - Truth Table에서 Output이 1인 경우: AND로 표현, 그 경우를 OR로 연결  
 -> Hidden Layer: 각 경우 확인하는 AND Unit  
    Output Layer: 어느 경우든 만족했는지 확인하는 OR Unit  
  ==> 충분한 Hidden Unit이 있으면 One-Hidden-Layer MLP로 모든 Boolean Function을 표현할 수 있음!  
  ->But 표현가능하다 와 작은 Network로 표현가능하다는 다름  

**4. Depth: 중간 결과 재사용!**
 - Input이 N개 -> Truth Table에는 2^N개의 경우의 수
 이를 모두 표현하려면 Network가 매우 넓어질 수 있음  
 - Examples: Parity-XOR  
   : 각 경우를 AND Clause로 표현: so many units!  
   : 두 Input씩 XOR, 그 결과를 다시 XOR!  
   -> XOR 하나에 Perceptron 3개씩:   
      N개의 Input -> 3(N-1)개의 Perceptron  
      Balance할때의 Depth -> 2log2N  
 - Depth를 통해 복잡한 관계를 단계적으로 구성 가능  
  
**5. Decision Boundary: 간단한 판단 결합! like Depth**
  - Example: 점이 오각형 안에 있는가?  
    * 각 변에 대해 "이 선의 안쪽에 있는가?" -> 모두 참이면 Output이 1  
    * 각 Hidden Neuron: 하나의 Half-Plane 확인  
    * Output Neuron: 다섯 결과를 AND로 결합  
  - 복잡한 영역: 작은 영역을 결합해 표현 or approximate  
  - Decision Boundary가 3개-> 삼각형 모양으로 데이터 감쌈, 4개->사각형, 6개-> 육각형  
  ==> Limit: Cylinder 모양, 결정경계 Circle로 수렴  
  -> Circle Detector 
  
**6. Universal Approximation: 원하는 관계에 가까워질 수 있다**
  - Function을 작은 구간들로 나누고, 각 구간에 맞는 높이를 더하면 계단처럼 생긴 Approximate를 얻을 수 있음 -> like 구분구적법  
  - 적절한 Activation, 충분한 Width 필요  
  
  But 다음 사항들을 보장하지는 않음
  - 적은 Parameter로 표현할 수 있다는 보장  
  - Training이 그 Parameter를 찾아낸다는 보장  
  - 처음 보는 Data에서도 잘 작동한다는 보장  
  
**7. Output Activation과 Width도 제한을 만든다**
  - Output Activation이 Sigmoid: Output은 (0,1) 안에있음 -> 100이나 -5를 직접 내보낼 수는 x
  - Threshold Activation은 서로 다른 Input을 동일한 0/1 패턴으로 -> 버려진 정보는 뒤쪽 Layer가 복구 불가능!
  - ReLU와 같은 Graded Activation은 활성화된 영역에서 값의 크기도 전달하므로, Threshold보다 더 많은 정보를 다음 Layer로 넘길 수 있음

## Summary
1. 충분한 구조를 갖춘 MLP는 다양한 Boolean Function, Decision Boundary, Function Approximation을 표현할 수 있다.
2. Depth는 중간 결과를 결합하고 재사용하여 일부 문제를 훨씬 적은 Unit으로 표현하게 한다.
3. Representation 가능성은 Training 성공을 보장하지 않으며, Width와 Activation에도 제한이 있다.