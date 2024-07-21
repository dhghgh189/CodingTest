# 분수의 덧셈 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/120808)

## 문제 설명
첫 번째 분수의 분자와 분모를 뜻하는 `numer1`, `denom1`, 두 번째 분수의 분자와 분모를 뜻하는   
`numer2`, `denom2`가 매개변수로 주어집니다. 두 분수를 더한 값을 기약 분수로 나타냈을 때   
분자와 분모를 순서대로 담은 배열을 return 하도록 solution 함수를 완성해보세요.

## 제한사항
- 0 < `numer1`, `denom1`, `numer2`, `denom2` < 1,000   

## 입출력 예
|numer1|denom1|numer2|denom2|result|
|------|---|---|---|---|
|1|2|3|4|[5, 4]|
|9|2|1|3|[29, 6]|

### 입출력 예 설명

**입출력 예 #1**
  - (1 / 2) + (3 / 4) = 5 / 4입니다. 따라서 [5, 4]를 return 합니다.
  
**입출력 예 #2**
  - (9 / 2) + (1 / 3) = 29 / 6입니다. 따라서 [29, 6]을 return 합니다.
  
## 작성한 답

```cs
public int[] solution(int numer1, int denom1, int numer2, int denom2) 
{
    int index1;
    int index2;
    int maxGongYaksu = 0;
    int[] answer = new int[2];
    
    // answer[0] : 분자   
    // answer[1] : 분모
    // 1. 통분하여 분수 덧셈 계산
    answer[0] = (numer1 * denom2) + (numer2 * denom1);
    answer[1] = denom1 * denom2;
    
    // 약분을 위해 최대공약수를 구할 때, 분모와 분자중
    // 더 큰 수까지 반복하면서 최대공약수를 구하는건 의미가 없으므로 
    // 더 작은 수를 찾아 반복의 length로 사용
    if (answer[0] < answer[1])
    {
        index1 = 0; // 분자가 더 작다
        index2 = 1; // 분모가 더 크다
    }
    else
    {
        index1 = 1; // 분모가 더 작다
        index2 = 0; // 분자가 더 크다
    }
    
    while (true)
    {
        for (int i = 1; i <= answer[index1]; i++)
        {
            if (answer[index1] % i == 0)
            {
                if (answer[index2] % i == 0)
                {
                    // 분자와 분모에 대해 공약수인 경우 변수에 저장
                    maxGongYaksu = i;
                }
            }
        }
        
        // 분모와 분자의 공약수가 1인 경우 더이샹 약분되지 않으므로 기약분수 완성
        if (maxGongYaksu == 1)
        {
            break;
        }
        else
        {
            // 아직 기약분수 조건에 맞지 않으므로 약분 진행 
            answer[index1] /= maxGongYaksu;
            answer[index2] /= maxGongYaksu;
        }
    }
    
    return answer;
}
```

- 우선 분수 덧셈을 위해 통분을 진행한 후 분수를 더하여 배열에 저장해둔다. (분모로 통분)
  ```cs  
  // 분자
  answer[0] = (numer1 * denom2) + (numer2 * denom1)   
  // 분모
  answer[1] = denom1 * denom2
  ```
  
- 배열의 요소 중 더 작은 수를 가지는 index와 큰 수를 가지는 index를 따로 저장한다.
  ```cs
  // 약분을 위해 최대공약수를 구할 때, 분모와 분자중
  // 더 큰 수까지 반복하면서 최대공약수를 구하는건 의미가 없으므로 
  // 더 작은 수를 찾아 반복의 length로 사용
  if (answer[0] < answer[1])
  {
      index1 = 0; // 분자가 더 작다
      index2 = 1; // 분모가 더 크다
  }
  else
  {
      index1 = 1; // 분모가 더 작다
      index2 = 0; // 분자가 더 크다
  }
  ```

- 배열에 저장된 분수를 기약분수로 만들로 만들기 위해 약분이 필요하므로 최대공약수를 구한다.     
  ```cs
  // while 반복 생략
  for (int i = 1; i <= answer[index1]; i++)
  {
      if (answer[index1] % i == 0)
      {
          if (answer[index2] % i == 0)
          {
              // 분자와 분모에 대해 공약수인 경우 변수에 저장
              maxGongYaksu = i;
          }
      }
  }
  ```

- 구한 최대공약수가 1이면 기약분수이므로 끝, 아니면 약분 후 최대공약수를 다시 구한다.
  ```cs
  // 분모와 분자의 공약수가 1인 경우 더이샹 약분되지 않으므로 기약분수 완성
  if (maxGongYaksu == 1)
  {
      // while 반복 종료
      break;
  }
  else
  {
      // 아직 기약분수 조건에 맞지 않으므로 약분 진행 
      answer[index1] /= maxGongYaksu;
      answer[index2] /= maxGongYaksu;
  }
  ```

- 기약분수가 완성되면 배열 return   
  -> **return answer**