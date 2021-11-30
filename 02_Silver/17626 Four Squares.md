# [17626 Four Squares](https://www.acmicpc.net/problem/17626)

## 코드

```C#
using System;
using System.Linq;

class Program
{
    public static void Main(string[] args)
    {
        int n = int.Parse(Console.ReadLine());
        int[] squares = new Int32[223];

        for (int i = 1; i <= 223; i++) {
            squares[i - 1] = i * i;
        }
        int answer = 4;

        void GetSquareNumber(int k, int level)
        {
            if (level > answer) return;
            if (squares.Contains(k)) {
                answer = Math.Min(answer, level);
                return;
            }
            if (level == 3) return;
            foreach (int s in squares)
            {
                if (s > k) break;
                GetSquareNumber(k - s, level + 1);
            }
        }
        GetSquareNumber(n, 1);
        Console.WriteLine(answer);
    }
}
```



## 메모

- 최대 3번까지 재귀 호출하는 재귀 함수를 이용했다.
- Array의 containment 확인을 위한 메서드`Contains`가 기억이 나지 않아 조금 헤맸다.
- `Linq`의 `Enumerable.Contains()`