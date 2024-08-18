# 문자열 내 마음대로 정렬하기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/12915)

## 문제 설명
문자열로 구성된 리스트 strings와 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다.   
예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.

## 제한사항
- strings는 길이 1 이상, 50이하인 배열입니다.
- strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
- strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
- 모든 strings의 원소의 길이는 n보다 큽니다.
- 인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

## 입출력 예
|strings|n|return|
|------|---|---|
|["sun", "bed", "car"]|1|["car", "bed", "sun"]|
|["abce", "abcd", "cdx"]|2|["abcd", "abce", "cdx"]|

### 입출력 예 설명

**입출력 예 #1**
  - "sun", "bed", "car"의 1번째 인덱스 값은 각각 "u", "e", "a" 입니다.   
    이를 기준으로 strings를 정렬하면 ["car", "bed", "sun"] 입니다.
  
**입출력 예 #2**
  - "abce"와 "abcd", "cdx"의 2번째 인덱스 값은 "c", "c", "x"입니다. 따라서 정렬 후에는 "cdx"가 가장 뒤에 위치합니다.   
    "abce"와 "abcd"는 사전순으로 정렬하면 "abcd"가 우선하므로, 답은 ["abcd", "abce", "cdx"] 입니다.
  
## 작성한 답

```cs
public string[] solution(string[] strings, int n)
{
    for (int keyIndex = 1; keyIndex < strings.Length; keyIndex++)
    {
        int i = keyIndex - 1;
        string key = strings[keyIndex];
        while (i >= 0)
        {
            // strings[i][n] 문자가 key[n] 문자 보다 크면 strings[i]를 한칸 뒤로 밀어
            // 삽입될 위치를 확보
            if (strings[i][n] > key[n])
            {
                strings[i + 1] = strings[i];
                i--;
            }
            // 만약 두 문자열의 n번째 문자가 같고,
            // strings[i]가 key보다 사전상 뒤에 오는 문자열이였다면 
            // 마찬가지로 strings[i]를 한칸 뒤로 밀어 삽입 위치 확보
            else if (strings[i][n] == key[n] && strings[i].CompareTo(key) > 0)
            {
                strings[i + 1] = strings[i];
                i--;
            }
            // strings[i][n] 문자가 key[n] 보다 작으면 삽입할 위치없음
            else
            {
                break;
            }
        }

        // 결정된 위치에 key값 삽입
        strings[i + 1] = key;
    }

    return strings;
}
```

- 단어를 정렬하기 위해 삽입 정렬 알고리즘을 사용, 1번째 인덱스 값부터 key로 선정하여
  마지막 요소까지 반복한다.
  ```cs  
  for (int keyIndex = 1; keyIndex < strings.Length; keyIndex++)
  ```
  
- 현재 keyIndex의 앞에 위치하는 요소들을 key값과 비교하여 정렬한다.
  ```cs
  int i = keyIndex - 1;
  string key = strings[keyIndex];
  while (i >= 0)
  {
      // strings[i][n] 문자가 key[n] 문자 보다 크면 strings[i]를 한칸 뒤로 밀어
      // 삽입될 위치를 확보
      if (strings[i][n] > key[n])
      {
        strings[i + 1] = strings[i];
        i--;
      }
      // 만약 두 문자열의 n번째 문자가 같고,
      // strings[i]가 key보다 사전상 뒤에 오는 문자열이였다면 
      // 마찬가지로 strings[i]를 한칸 뒤로 밀어 삽입 위치 확보
      else if (strings[i][n] == key[n] && strings[i].CompareTo(key) > 0)
      {
          strings[i + 1] = strings[i];
          i--;
      }
      // strings[i][n] 문자가 key[n] 보다 작으면 삽입할 위치없음
      else
      {
          break;
      }
  }

  // 결정된 위치에 key값 삽입
  strings[i + 1] = key;
  ```

- 정렬이 완료된 배열을 return   
  -> **return strings**