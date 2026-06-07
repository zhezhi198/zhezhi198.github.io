[AtCoder Beginner Contest 461](https://atcoder.jp/contests/abc461)
A,B题目比较直接，就直接给出代码了。
A
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
    ll x, y;
    cin >> x >> y;
    cout << (x <= y ? "Yes" : "No") << endl;
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
B

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
    vll a(n + 1, 0), b(n + 1, 0);
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    for (int i = 1; i <= n; i++)
        cin >> b[i];
    for (int i = 1; i <= n; i++)
    {
        if (b[a[i]] != i)
        {
            cout << "No" << endl;
            return;
        }
    }
    cout << "Yes" << endl;
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
## C 
问题陈述



有 $N$ 宝石。 $i$ 第1颗宝石的颜色（以整数表示）为 $C_i$ ，其值为 $V_i$ 。



从这些 $N$ 宝石中选择 $K$ 宝石。在这里，所选的宝石必须至少有M不同的颜色。



找到所选宝石的最大可能总价值。（在给定的输入中，这种选择总是可能的。）
# # #约束



—— $1 \leq M \leq K \leq N \leq 2 \times 10^5$

—— $1 \leq C_i \leq N$

—— $1 \leq V_i \leq 10^9$

-存在至少具有不同颜色的宝石。

—所有输入值均为整数。

思路过程：看题目的第一眼以为是背包问题，但是考虑到必须控制种类不少于M种，背包比较难以实现吧，然后想了想觉得是贪心，那首先我们得保证选了M个不同的颜色，我们还得保证这M个是不同颜色之中最大的M个，剩下的没有颜色限制了再选K-M个最大值即可，贪心思路也比较显然。

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

vll id[N];
void solve()
{
    ll n, k, m;
    cin >> n >> k >> m;
    vll tmp;
    for (int i = 1; i <= n; i++)
    {
        ll c, v;
        cin >> c >> v;
        id[c].push_back(v);
        tmp.push_back(c);
    }
    sort(all(tmp));
    tmp.erase(unique(all(tmp)), tmp.end());
    priority_queue<PLL, vector<PLL>> q;
    for (int i = 0; i < tmp.size(); i++)
    {
        ll x = tmp[i];
        sort(all(id[x]));
        q.push({id[x].back(), x});
    }
    // for(auto x:tmp) cout<<x<<" ";
    // while (q.size())
    // {
    //     auto [v, c] = q.top();
    //     q.pop();
    //     cout << v << " " << c << endl;
    // }
    ll ans = 0, cnt = k - m;
    for (int i = 1; i <= m; i++)
    {
        auto [v, c] = q.top();
        q.pop();
        ans += v;
        id[c].pop_back();
    }
    priority_queue<ll> pq;
    for (int i = 0; i < tmp.size(); i++)
    {
        ll x = tmp[i];
        for (auto x : id[x])
        {
            pq.push(x);
        }
    }
    while (cnt--)
    {
        auto t = pq.top();
        ans += t;
        pq.pop();
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
D 
问题陈述



有一个 $H \times W$ 网格，每个单元格包含一个整数 $0$ 或 $1$ 。

写入每个单元格的整数信息以 $H$ 字符串 $S_1, S_2, \dots, S_H$ 表示，长度为 $W$ 。如果 $S_i$ 的 $j$ 第一个字符为‘ 0 ’，那么 $0$ 将被写入网格顶部的 $i$ 第一行和左侧的 $j$ 第一行的单元格中；如果 $S_i$ 的 $j$ \的第一个字符为‘ 1 ’，则将 $1$ 写入该单元格。



找出写的整数之和等于 $K$ 的矩形区域的个数。

更正式地说，找出满足下列所有条件的整数 $(r_1, c_1, r_2, c_2)$ 的四倍数的个数：



—— $1 \le r_1 \le r_2 \le H$

—— $1 \le c_1 \le c_2 \le W$

-从上开始的第49118912行和从左开始的第30533166列的单元格中，所有满足 $r_1 \le i \le r_2, c_1 \le j \le c_2$ 的整数对 $(i, j)$ 之和等于 $K$ 。

# # #约束



— $H$ 和 $W$ 是介于 $1$ 和 $500$ 之间的整数。

— $K$ 是一个介于 $0$ 到 $HW$ 之间的整数。

— $S_i$ 是长度为 $W$ 的字符串，由‘ 0 ’和‘ 1 ’组成。

思考过程：读题之后发现有一个显然的暴力方法，二维前缀然后枚举这两个点的坐标，但是四重for循环是过不了的，于是我考虑优化去掉一层for循环，在预处理完前缀和之后，我在寻找第二个点进行了优化，我们可以优化最后一列的枚举，考虑到在固定第一个点和第二个点的x坐标之后，随着第二个点y坐标的增大，区域内的值是单调不减的，于是我可以二分优化查找过程 从w优化成log w ，找到存在的满足的左右边界即可。

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
int n, m, k;
char g[502][520];
int pre[520][521];
void solve()
{
    cin >> n >> m >> k;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cin >> g[i][j];
            if (g[i][j] == '1')
                pre[i][j] = 1;
        }
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            pre[i][j] += pre[i - 1][j] + pre[i][j - 1] - pre[i - 1][j - 1];
        }
    }
    auto ckl = [&](ll x, ll y, ll nx) -> ll
    {
        ll l = y - 1, r = m + 1;
        while (l + 1 < r)
        {
            ll mid = (l + r) >> 1;
            if (pre[nx][mid] - pre[x - 1][mid] - pre[nx][y - 1] + pre[x - 1][y - 1] < k)
                l = mid;
            else
                r = mid;
        }
        return r;
    };
    auto ckr = [&](ll x, ll y, ll nx) -> ll
    {
        ll l = y - 1, r = m + 1;
        while (l + 1 < r)
        {
            ll mid = (l + r) >> 1;
            if (pre[nx][mid] - pre[x - 1][mid] - pre[nx][y - 1] + pre[x - 1][y - 1] <= k)
                l = mid;
            else
                r = mid;
        }
        return l;
    };
    ll ans = 0;
    for (int x = 1; x <= n; x++)
    {
        for (int y = 1; y <= m; y++)
        {
            for (int nx = x; nx <= n; nx++)
            {
                ll L = ckl(x, y, nx), R = ckr(x, y, nx);
                if (L == m + 1 || R == y - 1)
                    continue;
                ans += R - L + 1;
            }
        }
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
E 
问题陈述



有一个 $N \times N$ 网格。最初，所有的细胞都被涂成白色。



按给定顺序处理 $Q$ 查询。每个查询都是下列查询之一：



—类型 $1$ ：给出一个整数 $R$ 。从网格顶部开始，将 $R$ \第一行中的所有单元格涂成黑色。

—类型 $2$ ：给出一个整数 $C$ 。将从网格左边开始的第 $C$ 列中的所有单元格涂成白色。



处理完每个查询后，输出该点网格中黑色单元格的数量。
# # #约束



—— $1 \leq N, Q \leq 3 \times 10^5$

—对于类型为 $1$ 的查询，使用 $1 \leq R \leq N$ 。

—对于类型为 $2$ 的查询，使用 $1 \leq C \leq N$ 。

—所有输入值均为整数。
思考过程：读完题目我首先想到了线段树这种数据结构，但是一开始觉得这种二维网状结构和行和列的操作难以维护，一时间没想到突破点。后来从题意出发，我们每次关心的是操作完之后有多少个黑色的点，那么黑色的点只有在当前点被行操作后覆盖，或者说至少在染成白色之后再次把他染成黑色，那么此时它必然是黑色的，这种操作先后造成的不同结果让我们想到了时间戳，我们可以用数组维护行和列操作的时间戳，然后用树状数组维护当前行或者列操作的时间戳出现的频率，这个是为了快速算出当前修改新增多少黑色的点，明白操作先后对结果的影响之后基本看代码能想明白了。

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
const int N = 3e5 + 10, M = 2 * N, K = 26;
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
struct BIT
{
    int tr[N];
    int limit;
    void init(int n)
    {
        limit = n;
        for (int i = 0; i <= n; i++)
            tr[i] = 0;
    }

    void modify(int k, int c)
    {
        for (int i = k; i <= limit; i += lowbit(i))
        {
            tr[i] += c;
        }
    }

    int query(int k)
    {
        int res = 0;
        for (int i = k; i; i -= lowbit(i))
        {
            res += tr[i];
        }
        return res;
    }
} trR, trC;
int tR[N], tC[N];
void solve()
{
    int n, q;
    cin >> n >> q;
    trR.init(q + 1);
    trC.init(q + 1);
    for (int i = 1; i <= n; i++)
    {
        tR[i] = 1;
        tC[i] = 1;
    }
    trR.modify(1, n);
    trC.modify(1, n);
    ll cnt = 0;
    for (int i = 1; i <= q; i++)
    {
        int op, idx;
        cin >> op >> idx;
        int t = i + 1;
        if (op == 1)
        {
            int old = tR[idx];
            cnt += n - trC.query(old - 1);
            trR.modify(old, -1);
            trR.modify(t, 1);
            tR[idx] = t;
        }
        else
        {
            int old = tC[idx];
            cnt -= n - trR.query(old);
            trC.modify(old, -1);
            trC.modify(t, 1);
            tC[idx] = t;
        }
        cout << cnt << endl;
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
