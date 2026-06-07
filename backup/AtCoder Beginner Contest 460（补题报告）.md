[AtCoder Beginner Contest 461](https://atcoder.jp/contests/abc461)

E - x + y ≡ x + y

问题陈述



对于正整数 $a$ 和 $b$ ，定义 $\mathrm{concat}(a, b)$ 为依次写入 $a$ 和 $b$ 形成的整数。 $\mathrm{concat}(a, b)$ 的正式定义如下。



—设 $A$ 和 $B$ 分别是由 $a$ 和 $b$ 写成的十进制字符串。设 $C$ 为由 $A$ 和 $B$ 按此顺序连接而成的字符串。 $C$ 的值被解释为十进制的整数为 $\mathrm{concat}(a, b)$ 。



例如，如果 $a = 123$ 和 $b = 45$ ，则 $\mathrm{concat}(a, b) = 12345$ 。



给定正整数 $N$ 和 $M$ 。

求不大于 $N$ 的正整数对 $(x, y)$ 的模 $998244353$ ，使 $\mathrm{concat}(x, y) \equiv x + y \pmod{M}$ 。



给你 $T$ 个测试用例；解决每一个问题。

# # #约束



—— $1 \leq T \leq 10^4$

—— $1 \leq N \leq 10^{18}$

—— $2 \leq M \leq 10^9$

—所有输入值均为整数。

思路:concat(x,y)=x*10^len(y)+y≡(x+y) %m 可以转化为x*(10^len(y)-1)%m=0,把(10^len(y)-1)看成c，那么就是x*c%m==0，设g=gcd(c,m)，我们可以知道x的上限其实是n/（m/g）向下取整 下限是1，那么我们可以知道x的个数，我们枚举y的位数，也可以知道在当前位数情况下符合条件的数量，答案就是求累乘的和就行，注意取模。

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
// #define lc(p) tr[p].lc
// #define rc(p) tr[p].rc
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x) & (-x))
#define mem(a, x) memset(a, x, sizeof a)
const double eps = 1e-5;
const int N = 1e5 + 10, M = 2 * N, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const ll base1 = 131, base2 = 13331;
const double PI = acos(-1.0);
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template <typename T>
bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }
mt19937_64 rng(chrono::steady_clock::now().time_since_epoch().count());
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
    ll n, m;
    cin >> n >> m;
    ll res = 0;
    ull pw = 1;
    for (ll len = 1; len <= 19; len++)
    {
        pw *= 10;
        ull L = pw / 10;
        ull R = min((ull)n, pw - 1);
        if (L > R)
            break;
        ll p = (qmi(10, len, m) - 1 + m) % m;
        ll g = gcd(p, m);
        ll cx = n / (m / g);
        ll cy = R - L + 1;
        res = (res + (cx % Md3) * (cy % Md3)) % Md3;
    }
    cout << res << endl;
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

## F - Farthest Pair Query

问题陈述



有一个顶点为 $N$ 的树。顶点编号为 $1, 2, \ldots, N$ ，第 $i$ 条边连接顶点 $U_i$ 和 $V_i$ 。



最初，所有顶点都涂成黑色。



按顺序处理下列形式的 $Q$ 查询，并为每个查询找到答案。



—给出整数 $x$ $(1 \leq x \leq N)$ 。如果顶点 $x$ 为白色，则将其重涂为黑色；如果顶点 $x$ 是黑色的，重新涂成白色。然后，找出两个黑色顶点之间的最大距离。这里，树上两个顶点之间的距离是它们之间简单路径上的边数。



在给定的输入中，在按顺序处理查询时，总是至少有两个黑色顶点。
# # #约束



—— $3 \leq N \leq 10^5$

—— $1 \leq U_i, V_i \leq N$

-给定的图是一个树。

—— $1 \leq Q \leq 10^5$

—对于每个查询， $1 \leq x \leq N$ 。

-总是有至少两个黑色顶点。

—所有输入值均为整数。

思考：首先得知道一个结论
树的直径合并定理【前提条件】在一棵树上，有两个完全没有任何交集的点集，我们叫它集合 $X$ 和集合 $Y$。假设集合 $X$ 里离得最远的两个点（即 $X$ 的直径端点）是 $A$ 和 $B$。假设集合 $Y$ 里离得最远的两个点（即 $Y$ 的直径端点）是 $C$ 和 $D$。【核心结论】现在我们要把集合 $X$ 和集合 $Y$ 合并成一个大集合 $Z$ ($Z = X \cup Y$)。那么，大集合 $Z$ 的直径端点，必定在 $A, B, C, D$ 这四个点之中产生！

