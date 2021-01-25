# Problem J: Coin Collector

[Link](https://acm.sustech.edu.cn/onlinejudge/problem.php?cid=1090&pid=9)

Time Limit: 2 Sec Memory Limit: 128 MB

To celebrate the 10th anniversary of SUSTech, coins are falling from the heaven! \(Bob\) is on the way to collect them. Now there are some coins. The coin with index \(i\) will arrive in the ground at \(t_i\) second and at \(x_i\) position, value of which is \(y_i\). If at \(t_i\) second \(Bob\) is exactly at \(x_i\) position, he can collect that coin. In addition, each coin is so magical that only if \(Bob\) collect the coin with index \(j\) last time, which is less or equal than \(r_i(j \leq r_i)\), can he collect the coin with index \(i\). Particularly, \(Bob\) can immediately collect the FIRST coin by ignoring this magic. Meanwhile, it's known that if \(t_i > t_j\), then there will be \(x_i \geq x_j\). It's guarantee that if \(t_i = t_j\), there will not be \(x_i = x_j\).

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
#include <iostream>
#include <array>
#include <algorithm>
#include <map>
#include <iterator>
 
using namespace std;
 
#define MAXN 100100
 
typedef long long ll;
 
ll n;
 
array<array<ll, 5>, MAXN> s;
 
map<ll, ll> arr[MAXN];
 
void map_add(map<ll, ll> &m, ll k, ll v) {
    auto iter = m.lower_bound(k);
    if(iter->second >= v) {
        return;
    }
    m[k] = v;
    if(m.size() == 1) return;
    iter = m.lower_bound(k);
    if(iter == m.begin()) return;
    /*
    cout << "map_add" << endl;
    for(auto i = m.begin(); i != m.end(); ++i) {
        cout << i->first << " " << i->second << endl;
    }
    cout << "iter" << endl;
    cout << iter->first << " " << iter->second << endl;
    */
    while(1) {
        iter = std::prev(iter);
        // cout << m.size() << " " << iter->first << " " << iter->second << endl;
        if(iter->second >= v) return;
        iter = m.erase(iter);
        if(iter == m.begin()) return;
    }
     
}
 
void arr_add(ll i, ll k, ll v) {
    while(i <= n) {
        map_add(arr[i], k, v);
        i += (i & -i);
    }
}
 
ll arr_query(ll i, ll k) {
    ll ret = 0;
    while(i > 0) {
        auto iter = arr[i].lower_bound(k);
        if(iter != arr[i].end() && iter->second > ret) {
            ret = iter->second;
        }
        i -= (i & -i);
    }
    return ret;
}
 
int main() {
    while(cin >> n) {
        for(ll i = 0; i <= n; ++i) {
            arr[i].clear();
        }
        for(ll i = 0; i < n; ++i) {
            cin >> s[i][0] >> s[i][1] >> s[i][2] >> s[i][3];
            s[i][4] = i + 1;
        }
             
        sort(s.begin(), s.begin() + n);
         
        ll ans = 0;
        for(ll i = 0; i < n; ++i) {
            // printf("i %d %d %d %d %d %d\n", i, s[i][0], s[i][1], s[i][2], s[i][3], s[i][4]);
            ll k = s[i][1] - s[i][0];
            ll r = s[i][3];
            ll ind = s[i][4];
            ll ay = arr_query(r, k) + s[i][2];
            arr_add(ind, k, ay);
            if(ay > ans) ans = ay;
        }
        cout << ans << endl;
    }
    return 0;
}
```
