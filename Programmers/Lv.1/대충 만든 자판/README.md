# 대충 만든 자판 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/160586)

## 문제 설명
휴대폰의 자판은 컴퓨터 키보드 자판과는 다르게 하나의 키에 여러 개의 문자가 할당될 수 있습니다. 키 하나에 여러 문자가 할당된 경우, 동일한 키를 연속해서 빠르게 누르면 할당된 순서대로 문자가 바뀝니다.
예를 들어, 1번 키에 "A", "B", "C" 순서대로 문자가 할당되어 있다면 1번 키를 한 번 누르면 "A", 두 번 누르면 "B", 세 번 누르면 "C"가 되는 식입니다.
같은 규칙을 적용해 아무렇게나 만든 휴대폰 자판이 있습니다. 이 휴대폰 자판은 키의 개수가 1개부터 최대 100개까지 있을 수 있으며, 특정 키를 눌렀을 때 입력되는 문자들도 무작위로 배열되어 있습니다. 또, 같은 문자가 자판 전체에 여러 번 할당된 경우도 있고, 키 하나에 같은 문자가 여러 번 할당된 경우도 있습니다. 심지어 아예 할당되지 않은 경우도 있습니다. 따라서 몇몇 문자열은 작성할 수 없을 수도 있습니다.
이 휴대폰 자판을 이용해 특정 문자열을 작성할 때, 키를 최소 몇 번 눌러야 그 문자열을 작성할 수 있는지 알아보고자 합니다.
1번 키부터 차례대로 할당된 문자들이 순서대로 담긴 문자열배열 `keymap`과 입력하려는 문자열들이 담긴 문자열 배열 `targets`가 주어질 때, 각 문자열을 작성하기 위해 키를 최소 몇 번씩 눌러야 하는지 순서대로 배열에 담아 return 하는 solution 함수를 완성해 주세요.

단, 목표 문자열을 작성할 수 없을 때는 -1을 저장합니다.

## 제한사항
- 1 ≤ `keymap`의 길이 ≤ 100
  - 1 ≤ `keymap`의 원소의 길이 ≤ 100
  - `keymap[i]`는 i + 1번 키를 눌렀을 때 순서대로 바뀌는 문자를 의미합니다.
    - 예를 들어 `keymap[0]` = "ABACD" 인 경우 1번 키를 한 번 누르면 A, 두 번 누르면 B, 세 번 누르면 A 가 됩니다.
  - `keymap`의 원소의 길이는 서로 다를 수 있습니다.
  - `keymap`의 원소는 알파벳 대문자로만 이루어져 있습니다.
- 1 ≤ `targets`의 길이 ≤ 100
  - 1 ≤ `targets`의 원소의 길이 ≤ 100
  - `targets`의 원소는 알파벳 대문자로만 이루어져 있습니다.

## 입출력 예
|keymap|targets|result|
|------|---|---|
|["ABACD", "BCEFD"]|["ABCD", "AABB"]|[9, 4]|
|["AA"]|["B"]|[-1]|
|["AGZ", "BSSS"]|["ASA","BGZ"]|[4, 6]|

### 입출력 예 설명

**입출력 예 #1**
  - "ABCD"의 경우,
  - 1번 키 한 번 → A
  - 2번 키 한 번 → B
  - 2번 키 두 번 → C
  - 1번 키 다섯 번 → D
  - 따라서 총합인 9를 첫 번째 인덱스에 저장합니다.
  - "AABB"의 경우,
  - 1번 키 한 번 → A
  - 1번 키 한 번 → A
  - 2번 키 한 번 → B
  - 2번 키 한 번 → B
  - 따라서 총합인 4를 두 번째 인덱스에 저장합니다.
  - 결과적으로 [9, 4]를 return 합니다.
  
**입출력 예 #2**
  - "B"의 경우, 'B'가 어디에도 존재하지 않기 때문에 -1을 첫 번째 인덱스에 저장합니다.
  - 결과적으로 [-1]을 return 합니다.
  
**입출력 예 #3**
  - "ASA"의 경우,
  - 1번 키 한 번 → A
  - 2번 키 두 번 → S
  - 1번 키 한 번 → A
  - 따라서 총합인 4를 첫 번째 인덱스에 저장합니다.
  - "BGZ"의 경우,
  - 2번 키 한 번 → B
  - 1번 키 두 번 → G
  - 1번 키 세 번 → Z
  - 따라서 총합인 6을 두 번째 인덱스에 저장합니다.
  - 결과적으로 [4, 6]을 return 합니다.

## 작성한 답

