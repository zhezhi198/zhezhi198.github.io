[比赛](https://codeforces.com/contest/2184)
# A. Social Experiment 

## 题目大意

现在有 $n$ 个人要参加一个大型社会实验。规则如下：

1.  **必须组队**：这 $n$ 个人必须全部分配到小队里，每个小队的人数只能是 **2人** 或者 **3人**（不能有落单的，也不能有其他人数の队）。
2.  **选边站**：组好队后，每个小队必须在两个“文明”阵营中选一个加入（比如阵营 A 和阵营 B）。

现在的目标是：通过合理的分组和选边，让这两个阵营的**总人数差值最小**。请问这个最小的差值是多少？

---

## 输入格式

- 第一行包含一个整数 $t$ ($1 \le t \le 10^4$)，表示测试数据的组数。
- 接下来 $t$ 行，每行包含一个整数 $n$ ($2 \le n \le 10^4$)，表示参与实验的总人数。

## 输出格式

- 对于每组数据，输出一个整数，表示两个阵营人数可能的**最小差值**。

---

## 样例

### Input
```text
3
2
5
12
```
### Output
```text
2
1
0
```
>A比较简单直接给代码
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
template <typename T>
struct BIT1
{
    int n;
    vector<T> tr;
    BIT1(int n) : n(n), tr(n + 1) {}
    void add(int x, T v)
    {
        for (; x <= n; x += x & -x)
            tr[x] += v;
    }
    T sum(int x)
    {
        T r = 0;
        for (; x; x -= x & -x)
            r += tr[x];
        return r;
    }
    T range(int l, int r) { return sum(r) - sum(l - 1); }
};
template <typename T>
struct BIT2
{
    int n, m;
    vector<vector<T>> t1, t2, t3, t4;
    BIT2(int n_ = 0, int m_ = 0) { init(n_, m_); }
    void init(int n_, int m_)
    {
        n = n_;
        m = m_;
        t1.assign(n + 1, vector<T>(m + 1, T{}));
        t2.assign(n + 1, vector<T>(m + 1, T{}));
        t3.assign(n + 1, vector<T>(m + 1, T{}));
        t4.assign(n + 1, vector<T>(m + 1, T{}));
    }
    void _add(int x, int y, const T &v)
    {
        for (int i = x; i <= n; i += i & -i)
            for (int j = y; j <= m; j += j & -j)
            {
                t1[i][j] += v;
                t2[i][j] += v * x;
                t3[i][j] += v * y;
                t4[i][j] += v * x * y;
            }
    }
    void rangeAdd(int x1, int y1, int x2, int y2, const T &v)
    {
        _add(x1, y1, v);
        _add(x1, y2 + 1, -v);
        _add(x2 + 1, y1, -v);
        _add(x2 + 1, y2 + 1, v);
    }
    T prefixSum(int x, int y)
    {
        T r{};
        for (int i = x; i > 0; i -= i & -i)
            for (int j = y; j > 0; j -= j & -j)
                r += t1[i][j] * (x + 1) * (y + 1) - t2[i][j] * (y + 1) - t3[i][j] * (x + 1) + t4[i][j];
        return r;
    }
    T rangeSum(int x1, int y1, int x2, int y2)
    {
        if (x1 > x2 || y1 > y2)
            return T{};
        return prefixSum(x2, y2) - prefixSum(x1 - 1, y2) - prefixSum(x2, y1 - 1) + prefixSum(x1 - 1, y1 - 1);
    }
};
struct Random
{
    mt19937_64 rng;
    Random() : rng(chrono::steady_clock::now().time_since_epoch().count()) {}
    ull rand_ull(ull max_val = -1) { return rng() % (max_val + 1); }
    ll rand_ll(ll l, ll r) { return uniform_int_distribution<ll>(l, r)(rng); }
    int rand_int(int l, int r) { return uniform_int_distribution<int>(l, r)(rng); }
    double rand_db(double l, double r) { return uniform_real_distribution<double>(l, r)(rng); }
    bool rand_bool(double p = 0.5) { return bernoulli_distribution(p)(rng); }
    template <typename T>
    void shuffle(vector<T> &v) { std::shuffle(v.begin(), v.end(), rng); }
};
ll qmi(ll a, ll b, ll p)
{
    ll res = 1 % p;
    a %= p;
    while (b)
    {
        if (b & 1)
            res = res * a % p;
        a = a * a % p;
        b >>= 1;
    }
    return res;
}
/*

*/

void solve()
{
    ll n;
    cin >> n;
    if (n < 4)
    {
        if (n > 1)
        {
            cout << n << endl;
        }
    }
    else
    {
        cout << n % 2 << endl;
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
```

# B. Hourglass 

## 题目大意

瓦迪姆（Vadim）手里有一个沙漏。这个沙漏里的沙子完全漏完需要 **$s$** 分钟。

游戏规则如下：
1.  **开始**：一开始沙子都在上面，开始计时，沙子开始往下漏。
2.  **翻转**：瓦迪姆是个强迫症，每隔固定的 **$k$** 分钟（即第 $k, 2k, 3k...$ 分钟），他都会瞬间把沙漏倒过来。
    * **情况A（沙子没漏完）**：直接倒过来，原来漏下去的沙子变成了上面的沙子，开始往下漏。
    * **情况B（沙子早就漏完了）**：沙漏已经空了一段时间了，倒过来后，原本下面所有的沙子（也就是满的 $s$ 分钟量的沙子）到了上面，开始往下漏。
3.  **结束**：瓦迪姆在第 **$m$** 分钟时必须离开去办事。此时他**停止翻转**（如果在第 $m$ 分钟正好该翻转，他也会翻转完再走）。

**问题是**：当瓦迪姆在第 $m$ 分钟离开的那一瞬间，沙漏上方**还剩下**多少分钟的沙子没有漏完？

---

## Input 

- 第一行包含一个整数 $t$ ($1 \le t \le 10^4$)，表示测试数据的组数。
- 接下来 $t$ 行，每行包含三个整数：
  - $s$：沙漏的总容量（漏完需要的时间）。
  - $k$：瓦迪姆翻转沙漏的间隔时间。
  - $m$：瓦迪姆离开的时间（总时长）。
- 数据范围：1 ≤ s, k, m ≤ 10^9。

## Output 

- 对于每一组测试数据，输出一个整数：瓦迪姆离开后，沙子还能继续漏多少分钟（即离开瞬间上方剩余的沙量）。

---

## Example 

### Input
```text
6
8 8 12
5 10 17
12 2 3
16 7 7
1 1 10
2 60 15
```
### Output
```text
4
0
1
7
1
0
```
## 解题思路

这道题的数据范围非常大（m 高达 $10^9$），所以**绝对不能**用循环一分钟一分钟地模拟沙漏流动，否则会超时（TLE）。我们需要通过数学规律直接计算出结果。

解题的关键在于对比 **沙漏容量 $s$** 和 **翻转间隔 $k$** 的大小关系，分两种情况讨论：

### 1. 情况一：沙漏容量小，翻转间隔长 ($s \le k$)

想象你有一个很小的杯子，但很久才倒一次水。
* **现象**：在下一次翻转之前，沙漏里的沙子早就漏光了。
* **规律**：这意味着每次翻转的瞬间，沙漏上方都是空的，下方是满的。**只要一翻转，上方立刻重置为满状态 ($s$)**。
* **计算逻辑**：
    1.  不管中间翻了多少次，我们只关心最后一次翻转后过了多久。计算 `res = m % k`。
    2.  如果 `res == 0`，说明正好刚翻完就走了，上方是满的，答案是 **$s$**。
    3.  如果 `res > 0`，说明翻转后已经漏了 `res` 分钟：
        * 如果漏的时间超过了容量 (`res >= s`)，说明漏光了，答案是 **0**。
        * 否则，剩下的就是 **$s - res$**。

### 2. 情况二：沙漏容量大，翻转间隔短 (s > k)

想象你有一个巨大的桶，但手速很快，不停地翻转。

* **现象**：沙子根本来不及漏完，就被你翻回去了。这会导致沙漏里的沙子在两个状态之间“反复横跳”。
* **规律（循环节）**：
    * **初始状态（第0轮）**：上方有 $s$。
    * **第1次翻转后（奇数轮）**：刚才漏下去的 $k$ 变成了上方，开始漏。
    * **第2次翻转后（偶数轮）**：下方原本剩下的加上刚才接住的，又变回了 $s$。
    * **结论**：
        * **偶数次**翻转后，该阶段以 $s$ 开局。
        * **奇数次**翻转后，该阶段以 $k$ 开局。
* **计算逻辑**：
    1. 算出总共翻转了多少次：`cnt = m / k`。
    2. 算出最后一次翻转后过了多久：`res = m % k`。
    3. 判断 `cnt` 的奇偶性：
        * **奇数**：初始量是 $k$。答案是 **$k - res$** （因为 s > k，所以 $k$ 分钟内沙子肯定够漏，只需直接相减）。
        * **偶数**：初始量是 $s$。答案是 **$s - res$** （同理，因为 k < s，肯定够漏）。

---
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
template <typename T>
struct BIT1
{
    int n;
    vector<T> tr;
    BIT1(int n) : n(n), tr(n + 1) {}
    void add(int x, T v)
    {
        for (; x <= n; x += x & -x)
            tr[x] += v;
    }
    T sum(int x)
    {
        T r = 0;
        for (; x; x -= x & -x)
            r += tr[x];
        return r;
    }
    T range(int l, int r) { return sum(r) - sum(l - 1); }
};
template <typename T>
struct BIT2
{
    int n, m;
    vector<vector<T>> t1, t2, t3, t4;
    BIT2(int n_ = 0, int m_ = 0) { init(n_, m_); }
    void init(int n_, int m_)
    {
        n = n_;
        m = m_;
        t1.assign(n + 1, vector<T>(m + 1, T{}));
        t2.assign(n + 1, vector<T>(m + 1, T{}));
        t3.assign(n + 1, vector<T>(m + 1, T{}));
        t4.assign(n + 1, vector<T>(m + 1, T{}));
    }
    void _add(int x, int y, const T &v)
    {
        for (int i = x; i <= n; i += i & -i)
            for (int j = y; j <= m; j += j & -j)
            {
                t1[i][j] += v;
                t2[i][j] += v * x;
                t3[i][j] += v * y;
                t4[i][j] += v * x * y;
            }
    }
    void rangeAdd(int x1, int y1, int x2, int y2, const T &v)
    {
        _add(x1, y1, v);
        _add(x1, y2 + 1, -v);
        _add(x2 + 1, y1, -v);
        _add(x2 + 1, y2 + 1, v);
    }
    T prefixSum(int x, int y)
    {
        T r{};
        for (int i = x; i > 0; i -= i & -i)
            for (int j = y; j > 0; j -= j & -j)
                r += t1[i][j] * (x + 1) * (y + 1) - t2[i][j] * (y + 1) - t3[i][j] * (x + 1) + t4[i][j];
        return r;
    }
    T rangeSum(int x1, int y1, int x2, int y2)
    {
        if (x1 > x2 || y1 > y2)
            return T{};
        return prefixSum(x2, y2) - prefixSum(x1 - 1, y2) - prefixSum(x2, y1 - 1) + prefixSum(x1 - 1, y1 - 1);
    }
};
struct Random
{
    mt19937_64 rng;
    Random() : rng(chrono::steady_clock::now().time_since_epoch().count()) {}
    ull rand_ull(ull max_val = -1) { return rng() % (max_val + 1); }
    ll rand_ll(ll l, ll r) { return uniform_int_distribution<ll>(l, r)(rng); }
    int rand_int(int l, int r) { return uniform_int_distribution<int>(l, r)(rng); }
    double rand_db(double l, double r) { return uniform_real_distribution<double>(l, r)(rng); }
    bool rand_bool(double p = 0.5) { return bernoulli_distribution(p)(rng); }
    template <typename T>
    void shuffle(vector<T> &v) { std::shuffle(v.begin(), v.end(), rng); }
};
ll qmi(ll a, ll b, ll p)
{
    ll res = 1 % p;
    a %= p;
    while (b)
    {
        if (b & 1)
            res = res * a % p;
        a = a * a % p;
        b >>= 1;
    }
    return res;
}
/*

*/

void solve()
{
    ll s, k, m;
    cin >> s >> k >> m;
    if (s <= k)
    {
        ll res = m % k;
        if (res == 0)
        {
            cout << s << endl;
        }
        else
        {
            if (res >= s)
            {
                cout << 0 << endl;
            }
            else
            {
                cout << s - res << endl;
            }
        }
    }
    else
    {
        ll cnt = m / k;
        ll a1 = k, b1 = s - k; // 从上往下漏
        ll a2 = s, b2 = 0;
        ll res = m % k;
        if (cnt & 1)
        {
            if (a1 >= res)
            {
                cout << a1 - res << endl;
            }
            else
            {
                cout << 0 << endl;
            }
        }
        else
        {
            if (a2 >= res)
            {
                cout << a2 - res << endl;
            }
            else
            {
                cout << 0 << endl;
            }
        }
    }
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
# C. Huge Pile 

## 题目大意

安德烈（Andrei）手里原本有一大堆苹果，数量为 **n** 个。

他可以对苹果堆进行“分裂”操作，规则如下：
1.  **分裂规则**：如果你手头有一堆 **x** 个苹果，你可以把它分成两堆。
    * 一堆的数量是 **x / 2 (向下取整)**。
    * 另一堆的数量是 **x / 2 (向上取整)**。
    * *通俗地说：如果是偶数，就平分；如果是奇数，一边比另一边多一个。*
2.  **时间成本**：每一次分裂操作消耗 **1 分钟**。

**目标**：
安德烈想要得到一堆**恰好**包含 **k** 个苹果的堆。
请问：他**最少**需要多少分钟才能得到这一堆？如果无论怎么分都得不到数量恰好为 k 的堆，请输出 **-1**。

---

## Input 

-   第一行包含一个整数 t (1 ≤ t ≤ 10^4)，表示测试数据的组数。
-   接下来 t 行，每行包含两个整数 n 和 k：
    -   **n**：初始那一大堆苹果的数量。
    -   **k**：安德烈想要得到的目前堆的数量。
    -   数据范围：1 ≤ n, k ≤ 10^9。

## Output

-   对于每一组测试数据，输出一行：
    -   如果能得到 k 个苹果的堆，输出**最少分钟数**。
    -   如果不可能得到，输出 **-1**。

---

## Example 

### Input
```text
4
10 3
11 5
21 4
1000000000 1
```

### Output
```text
2
1
-1
29
```
>思路:题目挺直白的，上取整和下取整，最少看多少次可以得到k这个数，其实根据样例发现，我们可以知道上取整和下取整，这样其实就是左边界和右边界，然而我们通过一些样例的模拟就会发现其实左边界和右边界永远是相邻的，那无法就是枚举在n里面的2的p次幂，n最大是1e9，大概是29.3左右，我们取30然后枚举一遍，出现了说明，可以找到，直接返回次数，没出现说明不可能找到就输出-1.

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
template <typename T>
struct BIT1
{
    int n;
    vector<T> tr;
    BIT1(int n) : n(n), tr(n + 1) {}
    void add(int x, T v)
    {
        for (; x <= n; x += x & -x)
            tr[x] += v;
    }
    T sum(int x)
    {
        T r = 0;
        for (; x; x -= x & -x)
            r += tr[x];
        return r;
    }
    T range(int l, int r) { return sum(r) - sum(l - 1); }
};
template <typename T>
struct BIT2
{
    int n, m;
    vector<vector<T>> t1, t2, t3, t4;
    BIT2(int n_ = 0, int m_ = 0) { init(n_, m_); }
    void init(int n_, int m_)
    {
        n = n_;
        m = m_;
        t1.assign(n + 1, vector<T>(m + 1, T{}));
        t2.assign(n + 1, vector<T>(m + 1, T{}));
        t3.assign(n + 1, vector<T>(m + 1, T{}));
        t4.assign(n + 1, vector<T>(m + 1, T{}));
    }
    void _add(int x, int y, const T &v)
    {
        for (int i = x; i <= n; i += i & -i)
            for (int j = y; j <= m; j += j & -j)
            {
                t1[i][j] += v;
                t2[i][j] += v * x;
                t3[i][j] += v * y;
                t4[i][j] += v * x * y;
            }
    }
    void rangeAdd(int x1, int y1, int x2, int y2, const T &v)
    {
        _add(x1, y1, v);
        _add(x1, y2 + 1, -v);
        _add(x2 + 1, y1, -v);
        _add(x2 + 1, y2 + 1, v);
    }
    T prefixSum(int x, int y)
    {
        T r{};
        for (int i = x; i > 0; i -= i & -i)
            for (int j = y; j > 0; j -= j & -j)
                r += t1[i][j] * (x + 1) * (y + 1) - t2[i][j] * (y + 1) - t3[i][j] * (x + 1) + t4[i][j];
        return r;
    }
    T rangeSum(int x1, int y1, int x2, int y2)
    {
        if (x1 > x2 || y1 > y2)
            return T{};
        return prefixSum(x2, y2) - prefixSum(x1 - 1, y2) - prefixSum(x2, y1 - 1) + prefixSum(x1 - 1, y1 - 1);
    }
};
struct Random
{
    mt19937_64 rng;
    Random() : rng(chrono::steady_clock::now().time_since_epoch().count()) {}
    ull rand_ull(ull max_val = -1) { return rng() % (max_val + 1); }
    ll rand_ll(ll l, ll r) { return uniform_int_distribution<ll>(l, r)(rng); }
    int rand_int(int l, int r) { return uniform_int_distribution<int>(l, r)(rng); }
    double rand_db(double l, double r) { return uniform_real_distribution<double>(l, r)(rng); }
    bool rand_bool(double p = 0.5) { return bernoulli_distribution(p)(rng); }
    template <typename T>
    void shuffle(vector<T> &v) { std::shuffle(v.begin(), v.end(), rng); }
};
ll qmi(ll a, ll b, ll p)
{
    ll res = 1 % p;
    a %= p;
    while (b)
    {
        if (b & 1)
            res = res * a % p;
        a = a * a % p;
        b >>= 1;
    }
    return res;
}
/*

*/

void solve()
{
    ll n, k;
    cin >> n >> k;
    if (n == k)
    {
        cout << 0 << endl;
        return;
    }
    ll l = 0, r = 0, p = 0;
    rep(i, 1, 30)
    {
        p = (ll)(1 << i);
        l = n / p, r = (n + p - 1) / p;
        if (k == l || k == r)
        {
            cout << i << endl;
            return;
        }
    }
    cout << -1 << endl;
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
# D. Unfair Game (不公平的游戏)

## 题目大意

鲍勃（Bob）和爱丽丝（Alice）在玩一个猜数字游戏。
1.  **游戏设置**：鲍勃心里想了一个从 **1** 到 **n** 的数字。
    * 题目保证 **n** 一定是 **2 的次幂**（比如 1, 2, 4, 8, 16...）。
    * 一开始，爱丽丝只知道这个数字是**奇数**还是**偶数**。
2.  **爱丽丝的操作**：爱丽丝想把这个数字变成 **0**。每一轮她可以做两件事中的一件：
    * 把数字 **减 1**。
    * 把数字 **除以 2**（前提是当前数字必须是偶数）。
3.  **鲍勃的反馈**：爱丽丝每操作一次，鲍勃就要告诉她关于新数字的一个信息：
    * 如果数字变成 **0**，鲍勃回复 **-1**（爱丽丝赢了）。
    * 如果数字不是 0，鲍勃回复这个数字**末尾有几个连续的 0**（二进制下）。
        * 通俗点说：也就是这个数字能被 $2^x$ 整除，但不能被 $2^{x+1}$ 整除，鲍勃告诉她 **x**。
        * *比如：数字变成 12 (二进制 1100)，末尾有 2 个零，鲍勃回复 2。*
        * *比如：数字变成 5 (二进制 101)，末尾有 0 个零，鲍勃回复 0。*
4.  **游戏限制**：
    * 爱丽丝非常聪明，每次都会采取最优策略让自己最快赢。
    * 但是，游戏规定最多只能玩 **k** 步。如果 **k** 步之内（含 k 步）爱丽丝没能把数字变成 0，那鲍勃就赢了。

**问题是**：
给定 **n** 和 **k**，在 **1 到 n** 这一堆数字里，有多少个数字是爱丽丝**无法在 k 步之内猜出来（变成 0）**的？
鲍勃想选这些让他稳赢的数字。

---

## Input

* 第一行是一个整数 **t** ($1 \le t \le 10^4$)，表示有几组测试数据。
* 接下来每行给两个整数 **n** 和 **k** ($1 \le n, k \le 10^9$)。
    * **n** 是数字范围上限（保证是 $2^d$）。
    * **k** 是最大允许的步数。

## Output

* 对于每组数据，输出一个整数：**爱丽丝无法在 k 步内获胜的初始数字的个数**。

---

## Example

### Input
```text
7
4 1
4 2
4 3
4 4
4 5
16 5
16 1
```
### Output
```text
3
2
0
0
0
4
15

```
## 核心思路

首先，我们需要搞清楚把一个数字 $x$ 变成 0 到底需要多少步。
爱丽丝的策略其实是被**强制**的：
- 如果是偶数，必须除以 2（消除末尾的 0）。
- 如果是奇数，必须减 1（消除末尾的 1）。

让我们观察操作对二进制位的影响：
1.  **除以 2**：相当于二进制右移一位，**步数 +1**。
2.  **减 1**：相当于把末尾的 `1` 变成 `0`。注意，这会让数字变回偶数，下一步必须除以 2。所以，消除一个 `1` 的代价其实是 **步数 +2**（一次减1，一次除2）。
    * *特例*：到了最后一步（数字是 1）时，减 1 直接变 0，不需要再除以 2。

**推导步数公式**：
假设一个数字 $x$，它的二进制表示中：
- 最高位是第 $i$ 位（即 $2^i \le x < 2^{i+1}$）。
- 在第 $0$ 到 $i-1$ 位这 $i$ 个低位中，有 $j$ 个是 `1`。

那么消除这个数字需要的总步数 $S$ 为：
$$S = (i + 1) + j$$
* $(i + 1)$ 是因为所有位最终都要被移走（基础步数）。
* $j$ 是因为低位的每一个 `1` 都会额外增加一次“减1”的操作。

## 计数问题

题目要求的是：有多少个数字满足 **需要步数 > k**。
由于 $n=2^d$，我们可以按最高位 $i$（从 $0$ 到 $d-1$）进行分类讨论。

对于固定的最高位 $i$（即数字范围 $[2^i, 2^{i+1}-1]$），这部分数字共有 $2^i$ 个。
我们需要统计其中有多少个数字满足：
$$i + 1 + j > k \quad \Rightarrow \quad j > k - i - 1 \quad \Rightarrow \quad j \ge k - i$$
其中 $j$ 是低 $i$ 位中 `1` 的个数。

这是一个经典的组合数问题！在 $i$ 个位置中，选出 $j$ 个位置放 `1`，方案数就是 $C(i, j)$。
所以我们只需要遍历所有的 $i$，然后累加 $\sum C(i, j)$ 即可。

**特殊边界**：
数字 $n$ 本身是 $2^d$。它的低位没有 1，步数是 $d+1$。
如果 $d+1 > k$，那么 $n$ 也是一个计数对象，答案加 1。

## 代码实现

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define endl '\n'

// 组合数表
ll c[101][101];

// 预处理组合数
void init()
{
    rep(i, 0, 60)
    {
        c[i][0] = 1;
        rep(j, 1, i)
        {
            c[i][j] = c[i - 1][j - 1] + c[i - 1][j];
        }
    }
}

void solve()
{
    ll n, k;
    cin >> n >> k;
    
    // 计算 n 是 2 的多少次幂 (n = 2^d)
    ll s = n;
    ll d = 0;
    while (s > 1)
    {
        s >>= 1;
        d++;
    }
    
    ll ans = 0;
    
    // 枚举最高位 i (从 0 到 d-1)
    // 对应的数字范围是 [2^i, 2^{i+1}-1]
    rep(i, 0, d - 1)
    {
        // 我们需要找步数 > k 的数字
        // 步数公式: steps = i + 1 + j (j是低位中1的个数)
        // 条件: i + 1 + j > k  =>  j >= k - i
        
        // mn 是 j 的下界
        // 注意 k-i 可能为负，要取 max(0)
        ll mn = max(k - i, ll(0)); 
        
        // 累加所有满足条件的组合数
        rep(j, mn, i)
        {
            ans += c[i][j];
        }
    }
    
    // 特殊处理 n 本身 (2^d)
    // 它的步数是 d + 1
    if (d + 1 > k)
    {
        ans++;
    }
    
    cout << ans << endl;
}

int main()
{
    IOS;
    init(); // 别忘了初始化
    int _ = 1;
    cin >> _; 
    while (_--)
    {
        solve();
    }
    return 0;
}
```
## 思考:
### 代码细节：为什么是 `while (s > 1)`？

在计算 $n = 2^d$ 中的指数 $d$ 时，我们本质上是在计算 **最高位的 1 在第几位**（从第 0 位开始数）。

-   **目标**：我们要让那个 `1` 只要移动到最右边（变成数值 1）就停止。
-   如果写成 `while (s > 0)`，当 `s` 变成 1 时循环还会继续执行一次，把 `1` 移出了边界变成了 `0`，导致统计出的 $d$ 多了 1。

**举个栗子**：
假设 $n = 4$ ($100_2$)，我们要求的是 $d=2$。
1.  `100` -> `010` (移 1 次)
2.  `010` -> `001` (移 2 次) -> **此时 s=1，应当停止！**
3.  如果继续移 -> `000` (移 3 次) -> **这就错了**。

所以循环条件必须是 `s > 1`，保证当 $s$ 减小到 1 时立刻终止。
然后关于组合数的不同求法我讲写一篇博客挂在这里，后会有期。

# E. Exquisite Array 

## 题目大意

给你一个长度为 $n$ 的数组 $p$，里面的数字是 $1$ 到 $n$ 的乱序排列（也就是 $1 \sim n$ 每个数恰好出现一次）。

我们需要定义什么是 **“精美子数组”**。
如果一个子数组（原数组中连续的一段）满足以下两个条件，它就是“$k$-精美”的：
1.  **长度至少为 2**（至少包含两个数）。
2.  **相邻差值大**：在这个子数组里，任意两个相邻的数字，它们的差的绝对值都必须 **大于等于 $k$**。

**你的任务是：**
不用你去求某一个特定的 $k$，而是要你把 **$k$ 从 $1$ 到 $n-1$** 的所有情况都算一遍。
也就是说，你需要分别算出：
- 当 $k=1$ 时，有多少个符合条件的子数组？
- 当 $k=2$ 时，有多少个符合条件的子数组？
- ...
- 当 $k=n-1$ 时，有多少个符合条件的子数组？

请按顺序输出这些数量。

---

## Input 

- 第一行包含一个整数 $t$ ($1 \le t \le 25000$)，表示测试数据的组数。
- 接下来每个测试用例包含两行：
    - 第一行是一个整数 $n$ ($2 \le n \le 10^5$)，表示数组的长度。
    - 第二行包含 $n$ 个整数 $p_1, p_2, \dots, p_n$，代表这个排列。
- 数据范围保证：所有测试用例的 $n$ 之和不超过 $2 \cdot 10^5$。

## Output 

- 对于每组测试数据，输出一行，包含 $n-1$ 个整数。
- 第 $i$ 个整数表示当 $k=i$ 时，满足条件的子数组的数量。

---

## Example 

### Input
```text
3
5
5 1 4 2 3
3
3 2 1
4
3 1 2 4
```
### Output
```text
10 6 3 1 
3 0 
6 2 0 
```


**你的任务是：**
不用求某一个 $k$，而是要一口气算出当 $k=1, k=2, \dots, k=n-1$ 时，分别有多少个符合条件的子数组？

---

## 2. 核心思路：为什么要“倒着算”？

### 暴力做法的局限
如果我们老老实实地对于每一个 $k$，都去遍历一遍数组找答案，时间复杂度会爆炸（大约是 $O(n^2)$），而这道题 $n$ 最大有 $10^5$，肯定会超时。

### 逆向思维 (Key Point!)
我们需要观察一个有趣的性质：**$k$ 越大，条件越苛刻；**$k$ 越小，条件越宽松。**

* 如果两个数的差是 5，那么当 $k=5$ 时它符合条件。
* 当 $k$ 降到 4, 3, 2, 1 时，它依然符合条件！

这启发我们：**与其从 $k=1$ 算到 $k=n-1$，不如反过来，从 $k=n-1$ 算到 $k=1$。**

* 当 $k$ 很大时，几乎没有相邻数满足条件，答案很可能是 0。
* 随着 $k$ 慢慢变小，会有越来越多的相邻位置“解锁”（差值 $\ge k$）。
* 我们只需要把这些**新解锁的位置**连起来，算出贡献即可。不需要每次都重头数。

---

## 3. 算法设计：并查集连连看

我们可以把数组看成 $n$ 个点，相邻的两个数之间有一条“边”。
边的“权重”就是这两个数的差值。

1.  **预处理**：算出所有相邻位置的差值，比如 `pair(差值, 位置下标)`。
2.  **排序**：把这些边按差值**从大到小**排序。
3.  **开始遍历**：从 $k = n-1$ 开始往下数。
4.  **激活边**：把所有差值 $\ge k$ 的边“激活”。
5.  **连通块维护 (并查集)**：
    * 如果一条边被激活了，它就形成了一个连通的小段。
    * 如果这条边的左边也激活了，就把它们**合并**成一大段。
    * 如果这条边的右边也激活了，也**合并**起来。

### 数学小课堂：怎么算子数组个数？
假设我们现在有一条连通的“长链”，它由 $L$ 条边组成（连接了 $L+1$ 个数字）。
那么它包含的合法子数组数量是：
$$\text{Count} = 1 + 2 + \dots + L = \frac{L \times (L+1)}{2}$$

我们在合并并查集时，只需要：
1.  **减去** 左边那段旧的贡献。
2.  **减去** 右边那段旧的贡献。
3.  **加上** 合并后新长段的贡献。

---

## 4. 图解演示

假设数组是：`3 1 2 4` ($n=4$)。
相邻差值分别是：
- 下标1: `|3-1|=2`
- 下标2: `|1-2|=1`
- 下标3: `|2-4|=2`

排序后的边任务队列：`(差2, Pos1), (差2, Pos3), (差1, Pos2)`。

#### 第一轮：k=3
没有任何边的差值 $\ge 3$。
* 当前连通块：无。
* **答案 res[3] = 0**。

#### 第二轮：k=2
任务队列里有两条边满足 $\ge 2$：Pos1 和 Pos3。
1.  **激活 Pos1** (`3-1`)：
    * 它是一个独立的长度为 1 的边。
    * 贡献 $\frac{1 \times 2}{2} = 1$。
    * 目前总分 `now = 1`。
2.  **激活 Pos3** (`2-4`)：
    * 它也是独立的（Pos2还没激活，连不上）。
    * 贡献 $+1$。
    * 目前总分 `now = 2`。
* **答案 res[2] = 2**。

#### 第三轮：k=1
任务队列里有 Pos2 (`1-2`) 满足 $\ge 1$。
1.  **激活 Pos2**：
    * 先把自己算作长度 1，`now += 1` (目前 now=3)。
    * **向左看**：Pos1 已经是激活状态 -> **合并！**
        * 减去 Pos1 的旧贡献 (1)，减去 Pos2 的旧贡献 (1)。
        * 合并后长度变成 2。加上新贡献 $\frac{2 \times 3}{2} = 3$。
        * 目前 now = 3 - 1 - 1 + 3 = 4。
    * **向右看**：Pos3 也是激活状态 -> **合并！**
        * 减去左边大块(Pos1+Pos2)的旧贡献 (3)，减去 Pos3 的旧贡献 (1)。
        * 合并后长度变成 3。加上新贡献 $\frac{3 \times 4}{2} = 6$。
        * 目前 now = 4 - 3 - 1 + 6 = 6。
* **答案 res[1] = 6**。

---

## 5. AC 代码详解

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<ll, ll> PLL;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define endl '\n'
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define dep(i, x, n) for (ll i = x; i >= n; i--)
const int N = 1e5 + 10;
ll p[N], sz[N]; // p是并查集父节点，sz是连通块的“边数”
bool st[N];     // st[i] 标记第 i 条边是否已经激活
ll n;
ll find(int x) {
    if (p[x] != x)
        p[x] = find(p[x]);
    return p[x];
}

// 计算公式：长度为 x 的边，能贡献多少个子数组
// 等差数列求和: 1 + 2 + ... + x
ll calc(ll x) {
    return (x * (x + 1)) / 2;
}

void init() {
    rep(i, 0, n) {
        p[i] = i;
        sz[i] = 1; // 初始时，每个连通块只有它自己这一条边，长度为1
        st[i] = false;
    }
}

void solve() {
    cin >> n;
    init();
    vector<ll> a(n + 1, 0);
    rep(i, 1, n) cin >> a[i];
    
    // 1. 预处理：计算所有相邻差值
    vector<PLL> q;
    rep(i, 1, n - 1) {
        // 存储 {差值, 边的下标}
        // 下标 i 代表连接 a[i] 和 a[i+1] 的边
        q.push_back({abs(a[i + 1] - a[i]), i});
    }
    
    // 2. 排序：按差值从大到小排
    // 这样我们就可以从最大的 k 开始处理
    sort(all(q), [&](PLL x, PLL y) { return x.fi > y.fi; });

    ll now = 0; // 全局变量：当前 k 下所有合法子数组的总数
    vector<ll> res(n);
    ll j = 0; // q 的指针

    // 3. 倒序枚举 k
    dep(k, n - 1, 1) {
        // 把所有 差值 >= k 的边加入进来
        while (j < n - 1 && q[j].fi >= k) {
            ll x = q[j].se; // 当前边的位置
            st[x] = true;   // 标记为激活
            
            // 刚加入一条边，先把它当做独立的连通块
            // 长度为1，贡献是 calc(1) = 1
            now += calc(1);

            // 定义合并函数：合并 u 和 v 所在的集合
            auto merge = [&](int u, int v) -> void {
                int ru = find(u);
                int rv = find(v);
                if (ru != rv) {
                    // 核心逻辑：减去两个旧的，加上一个新的
                    now -= calc(sz[ru]);
                    now -= calc(sz[rv]);
                    
                    p[rv] = ru;       // 并查集挂载
                    sz[ru] += sz[rv]; // 长度累加
                    
                    now += calc(sz[ru]); // 加上合并后大块的贡献
                }
            };

            // 检查左边的边 (x-1) 是否激活，如果激活就合并
            if (x > 1 && st[x - 1]) {
                merge(x - 1, x);
            }
            // 检查右边的边 (x+1) 是否激活，如果激活就合并
            if (x < n - 1 && st[x + 1]) {
                merge(x, x + 1);
            }
            j++;
        }
        // 记录当前 k 的答案
        res[k] = now;
    }

    // 4. 输出结果
    rep(i, 1, n - 1) {
        cout << res[i] << " ";
    }
    cout << endl;
}

int main() {
    IOS;
    int _ = 1;
    cin >> _; 
    while (_--) {
        solve();
    }
    return 0;
}
```
# F. Cherry Tree

## 题目大意

给你一棵有 $n$ 个节点的树，树的根节点是 **1** 号节点。
这棵树的每一个**叶子节点**（没有子节点的节点）上都长着一颗樱桃。

你的目标是：**收集所有的樱桃**。

为了收集樱桃，你可以执行多次“摇树”操作。规则如下：

1.  **摇晃规则**：你可以选择树上的任意一个节点 $v$ 进行摇晃。
    - 一旦摇晃了节点 $v$，以 $v$ 为根的**整个子树**里所有的叶子上的樱桃都会掉下来。
    - 如果 $v$ 本身就是叶子，那它上面的樱桃就掉下来。

2.  **安全规则（不能重复）**：
    - 如果某个叶子上的樱桃已经掉下来了，你就不能再次让它掉下来（也就是说，不能通过摇晃另一个祖先节点再次覆盖这个叶子）。
    - 否则树会断掉（任务失败）。
    - **简单说就是**：你选出的这组节点，它们管辖的叶子区域不能有重叠，并且必须刚好覆盖所有叶子。

3.  **神秘传说（核心限制）**：
    - 你一共摇晃的节点总数量，必须是 **3 的倍数**。

**问**：能不能找到一种摇树方案，既能收集完所有樱桃，又不弄断树，且摇晃的节点数还能被 3 整除？

---

## Input 

- 第一行包含一个整数 $t$ ($1 \le t \le 10^4$)，表示测试数据的组数。
- 对于每组测试数据：
    - 第一行包含一个整数 $n$ ($2 \le n \le 2 \cdot 10^5$)，表示节点的数量。
    - 接下来 $n-1$ 行，每行包含两个整数 $u$ 和 $v$，表示节点 $u$ 和 $v$ 之间有一条边（保证是一棵树）。

## Output 

- 对于每组数据，如果能满足条件，输出 `YES`。
- 否则，输出 `NO`。
- （输出不区分大小写，`Yes`, `yes`, `YES` 都可以）。

---

## Example 

### Input
```text
3
4
1 2
1 3
1 4
3
1 2
1 3
9
1 2
3 1
2 4
5 2
5 6
3 7
8 3
8 9
```
### Output
```text
YES
NO
YES
```
## 1. 题目大意 

我们要在一棵树上收集所有叶子节点的樱桃。
规则有点特别：
1.  **摇树**：你可以摇任意一个节点。一摇，这个节点下面所有子树里的樱桃全都会掉下来。
2.  **不能重复**：每个叶子的樱桃只能掉一次。如果你摇了根节点，就不能再摇下面的子节点了；反之，如果你分别摇了下面的子节点，就不能再摇上面的根节点。
    * *潜台词：我们要么直接搞定当前节点，要么让子节点们自己搞定，把子树覆盖满。*
3.  **3的倍数**：最终你一共摇了多少次节点？这个总次数必须是 **3 的倍数**。

问：能不能做到？

---

## 2. 核心思路：树形 DP

### 为什么要用 DP？
对于任意一个节点 $u$，想要搞定以它为根的子树，有两种策略：
1.  **直接摇 $u$**：
    * 不管是啥结构，我直接摇 $u$，咔嚓一下，下面所有叶子都搞定了。
    * **代价**：操作次数 = 1。
2.  **不摇 $u$，让儿子们自己摇**：
    * 我如果不摇 $u$，那 $u$ 的每一个子节点 $v$ 就必须自己负责搞定它们自己的子树。
    * **代价**：操作次数 = 所有子节点操作次数之和。

这就出现了分歧！
* 如果不摇 $u$，子节点 $v_1$ 可能花了 2 次， $v_2$ 可能花了 4 次，合起来就是 6 次。
* 如果我们关心的是总次数能否被 3 整除，那我们不需要记录具体的次数（比如 100 次还是 200 次），只需要记录 **模 3 后的余数**。

### 状态定义
我们需要定义 `f[u][r]`，其中 $r$ 是 $0, 1, 2$。
* `f[u][0] = true`：表示以 $u$ 为根的子树，可以通过 $3k$ 次操作搞定。
* `f[u][1] = true`：表示以 $u$ 为根的子树，可以通过 $3k+1$ 次操作搞定。
* `f[u][2] = true`：表示以 $u$ 为根的子树，可以通过 $3k+2$ 次操作搞定。

最终答案就是看根节点 `f[1][0]` 是不是 `true`。

---

## 3. 状态转移逻辑 (背包思想)

假设节点 $u$ 有很多子节点 $v_1, v_2, \dots$。
如果我们选择**“不摇 u”**策略，那总次数就是所有子节点次数相加：
$$\text{Total} = \text{Cost}(v_1) + \text{Cost}(v_2) + \dots$$
在模 3 意义下，这就是一个**分组背包**或者简单的**余数累加**问题。

* 初始化：刚开始只有一种情况，余数是 0（什么都不做）。
* 来了一个子节点 $v$，它可能贡献余数 0, 1, 或 2。
* 我们用临时数组 `nxt` 更新当前的余数集合。
    * 比如之前能凑出余数 1，现在 $v$ 能凑出余数 2，那 $1+2=3 \to 0$，我们就凑出了余数 0。

**特殊情况：直接摇 u**
除了累加子节点，我们还有一种选择：直接摇 $u$。
这就简单粗暴了，不管子节点怎么弄，直接把 $u$ 视为 1 次操作。
所以，对于任何节点 $u$，`f[u][1]` 总是可以为 `true`（只要它里面包含叶子，或者它自己是叶子）。
* *注：代码里需要注意叶子节点的判定，不过题目逻辑上直接置 `f[u][1]=true` 是通用的，因为摇自己总是花费 1。*

---

## 4. 图解转移过程

假设节点 u 有两个子节点 A 和 B。

* **子节点 A** 能提供的余数集合：`{1}` (代表 A 只能花 1 次)
* **子节点 B** 能提供的余数集合：`{1, 2}` (代表 B 能花 1 次或 2 次)

**初始状态**：`st = {0}` (一开始还没有合并任何子节点，余数为 0)

**第一步：合并 A**
* 当前累加状态是 `{0}`。
* 子节点 A 提供余数 `1`。
* 进行组合：0 + 1 = 1。
* **合并后状态**：`{1}`。

**第二步：合并 B**
* 当前累加状态是 `{1}`。
* 子节点 B 提供余数 `1` 和 `2`。
* 组合情形 1：1 (来自当前) + 1 (来自 B) = 2。
* 组合情形 2：1 (来自当前) + 2 (来自 B) = 3，对 3 取模后变成 0。
* **合并后状态**：`{0, 2}` (这是“不摇 u，只靠子节点”能凑出的余数)。

**第三步：考虑摇 u 自己 (必须考虑的策略)**
* 除了上面靠子节点凑出来的 `{0, 2}`，我们永远可以选择**直接摇 u**。
* 摇 u 的花费固定是 1。
* 所以我们将 `1` 也加入最终的可能集合中。
* **最终 u 的状态集合**：`{0, 1, 2}` (即 u 节点可以向上层汇报：我也能凑出 0、1 或 2)。
---

## 5. AC 代码详解

```cpp
#include <bits/stdc++.h>
using namespace std;

// 常用宏定义
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define endl '\n'
#define rep(i, x, n) for (int i = x; i <= n; i++)
#define out(x) cout << ((x) ? "YES" : "NO") << endl

const int N = 2e5 + 10;
const int M = 2 * N;

// 邻接表存图
int h[N], e[M], ne[M], idx;
// DP 数组：f[u][0/1/2]
bool f[N][3]; 
int n;

void add(int a, int b) {
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

void init() {
    idx = 0;
    rep(i, 0, n) {
        h[i] = -1;
        f[i][0] = f[i][1] = f[i][2] = false;
    }
}

// 核心 DFS 函数
void dfs(int u, int pa) {
    // st 数组用来存“累加子节点”产生的余数集合
    // 初始状态是 {0} (也就是 true, false, false)
    bool st[3] = {true, false, false};
    bool is_leaf = true; // 标记是否是叶子

    for (int i = h[u]; ~i; i = ne[i]) {
        int j = e[i];
        if (j == pa) continue; // 别倒着搜回去了
        
        is_leaf = false;
        dfs(j, u); // 先递归搞定子节点
        
        // --- 核心转移逻辑：合并子节点 j 的结果 ---
        bool nxt[3] = {false, false, false}; // 临时数组存合并后的新状态
        
        // 枚举之前已经凑出的余数 r1
        for (int r1 = 0; r1 < 3; r1++) {
            if (st[r1]) { // 如果 r1 存在
                // 枚举子节点 j 能提供的余数 r2
                for (int r2 = 0; r2 < 3; r2++) {
                    if (f[j][r2]) { // 如果 j 能凑出 r2
                        // 组合出了新余数 (r1 + r2) % 3
                        nxt[(r1 + r2) % 3] = true;
                    }
                }
            }
        }
        // 更新 st 状态
        for (int k = 0; k < 3; k++) st[k] = nxt[k];
    }

    // 策略 1：直接摇 u 自己
    // 代价总是 1。无论是不是叶子，摇 u 总是合法的操作，花费 1。
    f[u][1] = true;

    // 策略 2：不摇 u，让子节点凑
    // 只有当 u 不是叶子时，这个策略才有效
    // (如果是叶子，没子节点凑，必须摇自己，也就是上面那行)
    if (!is_leaf) {
        for (int k = 0; k < 3; k++) {
            if (st[k]) {
                f[u][k] = true;
            }
        }
    }
}

void solve() {
    cin >> n;
    init();
    rep(i, 1, n - 1) {
        int u, v;
        cin >> u >> v;
        add(u, v);
        add(v, u);
    }
    
    dfs(1, 0);
    
    // 只要根节点能凑出余数 0，就是 YES
    if (f[1][0]) {
        out(1);
    } else {
        out(0);
    }
}

int main() {
    IOS;
    int _ = 1;
    cin >> _; 
    while (_--) {
        solve();
    }
    return 0;
}
```
# G. Nastiness of Segments 

## 题目大意

安德烈（Andrey）有一排积木，编号从 **1** 到 **n**，每个积木上都写着一个数字 **a[i]**。

这道题定义了一个核心概念叫 **“讨厌的数” **，记作 **d**。
对于一个查询区间 `[l, r]`，如果一个非负整数 `d` ($0 \le d \le r-l$) 满足以下条件，它就是“讨厌的”：

* 从起点 **l** 开始，往后取 **d** 个位置（即区间 `[l, l+d]`）。
* 这一小段里的 **最小值** 恰好等于 **d**。

用公式表示就是：
`min(a[l], a[l+1], ..., a[l+d]) = d`

你的任务是处理 **q** 次操作，操作分为两种：

1.  **修改操作**：把第 `i` 个积木上的数字改成 `x`。
2.  **查询操作**：给定一个区间 `[l, r]`，请你算出这个区间里一共有多少个合法的“讨厌的数” `d`。

---

## Input 

-   第一行包含一个整数 **t** ($1 \le t \le 10^4$)，表示测试数据的组数。
-   每个测试用例的第一行包含两个整数 **n** 和 **q** ($1 \le n, q \le 2 \cdot 10^5$)，分别表示积木数量和操作次数。
-   下一行包含 **n** 个整数 $a_1, a_2, \dots, a_n$，表示积木上初始的数字。
-   接下来 **q** 行描述操作：
    -   `1 i x`：**修改操作**。把位置 `i` 的数改成 `x`。
    -   `2 l r`：**查询操作**。查询区间 `[l, r]` 的“讨厌程度”（即满足条件的 `d` 的个数）。

数据范围保证所有测试用例的 **n** 和 **q** 之和都不超过 $2 \cdot 10^5$。

## Output 

-   对于每一个类型为 2 的查询操作，输出一行一个整数，表示该区间内“讨厌的数”的个数。

---

## Example 

### Input
```text
1
5 5
1 2 3 4 5
2 1 5
1 1 5
1 2 5
1 3 1
2 1 5
```
### Output
```text
1
0
```
>思路：线段树+二分
代码：
```
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
const int N = 2e5 + 10, M = 2 * N, K = 26;
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
template <typename T>
struct BIT1
{
    int n;
    vector<T> tr;
    BIT1(int n) : n(n), tr(n + 1) {}
    void add(int x, T v)
    {
        for (; x <= n; x += x & -x)
            tr[x] += v;
    }
    T sum(int x)
    {
        T r = 0;
        for (; x; x -= x & -x)
            r += tr[x];
        return r;
    }
    T range(int l, int r) { return sum(r) - sum(l - 1); }
};
template <typename T>
struct BIT2
{
    int n, m;
    vector<vector<T>> t1, t2, t3, t4;
    BIT2(int n_ = 0, int m_ = 0) { init(n_, m_); }
    void init(int n_, int m_)
    {
        n = n_;
        m = m_;
        t1.assign(n + 1, vector<T>(m + 1, T{}));
        t2.assign(n + 1, vector<T>(m + 1, T{}));
        t3.assign(n + 1, vector<T>(m + 1, T{}));
        t4.assign(n + 1, vector<T>(m + 1, T{}));
    }
    void _add(int x, int y, const T &v)
    {
        for (int i = x; i <= n; i += i & -i)
            for (int j = y; j <= m; j += j & -j)
            {
                t1[i][j] += v;
                t2[i][j] += v * x;
                t3[i][j] += v * y;
                t4[i][j] += v * x * y;
            }
    }
    void rangeAdd(int x1, int y1, int x2, int y2, const T &v)
    {
        _add(x1, y1, v);
        _add(x1, y2 + 1, -v);
        _add(x2 + 1, y1, -v);
        _add(x2 + 1, y2 + 1, v);
    }
    T prefixSum(int x, int y)
    {
        T r{};
        for (int i = x; i > 0; i -= i & -i)
            for (int j = y; j > 0; j -= j & -j)
                r += t1[i][j] * (x + 1) * (y + 1) - t2[i][j] * (y + 1) - t3[i][j] * (x + 1) + t4[i][j];
        return r;
    }
    T rangeSum(int x1, int y1, int x2, int y2)
    {
        if (x1 > x2 || y1 > y2)
            return T{};
        return prefixSum(x2, y2) - prefixSum(x1 - 1, y2) - prefixSum(x2, y1 - 1) + prefixSum(x1 - 1, y1 - 1);
    }
};
struct Random
{
    mt19937_64 rng;
    Random() : rng(chrono::steady_clock::now().time_since_epoch().count()) {}
    ull rand_ull(ull max_val = -1) { return rng() % (max_val + 1); }
    ll rand_ll(ll l, ll r) { return uniform_int_distribution<ll>(l, r)(rng); }
    int rand_int(int l, int r) { return uniform_int_distribution<int>(l, r)(rng); }
    double rand_db(double l, double r) { return uniform_real_distribution<double>(l, r)(rng); }
    bool rand_bool(double p = 0.5) { return bernoulli_distribution(p)(rng); }
    template <typename T>
    void shuffle(vector<T> &v) { std::shuffle(v.begin(), v.end(), rng); }
};
ll qmi(ll a, ll b, ll p)
{
    ll res = 1 % p;
    a %= p;
    while (b)
    {
        if (b & 1)
            res = res * a % p;
        a = a * a % p;
        b >>= 1;
    }
    return res;
}
/*

*/
int n, q;
int a[N];

struct Node
{
    int l, r;
    int mn;
} t[N * 4];

void pushup(int p)
{

    t[p].mn = min(t[lc].mn, t[rc].mn);
}

void build(int p, int l, int r)
{
    t[p].l = l;
    t[p].r = r;
    if (l == r)
    {
        t[p].mn = a[l];
        return;
    }

    int mid = (l + r) >> 1;
    build(lc, l, mid);
    build(rc, mid + 1, r);
    pushup(p);
}

void modify(int p, int x, int v)
{
    if (t[p].l == t[p].r)
    {
        t[p].mn = v;
        return;
    }
    int mid = (t[p].l + t[p].r) >> 1;
    if (x <= mid)
        modify(lc, x, v);
    else
        modify(rc, x, v);
    pushup(p);
}

int query(int p, int l, int r)
{
    if (l <= t[p].l && t[p].r <= r)
    {
        return t[p].mn;
    }
    int mid = (t[p].l + t[p].r) >> 1;
    int res = INF;
    if (l <= mid)
        res = min(res, query(lc, l, r));
    if (r > mid)
        res = min(res, query(rc, l, r));
    return res;
}

void solve()
{
    cin >> n >> q;
    rep(i, 1, n) cin >> a[i];

    build(1, 1, n);

    while (q--)
    {
        int op;
        cin >> op;
        if (op == 1)
        {
            int i, x;
            cin >> i >> x;
            modify(1, i, x);
        }
        else
        {
            int l, r;
            cin >> l >> r;

            int L = -1, R = r - l + 1;
            bool ck = false;

            while (L + 1 < R)
            {
                int d = L + (R - L) / 2;

                int mn = query(1, l, l + d);

                if (mn == d)
                {
                    ck = true;
                    break;
                }
                else if (mn > d)
                {

                    L = d;
                }
                else
                {

                    R = d;
                }
            }

            if (ck)
                cout << 1 << endl;
            else
                cout << 0 << endl;
        }
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
```