# 두 수의 합 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/120802)

## 문제 설명
정수 `num1`과 `num2`가 주어질 때, `num1`과 `num2`의 합을 return하도록 solution 함수를 완성해주세요.

## 제한사항
- -50,000 ≤ `num1` ≤ 50,000
- -50,000 ≤ `num2` ≤ 50,000

## 입출력 예
|num1|num2|result|
|------|---|---|
|2|3|5|
|100|2|102|

### 입출력 예 설명

**입출력 예 #1**
  - `num1`이 2이고 `num2`가 3이므로 2 + 3 = 5를 return 합니다.
  
**입출력 예 #2**
  - `num1`이 100이고 `num2`가 2이므로 100 + 2 = 102를 return 합니다.
  
## 작성한 답

```cs
public int solution(int num1, int num2) 
{
    return (num1 + num2);
}
```

- 매개변수로 주어진 num1과 num2에 대해 +연산 결과값을 반환