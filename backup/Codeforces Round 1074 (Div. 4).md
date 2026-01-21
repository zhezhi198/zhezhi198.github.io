[进入比赛](https://codeforces.com/contest/2185)
# A. 完美的根 

**时间限制：** 1 秒  
**内存限制：** 256 MB  
**输入：** 标准输入  
**输出：** 标准输出  

## 题目描述

如果存在一个整数 $y$ 使得 $\sqrt{y} = x$，则正整数 $x$ 被称为一个**完全根**。

例如，5 是一个完全根，因为 $\sqrt{25} = 5$。

对于每个测试用例，请输出 $n$ 个**不同**的完全根。
注意：这些值只需要在当前测试用例中互不相同即可；在不同的测试用例中，你可以重复使用相同的值。

### 输入格式
输入的第一行包含一个整数 $t$ ($1 \le t \le 20$) —— 测试用例的数量。

每个测试用例只有一行，包含一个整数 $n$ ($1 \le n \le 20$) —— 需要输出的完全根的个数。

### 输出格式
对于每个测试用例，输出 $n$ 个不同的完全根。每个完全根 $x$ 必须在 $1 \le x \le 10^9$ 的范围内。

## 样例

**输入**
```text
3
1
2
5
```
**输出**
```text
1
2 4
2 102 43 1 21
```
>正数n是n*n的一个平方根，直接输出n个正数就行。
代码:
```cpp
#include <bits/stdc++.h>
using namespace std;
// CJX__//
typedef long long ll; // 不开long long 见祖宗
typedef unsigned long long ull;
typedef __int128 i128;
typedef pair<int, int> PII;
typedef pair<ll, ll> PLL;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef vector<double> vd;
typedef vector<PII> vPII;
#define IOS                  \
    ios::sync_with_stdio(0); \
    cin.tie(0);              \
    cout.tie(0);
#define debug(...) cout << "[debug] " #__VA_ARGS__ " = " << (__VA_ARGS__) << endl;
#define out(x) cout << ((x) ? "YES" : "NO") << endl
#define mod(x, P) (((x) % (P) + (P)) % (P))
#define endl '\n'
#define gcd __gcd
#define lc p << 1
#define rc p << 1 | 1
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x) & (-x))
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define dep(i, x, n) for (ll i = x; i >= n; i--)
#define mem(a, x) memset(a, x, sizeof a)
const double eps = 1e-5;
const int N = 1e5 + 10, M = 2 * N, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const ll base1 = 131, base2 = 13331;
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template <typename T>
bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }
/*

*/
ll n;
void solve()
{
    cin >> n;
    rep(i, 1, n) cout << i << " ";
    cout << endl;
}

int main()
{
    IOS;

    int _ = 1;
    cin >> _; // 如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
# B. 前缀最大值 

**时间限制：** 1.5 秒  
**内存限制：** 256 MB  
**输入：** 标准输入  
**输出：** 标准输出  

## 题目描述

给定一个包含 $n$ 个整数的数组 $a_1, a_2, \dots, a_n$。

定义一个数组的**“值”**为该数组每个前缀的最大值之和。
更正式地说，数组 $a$ 的值为：
$$\sum_{i=1}^{n} \max(a_1, \dots, a_i)$$

例如，数组 $[1, 2, 1]$ 的值为：
$$\max(1) + \max(1, 2) + \max(1, 2, 1) = 1 + 2 + 2 = 5$$

你可以选择两个下标 $i$ 和 $j$ 并交换元素 $a_i$ 和 $a_j$。**这个操作最多只能执行一次**（也可以不执行）。

请找出在执行最多一次操作后，数组 $a$ 可能达到的**最大值**。

### 输入格式
输入的第一行包含一个整数 $t$ ($1 \le t \le 100$) —— 测试用例的数量。

每个测试用例的第一行包含一个整数 $n$ ($2 \le n \le 50$) —— 数组 $a$ 的长度。

第二行包含 $n$ 个整数 $a_1, a_2, \dots, a_n$ ($1 \le a_i \le 10^4$) —— 数组 $a$ 的元素。

### 输出格式
对于每个测试用例，输出执行交换操作（或不交换）后，数组 $a$ 能达到的最大可能值。

## 样例

**输入**
```text
4
5
2 1 4 5 3
2
5 1
3
3 2 1
2
6 7
```
**输出**
```text
25
10
9
14
```
>很明显把最大值用最多次，放在数组第一个位置就可以了。
代码:
```
cpp
#include <bits/stdc++.h>
using namespace std;
// CJX__//
typedef long long ll; // 不开long long 见祖宗
typedef unsigned long long ull;
typedef __int128 i128;
typedef pair<int, int> PII;
typedef pair<ll, ll> PLL;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef vector<double> vd;
typedef vector<PII> vPII;
#define IOS                  \
    ios::sync_with_stdio(0); \
    cin.tie(0);              \
    cout.tie(0);
#define debug(...) cout << "[debug] " #__VA_ARGS__ " = " << (__VA_ARGS__) << endl;
#define out(x) cout << ((x) ? "YES" : "NO") << endl
#define mod(x, P) (((x) % (P) + (P)) % (P))
#define endl '\n'
#define gcd __gcd
#define lc p << 1
#define rc p << 1 | 1
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x) & (-x))
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define dep(i, x, n) for (ll i = x; i >= n; i--)
#define mem(a, x) memset(a, x, sizeof a)
const double eps = 1e-5;
const int N = 1e5 + 10, M = 2 * N, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const ll base1 = 131, base2 = 13331;
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template <typename T>
bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }
/*

*/

