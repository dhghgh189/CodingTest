# 자릿수 더하기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/12931)

## 문제 설명
자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.   
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

## 제한사항
- N의 범위 : 100,000,000 이하의 자연수

## 입출력 예
|N|answer|
|------|---|
|123|6|
|987|24|

### 입출력 예 설명

**입출력 예 #1**
  - 문제의 예시와 같습니다.
  
**입출력 예 #2**
  - 9 + 8 + 7 = 24이므로 24를 return 하면 됩니다.

## 작성한 답

```cs
public int solution(int n)
{
    int answer = 0;

    // 자리수를 구한다.
    int length = n.ToString().Length;

    // 자리수만큼 반복
    for (int i = 0; i < length; i++)
    {
        // 한자리씩 떼서 더한다.
        answer += n % 10;
        // 더한 자리수를 제외하고 저장
        n /= 10;
    }

    return answer;
}
```

- 먼저 입력된 숫자의 자리수를 구한다.
  ```cs
  // 자리수를 구한다.
  int length = n.ToString().Length;
  ```

- 자리수 만큼 반복하며 각각 더한다.
  ```cs
  // 자리수만큼 반복
  for (int i = 0; i < length; i++)
  {
      // 한자리씩 떼서 더한다.
      answer += n % 10;
      // 더한 자리수를 제외하고 저장
      n /= 10;
  }
  ```

- 결과값을 return   
  -> **return answer**