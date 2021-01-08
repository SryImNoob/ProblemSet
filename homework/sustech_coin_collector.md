# Problem J: Coin Collector

Time Limit: 2 Sec Memory Limit: 128 MB

To celebrate the 10th anniversary of SUSTech, coins are falling from the heaven! \(Bob\) is on the way to collect them. Now there are some coins. The coin with index \(i\) will arrive in the ground at \(t_i\) second and at \(x_i\) position, value of which is \(y_i\). If at \(t_i\) second \(Bob\) is exactly at \(x_i\) position, he can collect that coin. In addition, each coin is so magical that only if \(Bob\) collect the coin with index \(j\) last time, which is less or equal than \(r_i(j \leq r_i)\), can he collect the coin with index \(i\). Particularly, \(Bob\) can immediately collect the FIRST coin by ignoring this magic. Meanwhile, it's known that if \(t_i < t_j\), then there will be \(x_i <= x_j\). It's guarantee that if \(t_i = t_j\), there will not be \(x_i = x_j\).

At the beginning, \(Bob\) can start at any position he wants. Each second, \(Bob\) can move to \(x_i + 1\) or \(x_i - 1\) if he is now at \(x_i\). He wants to maximize the sum of the values of all coins he collects. Can you tell him?

## Input

The first line contains an integer \(n\) indicating the total number of coins.

Next \(n\) lines, each line consists of four integers \(t_i,x_i,y_i,r_i\), describing the information of each coin.

\(1\leq n \leq 10^5\), \(1 \leq t_i,x_i,y_i \leq 10^9\), \(1 \leq r_i \leq n\)

## Output

In a single line, print out the answer representing the max sum of the value \(Bob\) can get.

## Sample Input

```
5
1 1 1 5
2 2 1 5
5 4 1 5
4 4 2 5
3 2 5 1
```

## Sample Output

```
7
```

## Solution

```cpp
```