void solve()
{
    ll n;
    cin >> n;
    ll mx = 0;
    rep(i, 1, n)
    {
        ll x;
        cin >> x;
        cmax(mx, x);
    }
    cout << mx * n << endl;
}

int main()
{
    IOS;

    int _ = 1;
    cin >> _; // 如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
# C. 移位 MEX 

**时间限制：** 2 秒  
**内存限制：** 256 MB  
**输入：** 标准输入  
**输出：** 标准输出  

## 题目描述

给定一个包含 $n$ 个整数的数组 $a_1, a_2, \dots, a_n$。你允许执行以下操作**一次**：

选择一个整数 $x$（可以是负数），然后对于每一个 $i$ ($1 \le i \le n$)，将 $a_i$ 更新为 $a_i + x$。

例如，如果 $a = [1, 3, 4, 2]$，并且你选择 $x = 3$ 执行操作，那么数组 $a$ 将变为 $[4, 6, 7, 5]$。

请输出在执行完操作后，数组的 $\text{MEX}(a)$ 可能达到的**最大值**。

> **MEX 定义：**
> **MEX(a)** 定义为数组中**不包含**的最小非负整数。
> 例如：`MEX([1, 2, 0, 5]) = 3`，`MEX([1, 2, 4, 9]) = 0`。

### 输入格式
输入的第一行包含一个整数 $t$ ($1 \le t \le 1000$) —— 测试用例的数量。

每个测试用例的第一行包含一个整数 $n$ ($1 \le n \le 3000$) —— 数组 $a$ 的长度。

第二行包含 $n$ 个整数 $a_1, a_2, \dots, a_n$ ($-10^9 \le a_i \le 10^9$) —— 数组 $a$ 的元素。

保证所有测试用例中 $n$ 的总和不超过 $3000$。

### 输出格式
对于每个测试用例，输出操作执行后 $\text{MEX}(a)$ 的最大可能值。

## 样例

**输入**
```text
6
1
4
5
0 1 1 2 3
2
1 1
4
4 2 3 6
5
2 4 1 0 -1
6
-1 1 2 3 5 6
```
**输出**
```text
1
4
1
3
4
3
```
>思路:给数组中每个值+x相当于把平移值轴，根据mex的性质，显然既然可以平移，那么mex的值可以转换为最长连续数组的长度吗？
代码：
```
cpp
#include <bits/stdc++.h>
using namespace std;
// CJX__//
typedef long long ll; // 不开long long 见祖宗
typedef unsigned long long ull;
typedef __int128 i128;
typedef pair<int, int> PII;
typedef pair<ll, ll> PLL;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef vector<double> vd;
typedef vector<PII> vPII;
#define IOS                  \
    ios::sync_with_stdio(0); \
    cin.tie(0);              \
    cout.tie(0);
#define debug(...) cout << "[debug] " #__VA_ARGS__ " = " << (__VA_ARGS__) << endl;
#define out(x) cout << ((x) ? "YES" : "NO") << endl
#define mod(x, P) (((x) % (P) + (P)) % (P))
#define endl '\n'
#define gcd __gcd
#define lc p << 1
#define rc p << 1 | 1
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x) & (-x))
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define dep(i, x, n) for (ll i = x; i >= n; i--)
#define mem(a, x) memset(a, x, sizeof a)
const double eps = 1e-5;
const int N = 1e5 + 10, M = 2 * N, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const ll base1 = 131, base2 = 13331;
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template <typename T>
bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }
/*

*/

void solve()
{
    ll n;
    cin >> n;
    vll a(n + 1, 0);
    rep(i, 1, n) cin >> a[i];
    sort_range(a, 1, n);
    ll len = 1, mx = 1;
    rep(i, 2, n)
    {

        if (a[i] == a[i - 1])
            continue;
        else if (a[i] == a[i - 1] + 1)
        {
            len++;
            cmax(mx, len);
        }
        else
        {
            len = 1;
        }
     }
    cout << mx << endl;
}

int main()
{
    IOS;

    int _ = 1;
    cin >> _; // 如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
# D. 内存溢出 

**时间限制：** 2 秒  
**内存限制：** 256 MB  
**输入：** 标准输入  
**输出：** 标准输出  

## 题目描述

Bessie 有一个包含 $n$ 个整数的数组 $a_1, a_2, \dots, a_n$。
她会对数组执行 $m$ 次操作。第 $i$ 次操作将 $a_{b_i}$ 修改为 $a_{b_i} + c_i$。

不幸的是，由于内存成本上升，Bessie 的计算机内存有限。
如果在**任何时候**数组中的**任意**元素大于 $h$，她的计算机就会崩溃，并且数组中的**每个元素都会被重置为初始值**。
（注意：崩溃后，导致崩溃的那次操作及之前的所有操作效果都消失了，系统重新从下一次操作开始计算）。

请输出在所有操作执行完毕后，数组 $a$ 的最终状态。

### 输入格式
输入的第一行包含一个整数 $t$ ($1 \le t \le 10^4$) —— 测试用例的数量。

每个测试用例的第一行包含三个整数 $n, m, h$ ($1 \le n, m \le 2 \cdot 10^5, 1 \le h \le 10^9$) —— 数组 $a$ 的长度、操作次数以及计算机允许的最大值。

第二行包含 $n$ 个整数 $a_1, a_2, \dots, a_n$ ($0 \le a_i \le h$) —— 初始数组 $a$。

接下来的 $m$ 行，每行包含两个整数 $b_i, c_i$ ($1 \le b_i \le n, 0 \le c_i \le 10^9$) —— Bessie 对数组执行的操作（下标 $b_i$ 增加 $c_i$）。

保证所有测试用例中 $n$ 和 $m$ 的总和不超过 $2 \cdot 10^5$。

### 输出格式
对于每个测试用例，输出所有操作执行完毕后的数组 $a$。

## 样例

**输入**
```text
3
3 4 5
1 2 1
1 4
2 4
3 3
2 0
5 3 1
1 1 1 1 1
1 1
1 1
2 1
4 4 1
1 0 0 0
1 1
4 4
3 3
4 4
```
**输出**
```text
3
3 4 5
1 2 1
1 4
2 4
3 3
2 0
5 3 1
1 1 1 1 1
1 1
1 1
2 1
4 4 1
1 0 0 0
1 1
4 4
3 3
4 4
```
>思路:正常的模拟肯定要超时，我们可以用vector<pari<>>记录当前操作的<下标，增值>(类似时间戳),当然如果没有超过h的话，要给数组本身增值，如果超过了呢，那么就一边出栈，一边还原之前的值。
时间复杂度大概是(n+m)，因为对于每次操作，我们要么合法，让它入栈，要么不合法让它出栈，均摊下来就是m的复杂度。
代码:
```cpp
#include <bits/stdc++.h>
using namespace std;
// CJX__//
typedef long long ll; // 不开long long 见祖宗
typedef unsigned long long ull;
typedef __int128 i128;
typedef pair<int, int> PII;
typedef pair<ll, ll> PLL;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef vector<double> vd;
typedef vector<PII> vPII;
#define IOS                  \
    ios::sync_with_stdio(0); \
    cin.tie(0);              \
    cout.tie(0);
#define debug(...) cout << "[debug] " #__VA_ARGS__ " = " << (__VA_ARGS__) << endl;
#define out(x) cout << ((x) ? "YES" : "NO") << endl
#define mod(x, P) (((x) % (P) + (P)) % (P))
#define endl '\n'
#define gcd __gcd
#define lc p << 1
#define rc p << 1 | 1
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x) & (-x))
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define dep(i, x, n) for (ll i = x; i >= n; i--)
#define mem(a, x) memset(a, x, sizeof a)
const double eps = 1e-5;
const int N = 1e5 + 10, M = 2 * N, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const ll base1 = 131, base2 = 13331;
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template <typename T>
bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }

