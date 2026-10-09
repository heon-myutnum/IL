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
  * 
