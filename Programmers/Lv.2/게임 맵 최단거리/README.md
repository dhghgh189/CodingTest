# 게임 맵 최단거리 [(Link)](https://school.programmers.co.kr/learn/courses/30/lessons/1844)

## 문제 설명
ROR 게임은 두 팀으로 나누어서 진행하며, 상대 팀 진영을 먼저 파괴하면 이기는 게임입니다.   
따라서, 각 팀은 상대 팀 진영에 최대한 빨리 도착하는 것이 유리합니다.   

지금부터 당신은 한 팀의 팀원이 되어 게임을 진행하려고 합니다.   
다음은 5 x 5 크기의 맵에, 당신의 캐릭터가 (행: 1, 열: 1) 위치에 있고,   
상대 팀 진영은 (행: 5, 열: 5) 위치에 있는 경우의 예시입니다.   

![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/dc3a1b49-13d3-4047-b6f8-6cc40b2702a7/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B51_sxuruo.png)   

위 그림에서 검은색 부분은 벽으로 막혀있어 갈 수 없는 길이며, 흰색 부분은 갈 수 있는 길입니다.   
캐릭터가 움직일 때는 동, 서, 남, 북 방향으로 한 칸씩 이동하며, 게임 맵을 벗어난 길은 갈 수 없습니다.   
아래 예시는 캐릭터가 상대 팀 진영으로 가는 두 가지 방법을 나타내고 있습니다.   

- 첫 번째 방법은 11개의 칸을 지나서 상대 팀 진영에 도착했습니다.   
![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/9d909e5a-ca95-4088-9df9-d84cb804b2b0/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B52_hnjd3b.png)   
- 두 번째 방법은 15개의 칸을 지나서 상대팀 진영에 도착했습니다.   
![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b7cd629-a3c2-4e02-b748-a707211131de/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B53_ntxygd.png)   

위 예시에서는 첫 번째 방법보다 더 빠르게 상대팀 진영에 도착하는 방법은 없으므로,   
이 방법이 상대 팀 진영으로 가는 가장 빠른 방법입니다.   

만약, 상대 팀이 자신의 팀 진영 주위에 벽을 세워두었다면 상대 팀 진영에 도착하지 못할 수도 있습니다.   
예를 들어, 다음과 같은 경우에 당신의 캐릭터는 상대 팀 진영에 도착할 수 없습니다.   

![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/d963b4bd-12e5-45da-9ca7-549e453d58a9/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B54_of9xfg.png)   

게임 맵의 상태 maps가 매개변수로 주어질 때, 캐릭터가 상대 팀 진영에 도착하기 위해서 지나가야 하는 칸의 개수의 최솟값을 return 하도록   
solution 함수를 완성해주세요. 단, 상대 팀 진영에 도착할 수 없을 때는 -1을 return 해주세요.   

## 제한사항
- maps는 n x m 크기의 게임 맵의 상태가 들어있는 2차원 배열로, n과 m은 각각 1 이상 100 이하의 자연수입니다.  
  - n과 m은 서로 같을 수도, 다를 수도 있지만, n과 m이 모두 1인 경우는 입력으로 주어지지 않습니다.   
- maps는 0과 1로만 이루어져 있으며, 0은 벽이 있는 자리, 1은 벽이 없는 자리를 나타냅니다.   
- 처음에 캐릭터는 게임 맵의 좌측 상단인 (1, 1) 위치에 있으며, 상대방 진영은 게임 맵의 우측 하단인 (n, m) 위치에 있습니다.   

## 입출력 예
|maps|answer|
|------|---|
|[[1,0,1,1,1],[1,0,1,0,1],[1,0,1,1,1],[1,1,1,0,1],[0,0,0,0,1]]|11|
|[[1,0,1,1,1],[1,0,1,0,1],[1,0,1,1,1],[1,1,1,0,0],[0,0,0,0,1]]|-1|

### 입출력 예 설명

**입출력 예 #1**
  - 주어진 데이터는 다음과 같습니다.
  
  ![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/6db71f7f-58d3-4623-9fab-7cd99fa863a5/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B56_lgjvrb.png)   
  
  캐릭터가 적 팀의 진영까지 이동하는 가장 빠른 길은 다음 그림과 같습니다.

  ![](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/d223d017-b3e2-4772-9045-a565133d45ff/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B52_hnjd3b%20%281%29.png)

  따라서 총 11칸을 캐릭터가 지나갔으므로 11을 return 하면 됩니다.

**입출력 예 #2**
  - 문제의 예시와 같으며, 상대 팀 진영에 도달할 방법이 없습니다. 따라서 -1을 return 합니다.

## 작성한 답

