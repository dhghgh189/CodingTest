# 두 수의 곱 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/120804)

## 문제 설명
정수 `num1`, `num2`가 매개변수로 주어집니다. `num1`과 `num2`를 곱한 값을 return하도록 solution 함수를 완성해주세요.

## 제한사항
- 0 ≤ `num1` ≤ 100
- 0 ≤ `num2` ≤ 100

## 입출력 예
|num1|num2|result|
|------|---|---|
|3|4|12|
|27|19|513|

### 입출력 예 설명

**입출력 예 #1**
  - `num1`이 3, `num2`가 4이므로 3 * 4 = 12를 return 합니다.
  
**입출력 예 #2**
  - `num1`이 27, `num2`가 19이므로 27 * 19 = 513을 return 합니다.
  
## 작성한 답

```cs
public int solution(int num1, int num2) 
{
    return (num1 * num2);
}
```

- 매개변수로 주어진 num1과 num2에 대해 * 연산 결과값을 반환