考虑到题目有单点修改和一些查询操作，很难不想到用线段树维护一些信息，由于上面的结论，我们可以想到要维护的区间[l,r]，当然其实是dfn序下产生的区间，我们还得维护区间内最长的黑点的距离，也就是直径，我们用u表示其中的一个黑点的编号，v表示另外一个黑点的编号，剩下的维护d，也就是区间直径的距离。剩下的就是维护过程了，最难的部分可能还是merge部分，即我如何合并两个区间的情况下仍然正确的维护区间的信息呢，显然根据以上结论我们可以知道 两个区间假设都存在黑点的情况下，一共是四个点，一共有C（4，2）中组合，我们枚举之后找到最大的长度，编号，相应的更新信息就行了。
我的线段树不够熟练，写了好一会才写对，当然我觉得我的代码最后那个query是大可不必的，因为答案直接就是tr[1].d就可以了。

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
// #define lc(p) tr[p].lc
// #define rc(p) tr[p].rc
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x) & (-x))
#define mem(a, x) memset(a, x, sizeof a)
const double eps = 1e-5;
const int N = 1e5 + 10, M = 2 * N, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const ll base1 = 131, base2 = 13331;
const double PI = acos(-1.0);
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template <typename T>
bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template <typename T>
bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template <typename T>
void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }
mt19937_64 rng(chrono::steady_clock::now().time_since_epoch().count());
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
int h[N], e[M], ne[M], idx;
int dfn[N], rnk[N], sz[N];
int id;
int dep[N];
int f[N][K];
void add(int a, int b)
{
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

void dfs(int u, int pa)
{
    dfn[u] = ++id;
    rnk[id] = u;
    sz[u] = 1;
    dep[u] = dep[pa] + 1;
    f[u][0] = pa;
    for (int i = 1; i <= 21; i++)
    {
        f[u][i] = f[f[u][i - 1]][i - 1];
    }
    for (int i = h[u]; ~i; i = ne[i])
    {
        int j = e[i];
        if (j == pa)
            continue;
        dfs(j, u);
        sz[u] += sz[j];
    }
}

int lca(int a, int b)
{
    if (dep[a] < dep[b])
        swap(a, b);
    for (int i = 21; i >= 0; i--)
    {
        if (dep[f[a][i]] >= dep[b])
        {
            a = f[a][i];
        }
    }
    if (a == b)
        return a;
    for (int i = 21; i >= 0; i--)
    {
        if (f[a][i] != f[b][i])
        {
            a = f[a][i];
            b = f[b][i];
        }
    }
    return f[a][0];
}

int far(int a, int b)
{
    int r = lca(a, b);
    return dep[a] + dep[b] - 2 * dep[r];
}

struct node
{
    int l, r;
    int u, v;
    int d;
} tr[N << 2];

node merge(node a, node b)
{
    if (!a.u)
        return b;
    if (!b.u)
        return a;

    node res;
    int d[6] = {a.d, b.d, far(a.u, b.u), far(a.u, b.v), far(a.v, b.u), far(a.v, b.v)};
    ll mx = -1, pos = 0;
    for (int i = 0; i < 6; i++)
    {
        if (d[i] > mx)
        {
            mx = d[i];
            pos = i;
        }
    }
    res.d = mx;
    if (pos == 0)
    {
        res.u = a.u, res.v = a.v;
    }
    else if (pos == 1)
    {
        res.u = b.u, res.v = b.v;
    }
    else if (pos == 2)
    {
        res.u = a.u, res.v = b.u;
    }
    else if (pos == 3)
    {
        res.u = a.u, res.v = b.v;
    }
    else if (pos == 4)
    {
        res.u = a.v, res.v = b.u;
    }
    else
    {
        res.u = a.v, res.v = b.v;
    }
    return res;
}

void pushup(int p)
{
    node t = merge(tr[lc], tr[rc]);
    tr[p].u = t.u;
    tr[p].v = t.v;
    tr[p].d = t.d;
}

void build(int p, int l, int r)
{
    tr[p] = {l, r, 0, 0, -1};
    if (l == r)
    {
        tr[p].u = tr[p].v = rnk[l];
        tr[p].d = 0;
        return;
    }
    int mid = (l + r) >> 1;
    build(lc, l, mid);
    build(rc, mid + 1, r);
    pushup(p);
}

void modify(int p, int k)
{
    int l = tr[p].l, r = tr[p].r;
    if (l == k && r == k)
    {
        if (tr[p].u)
        {
            tr[p].u = tr[p].v = 0;
            tr[p].d = -1;
        }
        else
        {
            tr[p].u = tr[p].v = rnk[k];
            tr[p].d = 0;
        }
        return;
    }
    int mid = (l + r) >> 1;
    if (k <= mid)
        modify(lc, k);
    if (k > mid)
        modify(rc, k);
    pushup(p);
}

int query(int p, int x, int y)
{
    int l = tr[p].l, r = tr[p].r;
    if (x <= l && y >= r)
    {
        return tr[p].d;
    }
    int res = 0;
    int mid = (l + r) >> 1;
    if (x <= mid)
        cmax(res, query(lc, x, y));
    if (y > mid)
        cmax(res, query(rc, x, y));
    return res;
}

void init()
{
    idx = 0;
    for (int i = 1; i <= n; i++)
    {
        h[i] = -1;
    }
}

void solve()
{
    cin >> n;
    init();
    for (int i = 1; i < n; i++)
    {
        int u, v;
        cin >> u >> v;
        add(u, v);
        add(v, u);
    }
    dfs(1, 0);
    cin >> q;
    build(1, 1, n);
    while (q--)
    {
        ll x;
        cin >> x;
        modify(1, dfn[x]);
        cout << max(0, query(1, 1, n)) << endl;
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
后面的G题，目前能力有限先补到F吧，前面的A,B,C,D到没什么，D是一个类似观察规律的题目，倒也没有什么启发意义，C是一个排序双指针题目，6分钟写完，中间还debug了一下，发现有一种情况另外一遍的指针忘记增加了，基本上还是没啥问题，前面的都没啥好说的了。
目前从补题来看线段树能力可能还是略显生疏，会加强训练的。
或许等有足够实力了会把最后一题补上，后会有期！