```cs
public int solution(int[,] maps)
{
    int answer = 0;

    int sizeY = maps.GetLength(0);
    int sizeX = maps.GetLength(1);

    // BFS로 탐색, visited[,]와 parent[,] 배열을 사용
    // 탐색 종료 후 visited[n-1, m-1]이 false면 -1
    // visited[n-1, m-1]이 true면 parent[n-1, m-1]부터 카운팅
    
    bool[,] visited = new bool[sizeY, sizeX];
    Node[,] parent = new Node[sizeY, sizeX];

    Queue<Node> queue = new Queue<Node>();
    // 시작점 위치
    Node start = new Node() { x = 0, y = 0 };
    // 결승점 위치
    Node end = new Node() { x = sizeX - 1, y = sizeY - 1 };

    // 초기화
    visited[start.y, start.x] = true;
    queue.Enqueue(start);

    while (queue.Count > 0)
    {
        Node current = queue.Dequeue();

        foreach (Point dir in direction)
        {
            // current.y로부터 i만큼 떨어진 곳 (인접한 y)
            int nextY = current.y + dir.y;
            // current.x로부터 j만큼 떨어진 곳 (인접한 x)
            int nextX = current.x + dir.x;

            // nextY 위치가 유효하지 않다
            if (nextY < 0 || nextY >= sizeY)
                continue;

            // nextX 위치가 유효하지 않다
            if (nextX < 0 || nextX >= sizeX)
                continue;

            // next 위치가 벽이 아니고, 아직 발견되지 않았었다면
            if (maps[nextY, nextX] == 1 &&
                visited[nextY, nextX] == false)
            {
                // 위치 발견 여부 저장
                visited[nextY, nextX] = true;
                // next 위치는 current를 통해 발견했음을 저장
                parent[nextY, nextX] = current;
                // 추후 next 위치를 방문하기 위해 기억한다.
                queue.Enqueue(new Node() { x = nextX, y = nextY });
            }
        }
    }

    // 결승점으로 가는 길이 발견되지 않았다면
    // 도달할 수 없는 정점이다.
    if (visited[end.y, end.x] == false)
    {
        return -1;
    }

    Node now = end;

    // 결승점부터 출발점 까지 역추적하면서 몇번 이동하는지를 카운팅
    while (now != null)
    {
        answer++;
        now = parent[now.y, now.x];
    }

    return answer;
}

// 각 위치의 정보를 저장하기 위한 Node 클래스
public class Node
{
    public int x;
    public int y;

    public Node()
    {
        x = y = -1;
    }
}

// 위치를 나타내는 Point 구조체
public struct Point
{
    public int x;
    public int y;
}

// 동서남북 방향을 나타내기 위한 direction 배열
public Point[] direction =
{
    new Point() { x = 1, y = 0 },       // 동
    new Point() { x = -1, y = 0 },      // 서
    new Point() { x = 0, y = 1 },       // 남
    new Point() { x = 0, y = -1 }       // 북
};
```

- 위치를 나타내는 Point 구조체 및 동서남북 방향을 나타내기 위한 direction 배열 선언
  ```cs  
  public struct Point
  {
      public int x;
      public int y;
  }

  public Point[] direction =
  {
      new Point() { x = 1, y = 0 },       // 동
      new Point() { x = -1, y = 0 },      // 서
      new Point() { x = 0, y = 1 },       // 남
      new Point() { x = 0, y = -1 }       // 북
  };
  ```
  
- 각 위치의 정보를 저장하기 위한 Node 클래스 선언
  ```cs
  public class Node
  {
      public int x;
      public int y;
  
      public Node()
      {
          x = y = -1;
      }
  }
  ```

- 필요한 초기화 작업들을 진행   
  ```cs
  // 입력된 map의 sizeY
  int sizeY = maps.GetLength(0);
  // 입력된 map의 sizeX
  int sizeX = maps.GetLength(1);  
  // 발견여부를 저장할 visited
  bool[,] visited = new bool[sizeY, sizeX];
  // 어느 위치로부터 발견됬는지를 저장할 parent
  Node[,] parent = new Node[sizeY, sizeX];  
  // 다음 방문지점을 기억할 queue
  Queue<Node> queue = new Queue<Node>();  
  // 시작 위치
  Node start = new Node() { x = 0, y = 0 };
  // 결승점 위치
  Node end = new Node() { x = sizeX - 1, y = sizeY - 1 };  
  // 시작위치 발견여부 갱신
  visited[start.y, start.x] = true;
  // 시작위치를 기억한다.
  queue.Enqueue(start);
  ```

- queue에 다음 방문위치가 존재할 동안 반복하면서 탐색 진행
  ```cs
  while (queue.Count > 0)
  {
      Node current = queue.Dequeue();

      foreach (Point dir in direction)
      {
          // current.y로부터 i만큼 떨어진 곳 (인접한 y)
          int nextY = current.y + dir.y;
          // current.x로부터 j만큼 떨어진 곳 (인접한 x)
          int nextX = current.x + dir.x;
          // nextY 위치가 유효하지 않다
          if (nextY < 0 || nextY >= sizeY)
              continue;
          // nextX 위치가 유효하지 않다
          if (nextX < 0 || nextX >= sizeX)
              continue;
          // next 위치가 벽이 아니고, 아직 발견되지 않았었다면
          if (maps[nextY, nextX] == 1 &&
              visited[nextY, nextX] == false)
          {
              // 위치 발견 여부 저장
              visited[nextY, nextX] = true;
              // next 위치는 current를 통해 발견했음을 저장
              parent[nextY, nextX] = current;
              // 추후 next 위치를 방문하기 위해 기억한다.
              queue.Enqueue(new Node() { x = nextX, y = nextY });
          }
      }
  }
  ```

- 탐색이 종료되면 경로를 역 추적하여 이동 횟수를 계산한다.
  ```cs
  // 결승점으로 가는 길이 발견되지 않았다면
  // 도달할 수 없는 정점이다.
  if (visited[end.y, end.x] == false)
  {
      return -1;
  }

  Node now = end;

  // 결승점부터 출발점 까지 역추적하면서 몇번 이동하는지를 카운팅
  while (now != null)
  {
      answer++;
      now = parent[now.y, now.x];
  }
  ```

- 계산이 끝나면 결과 return   
  -> **return answer**