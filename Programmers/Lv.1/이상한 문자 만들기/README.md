# 이상한 문자 만들기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/12930)

## 문제 설명
문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다.   
각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

## 제한사항
- 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
- 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

## 입출력 예
|s|return|
|------|---|
|"try hello world"|"TrY HeLlO WoRlD"|

## 작성한 답

```cs
public string solution(string s)
{
    StringBuilder sb = new StringBuilder();

    // 우선 모든 문자열을 대문자로 만든다.
    s = s.ToUpper();

    // 문자열을 공백기준으로 나눈다.
    string[] words = s.Split(' ');

    foreach (string word in words)
    {
        for (int i = 0; i < word.Length; i++)
        {
            // 짝수번째는 대문자 그대로, 홀수번째는 소문자로 바꿔 저장
            // ascii 코드 상 대문자에 32를 더해주면 소문자다
            sb.Append(i % 2 == 0 ? word[i] : (char)(word[i] + 32));
        }
        // 한 단어가 완성되고 나면 공백 추가
        sb.Append(' ');
    }
    // 마지막 공백은 제거
    sb.Remove(sb.Length - 1, 1);

    return sb.ToString();
}
```

- 먼저 모든 문자열을 대문자로 변환하여 추후 짝수 변환 필요없이 홀수만 소문자로 변환하도록 한다.
  ```cs
  // 우선 모든 문자열을 대문자로 만든다.
  s = s.ToUpper();
  ```

- 문자열을 공백기준으로 나눠놓는다.
  ```cs
  // 문자열을 공백기준으로 나눈다.
  string[] words = s.Split(' ');
  ```

- 나눠놓은 문자열들을 반복하면서 짝수번째는 그대로, 홀수번째는 소문자로 변환하여 builder에 저장한다.
  ```cs
  foreach (string word in words)
  {
      for (int i = 0; i < word.Length; i++)
      {
          // 짝수번째는 대문자 그대로, 홀수번째는 소문자로 바꿔 저장
          // ascii 코드 상 대문자에 32를 더해주면 소문자다
          sb.Append(i % 2 == 0 ? word[i] : (char)(word[i] + 32));
      }
      // 한 단어가 완성되고 나면 공백 추가
      sb.Append(' ');
  }
  ```

- 마지막 번째 공백은 제거한다.
  ```cs
  // 마지막 공백은 제거
    sb.Remove(sb.Length - 1, 1);
  ```

- 완성된 문자열을 return   
  -> **return sb.ToString()**