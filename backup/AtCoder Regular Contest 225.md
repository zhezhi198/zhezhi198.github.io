[AtCoder Regular Contest 225](https://atcoder.jp/contests/arc225/tasks/arc225_a)
问题陈述



存在 $N \times N$ 网格 $X$ 。让 $(i,j)$ 表示从顶部开始的第 $i$ 行和从左侧开始的第 $j$ 列的单元格。我们称共享一条边的两个单元格为相邻的。



单元格 $(i,j)$ 被涂上颜色 $X_{i,j}$ 。颜色为 $1,2,3,4$ 之一，**相邻的单元格被涂上不同的颜色**。



您将准备一个 $N \times N$ 网格 $Y$ 并绘制每个单元格。设 $Y_{i,j}$ 表示绘制在 $Y$ 的单元格 $(i,j)$ 上的颜色。



找出一种满足以下条件的绘画方式。



— $Y$ 的每个单元格的颜色是 $1,2,3,4$ 中的一个。**相邻的单元格可能具有相同的颜色

-对于任意两个相邻的单元格 $(i_1,j_1)$ 和 $(i_2,j_2)$ ，如下所述成立。



—如果为 $|X_{i_1,j_1} - X_{i_2,j_2}|=1$ ，则为 $|Y_{i_1,j_1} - Y_{i_2,j_2}|\ge 2$ 。

—如果是 $|X_{i_1,j_1} - X_{i_2,j_2}|\ge2$ ，则为 $|Y_{i_1,j_1} - Y_{i_2,j_2}|\le 1$ 。



可以证明，满足这些条件的绘画方式总是存在的。
# # #约束



—— $2 \le N \le 500$

—— $1 \le X_{i,j} \le 4$

- ** $X$ **的相邻单元**被涂上不同的颜色

—所有输入值均为整数。

### Input

The input is given from Standard Input in the following format:

```
$N$
$X_{1,1}$ $X_{1,2}$ $\ldots$ $X_{1,N}$
$X_{2,1}$ $X_{2,2}$ $\ldots$ $X_{2,N}$
$\vdots$
$X_{N,1}$ $X_{N,2}$ $\ldots$ $X_{N,N}$
```

### Output

Output a $Y$ satisfying the conditions in the following format:

```
$Y_{1,1}$ $Y_{1,2}$ $\ldots$ $Y_{1,N}$
$Y_{2,1}$ $Y_{2,2}$ $\ldots$ $Y_{2,N}$
$\vdots$
$Y_{N,1}$ $Y_{N,2}$ $\ldots$ $Y_{N,N}$
```

思路：我们尝试找到一些相邻的条件去调整赋值，但问题是难以统一具体哪个数赋什么值，如果我们能找到每个数对应的映射关系，或许这个题目难度将大大减小，考虑到颜色只有4种，我们对穷举四种方案的全排列找到了两种映射方式，两种我都是尝试过了，都是正确的，所以剩下的填表即可

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
const int N = 1e3 + 10, M = 2 * N, K = 26;
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
我们通过打表出现1到4的所有数 发现有下面两种映射关系
2 4 1 3
3 1 4 2
*/
int n;
int g[N][N];
int t[N][N];
int arr[N];
bool st[N];
vll ans;
bool check(int arr[])
{
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            t[i][j] = arr[g[i][j]];
        }
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            for (int k = 0; k < 4; k++)
            {
                int nx = i + dx[k], ny = j + dy[k];
                if (nx < 1 || ny < 1 || nx > n || ny > n)
                    continue;
                ll d1 = abs(g[nx][ny] - g[i][j]);
                ll d2 = abs(t[nx][ny] - t[i][j]);
                if (d1 == 1 && d2 >= 2)
                    continue;
                if (d1 >= 2 && d2 <= 1)
                    continue;
                return false;
            }
        }
    }
    return true;
}

void dfs(int x)
{
    if (x > 4)
    {
        if (check(arr))
        {
            for (int i = 1; i <= 4; i++)
            {
                ans.push_back(arr[i]);
            }
        }
        return;
    }

    for (int i = 1; i <= 4; i++)
    {
        if (!st[i])
        {
            arr[x] = i;
            st[i] = true;
            dfs(x + 1);
            arr[x] = 0;
            st[i] = false;
        }
    }
}

void solve()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            cin >> g[i][j];
        }
    }
    // dfs(1);
    // for (auto x : ans)
    //     cout << x << " ";
    int f[5] = {0, 2, 4, 1, 3};
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            cout << f[g[i][j]] << " ";
        }
        cout << endl;
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
问题陈述



存在一个长度为 $N$ 的整数序列 $A$ 。 $A$ 的每个元素都是 $0$ 或 $1$ 。



爱丽丝和鲍勃玩一个游戏。从Alice开始，它们轮流执行以下操作。



