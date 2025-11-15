### 牛客小白月赛123
[点击进入比赛页面](https://ac.nowcoder.com/acm/contest/122725#question)

>以后就讲有点思路的题目吧，A,B,就不讲了！

## C诗超绊

<img width="943" height="855" alt="Image" src="https://github.com/user-attachments/assets/f5fa928e-6ef6-41bd-b848-c9714b2e5839" />

>思路：我们要用至多  次区间加操作（每次加同一个固定正整数 ） 使序列严格递增。显然，若能用某个  实现目标， 则对更大的  也可以实现，因此答案关于  是单调的，可用二分查找最小可行的 。
给定d，如何判断可行?
我们只需判断是否能够用不超过m次操作，使得每个位置满足a i′​ >a i−1′ (∀,i>1).由于每次操作将一段连续区间整体加 d， 可以等价地把操作理解为“将某些前缀区间的加次数累积起来”。 我们可以贪心地从左到右判断：
*设当前已经进行了若干次区间加，使得到位置 i−1 为止，序列已严格递增
*若此时 ai≤a(i-1) ，则至少需要让ai ​增加到 a(i-1)+1， 因此需要的额外加次数为t=(a(i-1)+1-ai)/d；
这些加法可视从位置i到结尾加上t次d，操作次数的总和累加上t。若累计操作次数总和<=m，即为合法的一个d的值。
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
    int n;
    ll m;
    cin >> n >> m;
    vector<ll> a(n);
    rep(i, 0, n - 1) cin >> a[i];

    auto check = [&](ll x, int n, ll m, const vector<ll> &a) -> bool
    {
        if (x == 0)
        {
            rep(i, 1, n - 1)
            {
                if (a[i] <= a[i - 1])
                    return false;
            }
            return true;
        }

        ll sum = 0;//总操作次数
        ll cnt = 0;//累计操作次数
        ll lt = a[0];

        rep(i, 1, n - 1)
        {
            ll now = a[i] + cnt * x;//当前值
            if (now <= lt)
            {
                ll d = lt + 1 - now;
                ll num = (d + x - 1) / x;
                sum += num;
                if (sum > m)
                    return false;
                cnt += num;
                lt = now + num * x;
            }
            else
            {
                lt = now;
            }
        }
        return sum <= m;
    };

    ll l = -1, r = 2e9 + 7;

    while (l + 1 < r)
    {
        ll mid = l + (r - l) / 2;
        if (check(mid, n, m, a))
        {
            r = mid;
        }
        else
        {
            l = mid;
        }
    }
    if (r == 2e9 + 7)
    {
        cout << -1 << endl;
    }
    else
    {
        cout << r << endl;
    }
}

