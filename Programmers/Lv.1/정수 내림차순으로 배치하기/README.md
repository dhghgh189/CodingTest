# 정수 내림차순으로 배치하기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/12933)

## 문제 설명
함수 solution은 정수 n을 매개변수로 입력받습니다.   
n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요.   
예를들어 n이 118372면 873211을 리턴하면 됩니다.

## 제한사항
- `n`은 1이상 8000000000 이하인 자연수입니다.

## 입출력 예
|n|return|
|------|---|
|118372|873211|

## 작성한 답

```cs
public long solution(long n)
{
    long answer = 0;

    // 최대 10자리의 수가 입력됨 (capacity 10)
    // 자리수들을 분리하여 저장할 리스트
    List<long> list = new List<long>(10);

    // 각 자리수 분리하여 리스트에 저장
    while (n != 0)
    {
        list.Add(n % 10);
        n /= 10;
    }

    // 삽입정렬 수행 (요소가 16자리 이하일 경우 빠름)
    long temp;
    for (int keyIndex = 1; keyIndex < list.Count; keyIndex++)
    {
        for (int j = 0; j < keyIndex; j++)
        {
            // keyIndex의 값보다 앞에 있는 j번째 값이 더 작은경우
            if (list[j] < list[keyIndex])
            {
                // key값을 j번째에 삽입하고 나머지 값을 뒤로 민다.
                temp = list[keyIndex];
                list.RemoveAt(keyIndex);
                list.Insert(j, temp);

                break;
            }
        }
    }

    // 분리된 자리수들을 다시 하나의 수로 합치기
    foreach (long value in list)
    {
        answer *= 10;
        answer += value;
    }

    return answer;
}
```

- 각각의 자릿수에 대해 정렬하기 위해 자릿수를 모두 분리한다. 
  ```cs
  // 자리수들을 분리하여 저장할 리스트
  List<long> list = new List<long>(10);

  // 각 자리수 분리하여 리스트에 저장
  while (n != 0)
  {
      list.Add(n % 10);
      n /= 10;
  }
  ```

- 분리된 수들에 대해 삽입 정렬(내림차순)을 진행
  ```cs
  // 삽입정렬 수행 (요소가 16자리 이하일 경우 빠름)
  long temp;
  for (int keyIndex = 1; keyIndex < list.Count; keyIndex++)
  {
      for (int j = 0; j < keyIndex; j++)
      {
          // keyIndex의 값보다 앞에 있는 j번째 값이 더 작은경우
          if (list[j] < list[keyIndex])
          {
              // key값을 j번째에 삽입하고 나머지 값을 뒤로 민다.
              temp = list[keyIndex];
              list.RemoveAt(keyIndex);
              list.Insert(j, temp);

              break;
          }
      }
  }
  ```

- 정렬된 자릿수를 모두 합쳐 하나의 수로 만든다
  ```cs
  // 분리된 자리수들을 다시 하나의 수로 합치기
  foreach (long value in list)
  {
      answer *= 10;
      answer += value;
  }
  ```

- 결과값을 return   
  -> **return answer**