/*

*/

void solve()
{
    ll n, m, h;
    cin >> n >> m >> h;
    vll a(n + 1, 0);
    rep(i, 1, n) cin >> a[i];
    vector<PLL>q;

    rep(i, 1, m)
    {
        ll k, c;
        cin >> k >> c;
        if (a[k] + c > h)
        {
            while(q.size())
            {
                auto [fi,se]=q.back();
                q.pop_back();
                a[fi]-=se;
            }
        }
        else
        {
            a[k] += c;
            q.push_back({k,c});
        }
    }
    rep(i, 1, n) cout << a[i] << " ";
    cout << endl;
}

int main()
{
    IOS;

    int _ = 1;
     cin>>_;//如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
# E. The Robotic Rush 

## 题目大意
在一条无限长的数轴上，有 $n$ 个机器人和 $m$ 个尖刺。机器人和尖刺的位置给定。
系统会下发 $k$ 条指令（`L` 或 `R`），所有机器人**同时**执行相同的移动操作。
如果机器人碰到尖刺，立即死亡。求每一步操作后存活的机器人数量。

## 解题思路

这道题的关键在于利用**相对运动**和**预处理**来降低复杂度。

### 1. 相对位移 
因为所有机器人动作一致，我们可以维护一个全局变量 `far` 表示当前的相对位移。
- 初始 `far = 0`。
- 指令 `L`: `far--`。
- 指令 `R`: `far++`。
机器人 $i$ 的实际位置 = $a[i] + far$。

### 2. 最近威胁与预处理
一个机器人只会被它**左边最近**或**右边最近**的尖刺杀死。
因此，我们可以预处理出每个机器人的“致死距离”：
- `l`: 向左走多少步撞到左侧尖刺。
- `r`: 向右走多少步撞到右侧尖刺。

在我的代码中，使用了**二分查找**（`ckl` 和 `ckr` 函数）来快速找到每个机器人左右两侧的尖刺位置。

### 3. 桶  与 懒删除
知道了每个机器人的致死距离后，我们不需要每一步都检查所有机器人。
我使用了两个桶数组 `dl` 和 `dr`：
- `dl[d]`: 存储所有“向左走 `d` 步会死”的机器人 ID。
- `dr[d]`: 存储所有“向右走 `d` 步会死”的机器人 ID。

### 4. 线性模拟
在处理指令时，我维护了一个 `st`  数组。
只有当 `far` 到达了一个**之前从未到达过**的位置时（说明探索了新的区域），才可能触发新的死亡。
此时，根据当前是向左还是向右，去遍历对应距离的桶（`dl` 或 `dr`），将里面的机器人标记为 `dead` 并从总数 `now` 中减去。

## AC 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
// CJX__//
typedef long long ll; // 不开long long 见祖宗
typedef unsigned long long ull;
typedef pair<int, int> PII;
typedef pair<ll, ll> PLL;
typedef vector<int> vi;
typedef vector<ll> vll;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define all(x) x.begin(), x.end()
#define INF 0x3f3f3f3f3f3f3f3f
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }

