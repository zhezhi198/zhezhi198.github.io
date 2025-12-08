### 牛客周赛121部分题解
[点击进入比赛](https://ac.nowcoder.com/acm/contest/124143#question)

## F

<img width="1248" height="1327" alt="Image" src="https://github.com/user-attachments/assets/bf4004bd-aad5-4e96-8126-1c97e3fd4af2" />


>思路:要询问一个区间的子序列是否可以通过乘积来得到一个完全平方数，那么我们想想想完全平方数的特征，从公式来看就是某个数的平方，也就是说这个数出现了两次，然而这样说在当前题意下仍然不够严谨，我们所说的某个数是不是也是其他数的乘积呢，仔细想想发现，我们发现可以定义为最小质因数的偶数次幂，这个最小可以有多个，但是必须是偶数幂。有了这个发现之后，我们尝试把每个数组中的数改成[1,100]内的质数的二进制，为什么可以这样，说来也巧，因为100以内的质因数只有差不多25个，于是我们的想法依然是可行的。那么让数组中的子序列出现完全平方数的判断转换为，我们选一些数，让这些数对应的特殊二进制数的异或最后为0，因为0可以表示所有(位)次幂是偶数次，也就是我们想要的完全平方数的状态。那么现在的问题是我们如何知道选那些数，可以或者说可能能让子序列成为完全平方数呢?结合异或的特点，我们的目的是让1变成0，最后全部变成0，那么我们选的就是那些可以使得异或结果变小的数，从大到小贪心就好。

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
ll prime[] = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97};
void solve()
{
    ll n, q;
    cin >> n >> q;
    vll a(n + 1, 0);
    rep(i, 1, n)
    {
        ll x;
        cin >> x;
        ll st = 0;
        rep(j, 0, 24)
        {
            ll cnt = 0;
            while (x % prime[j] == 0)
            {
                x /= prime[j];
                cnt++;
            }
            if (cnt & 1)
                st |= (1 << j);
        }
        a[i] = st;
    }
    rep(i, 1, q)
    {
        ll l, r;
        cin >> l >> r;
        if (r - l + 1 >= 26)
        {
            cout << "Yes" << endl;
            continue;
        }
        vll b;
        bool win = false;

        rep(k, l, r)
        {
            ll v = a[k];
            //  debug(k, v);
            for (auto x : b)
            {
                cmin(v, v ^ x);
            }
            if (v == 0)
            {
                win = true;
                break;
            }

            b.push_back(v);
            sort(all(b), greater<ll>());
        }

        if (win)
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }
}

