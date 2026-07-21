[Codeforces Round 1057 (Div. 2) ](https://codeforces.com/contest/2153)

# CF2153A Circle of Apple Trees

## 题目描述

有 $n$ 棵苹果树围成一个圆圈。每棵树上都有一个苹果，第 $i$ 棵树上的苹果美丽值为 $b_i$，其中 $1 \le i \le n$。你开始站在第 1 棵树前。

在每棵树前，你可以选择吃掉该树上的苹果，或者跳过不吃。每做出选择后，你会移动到下一棵树：从第 $i$ 棵树前往第 $i+1$ 棵树（$1 \le i \le n-1$），从第 $n$ 棵树则回到第 1 棵树。你会这样不断循环地经过这些树。

但你有一个特别的限制：只有当当前苹果的美丽值严格大于你上一次吃掉的苹果的美丽值时，你才能吃下去。例如，若 $b = [2, 1, 2, 3]$，你若在第 1 棵树吃了苹果（美丽值 $2$），则不能吃第 2、3 棵树的苹果，因为它们的美丽值都不大于 $2$。但你可以在第 4 棵树吃下苹果，因为 $b_4 = 3 > 2$。

注意，每遇到一个苹果时你都可以选择先跳过不吃，之后某轮循环再次遇到时再选择是否吃掉。

你的任务是，若你每一步都做出最优决策，最多能吃到多少个苹果。

## 输入格式

每组测试包含多个测试用例。第一行包含整数 $t$（$1 \le t \le 500$），表示测试用例数。

每组测试用例第一行包含一个整数 $n$（$1 \le n \le 100$），表示苹果树数量。

第二行包含 $n$ 个整数 $b_1, b_2, \ldots, b_n$（$1 \le b_i \le n$），表示每棵树上的苹果美丽值。

注意，所有测试用例中 $n$ 的总和没有额外限制。

## 输出格式

对每个测试用例，输出一个整数，表示你最多可以吃到的苹果数量。

## 输入输出样例 #1

### 输入 #1

```
3
4
2 2 2 2
5
1 4 5 1 2
6
5 4 2 1 2 3
```

### 输出 #1

```
1
4
5
```

## 说明/提示

在第一个样例中，所有苹果的美丽值都相同，无论你先吃哪一个，之后都无法再吃其它任何苹果。因此最多只能吃 1 个。

在第二个样例中，你可以按照如下方式吃掉 4 个苹果：

- 在第 1 棵树前跳过。
- 在第 2 棵树前跳过。
- 在第 3 棵树前跳过。
- 在第 4 棵树吃掉苹果（美丽值 $1$）。
- 在第 5 棵树吃掉苹果（美丽值 $2$）。
- 在第 1 棵树前跳过。由于第 1 棵树的美丽值（$b_1=1$）不大于上次吃掉的苹果美丽值（$b_5=2$），因此不能吃。
- 在第 2 棵树吃掉苹果（美丽值 $4$）。
- 在第 3 棵树吃掉苹果（美丽值 $5$）。

可以证明你无法吃到 5 个苹果。因此最多只能吃 4 个。

由 ChatGPT 5 翻译

思路:题目并没有说绕一圈就停止，而是说吃到不能再吃就停止，能吃的规则是吃的东西是严格单调递增的。那么我们考虑从小到大的最长上升段的长度即可。

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
    set<ll> st;
    for (int i = 1; i <= n; i++)
    {
        ll x;
        cin >> x;
        st.insert(x);
    }
    cout << st.size() << endl;
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
# CF2153B Bitwise Reversion

## 题目描述

给定三个非负整数 $x$，$y$ 和 $z$，判断是否存在三个非负整数 $a$、$b$、$c$，满足以下三个条件：

- $a \mathbin{\&} b = x$
- $b \mathbin{\&} c = y$
- $a \mathbin{\&} c = z$

其中 $\mathbin{\&}$ 表示[按位与运算](https://en.wikipedia.org/wiki/Bitwise_operation#AND)。

## 输入格式

输入包含多组测试数据。第一行包含一个整数 $t$（$1 \leq t \leq 10^4$），表示测试数据的组数。

接下来每组测试数据占一行，每行包含三个整数 $x$、$y$ 和 $z$（$0 \leq x, y, z \leq 10^9$），分别表示 $a \mathbin{\&} b$、$b \mathbin{\&} c$ 和 $a \mathbin{\&} c$ 的目标值。

## 输出格式

对于每组测试数据，如果存在符合条件的三个非负整数 $a$、$b$、$c$，输出 "YES"；否则输出 "NO"。

输出可以使用任意大小写形式，例如 "yEs"、"yes"、"Yes" 和 "YES" 都被认为是正答。

## 输入输出样例 #1

### 输入 #1

```
5
1 1 1
3 2 6
4 8 12
9 10 12
12730 3088 28130
```

### 输出 #1

```
YES
YES
NO
YES
NO
```

## 说明/提示

在第一个测试样例中，$a=3$，$b=5$，$c=9$ 满足条件：$3 \mathbin{\&} 5 = 1$，$5 \mathbin{\&} 9 = 1$，$3 \mathbin{\&} 9 = 1$。

在第二个测试样例中，$a=7$，$b=3$，$c=22$ 满足条件：$7 \mathbin{\&} 3 = 3$，$3 \mathbin{\&} 22 = 2$，$7 \mathbin{\&} 22 = 6$。

在第三个测试样例中，可以证明不存在非负整数 $a$、$b$、$c$ 使得 $a \mathbin{\&} b = 4$，$b \mathbin{\&} c = 8$，$a \mathbin{\&} c = 12$。

由 ChatGPT 5 翻译

思路：题目给出了x,y,z，他们分别是a&b,b&c,a&c的结果，这意味着a和b至少要有x对应2进制中1的每一位,b和c至少要有y对应二进制的每一位，以此类推，那么我们可以得到一个至少满足a&b=x,b&c=y,a&c=z的一个基本条件，我们只需最后检查一下是否能满足a&b=x,b&c=y,a&c=z即可。

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
    ll x, y, z;
    cin >> x >> y >> z;
    // cout<<log2(1e9+10)<<endl;
    ll a = 0, b = 0, c = 0;
    for (int k = 30; k >= 0; k--)
    {
        if ((x >> k) & 1)
        {
            a |= ((ll)1 << k);
            b |= ((ll)1 << k);
        }
    }
    for (int k = 30; k >= 0; k--)
    {
        if ((y >> k) & 1)
        {
            b |= ((ll)1 << k);
            c |= ((ll)1 << k);
        }
    }
    for (int k = 30; k >= 0; k--)
    {
        if ((z >> k) & 1)
        {
            a |= ((ll)1 << k);
            c |= ((ll)1 << k);
        }
    }
    if ((a & b) == x && (b & c) == y && (a & c) == z)
    {
        cout << "YES" << endl;
    }
    else
    {
        cout << "NO" << endl;
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
# CF2153C Symmetrical Polygons

## 题目描述

给定 $n$ 根木棍，第 $i$ 根木棍的长度为 $a_i$。你需要选择这些木棍的一个非空子集，并将它们作为一个多边形的边。每根被选中的木棍必须被完整地作为一个边使用，不能将两根或更多木棍端对端拼接以组成更长的边。

你的目标是用这些木棍组成立一个满足如下条件的多边形：

- 对称（Symmetrical）：存在一条对称轴，使得沿这条轴折叠时多边形的两半完全重合。
- 严格凸（Strictly convex）：所有的内角都严格小于 $180^\circ$。
- 非退化（Non-degenerate）：没有两条相邻的边部分或完全重合，没有零长度的边，且没有 $180^\circ$ 的角。

在所有可以组成立如上所述多边形的方案中，求最大可能的周长（即所有边长之和）。如果无法组成合法的多边形，则输出 $0$。

## 输入格式

每组测试包括多组测试数据。第一行包含一个整数 $t$（$1 \le t \le 10^4$），表示测试数据组数。

每组测试数据的第一行包含一个整数 $n$（$3 \le n \le 2 \cdot 10^5$），表示木棍的数量。

第二行包含 $n$ 个整数 $a_1, a_2, \ldots, a_n$（$1 \le a_i \le 10^9$），表示每根木棍的长度。

保证所有测试数据中 $n$ 的总和不超过 $2 \cdot 10^5$。

## 输出格式

对于每组测试数据，输出一个整数，表示可组成立如上所述非退化、对称且严格凸多边形的最大可能周长。如果无法组成立合法多边形，则输出 $0$。

## 输入输出样例 #1

### 输入 #1

```
5
3
5 5 7
3
4 5 7
3
5 5 10
7
4 3 5 1 5 3 3
4
2 3 5 7
```

### 输出 #1

```
17
0
0
23
0
```

## 说明/提示

在第一个测试用例中，你可以使用所有三根木棍构成一个等腰三角形。它沿着垂直虚线对称（见左图）。周长等于三条边之和：$5 + 5 + 7 = 17$。

在第二个测试用例中，用所有三根木棍围成的三角形不是对称的（见右图）。可以证明，无法用任意非空子集的木棍构成对称、非退化的凸多边形。

在第三个测试用例中，无法构成非退化多边形。若用三条边全部参与，长度为 $5$ 的两条边与长度为 $10$ 的边重合，形成了一条零面积的直线。

在第四个测试用例中，我们可以用三根长度为 $3$ 的木棍、两根长度为 $5$ 的木棍和一根长度为 $4$ 的木棍（见左图）构成一个对称的凸多边形。长度为 $1$ 的最后一根木棍不能被包括，否则得到的多边形将不再对称（见右图）。

在第五个测试用例中，不允许将长度为 $2$ 的木棍和 $3$ 的木棍连接形成长度为 $5$ 的木棍（这样就变成第一个测试用例的情形）。可以证明，无法用任意非空子集的木棍构成对称、非退化的凸多边形。

由 ChatGPT 5 翻译

思路：
首先得知道一个重要的结论：要构成一个多边形，得满足里面的边至少是3，其次呢，多边形里面的最长边*2<多边形的总周长(结论结尾证明)。
考虑到题目要求我们构成的多边形是对称的，且不存在小木棍的拼接是延续同方向拼接，但是可以舍弃边，那么边的种类可以分为两种，其一是构成对称的边，另外一种是对称之后剩余的边或者根本无法构成对称的边，这个我们称为落单边。回想构成多边形的要求，显然我们的对称边全是可以选的，因为他本身以及成对了，只需保证边数>=3即可，剩下的呢 我们考虑单边的贡献，单边如果不选可以对称，如果选一个依然可以对称，2个也是。那么单边的选取范围是[0,3],题目要求周长最大我们只需选择最长的贪心即可，但是不要忘记多边形的约束，舍弃掉一些不合理的可能。

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
    map<ll, ll> cnt;
    vll id;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i], cnt[a[i]]++;
        id.push_back(a[i]);
    }
    sort(all(id));
    id.erase(unique(all(id)), id.end());
    ll m = id.size() - 1;
    ll c1 = 0, c2 = 0;
    vll v;
    ll sum = 0;
    for (auto x : id)
    {
        c1 += cnt[x] % 2;
        c2 += cnt[x] / 2;
    }
    ll mx = 0;
    ll c = c2 * 2;
    for (auto x : id)
    {
        if (cnt[x] >= 2)
        {
            cmax(mx, x);
            sum += (cnt[x] / 2) * 2 * x;
            if (cnt[x] % 2 != 0)
            {
                v.push_back(x);
            }
        }
        else
        {
            v.push_back(x);
        }
    }
    sort(all(v), greater());
    ll ans = 0;
    if (c >= 3 && mx * 2 < sum)
    {
        ans = sum;
    }

    for (auto x : v)
    {
        ll now = max(mx, x);
        if (c + 1 >= 3 && now * 2 < sum + x)
        {
            cmax(ans, sum + x);
            break;
        }
    }

    for (int i = 0; i + 1 < v.size(); i++)
    {
        ll x1 = v[i], x2 = v[i + 1];
        ll now = max(mx, x1);
        if (c + 2 >= 3 && now * 2 < sum + x1 + x2)
        {
            cmax(ans, sum + x1 + x2);
            break;
        }
    }
    cout << ans << endl;
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
### 另外值得注意的一点是博主第一次交的时候Wa了，原因是 for (int i = 0; i + 1 < v.size(); i++)，for(int i=0;i<v.size()-1;i++) 你们觉得这两个哪个是正确的呢，还是都可以呢。如果有一个不可以是什么情况呢？？？ 
这份排版已经为你做好了 Markdown 优化，公式也全部使用了标准的 LaTeX 语法，你可以直接一键复制到你的 GitHub 博客里。

这里补充了完整的严谨表述，并加上了在算法竞赛中应用的小结，非常适合作为题解博客的数理基础部分：

---

## 定理：多边形构成条件（广义三角形不等式）

### 结论

给定 $n$ 条线段，长度分别为 $a_1, a_2, \dots, a_n$，令其总周长为 $S = \sum_{i=1}^n a_i$，且其中的最长边为 $a_{\max}$。

这 $n$ 条线段能够首尾相连，构成一个非退化（即面积严格大于 $0$）的 $n$ 边形，当且仅当满足以下不等式：


$$2 \times a_{\max} < S$$

将其展开，该条件等价于**最长边严格小于其余所有边之和**：


$$a_{\max} < S - a_{\max}$$

### 证明过程（基于向量模型）

**1. 建立向量模型**
假设这 $n$ 条线段已经首尾相连构成了一个非退化的 $n$ 边形。我们将每一条边定向，视为向量 $\vec{v_1}, \vec{v_2}, \dots, \vec{v_n}$，其方向为绕多边形一周的方向（统一逆时针或顺时针）。
此时，每个向量的模长即为对应的边长：$\vert{}\vec{v_i}\vert{} = a_i$。

**2. 闭合性转化**
因为多边形是闭合的，从起点出发沿着边走一圈最终会回到起点，所以所有向量的位移总和必然是零向量：


$$\sum_{i=1}^n \vec{v_i} = \vec{0}$$

**3. 分离最长边**
不妨设 $\vec{v_{\max}}$ 为长度最长的那条边对应的向量。将其单独移至等式的另一侧：


$$\sum_{i \neq \max} \vec{v_i} = -\vec{v_{\max}}$$

**4. 应用向量三角不等式**
对等式两边同时取模长：


$$\left\vert{} \sum_{i \neq \max} \vec{v_i} \right\vert{} = \vert{}-\vec{v_{\max}}\vert{} = a_{\max}$$

根据多个向量相加的三角不等式（一条折线的直线距离，总是小于等于各段折线长度之和），我们有：


$$\left\vert{} \sum_{i \neq \max} \vec{v_i} \right\vert{} \le \sum_{i \neq \max} \vert{}\vec{v_i}\vert{}$$

因为该多边形是**非退化**的，这意味着其余的边不可能与最长边完全处于同一条直线上（否则多边形会被压扁，面积为 $0$）。因此，这里的等号不成立，必须取**严格小于号**：


$$a_{\max} < \sum_{i \neq \max} a_i$$

**5. 结论变形**
在不等式两边同时加上 $a_{\max}$，即可得到：


$$2 \times a_{\max} < \sum_{i=1}^n a_i$$


即：


$$2 \times a_{\max} < S$$


必要性证明完毕。（充分性的构造证明较繁琐，但在算法判定中，掌握该充要条件已经完全足够）。

### 在算法竞赛中的应用

在 ACM/ICPC 或 OI 中处理几何判定题时，这个性质极其重要。它将复杂的“多边形空间构造判定”，降维成了单纯的**序列极值与前缀和判定**。

当你需要从一个数组中选取数字来构成多边形时，只需维护集合的 `sum` 和 `max`。这种代数转化非常适合配合排序、双指针或是动态规划（DP）来做状态转移，从而将高复杂度暴力求解优化到 $O(N \log N)$ 甚至 $O(N)$。

---
# CF2153D Not Alone

## 题目描述

一个长度为 $m$ 的环形数组 $b$ 被称为“优美”，如果其中每个元素至少有一个相邻元素等于它。形式化地，对于每个 $1\le i\le m$，必须满足以下条件之一：$b_i = b_{(i+m-2)\bmod m + 1}$，或 $b_i = b_{i\bmod m + 1}$，其中 $x \bmod y$ 表示 $x$ 除以 $y$ 的余数。

现在给定一个长度为 $n$ 的环形数组 $a$。你可以进行如下操作：每次将 $a$ 中的任意一个元素加 $1$ 或减 $1$。你的任务是计算最少需要多少次操作，才能使数组 $a$ 变成“优美”的环形数组。更正式地说，求在所有优美环形数组 $b$ 中，最小的 $\sum_{i=1}^n |b_i - a_i|$。

$^{\text{∗}}$ 在长度为 $m$ 的环形数组中：

- 对于每个下标 $2\le i\le m - 1$，第 $i$ 个元素的相邻元素分别是第 $i-1$ 和第 $i+1$ 个元素。
- 第 $1$ 个元素的相邻元素分别是第 $2$ 和第 $m$ 个元素。
- 第 $m$ 个元素的相邻元素分别是第 $m-1$ 和第 $1$ 个元素。

## 输入格式

输入包含多组测试用例。第一行为测试用例数 $t$（$1 \le t \le 10^4$）。接下来每组测试用例描述如下：

每组测试用例的第一行包含一个整数 $n$（$3 \le n \le 2\cdot 10^5$），表示数组 $a$ 的长度。

第二行包含 $n$ 个整数 $a_1, a_2, \ldots, a_n$（$1 \le a_i \le 10^9$），表示环形数组 $a$ 的元素。

保证所有测试用例中 $n$ 的总和不超过 $2\cdot 10^5$。

## 输出格式

对于每组测试用例，输出一个整数，表示最少的操作次数，使数组 $a$ 变为优美的环形数组。

## 输入输出样例 #1

### 输入 #1

```
4
5
1 1 1 1 1
4
2 100 99 3
5
2 2 5 9 5
6
1 1 1 2 1 2
```

### 输出 #1

```
0
2
4
1
```

## 说明/提示

在第一个测试用例中，$a$ 的所有元素都相等，因此该环形数组已经是优美的，无需任何操作。

在第二个测试用例中，可以按如下顺序进行操作：

- 将 $a_1$ 加 $1$，此时 $a = [3, 100, 99, 3]$。
- 将 $a_2$ 减 $1$，此时 $a = [3, 99, 99, 3]$。

进行这些操作后，每个元素都至少有一个相邻元素和它相等：

- $a_1$ 与 $a_4$ 相等。
- $a_2$ 与 $a_3$ 相等。
- $a_3$ 与 $a_2$ 相等。
- $a_4$ 与 $a_1$ 相等。

在第三个测试用例中，可以将 $a_4$ 连续减 $4$，此时 $a = [2, 2, 5, 5, 5]$，该数组为优美数组，因为每个元素都有至少一个相邻元素等于自己。

由 ChatGPT 5 翻译

这道题的证明确实是核心。在算法竞赛（尤其是 OI 和 ICPC）中，很多关于“分段贪心”或者“区间修改”的题目，本质上都是通过**三角不等式**将长区间的决策降维到极短区间的决策。

我按照你的排版习惯，帮你把这道题的完整博客补全了。其中“思路”部分我重点梳理了你觉得难讲的**证明过程**和**为什么只需要考虑长度为 2 和 3 的段**，逻辑非常严密且直观，你可以直接复制到你的 GitHub 博客中：

---

# CF2153D Not Alone

## 题目描述

一个长度为 $m$ 的环形数组 $b$ 被称为“优美”，如果其中每个元素至少有一个相邻元素等于它。形式化地，对于每个 $1\le i\le m$，必须满足以下条件之一：$b_i = b_{(i+m-2)\bmod m + 1}$，或 $b_i = b_{i\bmod m + 1}$，其中 $x \bmod y$ 表示 $x$ 除以 $y$ 的余数。

现在给定一个长度为 $n$ 的环形数组 $a$。你可以进行如下操作：每次将 $a$ 中的任意一个元素加 $1$ 或减 $1$。你的任务是计算最少需要多少次操作，才能使数组 $a$ 变成“优美”的环形数组。更正式地说，求在所有优美环形数组 $b$ 中，最小的 $\sum_{i=1}^n \vert{}b_i - a_i\vert{}$。

$^{\text{∗}}$ 在长度为 $m$ 的环形数组中：

* 对于每个下标 $2\le i\le m - 1$，第 $i$ 个元素的相邻元素分别是第 $i-1$ 和第 $i+1$ 个元素。
* 第 $1$ 个元素的相邻元素分别是第 $2$ 和第 $m$ 个元素。
* 第 $m$ 个元素的相邻元素分别是第 $m-1$ 和第 $1$ 个元素。

## 输入格式

输入包含多组测试用例。第一行为测试用例数 $t$（$1 \le t \le 10^4$）。接下来每组测试用例描述如下：

每组测试用例的第一行包含一个整数 $n$（$3 \le n \le 2\cdot 10^5$），表示数组 $a$ 的长度。

第二行包含 $n$ 个整数 $a_1, a_2, \ldots, a_n$（$1 \le a_i \le 10^9$），表示环形数组 $a$ 的元素。

保证所有测试用例中 $n$ 的总和不超过 $2\cdot 10^5$。

## 输出格式

对于每组测试用例，输出一个整数，表示最少的操作次数，使数组 $a$ 变为优美的环形数组。

## 输入输出样例 #1

### 输入 #1

```text
4
5
1 1 1 1 1
4
2 100 99 3
5
2 2 5 9 5
6
1 1 1 2 1 2

```

### 输出 #1

```text
0
2
4
1

```

## 思路

题目要求每个元素至少有一个相邻元素和它相等。这意味着在最终的“优美”数组中，相等的元素会“抱团”。也就是说，整个环形数组一定会被划分为若干个连续的段，**每一段内的元素完全相同，且每一段的长度至少为 2**。

那么这道题的核心难点（也就是 DP 状态设计的依据）来了：**最优解中，我们到底需要考虑多长的段？**

**结论：最优的划分方案中，每一段的长度只能是 2 或者 3。**

**证明如下：**
假设我们划出了一个长度为 $L$（$L \ge 4$）的段，我们需要把这 $L$ 个数全都变成同一个数 $v$。根据绝对值不等式的经典结论，$v$ 应当取这 $L$ 个数的中位数，此时总操作代价为 $\sum \vert{}a_i - v\vert{}$。

我们以 $L = 4$ 为例，设这四个数为 $a_1, a_2, a_3, a_4$。总代价为：


$$\vert{}a_1 - v\vert{} + \vert{}a_2 - v\vert{} + \vert{}a_3 - v\vert{} + \vert{}a_4 - v\vert{}$$


根据三角不等式（$\vert{}x\vert{} + \vert{}y\vert{} \ge \vert{}x - y\vert{}$），我们知道：


$$\vert{}a_1 - v\vert{} + \vert{}a_2 - v\vert{} \ge \vert{}a_1 - a_2\vert{}$$

$$\vert{}a_3 - v\vert{} + \vert{}a_4 - v\vert{} \ge \vert{}a_3 - a_4\vert{}$$


这说明，把 4 个数强行变成同一个数的代价，**必然大于或等于**将其拆分成两个“长度为 2 的段”的代价（即前两个数内部匹配，后两个数内部匹配）。

推而广之，任何长度 $L \ge 4$ 的整数，都可以被拆分为若干个 2 和 3 的和（例如 $4=2+2$，$5=2+3$，$6=3+3$）。而且拆分后的总代价**绝对不会变大**。因此，为了求最小代价，我们的 DP 状态只需要转移长度为 2 和 3 的情况即可！

**分段代价的计算：**

1. **长度为 2 的段（元素为 $x, y$）：** 将其变为相等的数，最优策略是变成它们之间的任意值，代价刚好是 $\vert{}x - y\vert{}$。
2. **长度为 3 的段（元素为 $x, y, z$）：** 最优策略是变成这三个数的中位数。总代价是三个数到中位数的距离之和，这在数学上刚好等于 $\max(x, y, z) - \min(x, y, z)$。

**DP 状态转移与环形处理：**
定义 $dp[i]$ 为前 $i$ 个元素划分完毕的最小代价：


$$dp[i] = \min \begin{cases} dp[i-2] + \vert{}a_i - a_{i-1}\vert{} \\ dp[i-3] + \max(a_{i-2}, a_{i-1}, a_i) - \min(a_{i-2}, a_{i-1}, a_i) \end{cases}$$

由于是环形数组，分段的“断点”可以在任意位置。但因为每段最长只有 3，所以无论最优解是怎么分段的，**原数组的第 1、2、3 个位置中，必定存在至少一个断点**。
因此，我们只需将原数组复制一倍拼接在后面，然后分别以第 1、2、3 个元素作为起点，跑 3 遍上述的线性 DP，最后取这三种情况的最小值即可完美解决环形问题。

## 代码

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
    vll a(2 * n + 2, 0);
    for (int i = 1; i <= n; i++)
    {
        ll x;
        cin >> x;
        a[i] = a[i + n] = x;
    }
    vll dp(2 * n + 2, INF);
    dp[0] = 0;
    ll ans = INF;
    for (int i = 2; i <= n; i++)
    {
        if (i >= 2)
        {
            dp[i] = min(dp[i], dp[i - 2] + abs(a[i] - a[i - 1]));
        }
        if (i >= 3)
        {
            dp[i] = min(dp[i], dp[i - 3] + max({a[i - 2], a[i - 1], a[i]}) - min({a[i - 2], a[i - 1], a[i]}));
        }
    }
    cmin(ans, dp[n]);
    for (int i = 1; i <= 2 * n + 1; i++)
        dp[i] = INF;
    dp[0] = 0;
    for (int i = 2; i <= n; i++)
    {
        ll now = i + 1;
        if (i >= 2)
        {
            dp[i] = min(dp[i], dp[i - 2] + abs(a[now] - a[now - 1]));
        }
        if (i >= 3)
        {
            dp[i] = min(dp[i], dp[i - 3] + max({a[now - 2], a[now - 1], a[now]}) - min({a[now - 2], a[now - 1], a[now]}));
        }
    }
    cmin(ans, dp[n]);
    for (int i = 1; i <= 2 * n; i++)
        dp[i] = INF;
    dp[0] = 0;
    for (int i = 2; i <= n; i++)
    {
        ll now = i + 2;
        if (i >= 2)
        {
            dp[i] = min(dp[i], dp[i - 2] + abs(a[now] - a[now - 1]));
        }
        if (i >= 3)
        {
            dp[i] = min(dp[i], dp[i - 3] + max({a[now - 2], a[now - 1], a[now]}) - min({a[now - 2], a[now - 1], a[now]}));
        }
    }
    cmin(ans, dp[n]);
    cout << ans << endl;
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