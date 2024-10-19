# 직사각형 별찍기 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/12969)

## 문제 설명
이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.   
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.

## 제한사항
- n과 m은 각각 1000 이하인 자연수입니다.

## 입출력 예
입력
```
5 3
```

출력
```
*****
*****
*****
```

## 작성한 답

```cs
public void solution()
{
    string[] s;

    Console.Clear();
    s = Console.ReadLine().Split(' ');

    int n = int.Parse(s[0]);
    int m = int.Parse(s[1]);

    // m만큼 반복하며 개행
    for (int i = 0; i < m; i++)
    {
        // n만큼 반복하며 별찍기
        for (int j = 0; j < n; j++)
        {
            Console.Write("*");
        }
        Console.WriteLine();
    }
}
```

- 먼저 n과 m을 입력받고 저장한다.
  ```cs
  string[] s;

  Console.Clear();
  s = Console.ReadLine().Split(' ');

  int n = int.Parse(s[0]);
  int m = int.Parse(s[1]);
  ```

- m만큼 반복하며 개행하고 n만큼 반복하며 별을 찍는다.
  ```cs
  // m만큼 반복하며 개행
  for (int i = 0; i < m; i++)
  {
      // n만큼 반복하며 별찍기
      for (int j = 0; j < n; j++)
      {
          Console.Write("*");
      }
      Console.WriteLine();
  }
  ```