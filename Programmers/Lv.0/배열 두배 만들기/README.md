# 배열 두배 만들기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/120809)

## 문제 설명
정수 배열 `numbers`가 매개변수로 주어집니다. `numbers`의 각 원소에   
두배한 원소를 가진 배열을 return 하도록 solution 함수를 완성해주세요.

## 제한사항
- -10,000 ≤ `numbers`의 원소 ≤ 10,000
- 1 ≤ `numbers`의 길이 ≤ 1,000

## 입출력 예
|numbers|result|
|------|---|
|[1, 2, 3, 4, 5]|[2, 4, 6, 8, 10]|
|[1, 2, 100, -99, 1, 2, 3]|[2, 4, 200, -198, 2, 4, 6]|

### 입출력 예 설명

**입출력 예 #1**
  - [1, 2, 3, 4, 5]의 각 원소에 두배를 한 배열 [2, 4, 6, 8, 10]을 return합니다.
  
**입출력 예 #2**
  - [1, 2, 100, -99, 1, 2, 3]의 각 원소에 두배를 한 배열 [2, 4, 200, -198, 2, 4, 6]을 return합니다.
  
## 작성한 답

```cs
public int[] solution(int[] numbers) 
{
    int[] answer = new int[numbers.Length];
    for (int i = 0; i<numbers.Length; i++)
    {
        answer[i] = numbers[i]*2;
    }
    return answer;
}
```

- 매개변수인 `numbers` 배열의 Length와 일치하는 크기의 배열 `answer`를 생성한다.   
  -> **int[] answer = new int[numbers.Length]**   
  
- `numbers` 배열의 Length 만큼 반복하면서 각 원소의 두배 값을 `answer` 배열에 저장한다. 
  ```cs
  for (int i = 0; i<numbers.Length; i++)
  {
      answer[i] = numbers[i]*2;
  }
  ```

- 반복 종료 후 `answer` 배열을 return 한다.   
  -> **return answer**