—选择 $A$ 中一个或多个为 $1$ 的元素，设置为 $0$ 。在这里，禁止同时选择相邻元素。



最先无法执行操作的玩家输了。



当两名玩家都达到最佳状态时，确定哪名玩家获胜。



给你 $T$ 个测试用例；每个都解出来。

# # #约束



—— $1 \le T \le 10^5$

—— $1 \le N \le 2\times 10^5$

- $A_i = 0$ 或 $A_i = 1$ 。

—所有测试用例 $N$ 之和不超过 $2\times 10^5$ 。

—所有输入值均为整数。

### Input

The input is given from Standard Input in the following format:

```
$T$
$\text{case}_1$
$\text{case}_2$
$\vdots$
$\text{case}_T$
```

Each case is given in the following format:

```
$N$
$A_1$ $A_2$ $\cdots$ $A_N$
```
# # #输出



输出 $T$ 行。 $i$ 第一行应该包含 `Alice` ，如果Alice赢了 $\text{case}_i$ ，如果Bob赢了 `Bob` 。

思路：从必败态找到启发，首先我们思考什么情况是必败态，先得了解清楚游戏规则，我们对应相邻位置的1，我们只能取单独的一个或者都不取，但是都不取是不是意味着在这段连续的1中你没有操作，那么显然启发我们当序列全是0或者1的连续段长度都是2，那么我们总可以在第二次操作把必败态转移给对方，这样显然，加上一些博弈的模拟，我们可以得知这是正确的。
所以我们得出的结论是 Bob要赢 无非是 全0 或者 有1的连续段必须长度全为2
否则Alice赢。

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
    ll n;
    cin >> n;
    vll a(n + 1, 0);
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    vll id;
    ll cnt = 0;
    for (int i = 1; i <= n; i++)
    {
        if (a[i] == 1)
        {
            cnt++;
        }
        else
        {
            if (cnt)
            {
                id.push_back(cnt);
            }
            cnt = 0;
        }
    }
    if (cnt)
        id.push_back(cnt);
    bool ck = false;
    if (id.size() == 0)
    {
        ck = false;
    }
    for (int i = 0; i < id.size(); i++)
    {
        ll x = id[i];
        if (x != 2)
        {
            ck = true;
            break;
        }
    }
    cout << (ck ? "Alice" : "Bob") << endl;
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
问题陈述



给你一个简单的连通无向图 $G$ ，有 $N$ 顶点和 $M$ 边。边 $i$ 连接顶点 $a_i$ 和 $b_i$ ，权值 $c_i$ 。这里，每条边的权值为 $0$ 或 $1$ 。



你得到一个非负整数 $K$ 。判断是否存在 $G$ 的生成树，使得组成生成树的边的权值之和恰好为 $K$ ，如果存在，就找到一个。



给你 $T$ 个测试用例；每个都解出来。

# # #约束



—— $1 \le T \le 10^5$

—— $2 \le N \le 2\times 10^5$

—— $N-1 \le M \le \min\left(\frac{N(N-1)}{2}, 2\times 10^5\right)$

—— $0 \le K \le N-1$

—— $1 \le a_i,b_i \le N$

- $c_i=0$ 或 $c_i=1$ 。

—图 $G$ 是简单且连通的。

—所有测试用例 $N$ 之和不超过 $2\times 10^5$ 。

—所有测试用例 $M$ 的和最多为 $2\times 10^5$ 。

—所有输入值均为整数。
# # #输入



输入来自标准输入，格式如下：



`` `
$T$
$\text{case}_1$
$\text{case}_2$
$\vdots$
$\text{case}_T$
` ``



每宗个案的格式如下：



`` `
$N$ $M$ $K$
$a_1$ $b_1$ $c_1$
$a_2$ $b_2$ $c_2$
$\vdots$
$a_M$ $b_M$ $c_M$
` `` 
# # #输出



输出 $T$ 行。 $i$ \第一行应该包含 $\text{case}_i$ 的答案。



如果不存在满足条件的生成树，则输出 `-1` 。



否则，设 $x_1,x_2,\cdots,x_{N-1}$ 为这种情况下构成生成树的边的个数，并以如下格式输出：



`` `
$x_1$ $x_2$ $\cdots$ $x_{N-1}$
` ``



$x_1,x_2,\cdots,x_{N-1}$ 可以是任意顺序。边号对应于每种情况下的输入顺序。如果存在多个解决方案，则接受其中任何一个。

