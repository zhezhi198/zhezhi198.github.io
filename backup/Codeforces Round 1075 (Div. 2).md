[Codeforces Round 1075 (Div. 2)](https://codeforces.com/contest/2189)
# A. 带有数字的表格 

| 每次测试时间限制 | 每次测试内存限制 | 输入 | 输出 |
| :--- | :--- | :--- | :--- |
| 1 秒 | 256 MB | 标准输入 | 标准输出 |

## 题目描述

Peter 画了一张大小为 $h \times l$ 的表格，里面初始填满了零。我们将其行从上到下编号为 $1$ 到 $h$，列从左到右编号为 $1$ 到 $l$。

Ned 提出了一个数字数组 $a_1, a_2, \dots, a_n$，并想要修改该表格。

Ned 的操作规则如下：
1. 从他的数组中选择 $2k$ 个数字（其中 $2k \le n$）。
2. 将这 $2k$ 个数字分成 $k$ 对。
3. 对于每一对 $(x, y)$，他获取位于行 $x$ 和列 $y$ 的单元格，并将 $1$ 添加到该单元格中的数字。
4. 如果这样的单元格不存在（即 $x > h$ 或 $y > l$），则该对对表格不执行任何操作。

Peter 支持 Ned 的倡议，并要求他最大化表中数字的总和。请帮助 Ned 计算他能达到的最大总和是多少。

## 输入格式

每个测试包含多个测试用例。第一行包含测试用例的数量 $t$ ($1 \le t \le 500$)。

测试用例的描述如下：
* 每个测试用例的第一行包含三个整数 $n, h, l$ ($2 \le n \le 100$, $1 \le h, l \le 1000$) —— 分别是数组的大小、表格的高度和表格的宽度。
* 每个测试用例的第二行包含 $n$ 个数字 $a_1, a_2, \dots, a_n$ ($1 \le a_i \le 1000$) —— 数组本身。

## 输出格式

对于每个测试用例，输出表中数字的最大可能总和。

## 样例 

### 输入
```text
7
2 1 1
1 1
5 2 2
1 2 2 3 2
8 4 2
7 2 2 2 3 4 4 2
7 3 6
10 4 1 3 5 4 6
2 4 4
5 5
7 6 3
10 4 1 3 5 4 6
4 1 1
1 1 1 1
```

### 输出
```text
1
2
3
2
0
2
2
```
>思路:由于GitHub的markdown格式太难调了，有时候写题解就去了一下午，有些不方便的证明我就写在纸上了，参考照片和代码。

![Image](https://github.com/user-attachments/assets/194a923b-5d55-4a00-bfd8-640ca16fe171)

AC代码:
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
    ll n, h, l;
    cin >> n >> h >> l;
    ll cnt1 = 0, cnt2 = 0, cnt3 = 0;
    rep(i, 1, n)
    {
        ll x;
        cin >> x;
        if (x <= h)
            cnt1++;
        if (x <= l)
            cnt2++;
        if (x <= h || x <= l)
            cnt3++;
    }
    cout << min({cnt1, cnt2, cnt3 / 2}) << endl;
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

# B. 青蛙的诅咒

| 每次测试时间限制 | 每次测试内存限制 | 输入 | 输出 |
| :--- | :--- | :--- | :--- |
| 1 秒 | 256 MB | 标准输入 | 标准输出 |

## 题目描述

在无限数轴上的点 $0$ 处，坐着一只青蛙。经过多年的冥想，青蛙已经掌握了 $n$ 种独特类型的魔法跳跃。

第 $i$ 种跳跃允许其向前跳转不超过 $a_i$ 个单位。换句话说，如果它位于整数点 $k$，则跳转后它可以降落在从 $k$ 到 $k+a_i$ 的任何整数点。

但魔法总是有代价的；它已经被诅咒了。在每次尝试第 $b_i$ 次使用第 $i$ 种跳跃类型之前（即在使用第 $i$ 种跳跃的第 $b_i$ 次、第 $2b_i$ 次、第 $3b_i$ 次……之前），青蛙都会回滚 $c_i$ 个单位！

换句话说，如果它在点 $k$ 且触发了回滚，它首先会发现自己在点 $k-c_i$，跳转后，它可以降落在从 $k-c_i$ 到 $k-c_i+a_i$ 的任何整数点。

青蛙的目标是到达数字为 $x$ 的点。请帮助青蛙找出它在到达目标的过程中必须忍受的**最少回滚次数**，或者确定它无法到达点 $x$。

## 输入格式

每个测试包含多个测试用例。第一行包含测试用例的数量 $t$ ($1 \le t \le 10^4$)。

测试用例的描述如下：
* 每个测试用例的第一行包含两个整数 $n$ 和 $x$ ($1 \le n \le 10^5$, $1 \le x \le 10^{18}$) —— 青蛙可以进行的跳跃类型数量及其最终目标。
* 接下来 $n$ 行，每行包含 3 个整数 $a_i, b_i, c_i$ ($1 \le a_i, b_i, c_i \le 10^6$) —— 描述第 $i$ 种跳跃类型的参数。

保证所有测试用例的 $n$ 之和不超过 $10^5$。

## 输出格式

对于每个测试用例，如果青蛙可以到达点 $x$，请输出它为此必须忍受的最小回滚次数。如果无法到达点 $x$，则输出 $-1$。

## 样例

### 输入
```text
6
1 1
3 3 3
1 7
4 2 5
2 4
1 2 3
2 2 4
5 8
12 1 11
10 1 4
1 1 3
1 2 5
2 1 7
1 1000000000000000000
1000000 4 654321
1 10
2 2 1
```
### 输出
```text
0
1
-1
2
298892990032
3
```
>思路:贪心，我们可以计算所有技能恰好都不回退时能走far这么远，记录一个mx，为一个周期(恰好回退时走了多远)走的最大值，如果我们算出far和mx后呢，如果far>目标值，意味着我们不用回退任何一次就能达到目标，如果达不到，mx<0 那么将无法达到了，mx>0，那么剩下的路程看要多少个走多少个mx能覆盖到(上取整),
AC代码：
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
    ll n, x;
    cin >> n >> x;
    ll far = 0, mx = -INF;
    rep(i, 1, n)
    {
        ll a, b, c;
        cin >> a >> b >> c;
        far += (b - 1) * a;
        ll d = a * b - c;
        cmax(mx, d);
    }
    if (far >= x)
    {
        cout << 0 << endl;
        return;
    }
    if (mx <= 0)
    {
        cout << -1 << endl;
        return;
    }
    cout << ((x - far) + mx - 1) / mx << endl;
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
# C1. 异或便利 (简易版)
| 每次测试时间限制 | 每次测试内存限制 | 输入 | 输出 |
| :--- | :--- | :--- | :--- |
| 2 秒 | 256 MB | 标准输入 | 标准输出 |

## 题目描述

这是问题的**简单版本**。版本之间的区别在于，在此版本中 $2 \le i \le n-1$。请注意，困难版本的正确解决方案不一定是简单版本的正确解决方案。

给定一个自然数 $n$。请找到一个长度为 $n$ 的排列 $p$，使得对于每个 $i$ ($2 \le i \le n-1$)，都存在一个 $j$ ($i \le j \le n$) 满足：
$$p_i = p_j \oplus i$$

可以证明，在问题的约束下，至少存在一种合适的排列 $p$。

* **注 1：** 长度为 $n$ 的排列是一个数组，由从 $1$ 到 $n$ 的 $n$ 个不同整数以任意顺序组成。例如，$ [2,3,1,5,4] $ 是一个排列，但 $[1,2,2]$ 不是排列（$2$ 在数组中出现两次），$[1,3,4]$ 也不是排列（$n=3$ 但数组中有 $4$）。
* **注 2：** $\oplus$ 表示按位异或运算。

## 输入格式

每个测试包含多个测试用例。第一行包含测试用例的数量 $t$ ($1 \le t \le 10^4$)。

测试用例的描述如下：
* 每个测试用例的唯一行包含一个整数 $n$ ($3 \le n \le 2 \cdot 10^5$) —— 排列的长度。

保证所有测试用例的 $n$ 之和不超过 $2 \cdot 10^5$。

## 输出格式

对于每个测试用例，输出 $n$ 个整数 $p_1, p_2, \dots, p_n$ —— 即你找到的排列 $p$。

如果有多个解决方案，您可以输出其中任何一个。

## 样例

### 输入
```text
2
3
6
```
### 输出
```text
2 1 3
3 6 2 5 1 4
```
>赛时思路:我在第一次写的时候想的是最朴素的解法，就给最后一个位置放1，后面填的数用数组存着，再开st数组标记哪些数已经被用过了。就从后往前一路填，当然这样很容易tle，不过我加上了一些优化居然过了，可能是数据水了，再加上这场不会被hack，所有...总之这种方法不可取
>思路：
其实核心思路和最初的朴素解法是一致的。我们需要满足题目要求的下标范围是 $[2, n-1]$。

我们的策略是：**先固定最后一个位置为 1**，即令 $p_n = 1$。

### 为什么选择填 1？
我们利用 $i \oplus 1$ 的性质，结果分为两种情况：
* 如果 $i$ 是奇数，则得到 $i-1$；
* 如果 $i$ 是偶数，则得到 $i+1$。

从 $2$ 到 $n-1$，下标不断进行奇偶交替。我们发现 $2^ 1 = 3$，$3 ^ 1 = 2$。在连续下标的基础上，$i ^ 1$ 本质上是**奇偶位值的互换**。因此，中间部分得到的就是一段连续互换的结果，我们可以直接根据下标求出对应的值。

### 下标为 1 的位置该填什么？
下标 $1$ 不必满足异或条件的限制，唯一的限制是必须构成**全排列**（即不能使用后面已经填过的数）。通过观察 $n$ 的奇偶性，我们发现：

* **若 $n$ 是奇数**：下标 $1$ 的位置填 $n-1$。
    * *原因*：此时 $n-1$ 是偶数，但在计算中它和 $n$ 发生了互换（即 $p_{n-1} = (n-1) \oplus 1 = n$），导致数值 $n-1$ 没有被使用，所以填入 $p_1$ 即可。
* **若 $n$ 是偶数**：下标 $1$ 的位置填 $n$。
    * *原因*：同理，此时数值 $n$ 是剩下的未被使用的数。

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
    vll p(n + 1, 0);
    p[n] = 1;
    if (n & 1)
    {
        p[1] = n - 1;
    }
    else
    {
        p[1] = n;
    }
    rep(i, 2, n - 1)
    {
        p[i] = 1 ^ i;
    }
    rep(i, 1, n) cout << p[i] << " ";
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
# C2. 异或便利 (困难版) 

| 每次测试时间限制 | 每次测试内存限制 | 输入 | 输出 |
| :--- | :--- | :--- | :--- |
| 2 秒 | 256 MB | 标准输入 | 标准输出 |

## 题目描述

这是问题的**困难版本**。版本之间的区别在于，在此版本中 $1 \le i \le n-1$。请注意，困难版本的正确解决方案不一定是简单版本的正确解决方案。

给定一个正整数 $n$。请找到一个长度为 $n$ 的排列 $p$，使得对于每个 $i$ ($1 \le i \le n-1$)，都存在一个 $j$ ($i \le j \le n$) 满足：
$$p_i = p_j \oplus i$$

或者确定不存在这样的排列。

* **注 1：** 长度为 $n$ 的排列是一个数组，由从 $1$ 到 $n$ 的 $n$ 个不同整数以任意顺序组成。例如，$[2,3,1,5,4]$ 是一个排列，但 $[1,2,2]$ 不是排列（$2$ 在数组中出现两次），$[1,3,4]$ 也不是排列（$n=3$ 但数组中有 $4$）。
* **注 2：** $\oplus$ 表示按位异或运算。

## 输入格式

每个测试包含多个测试用例。第一行包含测试用例的数量 $t$ ($1 \le t \le 10^4$)。

测试用例的描述如下：
* 每个测试用例的唯一行包含一个正整数 $n$ ($3 \le n \le 2 \cdot 10^5$) —— 排列的长度。

保证所有测试用例的 $n$ 之和不超过 $2 \cdot 10^5$。

## 输出格式

对于每个测试用例，如果存在合适的排列，则输出 $n$ 个整数 $p_1, p_2, \dots, p_n$ —— 即你找到的排列 $p$。否则，输出 $-1$。

如果存在多个解，则输出其中任何一个。

## 样例

### 输入
```text
2
3
4
```
### 输出
```text
2 1 3
-1
```
>思路:
## 解题思路与证明

我们通过固定 $p_n = 1$ 来简化问题，对于所有 $i \in [2, n-1]$，只要令 $p_i = p_n \oplus i = 1 \oplus i$，即可始终选择 $j = n$ 来满足题目条件 $p_i = p_j \oplus i$。

利用 $x \oplus 1$ 的性质（相邻的偶奇数互换，如 $2 \leftrightarrow 3$），该构造本质上是对区间内的数进行两两交换：

* **若 $n$ 为奇数**：区间内的最大偶数 $n-1$ 会被映射为 $n$（因为 $(n-1) \oplus 1 = n$），导致数值 $n-1$ 未被使用，因此令 $p_1 = n-1$。
* **若 $n$ 为偶数**：区间 $[2, n-1]$ 内的数恰好两两配对闭环互换，剩余最大值 $n$ 未被使用，因此令 $p_1 = n$。

此方案保证了每个 $i$ 都能找到 $j=n$ 满足等式，且所有填入的数恰好构成 $1$ 到 $n$ 的全排列。

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
    if (n - lowbit(n) == 0)
    {
        cout << -1 << endl;
        return;
    }
    vll p(n + 1, 0);
    if (n & 1)
    {
        p[n] = 1;
        p[1] = n - 1;
        rep(i, 2, n - 1)
        {
            p[i] = 1 ^ i;
        }
    }
    else
    {
        p[n] = 1;
        p[1] = lowbit(n) ^ 1;
        rep(i, 2, n - 1)
        {
            if (i == lowbit(n))
            {
                p[i] = n;
            }
            else
            {
                p[i] = 1 ^ i;
            }
        }
    }
    rep(i, 1, n) cout << p[i] << " ";
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
# D1. 小字符串 (简单版)

| 每次测试时间限制 | 每次测试内存限制 | 输入 | 输出 |
| :--- | :--- | :--- | :--- |
| 2 秒 | 256 MB | 标准输入 | 标准输出 |

## 题目描述

这是问题的**简单版本**。版本之间的区别在于，在此版本中保证字符串 $s$ 不包含字符 `?`。

对于由字符 `0` 和 `1` 组成的字符串 $w_1w_2\dots w_n$，我们将 $f(w)$ 定义为数组 $[0,1,\dots,n-1]$ 的排列 $p_1,p_2,\dots,p_n$ 的数量，使得对于从 $1$ 到 $n$ 的所有 $i$，满足以下条件：

* 如果 $w_i=1$，则存在 $1 \le l \le r \le n$，使得 $\text{mex}([p_l,p_{l+1},\dots,p_r])=i$。
* 如果 $w_i=0$，则**不存在** $1 \le l \le r \le n$，使得 $\text{mex}([p_l,p_{l+1},\dots,p_r])=i$。

给定一个由字符 `0` 和 `1` 组成的字符串 $s_1s_2\dots s_n$ 以及一个正整数 $c$。注意在此版本的问题中，字符串 $s$ 不包含 `?`。考虑所有可以通过将 $s$ 中的所有 `?` 字符替换为 `0` 和 `1` 获得的字符串 $w$（在此版本中，只有 $w=s$ 这一种情况）。

请在所有此类字符串 $w$ 中，找到 $f(w)$ 不能被 $c$ 整除的最小值，或者确定不存在这样的字符串 $w$。由于答案可能很大，请输出其对 $10^9+7$ 取模后的结果。

* **注：** 整数集合 $c_1,c_2,\dots,c_k$ 的最小排除值（MEX）定义为集合 $c$ 中未出现的最小非负整数 $x$。

## 输入格式

每个测试包含多个测试用例。第一行包含测试用例的数量 $t$ ($1 \le t \le 10^4$)。

测试用例的描述如下：
* 每个测试用例的第一行包含两个整数 $n$ 和 $c$ ($3 \le n \le 2 \cdot 10^5, 1 \le c \le 10^9$) —— 字符串的长度和限制函数值的数字。
* 每个测试用例的第二行包含一个长度为 $n$ 的字符串，由字符 `0` 和 `1` 组成 —— 即字符串 $s$。

保证所有测试用例的 $n$ 之和不超过 $2 \cdot 10^5$。

## 输出格式

对于每个测试用例，如果存在这样的字符串 $w$（可以通过替换 $s$ 中的 `?` 得到），使得 $f(w)$ 不能被 $c$ 整除，则输出所有此类字符串 $w$ 中 $f(w)$ 的最小值。答案应对 $10^9+7$ 取模。

如果不存在这样的字符串，则输出 $-1$。

## 样例

### 输入
```text
9
3 3
001
3 1
111
4 100
1001
6 100
111001
6 100
111101
5 8
10001
4 100
1110
21 123456789
111000111000111000111
3 4
101
```
### 输出
```text
-1
-1
4
96
64
12
-1
336892528
2
```
>思路:其实可以看成0>n-1这个在不断的插数，如果si=='1‘我们可以插在数字区间的左边或者右边，贡献为2，如果si==‘0’我们要从前面的数字区间插入以破坏连续区间构成的mex值贡献为i，我们默认字符串从0开始。注意不要被c恰好整除
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
    ll n, c;
    cin >> n >> c;
    string s;
    cin >> s;
    if (s.back() == '0')
    {
        cout << -1 << endl;
        return;
    }
    ll ans = 1, res = 1;
    rep(i, 0, n - 2)
    {
        if (s[i] == '1')
        {
            ans = (ans * 2) % Md7;
            res = (res * 2) % c;
        }
        else
        {
            ans = (ans * i) % Md7;
            res = (res * i) % c;
        }
    }
    if (res == 0)
    {
        cout << -1 << endl;
    }
    else
    {
        cout << ans << endl;
    }
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

<img width="1295" height="410" alt="Image" src="https://github.com/user-attachments/assets/56152a6b-0586-46f8-b7ce-2e4f48c854c5" />

<img width="1311" height="291" alt="Image" src="https://github.com/user-attachments/assets/daa79701-c65d-443f-84aa-3f30ca580edd" />

```
D2也差不多，给代码算了，思路差不多，只是判断整除麻烦.
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
    ll n, c;
    string s;
    cin >> n >> c >> s;
    vll pos;
    if (s[0] == '?')
    {
        s[0] = '1';
    }
    if (s[0] != '1')
    {
        cout << -1 << endl;
        return;
    }
    if (s[n - 1] == '?')
    {
        s[n - 1] = '1';
    }
    if (s[n - 1] != '1')
    {
        cout << -1 << endl;
        return;
    }
    ll w = 2;
    c /= gcd(c, (ll)2);
    rep(i, 1, n - 2)
    {
        if (s[i] == '0')
        {
            c /= gcd(c, i);
            w = w * i % Md7;
        }
        else if (s[i] == '1')
        {
            c /= gcd(c, (ll)2);
            w = w * 2 % Md7;
        }
        else
        {
            if (i == 1)
                continue;
            if (i % 2 == 0)
            {
                c /= gcd(c, (ll)2);
                w = w * 2 % Md7;
            }
            else
            {
                pos.push_back(i);
            }
        }
    }
    if (c == 1)
    {
        cout << -1 << endl;
        return;
    }
    ll m = pos.size();
    ll cnt = 0;
    while (c % 2 == 0)
    {
        c /= 2;
        cnt++;
    }
    if (c != 1)
    {
        rep(i, 0, m - 1)
        {
            w = w * 2 % Md7;
        }
        cout << w << endl;
        return;
    }
    cnt = min(cnt - 1, m);
    rep(i, 0, m - cnt - 1) w = w * pos[i] % Md7;
    rep(i, 0, cnt - 1) w = w * 2 % Md7;
    cout << w << endl;
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