```cs
public int[] solution(string[] keymap, string[] targets)
{
    int[] answer = new int[targets.Length];

    int targetCharIndex;
    int keymapCharIndex;
    int arrIndex;
    int minCount;

    for (int i = 0; i < targets.Length; i++)
    {
        // 변수 초기화
        targetCharIndex = 0;
        keymapCharIndex = 0;
        arrIndex = 0;
        minCount = -1;

        while (targetCharIndex < targets[i].Length)
        {
            bool bMatch = false;

            // target 문자와 arrIndex번째 key의 keymapCharIndex번째 문자를 비교
            bMatch = keymap[arrIndex][keymapCharIndex] == targets[i][targetCharIndex];
            
            // 일치한 경우
            if (bMatch)
            {
                // arrIndex 번째 key에서 몇번만에 target문자를 찾았는지 기록
                minCount = keymapCharIndex + 1;
                // 다음 key를 확인하기 위해 arrIndex +1
                arrIndex++;
                // key를 처음부터 순회하기 위해 keymapCharIndex를 초기화
                keymapCharIndex = 0;
            }
            // 일치하지 않은 경우
            else
            {
                // 다음 key문자를 확인하기 위해 keymapCharIndex +1
                keymapCharIndex++;

                // arrIndex번째 key의 모든 문자를 확인했거나
                // 이전에 찾았던 최소횟수보다 오래 걸린경우 
                if (keymapCharIndex >= keymap[arrIndex].Length ||
                    ((minCount != -1) && (keymapCharIndex >= minCount)))
                {
                    // 다음 key를 확인하기 위해 arrIndex +1
                    arrIndex++;
                    // key를 처음부터 순회하기 위해 keymapCharIndex를 초기화
                    keymapCharIndex = 0;
                }
            }

            // 모든 key 순회를 한 상황이면
            if (arrIndex >= keymap.Length)
            {
                // 모든 key에서 문자를 찾지 못한 경우
                if (minCount == -1)
                {
                    answer[i] = -1;
                    break;
                }
                else
                {
                    // minCount를 answer[i]에 누적하고 초기화
                    answer[i] += minCount;
                    minCount = -1;
                    // 다음 target 문자를 비교하기 위해 targetCharIndex+1
                    targetCharIndex++;
                    // 다시 첫 key부터 체크하기 위해 arrIndex 초기화
                    arrIndex = 0;
                }
            }
        }
    }

    return answer;
}
```

- 필요한 변수 선언
  ```cs
  // 변수 초기화
  targetCharIndex = 0; // target 문자열중 현재 찾고있는 문자의 index
  keymapCharIndex = 0; // keymap의 key문자열중 현재 검사중인 key문자의 index
  arrIndex = 0; // keymap 배열에서 현재 검사중인 keymap의 index
  minCount = -1; // 최소 횟수를 저장
  ```

- 먼저 현재 자판(keymap[arrIndex][keymapCharIndex])의 문자가 target문자 (targets[i][targetCharIndex])와 같은지를 체크
  ```cs
  bool bMatch = false;

  // target 문자와 arrIndex번째 key의 keymapCharIndex번째 문자를 비교
  bMatch = keymap[arrIndex][keymapCharIndex] == targets[i][targetCharIndex];
  ```

- 일치한 경우 minCount에 찾은 횟수를 기록해두고 다음 keymap을 체크할 수 있도록 변수값 조정
- 일치하지 않은 경우 현재 keymap의 모든 문자를 확인했는지, minCount에 값이 존재한다면
  minCount를 초과하지 않았는지 검사
  ```cs
  // 일치한 경우
  if (bMatch)
  {
      // arrIndex 번째 key에서 몇번만에 target문자를 찾았는지 기록
      minCount = keymapCharIndex + 1;
      // 다음 key를 확인하기 위해 arrIndex +1
      arrIndex++;
      // key를 처음부터 순회하기 위해 keymapCharIndex를 초기화
      keymapCharIndex = 0;
  }
  // 일치하지 않은 경우
  else
  {
      // 다음 key문자를 확인하기 위해 keymapCharIndex +1
      keymapCharIndex++;

      // arrIndex번째 key의 모든 문자를 확인했거나
      // 이전에 찾았던 최소횟수보다 오래 걸린경우 
      if (keymapCharIndex >= keymap[arrIndex].Length ||
          ((minCount != -1) && (keymapCharIndex >= minCount)))
      {
          // 다음 key를 확인하기 위해 arrIndex +1
          arrIndex++;
          // key를 처음부터 순회하기 위해 keymapCharIndex를 초기화
          keymapCharIndex = 0;
      }
  }
  ```

- 모든 keymap이 순회된 상황이라면 종료조건을 체크
    - minCount가 -1이라면 모든 keymap의 문자에서 target을 찾지 못한 것이므로 -1
    - minCount가 -1이 아니라면 keymap의 문자들 중 target을 찾은 것이므로 결과 횟수에 합산하고
      계속 진행한다.
  ```cs
  // 모든 key 순회를 한 상황이면
  if (arrIndex >= keymap.Length)
  {
      // 모든 key에서 문자를 찾지 못한 경우
      if (minCount == -1)
      {
          answer[i] = -1;
          break;
      }
      else
      {
          // minCount를 answer[i]에 누적하고 초기화
          answer[i] += minCount;
          minCount = -1;
          // 다음 target 문자를 비교하기 위해 targetCharIndex+1
          targetCharIndex++;
          // 다시 첫 key부터 체크하기 위해 arrIndex 초기화
          arrIndex = 0;
      }
  }
  ```

- 모든 작업이 끝난 후 결과값을 return   
  -> **return answer**