int main()
{
    IOS;

    int _ = 1;
    // cin>>_;//如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```

# [牛客周赛 124143] D. 恋恋的01串 - 题解

## 题目分析

### 1. 问题转化 (Problem Transformation)
题目要求我们输出每一个操作次数 $x$ 下的最大生存天数。直接求“给定 $x$ 能活多久”比较困难，因为贪心策略并不明显，可能会陷入局部最优。

我们可以利用 **逆向思维** 将问题转化为：

> **如果我想让第 $i$ 天变成“获得存在感（变为1）”的状态，且前 $i$ 天都合法，至少需要花费多少次操作？**

如果我们算出了到达第 $i$ 天的最小代价（设为 $cost$），那么在这个 $cost$ 下，我们以第 $i$ 天为跳板，至少还能向后存活 $k-1$ 天。

### 2. 状态定义 (DP State)
定义 $f[i]$ 表示：
**保证前 $i$ 天合法，且第 $i$ 天必须是 '1'（获得存在感）所需的最小操作次数。**

* **为什么要强制第 $i$ 天是 '1'？**
  因为 '1' 是我们存活的“存档点”。只有站在 '1' 上，我们才能向后展望 $k-1$ 天的“安全期”。

### 3. 状态转移方程
为了保证中间不中断，第 $i$ 天的上一个 '1'（设位置为 $j$）必须在最近的 $k$ 天内。
即 $j$ 的范围是：$[i-k, i-1]$。

转移方程为：

$$
f[i] = \min_{i-k \le j < i} \{ f[j] \} + \text{cost}(i)
$$

其中：
* $\text{cost}(i)$：如果原字符串 $s[i]$ 是 '0'，则需要 1 次操作，代价为 1；如果是 '1'，代价为 0。
* **边界条件**：$f[0] = 0$，我们假设有一个虚拟的第 0 天，视为天然存在的 '1'，且不需要花费操作次数。

### 4. 单调队列优化 (Monotonic Queue)
观察转移方程，我们需要在区间 $[i-k, i-1]$ 中找到 $f[j]$ 的最小值。这是一个经典的 **“滑动窗口求最小值”** 模型。

* **朴素做法**：如果直接遍历查找最小值，时间复杂度是 $O(NK)$，对于 $N=2 \times 10^5$ 的数据范围会超时。
* **优化做法**：利用 **单调队列 (Deque)** 维护一个下标 $j$ 的序列，使得队列中的 $f[j]$ 单调递增。
    * **队头（Front）**：永远是当前窗口 $[i-k, i-1]$ 内 $f[j]$ 最小的下标。
    * **队尾（Back）**：维护单调性，如果新来的 $f[i]$ 比队尾更优（更小），则弹出队尾。
* **复杂度**：每个元素最多进队一次、出队一次，时间复杂度优化为 **$O(N)$**。

### 5. 统计答案
计算出 $f[i]$ 后，如何更新最终答案？
如果我们让第 $i$ 天成为最后一个 '1'，那么我们可以凭借这个 '1' 再向后“苟” $k-1$ 天（但不能超过总天数 $n$）。

所以，花费 $f[i]$ 的代价，我们实际能存活的天数是：

$$
\text{days} = \min(n, i + k - 1)
$$

我们用一个数组 `ans` 记录答案：
1.  更新当前代价的最优解：`ans[f[i]] = max(ans[f[i]], days)`
2.  前缀最大值优化：如果花费 $x$ 能活 $D$ 天，那么花费 $x+1$（多一次操作机会不用）肯定也能活 $D$ 天。
    `ans[i] = max(ans[i], ans[i-1])`

---

## AC 代码 (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define endl '\n'

void solve()
{
    ll n, k;
    cin >> n >> k;
    string s;
    cin >> s;
    s = " " + s; // 调整为 1-based 索引

    // f[i]: 到达第 i 天且 s[i] 为 '1' 的最小操作次数
    vector<ll> f(n + 1);
    
    // 单调队列，存储下标，维护 f[idx] 的单调递增
    deque<ll> q;
    
    // 初始化：虚拟第 0 天
    q.push_back(0);
    f[0] = 0;
    
    // ans[x] 表示操作 x 次能存活的最大天数
    vector<ll> ans(n + 2, 0);
    // 即使一次都不操作，靠第 0 天也能活 min(n, k-1) 天
    ans[0] = min(n, k - 1);

    rep(i, 1, n)
    {
        // 1. 维护窗口：移除过期的下标 (距离当前 i 超过 k)
        while (!q.empty() && i - q.front() > k)
            q.pop_front();
        
        // 2. 状态转移：队头即为窗口内的最小值
        f[i] = f[q.front()] + (s[i] == '0');
        
        // 3. 记录答案：假设 i 是最后一个 1
        ll d = min(n, i + k - 1);
        ans[f[i]] = max(ans[f[i]], d);

        // 4. 维护单调性：新来的 f[i] 如果更优，剔除队尾劣质解
        while (!q.empty() && f[q.back()] >= f[i])
            q.pop_back();
        q.push_back(i);
    }

    // 前缀最大值优化：代价越大，存活天数只增不减
    rep(i, 1, n) ans[i] = max(ans[i], ans[i - 1]);
    
    rep(i, 0, n) cout << ans[i] << " ";
    cout << endl;
}

int main()
{
    IOS;
    int _ = 1;
    while (_--)
    {
        solve();
    }
    return 0;
}


>昨天想复杂了，其实简单的预处理加上二分就可以过，今天试着又写了一遍。


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
    string s;
    cin >> s;
    s = " " + s;
    ll l = 1, r = 1;
    vll ans(n + 2, 0);
    vll cost(n + 2, 0);

    ll res = 0;
    ll now = 0;
    for (l = 1; l <= n; l++)
    {
        if (s[l] == '0')
            now++;
        else
            now = 0;

        if (now == k)
        {
            res++;
            now = 0;
        }
        cost[l] = res;
    }
    auto check = [&](ll x) -> ll
    {
        ll l = -1, r = n + 1;
        while (l + 1 < r)
        {
            ll mid = l + (r - l) / 2;
            if (cost[mid] <= x)
            {
                l = mid;
            }
            else
            {
                r = mid;
            }
        }
        return l;
    };
    rep(x, 0, n)
    {
        ans[x] = check(x);
    }
    rep(i, 0, n)
    {
        cout << ans[i] << " ";
    }
    cout << endl;
}

int main()
{
    IOS;

    int _ = 1;
    // cin>>_;//如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```