int main()
{
    IOS;

    int _ = 1;
    cin >> _; // 多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
>主要是check函数比较难写，其实从差分的视角来看，我们无非就是让a数组的差分数组全>0，你可以想想对于a数组再做区间加法，如[l,r]区间内加上d，我们就会发现其实[l,r]之间的差分值是不会改变的，改变是只有al-a(l-1)的差分值和a(r+1)-ar的差分值，我们让l的差分值+d，让r+1的差分值减少了d，如果我们的选择的r是边界n，那么就无需要减去右边界的d，想清楚这些之后，我们只需要一个个算出需要修改的次数，累加起来看看是否合法，check函数就自然而然的写出来了。

## D春日影

<img width="938" height="2421" alt="Image" src="https://github.com/user-attachments/assets/5e4b0ccd-28f1-4a94-ade6-10a1ae9ab3d1" />

>感觉就是一个标准的分层图变式，然后跑一遍Dijkstra即可，注意审题应该就不会有很大的问题
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
const int N = 4e5 + 10, M = 2 * N, K = 26;
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

vector<PLL> g[N];
ll dist[N];
bool vis[N];

void solve()
{
    int n, m;
    cin >> n >> m;
    vll p(n + 1, INF);

    rep(i, 1, m)
    {
        int u, v;
        ll w;
        cin >> u >> v >> w;
        cmin(p[u], w);
        cmin(p[v], w);
        g[u].push_back({v, w});
        g[v].push_back({u, w});
        g[u + n].push_back({v, 0});
        g[v + n].push_back({u, 0});
    }

    rep(i, 1, n)
    {
        if (p[i] != INF)
        {
            g[i].push_back({i + n, 2 * p[i]});
        }
    }

    rep(i, 1, 2 * n)
    {
        dist[i] = INF;
        vis[i] = false;
    }
    dist[1] = 0;
    priority_queue<PLL, vector<PLL>, greater<PLL>> pq;
    pq.push({0, 1});
    while (!pq.empty())
    {
        auto [d, u] = pq.top();
        pq.pop();
        if (vis[u])
            continue;
        vis[u] = true;
        for (auto [v, w] : g[u])
        {
            if (cmin(dist[v], d + w))
            {
                pq.push({dist[v], v});
            }
        }
    }

    ll ans = min(dist[n], dist[n + n]);
    if (ans == INF)
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
    // cin >> _; // 如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
## F明弦音

<img width="1252" height="4510" alt="Image" src="https://github.com/user-attachments/assets/491dfff0-fce1-4824-9a3d-767f1bfbdb02" />

>带权并查集写的太少，读题的时候甚至还没意识到这一点，该加训了，唉。我觉得不太应该，最可悲的是学了的题目不会做，然后也不做出任何改变去弥补这个漏洞！！！

思路：
>题目要求我们维护三个操作
*加入约束 𝑎ᵤ − 𝑎ᵥ = 𝑘
*设置绝对赋值 𝑎ᵤ = 𝑘
*查询 𝑎ᵤ − 𝑎ᵥ 是否可唯一确定
关键点：新约束不能与已有约束矛盾，否则操作被忽略。
看到关系维护，又是求距离赋值的，可以往并查集和图论方面想。显然这个题目是带权并查集的典题，带权并查集的写法其实都差不多，主要是根据题目的要求会小改一些函数，比如merge函数，也许还会添加，但大差不差。

先给出AC代码：
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
const int N = 5e5 + 10, M = 2 * N, K = 26;
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

ll n, q;
ll p[N], d[N];

int find(int x)
{
    if (p[x] != x)
    {
        int fa = p[x];
        p[x] = find(p[x]);
        d[x] += d[fa];
    }
    return p[x];
}

void merge(int x, int y, ll k)
{
    int u = find(x), v = find(y);
    p[u] = v;
    d[u] = d[y] + k - d[x];
}

void solve()
{
    cin >> n >> q;
    rep(i, 0, n)
    {
        p[i] = i;
        d[i] = 0;
    }
    while (q--)
    {
        int op;
        ll u, v, k;
        cin >> op >> u;
        if (op == 1)
        {
            cin >> v >> k;
            if (find(u) != find(v))
            {
                cout << "OK" << endl;
                merge(u, v, k);
            }
            else
            {
                if (d[u] - d[v] != k)
                {
                    cout << "CONTRADICTION" << endl;
                }
                else
                {
                    cout << "OK" << endl;
                }
            }
        }
        else if (op == 2)
        {
            cin >> k;
            if (find(0) != find(u))
            {
                cout << "OK" << endl;
                merge(u, 0, k);
            }
            else
            {
                if (d[u] - d[0] != k)
                {
                    cout << "CONTRADICTION" << endl;
                }
                else
                {
                    cout << "OK" << endl;
                }
            }
        }
        else
        {
            cin >> v;
            if (find(u) != find(v))
            {
                cout << "UNKNOWN" << endl;
            }
            else
            {
                cout << d[u] - d[v] << endl;
            }
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
>其实题目最难的可能就是这个merge函数了，为什么是这样求呢？

<img width="1254" height="301" alt="Image" src="https://github.com/user-attachments/assets/2ec9c8d9-0958-4741-8248-feaebf3b316c" />

>其实你也可以自己画图，本质上就是把一个点走一圈距离为0，然后解方程求出某段特定的距离就好，没必要强行记住，写题目的时候推导就好，而且记住的下次也不一定会是这样，不如画图推导。