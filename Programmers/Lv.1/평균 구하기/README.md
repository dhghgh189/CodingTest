# 평균 구하기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/12944)

## 문제 설명
정수를 담고 있는 배열 arr의 평균값을 return하는 함수, solution을 완성해보세요.

## 제한사항
- arr은 길이 1 이상, 100 이하인 배열입니다.
- arr의 원소는 -10,000 이상 10,000 이하인 정수입니다.

## 입출력 예
|arr|return|
|------|---|
|[1,2,3,4]|2.5|
|[5,5]|5|

## 작성한 답

```cs
public double solution(int[] arr)
{
    double answer = 0;

    for (int i = 0; i < arr.Length; i++)
    {
        // 배열의 원소값들을 모두 합산
        answer += arr[i];
    }

    // 합산한 값을 배열 길이로 나눠서 평균 반환
    return (answer / arr.Length);
}
```

- 평균을 구하기 위해 먼저 모든 값을 합산한다.
  ```cs
  for (int i = 0; i < arr.Length; i++)
  {
      // 배열의 원소값들을 모두 합산
      answer += arr[i];
  }
  ```

- 합산한 값을 나눠 평균을 return   
  -> **return (answer / arr.Length)**