思路：先说题意..首先题目给的k是我们要选的1的边的数量，看能不能选k条1的边构造出一个最小生成数，并把生成树每条边的编号存下来输出，如果不行那么输出-1.首先我们要知道可以不可以那么我们可以想，能否通过某种方式我们得到构造生成树所需1的边的一个mx 和mn呢，如果k介于两者之间，那么显然意味着可能性存在，如果都不在范围内，那么显然不可能存在，输出-1.
那么问题转化为了两个子问题：
问题1：如何求出所需1的边的范围。
问题2：在求出问题1后我如何输出我选那些边可以构成。
先说问题1，在kruskal算法或者并查集算法中我们知道，首先每个点是单独的集合，我们考虑把边分为两类，一类是0边，一类是1边，我们在先让0边合并，可以得到一个或者多个连通块，这些连通块需要1边去连通构成生成树，这时可能有人会问，0边那么多条，我们不加约束的让这些边合并，最后的连通块都是一个样子吗，显然是的，至少每个点连通块内部是一致的，连通块的个数也是固定的，所以并不会产生较大的影响，这样我们可以得到最小所需k的数量。反过来先连通1的边再连通0，就可以得到最大的1的边的数量，问题1解决，想不清楚的话，并查集和图论知识没过关。
再说问题2：既然这时要满足k一定要在范围内，那么意味着最小的mn条1的边必选，剩下我们从1的边选，知道选1的边满足k条即可，最后判断一下是不是能构成生成树即可。

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
const int N = 2e5 + 10, M = 2 * N, K = 26;
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

int n, m, k;
int p[N];
ll cnt = 0;
vll ans;
struct node
{
    int u, v, w, id;
} tr[N];

bool cmp(node &x, node &y)
{
    return x.w > y.w;
}

int find(int x)
{
    if (p[x] != x)
        p[x] = find(p[x]);
    return p[x];
}

void merge(int a, int b)
{
    int pa = find(a), pb = find(b);
    if (pa != pb)
    {
        p[pa] = pb;
    }
}

