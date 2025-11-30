[进入比赛](https://ac.nowcoder.com/acm/contest/123788)

## E无穷无尽的树

<img width="1263" height="1344" alt="Image" src="https://github.com/user-attachments/assets/86f848b9-007e-4552-938c-d65ae8cbcf3c" />

>思路：树形dp即可，我们把叶子节点不予考虑即可。
代码：
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

int n;
int h[N], ne[M], e[M], idx;
int cnt[N];
int dep[N];
int d[N];

void add(int a, int b)
{
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

PII dfs(int u, int fa)
{
    dep[u] = dep[fa] + 1;

    if (d[u] == 1 && u != 1)
    {
        cnt[u] = 0;
        return {-1, 0};
    }

    int mx = dep[u], sz = 1;

    for (int i = h[u]; ~i; i = ne[i])
    {
        int j = e[i];
        if (j == fa)
            continue;

        PII t = dfs(j, u);

        if (t.fi == -1)
            continue;

        if (t.fi > mx)
        {
            mx = t.fi;
            sz = t.se;
        }
        else if (t.fi == mx)
        {
            sz += t.se;
        }
    }

    cnt[u] = sz;
    return {mx, sz};
}

void solve()
{
    mem(h, -1);
    idx = 0;
    cin >> n;

    if (n == 1)
    {
        cout << 0 << endl;
        return;
    }

    rep(i, 1, n) d[i] = 0;

    rep(i, 1, n - 1)
    {
        int a, b;
        cin >> a >> b;
        add(a, b);
        add(b, a);
        d[a]++;
        d[b]++;
    }

    dep[0] = 0;
    dfs(1, 0);

    rep(i, 1, n) cout << cnt[i] << " ";
    cout << endl;
}

int main()
{
    IOS;
    int _ = 1;
    // cin >> _;
    while (_--)
        solve();
    return 0;
}
```
## F无穷无尽的数

<img width="1262" height="1413" alt="Image" src="https://github.com/user-attachments/assets/f358cea4-6b78-42ac-a6ac-d0f1d58c691c" />

>思路:这题细节比较多，大概思路应该都知道，有一点点的分块思想，可能存在的l不完整块，中间完整周期的重复块，可能存在的右边不完整块，再用字符串哈希把这个数拼起来，中间重复部分因为具有周期性，那么可以用等比序列求和的公式，因为模数是一个大质数，除的那部分就转换成逆元。小心地取模就好。

>其实困难的是正确反映字符的位置，正确的取模，和最后正确代码的实现，思路往往是最先想到的。

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
const ll MOD = 998244353, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
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
ll n, l, r;
string s;
ll h[N], p[N];

ll qmi(ll a, ll b)
{
    ll res = 1;
    while (b)
    {
        if (b & 1)
            res = res * a % MOD;
        a = a * a % MOD;
        b >>= 1;
    }
    return res;
}

ll inv(ll x)
{
    return qmi(x, MOD - 2);
}

ll get(int l, int r)
{
    if (l > r)
        return 0;
    return (h[r] - h[l - 1] * p[r - l + 1] % MOD + MOD) % MOD;
}

void solve()
{
    cin >> n >> l >> r >> s;
    s = " " + s;
    p[0] = 1;
    rep(i, 1, n)
    {
        p[i] = p[i - 1] * 10 % MOD;
        h[i] = (h[i - 1] * 10 + (s[i] - '0')) % MOD;
    }
    ll len = r - l + 1;
    ll b1 = (l - 1) / n;
    ll b2 = (r - 1) / n;

    if (b1 == b2)
    {
        ll st = (l - 1) % n + 1;
        ll ed = (r - 1) % n + 1;
        cout << get(st, ed) << endl;
        return;
    }
    ll len2 = (r - 1) % n + 1;
    ll v2 = get(1, len2);
    ll len1 = n - ((l - 1) % n);
    ll v1 = get(n - len1 + 1, n);
    ll mlen = len - len1 - len2;
    ll c = mlen / n;
    ll vm = 0;
    if (c > 0)
    {
        ll q = p[n];
        vm = h[n] * (qmi(q, c) - 1 + MOD) % MOD * inv(q - 1) % MOD % MOD;
    }
    ll res = v2;
    if (c > 0)
    {
        res = (res + vm * qmi(10, len2) % MOD) % MOD;
    }
    res = (res + v1 * qmi(10, len2 + mlen) % MOD) % MOD;

    cout << res << endl;
}

int main()
{
    IOS;
    int _ = 1;
    // cin >> _;
    while (_--)
        solve();
    return 0;
}
```