/*

*/
void solve()
{
    ll n, m, k;
    cin >> n >> m >> k;
    vll a(n + 1, 0), b(m + 2, 0);
    
    // 读入机器人位置
    rep(i, 1, n) {
        cin >> a[i];
    }
    // 读入尖刺位置
    rep(i, 1, m) {
        cin >> b[i];
    }
    
    // 设置哨兵，防止越界，简化二分边界判断
    b[0] = -INF, b[m + 1] = INF;
    
    // 排序，为了后续二分查找
    sort_range(a, 1, n);
    sort_range(b, 1, m);

    // Lambda: 二分查找 <= x 的最大尖刺 (左边最近)
    auto ckl = [&](ll x) {
        ll l = 0, r = m + 1;
        while (l + 1 < r) {
            ll mid = (l + r) >> 1;
            if (b[mid] <= x) l = mid;
            else r = mid;
        }
        return b[l];
    };

    // Lambda: 二分查找 > x 的最小尖刺 (右边最近)
    // 注意：题意是不重合，所以找 >= 或 > 都可以，这里逻辑是找右侧威胁
    auto ckr = [&](ll x) {
        ll l = 0, r = m + 1;
        while (l + 1 < r) {
            ll mid = (l + r) >> 1;
            if (b[mid] < x) l = mid;
            else r = mid;
        }
        return b[r];
    };

    // dl[d]: 向左走 d 步会死的机器人列表
    // dr[d]: 向右走 d 步会死的机器人列表
    vector<vector<ll>> dl(k + 5), dr(k + 5);
    
    rep(i, 1, n)
    {
        // 计算致死距离
        ll l = a[i] - ckl(a[i]); // 左距离
        ll r = ckr(a[i]) - a[i]; // 右距离
        
        // 只有在 k 步内能撞上的才存入桶中
        if (l <= k) dl[l].push_back(i);
        if (r <= k) dr[r].push_back(i);
    }

    // offset 用于处理负数下标，st 数组记录相对位移是否访问过
    const int offset = 2e5 + 5;
    vector<bool> st(4e5 + 10, false);
    vector<bool> dead(n + 1, false);
    
    st[0 + offset] = true;
    ll far = 0; // 当前相对位移
    ll now = n; // 当前存活数
    
    string op;
    cin >> op;
    
    rep(i, 0, k - 1)
    {
        char s = op[i];
        if (s == 'L')
        {
            far -= 1;
            // 如果这个位置之前没到过（探索新区域）
            if (!st[far + offset])
            {
                st[far + offset] = true;
                ll d = abs(far);
                // 且距离在射程范围内
                if (d <= k)
                {
                    // 结算所有“向左走 d 步死”的机器人
                    for (auto id : dl[d])
                    {
                        if (!dead[id]) // 防止重复死亡
                        {
                            dead[id] = true;
                            now--;
                        }
                    }
                }
            }
        }
        else // s == 'R'
        {
            far += 1;
            if (!st[far + offset])
            {
                st[far + offset] = true;
                ll d = abs(far);
                if (d <= k)
                {
                    // 结算所有“向右走 d 步死”的机器人
                    for (auto id : dr[d])
                    {
                        if (!dead[id])
                        {
                            dead[id] = true;
                            now--;
                        }
                    }
                }
            }
        }
        cout << now << " ";
    }
    cout << endl;
}

