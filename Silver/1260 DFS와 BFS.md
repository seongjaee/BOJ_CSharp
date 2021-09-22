# 1260 DFS와 BFS

## 코드

```C#
using System;
using System.IO;
using System.Collections.Generic;
using System.Text;


class Program
{
    static StreamReader sr = new StreamReader(Console.OpenStandardInput());

    static void Main(string[] args)
    {
        int[] nmv = Array.ConvertAll(sr.ReadLine().Split(), int.Parse);
        int n = nmv[0];
        int m = nmv[1];
        int start = nmv[2];

        bool[] visited = new bool[n + 1];
        int[,] graph = new int[n + 1, n + 1];

        for (int i = 0; i < m; i++)
        {
            int[] input = Array.ConvertAll(sr.ReadLine().Split(), int.Parse);
            graph[input[0], input[1]] = 1;
            graph[input[1], input[0]] = 1;
        }

        StringBuilder sb = new StringBuilder();

        DFS(graph, visited, start, n, sb);
        sb.Append("\n");
        BFS(graph, start, n, sb);
        Console.WriteLine(sb);

        static void DFS(int[,] graph, bool[] visited, int node, int n, StringBuilder sb)
        {
            if (visited[node]) return;
            visited[node] = true;
            sb.Append($"{node} ");

            for (int i = 0; i <= n; i++)
            {
                if (graph[node, i] == 1)
                {
                    DFS(graph, visited, i, n, sb);
                }
            }
        }

        static void BFS(int[,] graph, int start, int n, StringBuilder sb)
        {
            Queue<int> queue = new Queue<int>();
            queue.Enqueue(start);
            bool[] visited = new bool[n + 1];

            while (queue.Count > 0)
            {
                int node = queue.Dequeue();
                if (visited[node]) continue;
                visited[node] = true;
                sb.Append($"{node} ");

                for (int i = 0; i <= n; i++)
                {
                    if (graph[node, i] == 1)
                    {
                        queue.Enqueue(i);
                    }
                }
            }
        }
    }
}
```

## 메모

- `int[,] graph = new int[n + 1, n + 1];` 으로 다차원 배열을 초기화할 수 있다.
- 다차원 배열의 인덱싱은 `graph[i, j]`로 콤마로 구분해서 인덱싱한다.
- 큐 자료구조는 `Queue<T>`, 네임스페이스는 `System.Collections.Generic`.
  - 삽입은 `Enqueue`, 삭제는 `Dequeue`
- 스택 자료구조는 `Stack<T>`

