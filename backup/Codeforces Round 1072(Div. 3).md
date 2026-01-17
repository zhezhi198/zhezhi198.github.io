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

### 2. 情况二：沙漏容量大，翻转间隔短 ($s > k$)

想象你有一个巨大的桶，但手速很快，不停地翻转。
* **现象**：沙子根本来不及漏完，就被你翻回去了。这会导致沙漏里的沙子在两个状态之间“反复横跳”。
* **规律（循环节）**：
    * **初始状态（第0轮）**：上方有 **$s$**。
    * **第1次翻转后（奇数轮）**：刚才漏下去的 **$k$** 变成了上方，开始漏。
    * **第2次翻转后（偶数轮）**：下方原本剩下的加上刚才接住的，又变回了 **$s$**。
    * **结论**：
        * **偶数次**翻转后，该阶段以 **$s$** 开局。
        * **奇数次**翻转后，该阶段以 **$k$** 开局。
* **计算逻辑**：
    1.  算出总共翻转了多少次：`cnt = m / k`。
    2.  算出最后一次翻转后过了多久：`res = m % k`。
    3.  判断 `cnt` 的奇偶性：
        * **奇数 **：初始量是 $k$。答案是 **$k - res$** （因为 $s>k$，所以 $k$ 分钟内沙子肯定够漏，只需直接相减）。
        * **偶数 **：初始量是 $s$。答案是 **$s - res$** （同理，因为 $k < s$，肯定够漏）。

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
7
4 1
4 2
4 3
4 4
4 5
16 5
16 1
```
先去做饭了，先写到这里