int main()
{
    IOS;
    int _ = 1;
    cin >> _;
    while (_--)
    {
        solve();
    }
    return 0;
}
```
# F. BattleCows 

**题目链接：** [F. BattleCows](https://codeforces.com/contest/1930/problem/F) 
## 题目大意

有 $2^n$ 头奶牛进行锦标赛（满二叉树结构）。每头奶牛初始在一个栈中。
比赛规则：
1. 奇数位置栈 vs 偶数位置栈。
2. 栈的“战斗力”是栈内所有元素异或和。
3. 战斗力高的获胜，若相等则左边获胜。
4. **获胜的栈跳到失败的栈上方合并**。

有 $q$ 次独立查询：将第 $b$ 头奶牛的值临时改为 $c$，问最终 $b$ 头顶上有多少头奶牛。

## 解题思路

这道题如果直接模拟栈的合并过程会比较繁琐。我们需要通过观察发现规律：

1.  **分治结构**：比赛过程本质上是一个满二叉树的归并过程。我们可以使用分治（递归）来模拟每一层的比赛。
2.  **胜负判定**：每一层比赛比较的是两个区间的异或和。我们可以使用**前缀异或数组 (`pre`)** 来 $O(1)$ 获取任意区间的原始异或和。
3.  **单点修改的处理**：
    查询是独立的，我们不需要真的修改数组或线段树。
    对于当前递归到的区间，如果包含目标奶牛 $b$，我们只需要计算该区间的异或和时，利用异或的性质：`新异或和 = 原异或和 ^ a[b] ^ c`。这样就可以动态获得修改后的值。
4.  **计算头顶数量**：
    题目问 $b$ 上面有多少牛。
    - 如果 $b$ 所在的栈 **赢了**：它会跳到别人头上，它头顶的数量**不变**。
    - 如果 $b$ 所在的栈 **输了**：对手的栈（大小为 `sz`）会压在它头上，它头顶的数量 **增加 `sz`**。
    
    因此，我们只需要从根节点向下递归，或者从叶子节点向上回溯。这里采用**自顶向下的分治**：
    - 递归找到 $b$ 所在的子区间。
    - 判断当前层 $b$ 所在的半区是否输了。如果输了，答案累加对手半区的大小 (`sz`)。

## 复杂度分析

- **预处理**：计算前缀异或和，时间复杂度为 `O(2^n)`。
- **查询**：每次查询只需要递归 `n` 层，每层为常数操作。单次查询复杂度为 `O(n)`。
- **总复杂度**：`O(2^n + n * q)`。
  在 `n <= 18` 且 `q <= 2*10^5` 的数据范围内，计算量约为 `2.6*10^5 + 3.6*10^6`，完全可以在 2 秒内轻松通过。

## AC 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

// 通用模板部分
typedef long long ll;
typedef vector<ll> vll;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define endl '\n'

void solve()
{
    ll n, q; 
    cin >> n >> q;
    ll len = 1 << n; // 总奶牛数 2^n
    
    // a: 原数组, pre: 前缀异或和数组
    vll a(len + 1, 0), pre(len + 2, 0);
    
    rep(i, 1, len)
    {
        cin >> a[i];
        pre[i] = pre[i - 1] ^ a[i];
    }
    
    while(q--)
    {
        ll b, c; 
        cin >> b >> c;
        
        // 定义分治递归函数
        // l, r: 当前处理的区间范围
        auto fz = [&](auto&& self, int l, int r) -> ll
        {
            if(l == r) return 0; // 叶子节点，没有对手，头顶数量为0
            
            int mid = (l + r) >> 1;
            ll sz = (r - l + 1) / 2; // 半区大小（对手栈的大小）
            
            // 计算左右半区原本的异或和
            ll L = pre[mid] ^ pre[l - 1];
            ll R = pre[r] ^ pre[mid];
            
            ll res = 0;
            
            if(b <= mid) // 目标奶牛在左半区
            {
                // 先递归下一层，获取底层的累积结果
                res = self(self, l, mid);
                
                // 修正左半区的异或和：去掉原来的 a[b]，加上新的 c
                L = L ^ a[b] ^ c;
                
                // 判断胜负：左区 vs 右区
                // 题目规则：值大的赢，相等左边赢。
                // 如果 L < R，说明左边输了。
                // 左边输了，右边整个栈(大小sz)会压在左边头上。
                if(L < R) res += sz;
            }
            else // 目标奶牛在右半区
            {
                res = self(self, mid + 1, r);
                
                // 修正右半区的异或和
                R = R ^ a[b] ^ c;
                
                // 如果 R <= L，说明右边输了（注意平局也是左边赢，所以右边输是 <=）
                // 右边输了，左边整个栈(大小sz)会压在右边头上。
                if(R <= L) res += sz;
            }
            
            return res;
        };
        
        // 从整个区间开始递归
        cout << fz(fz, 1, len) << endl;
    }
}

int main()
{
    IOS;
    int _ = 1;
    cin >> _;
    while (_--)
    {
        solve();
    }
    return 0;
}
```
# G. Mixing MEXes 