void solve()
{
    cin >> n >> m >> k;
    ans.clear();
    cnt = 0;
    vll e0, e1;
    vll ans;
    for (int i = 1; i <= m; i++)
    {
        int u, v, w;
        cin >> u >> v >> w;
        tr[i] = {u, v, w, i};
        if (w == 0)
            e0.push_back(i);
        else
        {
            e1.push_back(i);
        }
    }
    for (int i = 1; i <= n; i++)
    {
        p[i] = i;
    }
    ll mn1 = 0, mx1 = 0;
    for (auto x : e0)
    {
        auto [u, v, w, id] = tr[x];
        merge(u, v);
    }
    for (auto x : e1)
    {
        auto [u, v, w, id] = tr[x];
        int pu = find(u), pv = find(v);
        if (pu != pv)
        {
            mn1++;
            ans.push_back(id);
            merge(u, v);
        }
    }
    bool ok1 = false;
    ll c1 = 0;
    for (int i = 1; i <= n; i++)
    {
        if (p[i] == i)
        {
            c1++;
        }
    }
    if (c1 == 1)
        ok1 = true;
    for (int i = 1; i <= n; i++)
    {
        p[i] = i;
    }
    for (auto x : e1)
    {
        auto [u, v, w, id] = tr[x];
        int pu = find(u), pv = find(v);
        if (pu != pv)
        {
            mx1++;
            merge(u, v);
        }
    }
    for (auto x : e0)
    {
        auto [u, v, w, id] = tr[x];
        merge(u, v);
    }
    bool ok2 = false;
    ll c2 = 0;
    for (int i = 1; i <= n; i++)
    {
        if (p[i] == i)
        {
            c2++;
        }
    }
    if (c2 == 1)
        ok2 = true;
    if (!ok1 || !ok2)
    {
        cout << -1 << endl;
        return;
    }
    if (k < mn1 || k > mx1)
    {
        cout << -1 << endl;
        return;
    }
    for (int i = 1; i <= n; i++)
        p[i] = i;
    ll now = 0;
    for (auto x : ans)
    {
        auto [u, v, w, id] = tr[x];
        merge(u, v);
        now++;
    }
    sort(tr + 1, tr + m + 1, cmp);
    for (int i = 1; i <= m; i++)
    {
        auto [u, v, w, id] = tr[i];
        int pu = find(u), pv = find(v);
        if (pu != pv)
        {
            if (w == 1)
            {
                if (now < k)
                {
                    merge(u, v);
                    now++;
                    ans.push_back(id);
                }
            }
            else
            {
                merge(u, v);
                ans.push_back(id);
            }
        }
    }
    bool ok = false;
    ll c = 0;
    for (int i = 1; i <= n; i++)
    {
        if (p[i] == i)
            c++;
    }
    if (c == 1)
        ok = true;
    if (ok)
    {
        for (auto x : ans)
            cout << x << " ";
        cout << endl;
    }
    else
    {
        cout << -1 << endl;
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
问题陈述



**这个问题的设置与问题E类似，但操作的成本不同



存在 $(1,2,\ldots,N)$ 的一个排列 $P$ 。 $P$ 可以执行如下操作。



—选择满足 $1 \le i &lt; j \le N$ 的整数 $i$ 和 $j$ 。这里， $P_k=k$ 必须对满足 $i &lt; k &lt; j$ 的每一个整数 $k$ 都成立。然后，交换 $P_i$ 和 $P_j$ 。

此操作产生的**开销为 $\boldsymbol{j-i}$ **。



注意，如果 $i+1=j$ ，则没有整数 $k$ 满足 $i&lt;k&lt;j$ ，因此该操作始终可以执行。因此，总是存在一个将 $P$ 按升序排序的操作序列。



求将 $P$ 按升序排序所需的最小总代价。
# # #约束



—— $2 \le N \le 5\times 10^5$

—— $1 \le P_i \le N$

- $P$ 是 $(1,2,\ldots,N)$ 的一个排列。

—所有输入值均为整数。
# # #输出



输出答案。
###输出示例



`` `
6
` ``



例如，通过执行以下两个操作，可以将 $P$ 按升序排序，总开销为 $6$ 。



—第一次操作：选择 $i=4, j=5$ ，交换 $P_4, P_5$ 。这需要 $1$ 。

—第二次操作：选择 $i=1, j=6$ ，交换 $P_1, P_6$ 。这需要 $5$ 。



$P$ 不可能在代价小于 $6$ 的情况下按升序排序，所以答案是 $6$ 。

思路：我们可以得知每个点到目标距离d=p[i]-i 对于每个点都是这样，我们可以求一个总和，但是呢显然并不是每个点都要一步一步去交换，题目有一个快捷的方法能让从i到j的代价减少一半，这时我们抛出一个问题就是是不是每个点或者每对点都可以走这个快捷呢，显然是可以的。
 首先我们知道当一个点想移动到正确位置要往右移动的时候，右边必然出现一点要往左边移动，那么我们可以选择最后往右移动的点和这个点之后第一个要移动的点交换，显然可以使得一个交换到正确的位置，代价就是快捷的代码。可以用大量例子去证明，得出来全是正确的。
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
    ll n;
    cin >> n;
    vll a(n + 1, 0), p(n + 2, 0);
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
        p[a[i]] = i;
    }
    ll ans = 0;
    for (int i = 1; i <= n; i++)
    {
        ans += abs(p[a[i]] - a[i]);
    }
    cout << ans / 2 << endl;
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

问题陈述



这个问题的设置与问题D类似，但操作的成本不同



存在 $(1,2,\ldots,N)$ 的一个排列 $P$ 。 $P$ 可以执行如下操作。



—选择满足 $1 \le i &lt; j \le N$ 的整数 $i$ 和 $j$ 。这里， $P_k=k$ 必须适用于所有满足 $i &lt; k &lt; j$ 的整数 $k$ 。然后，交换 $P_i$ 和 $P_j$ 。

此操作产生的**成本为 $\boldsymbol{1}$ **。



请注意，如果{99578092}，则不存在满足 $i&lt;k&lt;j$ 的整数 $k$ ，因此始终可以执行该操作。因此，总是存在一个将 $P$ 按升序排序的操作序列。



求将 $P$ 按升序排序所需的最小总成本。

# # #约束



—— $2 \le N \le 5\times 10^5$

—— $1 \le P_i \le N$

- $P$ 是 $(1,2,\ldots,N)$ 的一个排列。

—所有输入值均为整数。

# # #输入



输入来自标准输入，格式如下：



`` `
$N$
$P_1$ $P_2$ $\ldots$ $P_N$
` `` 
# # #输出



输出答案。
思路：结论就是pi-i -对于逆序对的数量。
如何证明的想清楚就好

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
const int N = 5e5 + 10, M = 2 * N, K = 26;
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
ll n;
ll a[N], p[N];
ll tr[N];
ll s[N];
void modify(int k, int x)
{
    for (int i = k; i <= n; i += lowbit(i))
    {
        tr[i] += x;
    }
}

ll query(int k)
{
    ll res = 0;
    for (int i = k; i; i -= lowbit(i))
    {
        res += tr[i];
    }
    return res;
}

void init()
{
    for (int i = 1; i <= n; i++)
    {
        tr[i] = 0;
        s[i] = 0;
    }
}

void solve()
{
    cin >> n;
    init();
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
        p[a[i]] = i;
    }
    for (int i = 1; i <= n; i++)
    {
        ll x = a[i];
        s[i] = i - query(x - 1) - 1;
        modify(x, 1);
    }
    ll ans = 0;
    for (int i = 1; i <= n; i++)
    {
        ans += abs(p[a[i]] - a[i]);
        ans -= s[i];
    }
    cout << ans << endl;
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