**题目链接：** [G. Mixing MEXes](https://codeforces.com/contest/1930/problem/G)  
## 题目大意

给你 $n$ 个数组 $a_1, a_2, \dots, a_n$。
你需要执行以下操作 **恰好一次**：
1. 选择一个数组 $a_i$ 和其中一个元素 $x = a_{i,j}$。
2. 选择另一个数组 $a_k$ ($k \neq i$)。
3. 从 $a_i$ 中移除 $x$，并将 $x$ 添加到 $a_k$ 的末尾。

操作的**价值**定义为操作后所有数组的 MEX 之和，即 $\sum_{m=1}^{n} \text{MEX}(a_m)$。
求所有可能的不同操作（三元组 $(i, j, k)$ 不同）所产生的价值之**和**。

> **MEX 定义：**
> **MEX(a)** 定义为数组中**不包含**的最小非负整数。
> 例如：`MEX([1, 2, 0, 5]) = 3`，`MEX([1, 2, 4, 9]) = 0`。

## 解题思路

这就要求我们计算所有情况下的 $\sum \text{MEX}$ 的总和。直接模拟每次操作的时间复杂度太高，我们需要使用**贡献法**来分别计算变化的量。

### 1. 初始状态总和
首先，不管怎么操作，大部分数组的 MEX 是不会变的。
假设不做任何操作，所有数组的 MEX 之和为 $S = \sum \text{MEX}(a_i)$。
总共有 $L = \sum |a_i|$ 个元素可选（即总共有 $L$ 种移出元素的方式）。
对于每一种移出方式，有 $n-1$ 个目标数组可以接受这个元素。
所以，总的操作数量是 $L \times (n-1)$。
**基准答案**：`ans = S * L * (n - 1)`。

接下来我们只需要计算操作对基准答案的**增量（或减量）**。

### 2. 移除元素的影响 (减法贡献)
当我们从 `a[i]` 中移除元素 `x` 时，只有当 `x < MEX(a[i])` 且 `x` 在 `a[i]` 中**只出现了一次**时，`a[i]` 的 MEX 才会减小。
- 减小的量：`MEX(a[i])` 会变成 `x`。所以减少了 `MEX(a[i]) - x`。
- 这种情况发生了 `n - 1` 次（因为有 `n - 1` 个目标数组 `a[k]`）。
- 更新：`ans -= (MEX(a[i]) - x) * (n - 1)`。

### 3. 添加元素的影响 (加法贡献)
当我们把元素 $x$ 添加到 $a_k$ 中时，只有当 $x == \text{MEX}(a_k)$ 时，$a_k$ 的 MEX 才会增加。
- 此时 $a_k$ 的 MEX 会从 $x$ 变成一个新的值 `nmex`（即填补了空缺后，下一个缺失的数）。
- 增加的量：`nmex - MEX(a_k)`。
- 这种情况发生的次数：等于**所有数组中等于 $\text{MEX}(a_k)$ 的元素总个数**。我们用一个全局计数器 `cnt` 来记录每个数字在所有数组中出现的总次数。
- 更新：`ans += (nmex - MEX(a_k)) * cnt[MEX(a_k)]`。

### 4. 算法流程
1. **预处理**：计算所有数组的初始 MEX，计算总和 $S$，并统计所有数字的出现次数 `cnt`。
2. **初始化答案**：`ans = S * len * (n - 1)`。
3. **减法修正**：遍历每个数组的每个元素，如果它是“关键元素”（唯一且小于当前 MEX），从答案中减去相应的差值。
4. **加法修正**：遍历每个数组，假设该数组作为接收方 $a_k$。如果此时放入的元素恰好是它的 `MEX`，计算新的 `MEX` 并加上增量。

## 复杂度分析

- **预处理**：需要遍历所有输入元素，时间复杂度为 `O(Σ|a_i|)`。
- **修正计算**：
  - 减法部分遍历所有元素，复杂度为线性。
  - 加法部分虽然有 `while` 循环寻找新的 MEX，但在排序后每个元素最多被访问常数次，均摊复杂度也是线性的。
- **总复杂度**：`O(Σ|a_i| * log(max_len))`。
  - 主要的时间开销在于对每个数组进行排序。
  - 在题目给定的 `Σ|a_i| <= 2 * 10^5` 数据范围内，该算法非常高效，可以通过。

## AC 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll; 
typedef vector<ll> vll;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define all(x) x.begin(), x.end()
#define endl '\n'

const int N = 1000010; 
int cnt[N]; // 用于统计全局每个数字出现的次数

void solve()
{
    int n;
    cin >> n;
    
    vector<vector<int>> a(n);
    vector<int> pmex(n);
    
    ll sum = 0; // 初始所有数组 MEX 之和
    ll len = 0; // 所有元素的总个数
    
    // 1. 读入数据并预处理
    rep(i, 0, n - 1)
    {
        int l;
        cin >> l;
        a[i].resize(l);
        len += l; 
        
        rep(j, 0, l - 1)
        {
            cin >> a[i][j];
            cnt[a[i][j]]++; // 全局计数
        }
        sort(all(a[i])); // 排序方便求 MEX
    }

    // 2. 计算初始 MEX
    rep(i, 0, n - 1)
    {
        int m = 0;
        for (int x : a[i])
        {
            if (x == m) m++;
            else if (x > m) break;
        }
        pmex[i] = m;
        sum += m;
    }

    // 3. 初始基准答案：假设 MEX 都不变
    // 总操作次数 = 总元素数 * (n-1) 个目标数组
    ll ans = sum * len * (n - 1);

    // 4. 处理移除元素导致的 MEX 减小
    rep(i, 0, n - 1)
    {
        int sz = a[i].size();
        rep(j, 0, sz - 1)
        {
            int x = a[i][j];
            
            // 检查 x 是否只出现了一次
            bool check = true;
            if (j > 0 && a[i][j - 1] == x) check = false;
            if (j < sz - 1 && a[i][j + 1] == x) check = false;

            // 如果 x 是唯一的，且 x < MEX，移除它会导致 MEX 降低为 x
            if (check && x < pmex[i])
            {
                // 每次操作都会少算 (pmex[i] - x)
                // 共有 n-1 个接收数组，所以减去 (n-1) 倍
                ans -= (ll)(pmex[i] - x) * (n - 1);
            }
        }
    }

    // 5. 处理添加元素导致的 MEX 增加
    rep(i, 0, n - 1)
    {
        int tag = pmex[i]; // 当前数组缺少的数
        ll num = cnt[tag]; // 全局有多少个这个数可以被移过来
        
        if (num > 0)
        {
            // 如果把 tag 移进来，MEX 会变成多少？
            int nmex = tag + 1;
            
            // 在有序数组中找下一个缺失的数
            auto it = upper_bound(all(a[i]), tag);
            int idx = it - a[i].begin();
            
            while (idx < a[i].size())
            {
                if (a[i][idx] == nmex)
                {
                    nmex++;
                    // 跳过重复的数字
                    while (idx < a[i].size() && a[i][idx] < nmex) idx++;
                }
                else
                {
                    break; 
                }
            }

            // 增加的贡献 = (新MEX - 旧MEX) * 来源数的个数
            ans += (ll)(nmex - pmex[i]) * num;
        }
    }

    cout << ans << endl;

    // 清空计数数组，为下一组数据做准备
    rep(i, 0, n - 1)
    {
        for (int x : a[i]) cnt[x]--;
    }
}

int main()
{
    IOS;
    int _ = 1;
    cin >> _;
    while (_--)
    {
        solve();
    }
    return 0;
}
```
#  H. BattleCows 2 题解 

**题目链接：** [H. BattleCows 2](https://codeforces.com/contest/1930/problem/H)


## 题目大意

Farmer John 举办了一场锦标赛，有 $n$ 头奶牛，技能值为 $a_i$。
比赛规则：
1. 队伍最前面的两头牛进行对战，技能值高的获胜（平局时前面的赢）。
2. **赢家**的技能值变为 $x+y$（两人技能之和），**输家**离开队伍。
3. 比赛重复直到只剩一头牛。

**作弊机制**：每头牛最多可以作弊 $k$ 次。作弊时，即使它输了，也会被判为获胜，技能值同样变为 $x+y$，原本的赢家离开队伍。

**问题**：对于每头奶牛 $i$，如果将它从原位置移出并插入到某个位置 $x$（其他牛相对顺序不变），使得它能利用最多 $k$ 次作弊成为最终唯一的赢家。求这样的“好位置” $x$ 有多少个？

## 解题思路

### 1. 胜利条件的转化
一头牛要赢得最终胜利，无论它怎么赢（靠实力还是作弊），每次胜利后它的技能值都会变成“对手技能值 + 自己当前技能值”。
这意味着，如果一头牛赢到了最后，它的最终技能值一定是**所有参赛牛的技能值之和**。
或者更准确地说，如果奶牛 $i$ 在某个位置 $x$，它前面所有牛的技能和记为 `pre`。
- 如果 $a_i > pre$，它可以凭实力赢下前面的所有牛，技能值变为 $a_i + pre$。
- 如果 $a_i \le pre$，它必须消耗一次作弊机会才能赢下这一轮（相当于赢下这“一堆”牛），技能值也变为 $a_i + pre$。

### 2. 核心观察：关键对手
并非每一头牛都需要我们单独判断输赢。
对于奶牛 $i$ 来说，只有那些**初始技能值特别大**的牛才是威胁。
具体的威胁判定标准是：如果某头牛 $j$ 的技能值 $a_j >$ (它前面所有牛的技能和)，那么这头牛 $j$ 就是一个**“强者”**。
我们把这些“强者”记录在列表 `q` 中。对于其他普通牛，它们技能值较小，会被前面的累积和吞噬，不会成为阻碍。

### 3. 计算“好位置”
对于每头奶牛 $i$，我们想知道它插在哪个位置能赢。
位置可以分为两类：
1.  **位置 $x \le$ 某个临界点**：在这个位置，奶牛 $i$ 可以先吃掉前面的所有牛（可能需要作弊），然后带着累积的巨大技能值去挑战后面的牛。
2.  **位置 $x >$ 临界点**：在这个位置，前面的某些“强者”已经成长得太大了，奶牛 $i$ 即使作弊也可能不够用。

我们用**前缀和**数组 `pre` 和**二分查找**来确定这个“临界点” `pos`：
- `pos` 是奶牛 $i$ 能够凭实力（或者只作弊一次）战胜的最大的前缀位置。
- 具体来说，如果奶牛 $i$ 初始值就很大，它能吞掉的前缀就更长；否则它只能吞掉较短的前缀。

### 4. 贪心判定 (calc 函数)
对于一个区间 $[L, R]$ 内的每一个位置，我们需要判断奶牛 $i$ 是否能赢。
这转化为：奶牛 $i$ 在成长过程中，遇到列表 `q` 中的那些“强者”时，是否还有足够的作弊次数 $k$。
- 遍历所有“强者” $(j, val)$。
- 如果 $j$ 在 $i$ 的前面且 $a_i$ 打不过 $j$（需要作弊），消耗 $k$。
- 如果 $j$ 在 $i$ 的后面且成长后的 $i$ 打不过 $j$，消耗 $k$。
- 如果 $k < 0$，说明这个位置不可行。
- 只有满足条件的区间长度才会计入答案。

## 复杂度分析

- **预处理**：计算前缀和并筛选“强者”列表 `q`，时间复杂度 `O(n)`。
- **查询**：对于每头牛，二分查找临界点 `O(log n)`，然后遍历 `q` 列表进行检查。
  - 虽然看起来是 `O(n * |q|)`，但由于技能值呈指数级增长，“强者”的数量 `|q|` 非常少（最多 `O(log(Sum))`，约为 60 个）。
- **总复杂度**：`O(n * log(TotalSum))`。
  在 `2 * 10^5` 范围内非常快。

## AC 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

// 通用模板部分
typedef long long ll;
typedef vector<ll> vll;
typedef pair<ll, ll> PLL;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define all(x) x.begin(), x.end()
#define endl '\n'

// 更新最大值函数
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }

void solve()
{
    ll n, k;
    cin >> n >> k;
    
    // a: 技能值, pre: 前缀和
    vll a(n + 1, 0), pre(n + 1, 0);
    vector<PLL> q; // 存储“强者”：{下标, 需要的技能阈值}
    
    rep(i, 1, n)
    {
        cin >> a[i];
        pre[i] = pre[i - 1] + a[i];
        
        // 如果当前牛比前面所有牛的总和还大，它是一个潜在的威胁（强者）
        // 记录它，因为它可能会迫使别人消耗作弊次数
        if (a[i] > pre[i - 1])
        {
            q.push_back({i, a[i] - pre[i - 1]});
        }
    }
    
    // 逆序处理，方便后续遍历
    reverse(all(q));
    
    // 核心判定函数：在区间 [l, r] 内，奶牛 pos 是否有足够的作弊次数 cnt
    auto calc = [&](ll l, ll r, ll pos, ll cnt) -> ll
    {
        if (cnt < 0) return 0;
        
        // 遍历所有“强者”，检查是否会消耗作弊次数
        for (auto p : q)
        {
            auto [x, y] = p; // x: 强者下标, y: 阈值
            if (x != pos)
            {
                // 如果强者 x 在 pos 后面，或者 pos 打不过强者 x 的阈值 y
                // 这里的逻辑是：如果 x 是一个威胁，我们需要消耗一次作弊机会
                // (x > pos) 表示 x 在 pos 后面，如果不作弊可能会输
                // (a[pos] < y) 表示 pos 即使在前面，初始值太小也打不过 x
                if (x > pos || a[pos] < y)
                    cnt--;
                
                // 如果作弊次数不够了，说明当前的 l 位置不可行
                // 我们需要把 l 往后推，尝试缩短区间
                if (cnt < 0)
                    cmax(l, x + (x < pos));
            }
        }
        // 返回有效区间的长度
        return max((ll)0, r - l + 1);
    };

    // 二分查找函数：找到第一个前缀和 >= x 的位置
    // 用于确定奶牛 i 能凭实力（或一次作弊）吞噬到的最远边界
    auto f = [&](ll x) -> ll
    {
        ll l = 0, r = n + 1;
        while (l + 1 < r)
        {
            ll mid = l + (r - l) / 2;
            if (pre[mid] >= x)
                r = mid;
            else
                l = mid;
        }
        return r;
    };

    rep(i, 1, n)
    {
        ll pos = 0;
        // 分情况确定临界点 pos
        if (pre[i - 1] >= a[i])
        {
            // 情况1：a[i] 较小，打不过前面的前缀和
            // 它需要消耗作弊次数才能赢下第一场
            // pos 是它能成长到的位置
            pos = f(a[i]);
        }
        else
        {
            // 情况2：a[i] 很大，能直接吃掉前面的前缀
            // 它的技能会翻倍增长，pos 会更远
            pos = f(2 * a[i]) - 1;
        }
        
        if (pos > n) pos = n;
        
        // 计算两段区间的贡献：
        // 1. [1, pos]: 在这个范围内，它可能只需要 k 次作弊
        // 2. [pos+1, n]: 在这个范围内，它可能需要额外的一次作弊（因为初始就落后了），所以是 k-1
        ll ans = calc(1, pos, i, k) + calc(pos + 1, n, i, k - 1);
        cout << ans << " ";
    }
    cout << endl;
}

int main()
{
    IOS;
    int _ = 1;
    cin >> _;
    while (_--)
    {
        solve();
    }
    return 0;
}
```