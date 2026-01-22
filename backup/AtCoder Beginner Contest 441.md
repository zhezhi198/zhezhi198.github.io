[AtCoder Beginner Contest 441](https://atcoder.jp/contests/abc441)
ABC的比赛向来不写AB的，从C开始写。
## C-Sake or Water

### 问题陈述

有几个杯子，每个杯子里装着无色透明的液体。

具体来说，第 $i$ ($1 \leq i \leq N$) 个杯子含有 $A_i$ ml 的液体。

众所周知，这些杯子中 **恰好有 $K$ 个** 装的是清酒（米酒），其余的都是水。

然而，不知道哪些杯子里装的是清酒。

高桥可以选择一些（一个或多个）杯子，喝掉里面所有的液体。

找到他需要选择的 **最小杯数**，以确保他喝至少 $X$ ml 的清酒，而不管哪个杯子里装的是清酒。

如果无法选择，则打印 $-1$。

### 约束

- $1 \leq K \leq N \leq 3 \times 10^5$
- $1 \leq A_i \leq 10^9$
- $1 \leq X \leq 3 \times 10^{14}$
- 所有输入值均为整数。

### 输入

输入来自标准输入，格式如下：

```text
N K X
A_1 A_2 ... A_N
``` 
###输出
```


打印最少杯数高桥需要选择满足条件。如果无法选择，则打印 -1 。
```
思路:问最少杯数，那么是不是要考虑最坏的情况，我们知道n个杯子里面只有k个杯子里面是酒，那最坏的情况是最大的n-k杯子里面全是水，最后那k个杯子里面装的才是酒，我们需要在[n-k+1,n]（前提是已经从大到小排过序）寻早答案即可。

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
    ll n, k, x;
    cin >> n >> k >> x; // 总杯数/酒杯数/目标
    vll a(n + 1, 0), pre(n + 2, 0);
    rep(i, 1, n) cin >> a[i];
    sort(a.begin() + 1, a.end(), greater<ll>());
    rep(i, 1, n)
    {
        pre[i] = pre[i - 1] + a[i];
    }
    auto ck = [&](ll t) -> bool { // t>(n-k)
        ll wt = n - k;
        if (t <= wt)
            return false;
        ll sum = 0;

        return pre[t] - pre[wt] >= x;
    };
    ll l = n - k, r = n + 1;
    while (l + 1 < r)
    {
        ll mid = l + (r - l) / 2;
        if (ck(mid))
            r = mid;
        else
            l = mid;
    }
    if (r == n + 1)
        cout << -1 << endl;
    else
        cout << r << endl;
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
## D - Paid Walk

### 问题陈述

有一个有向图（不一定简单），有 $N$ 个顶点和 $M$ 条边，其中顶点编号为 $1, 2, \ldots, N$。

第 $i$ 条 ($1\leq i\leq M$) 边从顶点 $U_i$ 到顶点 $V_i$，代价为 $C_i$。此外，每个顶点的出度最多为 $4$。

找出满足以下条件的所有顶点 $v$ ($1\leq v\leq N$)：

> 从顶点 $1$ 到顶点 $v$ 存在一条同时满足以下两个条件的路径：
>
> - 它遍历 $L$ 条边。如果同一条边被遍历多次，每次遍历都会被计数。
> - 遍历边的代价总和至少为 $S$，最多为 $T$。（如果同一条边被遍历多次，每次的代价都会加到总和中。）

**什么是出度？**
顶点 $u$ 的出度是指从顶点 $u$ 出发的边的个数。即使多条边指向同一个顶点，它们也会被单独计数。

### 约束

- $1 \leq N \leq 2\times 10^5$
- $1 \leq M \leq 2\times 10^5$
- $1 \leq L \leq 10$
- $1 \leq S \leq T \leq 10^9$
- $1 \leq U_i, V_i \leq N$
- $1 \leq C_i \leq 10^8$
- 每个顶点的出度最多为 $4$。
- 所有输入值均为整数。

### 输入

输入来自标准输入，格式如下：

```text
N M L S T
U_1 V_1 C_1
U_2 V_2 C_2
...
U_M V_M C_M
```
# # #输出

以升序打印满足条件的顶点，以空格分隔。

如果没有满足条件的顶点，则打印空行。
思路：按照条件递归就行了。
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
/*

*/
ll n, m, step, s, t;
int h[N], e[N], ne[N], idx, w[N];
bool ans[N];
void add(int a, int b, int c)
{
    e[idx] = b, w[idx] = c, ne[idx] = h[a], h[a] = idx++;
}
void dfs(int u, int d, int pay)
{ // [节点，步数，花费]

    if (pay > t)
        return;

    if (d == step)
    {

        if (pay >= s && pay <= t)
        {
            ans[u] = true;
        }
        return;
    }
    for (int i = h[u]; ~i; i = ne[i])
    {
        int j = e[i];

        dfs(j, d + 1, pay + w[i]);
    }
}
void solve()
{
    mem(h, -1);
    mem(ans,0);
    cin >> n >> m >> step >> s >> t;
    rep(i, 1, m)
    {
        ll u, v, c;
        cin >> u >> v >> c;
        add(u, v, c);
    }
    dfs(1, 0, 0);
    rep(i, 1, n)
    {
        if (ans[i])
        {
            cout << i << " ";
        }
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
## E - A > B substring 

#### 问题陈述

给你一个长度为 $N$ 的字符串 $S$ ，它由三种字符组成：A"、"B "和 "C"。

在 $S$ 中有 $\dfrac{N(N+1)}2$ 个非空连续子串。求其中包含的`A`多于`B`的数量。

请注意，如果两个子串取自 $S$ 中的不同位置，即使它们是相等的字符串，也要分别计算。

什么是子串？

$S$ 的**子串**是删除 $S$ 开头的零个或多个字符和结尾的零个或多个字符后得到的字符串。  
例如，`AB`是`ABC`的子串，但`AC`不是`ABC`的子串。

#### 限制因素

- $1\le N\le5\times10 ^ 5$
- $S$ 是长度为 $N$ 的字符串，由 `A`、`B` 和 `C` 组成。
- $N$ 是一个整数。
#### 输入

输入内容由标准输入法提供，格式如下

```text
 N
 S
```

#### 输出

打印 $S$ 中 A 比 B 多的连续子串的个数。

## 2. 为什么不能用双指针 ？

看到“连续子串”和“计数”，很多人的第一反应是使用**双指针（滑动窗口）**。
通常双指针适用于具有**单调性**的问题：
> 如果区间 $[L, R]$ 满足条件，那么 $[L, R+1]$ 也满足（或反之）。

**但在本题中，单调性并不存在。**

### 反例分析
假设字符串为 `A B A`：
1. `[1, 1] = "A"` (A=1, B=0)。满足条件。
2. `[1, 2] = "AB"` (A=1, B=1)。**不**满足条件。
3. `[1, 3] = "ABA"` (A=2, B=1)。**又**满足条件。

当我们右移右指针 $R$ 时，子串的状态在“满足”和“不满足”之间反复横跳，无法确定何时该移动左指针 $L$。因此，标准的双指针无法直接解决此问题。

---

## 3. 核心思路：前缀和转化

既然无法通过滑动窗口维护，我们需要将问题转化为数学表达式。

### 第一步：数值映射
我们需要比较 A 和 B 的数量。至于 C，它只占位置，不影响 A 和 B 的差值。
我们可以定义一个权值数组：
- 遇到 `A`：权值为 $+1$
- 遇到 `B`：权值为 $-1$
- 遇到 `C`：权值为 $0$

### 第二步：前缀和推导

令 $P_i$ 表示字符串前 $i$ 个字符的权值之和（即前缀和），且规定 $P_0 = 0$。
那么，对于任意子串 $S[l \dots r]$ (其中 $1 \le l \le r \le N$)，其中 A 的数量减去 B 的数量可以表示为：

$$
(\text{Count}_A - \text{Count}_B) = P_r - P_{l-1}
$$

题目要求 A 的数量 **大于** B 的数量，即要求：

$$
P_r - P_{l-1} > 0
$$

移项得：

$$
P_{l-1} < P_r
$$

### 第三步：问题转化
现在的任务变成了：
**对于每一个右端点 $r$ (从 $1$ 到 $N$)，我们要找到有多少个左端点 $l$ ($1 \le l \le r$)，满足 P_{l-1} < P_r。**

也就是统计在 $r$ 之前，有多少个前缀和的值 **严格小于** 当前的前缀和 $P_r$。

---

## 4. 数据结构优化

这就变成了一个经典的**动态统计问题**（类似于求逆序对的变种）。
我们可以从左到右遍历 $i$ (从 $0$ 到 $N$)：
1. 计算当前的前缀和 `now`。
2. 查询在之前出现过的前缀和中，有多少个小于 `now`。
3. 将当前的 `now` 加入到数据结构中，供后续查询使用。

由于前缀和的值域范围是 $[-N, N]$，我们可以使用 **树状数组 ** 来维护频率。

**注意点：**
树状数组的下标必须是正整数。当前缀和可能为负数时，我们需要加上一个偏移量 `offset`（例如 $N+1$），将值域平移到 $[1, 2N+1]$。

---

## 5. 代码实现

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
void solve()
{
    ll n;
    cin >> n;
    string s;
    cin >> s;
    s = " " + s; // 1-based indexing
    
    // now: 当前的前缀和
    // ans: 最终答案
    // d: 偏移量，防止下标为负 (因为前缀和可能低至 -N)
    ll now = 0, ans = 0, d = n + 1;
    
    // 初始化树状数组，大小需要覆盖 [-N, N] 的范围
    // 偏移后范围是 [1, 2N+1]
    BIT1<int> tr(2 * n + 5);
    
    // 极其重要：
    // 先把 P_0 = 0 加入树状数组。
    // 代表左端点 l=1 时，我们需要比较的是 P_r 和 P_0。
    tr.add(0 + d, 1);
    
    rep(i, 1, n)
    {
        // 1. 更新当前前缀和
        if (s[i] == 'A')
            now++;
        else if (s[i] == 'B')
            now--;
        // 如果是 'C'，now 不变
        
        // 2. 查询：有多少个之前的 P_{l-1} 满足 P_{l-1} < now
        // 在树状数组中，即查询 sum(now + d - 1)
        ans += tr.sum(now + d - 1);
        
        // 3. 更新：将当前的 P_i 加入树状数组
        tr.add(now + d, 1);
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
### F - Must Buy
#### 问题陈述

一家商店出售 $N$ 件商品，编号为 $1$ , $2$ , $\ldots$ , $N$ .  
第 $i$ 项 $(1\leq i\leq N)$ 的价格为 $P &#95; i$ 日元，价值为 $V &#95; i$ 。该商店每种商品只有一种存货。

高桥选择一些商品，使总价最多为 $M$ 日元。  
在这里，可以保证 $M$ 至少是任何一件商品的价格。也就是说，对于任意 $1\leq i\leq N$ ，都存在一种选择方法，使得总价最多为 $M$ 日元，并且包含 $i$ 项。

对于每个 $1\leq i\leq N$ ，确定物品 $i$ 属于以下三个类别中的哪一类：

- A 类：为了使所选物品的总价值最大（同时使总价不超过 $M$ 日元），必须选择该物品。
- B 类：为了使所选物品的总价值最大化（同时使总价不超过 $M$ 日元），可以选择或不选择该物品。
- C 类：为了使所选物品的总价值最大化（同时使总价不超过 $M$ 日元），绝不能选择该物品。

#### 限制因素

- $1\leq N\leq 1000$
- $1\leq M\leq 5\times 10^4$
- $1\leq P &#95; i\leq M$
- $1\leq V &#95; i\leq 10^9$
- 所有输入值均为整数。

### 输入

输入内容由标准输入法提供，格式如下：

```text
N M
P_1 V_1
P_2 V_2
...
P_N V_N
``` 
#### 输出

打印由 `A`、`B` 和 `C` 组成的长度为 $N$ 的字符串。  
如果项目 $i$ $(1\leq i\leq N)$ 属于类别 $X$ （其中 $X$ 是 A、B 或 C），那么输出字符串的 $i$ -th 字符应该是 $X$ 。

---

## 2. 核心思路分析

### 判定条件转化
令：
- $V_{with}(i)$：强制**选择**第 $i$ 个物品时，能获得的最大总价值。
- $V_{without}(i)$：强制**不选**第 $i$ 个物品时，能获得的最大总价值。

那么分类逻辑如下：

1. **C 类**：即使我们强制选了它，也达不到全局最优。
    $V_{with}(i) <  V_{max} $

2. **A 类**：如果我们不选它，就无法达到全局最优。
   $V_{without}(i) < V_{max}$
   *(注意：如果 $V_{with}(i) < V_{max}$ 已经在第一步判定过了，所以走到这里隐含了 $V_{with}(i) == V_{max}$)*

3. **B 类**：选它或不选它，都有办法达到全局最优。
   $$V_{with}(i) == V_{max} \quad \text{且} \quad V_{without}(i) == V_{max}$$

---

### 性能瓶颈
如果我们对每个物品都重新跑一次 $O(NM)$ 的背包 DP：
- 计算 $N$ 个物品的情况，总复杂度会变成 $O(N^2 M)$。
- 代入数据： $1000 \times 1000 \times 50000 = 5 \times 10^{10}$，这显然会超时（TLE）。

我们需要一种方法，在 $O(NM)$ 的时间内预处理，然后用 $O(M)$ 的时间回答每个物品的查询。

## 3. 优化解法：前后缀 DP 

这是一个处理“**挖掉中间某一项**”问题的标准技巧。

### 定义状态
- **前缀 DP (`pre[i][j]`)**：只考虑前 $i$ 个物品（$1 \dots i$），恰好（或最多）花费 $j$ 元能获得的最大价值。
- **后缀 DP (`suf[i][j]`)**：只考虑后 $i$ 个物品（$i \dots N$），恰好（或最多）花费 $j$ 元能获得的最大价值。

### 状态转移
这两个数组都可以通过标准的 0/1 背包算法在 $O(NM)$ 内求出。
- `pre` 数组从 $1$ 推到 $N$。
- `suf` 数组从 $N$ 推到 $1$。

### 拼接答案 
当我们考虑第 $i$ 个物品时：
1. **排除 $i$ 的情况 ($V_{without}(i)$)**：
   我们需要组合“前 $i-1$ 个物品”和“后 $i+1$ 个物品”。
   我们可以枚举在前一部分花费 $j$ 元，那么后一部分最多只能花费 $M-j$ 元。
   $$V_{without}(i) = \max_{0 \le j \le M} \{ \text{pre}[i-1][j] + \text{suf}[i+1][M-j] \}$$

2. **强制选 $i$ 的情况 ($V_{with}(i)$)**：
   首先花费 $P_i$ 买下它，剩下的预算是 $M - P_i$。
   同样枚举分配给前半部分的预算 $j$：
   $$V_{with}(i) = V_i + \max_{0 \le j \le M-P_i} \{ \text{pre}[i-1][j] + \text{suf}[i+1][(M-P_i)-j] \}$$

### 复杂度分析
- 预处理 DP：O(NM)
- 每次查询合并：O(M)
- 总共有 $N$ 个物品，总时间复杂度：O(NM)
- 空间复杂度：O(NM)

代入数据 $1000 \times 50000 = 5 \times 10^7$，在 2.5 秒内可以通过。

---

## 4. 代码

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
const int N = 1e3 + 10, M = 5e4 + 10, K = 26;
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
ll n, m;
ll v[N], w[N];
ll pre[N][M];
ll suf[N][M];

void solve()
{
    cin >> n >> m;
    rep(i, 1, n) cin >> v[i] >> w[i];

    // 1. 前缀背包 DP
    rep(i, 1, n) {
        rep(j, 0, m) {
            pre[i][j] = pre[i - 1][j];
            if (j >= v[i])
                pre[i][j] = max(pre[i][j], pre[i - 1][j - v[i]] + w[i]);
        }
    }

    // 2. 后缀背包 DP
    dep(i, n, 1) {
        rep(j, 0, m) {
            suf[i][j] = suf[i + 1][j];
            if (j >= v[i])
                suf[i][j] = max(suf[i][j], suf[i + 1][j - v[i]] + w[i]);
        }
    }

    ll mx = pre[n][m]; // 全局最大价值
    string ans = "";

    rep(i, 1, n)
    {
        // 如果物品本身价格超过预算，直接判定为 C (永远买不起)
        if (v[i] > m) {
            ans += 'C';
            continue;
        }

        // 计算 p1: 强制选 i 的最大价值
        ll rem = m - v[i];
        ll p1 = 0;
        rep(j, 0, rem) {
            // 合并前缀和后缀
            p1 = max(p1, pre[i - 1][j] + suf[i + 1][rem - j] + w[i]);
        }

        // 计算 p2: 强制不选 i 的最大价值
        ll p2 = 0;
        rep(j, 0, m) {
            // 合并前缀和后缀
            p2 = max(p2, pre[i - 1][j] + suf[i + 1][m - j]);
        }

        // 分类讨论
        if (p1 < mx) ans += 'C';      // 选了反而变小 -> 绝不能选
        else if (p2 < mx) ans += 'A'; // 不选就变小 -> 必须选
        else ans += 'B';              // 选不选都能达到最大值 -> 可选可不选
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
## G - Takoyaki and Flip
#### 问题陈述

$N$ 块板从左到右排成一条直线。我们把从左边开始的第 $i$ 个盘子称为 $(1\le i\le N)$ 个盘子，第 $i$ 个盘子称为 $i$ 个盘子。最初，所有盘子都是正面朝上摆放的，盘子上也没有章鱼小丸子。

处理以下三种类型共 $Q$ 个查询：

- 类型 $1$ ：给定整数 $L,R,X$ 。对于 $i=L,L+1,\ldots,R$ ，如果盘子 $i$ 面朝上放置，则在盘子 $i$ 上放置 $X$ 章鱼烧。
- 输入 $2$ ：给你整数 $L,R$ 。对于 $i=L,L+1,\ldots,R$ ，如果盘子 $i$ 中至少有一个章鱼烧，则吃掉盘子 $i$ 中的所有章鱼烧。翻转盘子 $i$ （如果盘子正面朝上，则将其正面朝下放置；否则，将其正面朝上放置）。
- 输入 $3$ ：给你整数 $L,R$ 。在 $L,$ 个盘子中，打印一个盘子中最大的章鱼烧数量。 $L+1,\ldots,$ $R$ .
#### 限制因素

- $1\le N\le2\times10 ^ 5$
- $1\le Q\le2\times10 ^ 5$
- 在所有查询中， $1\le L\le R\le N$ 。
- 在类型 $1$ 查询中， $1\le X\le10 ^ 9$ 。
- 至少有一个 $3$ 类型的查询。
- 所有输入值均为整数。
### 输入

输入内容由标准输入法提供，格式如下：

```text
N Q
query_1
query_2
...
query_Q
```
### 输出

设 $q$ 为 $3$ 类型查询的数量。打印 $q$ 行。
第 $i$ 行 ($1 \le i \le q$) 应包含第 $i$ 个类型 $3$ 查询的答案。
## 2. 核心思路：双状态线段树

这道题的难点在于：**盘子的“朝向”和“数值”是耦合的**。
- 操作 1 只更新朝上的盘子。
- 操作 2 会改变盘子的朝向。
- 如果我们在线段树中只维护一个 `sum` 和一个布尔标记 `is_up`，在处理区间翻转（Flip）时，很难快速计算出翻转后应该加多少值，或者原来的值去了哪里。

### 破局点：平行世界法（INF 掩码技巧）

我们可以把每个盘子想象成有两个“面”：
- **`mx[1]` (Visible/Up)**：假设盘子**正面朝上**时，这一面的数值。
- **`mx[0]` (Hidden/Down)**：假设盘子**正面朝下**时，这一面的数值。

为了区分盘子当前到底是朝上还是朝下，我们引入 `-INF` 作为**无效状态的掩码**：

| 盘子实际状态 | `mx[1]` (Up 面) | `mx[0]` (Down 面) | 说明 |
| :--- | :--- | :--- | :--- |
| **正面朝上** | `Val` (真实值) | `-INF` (无效) | 此时只能操作 Up 面 |
| **正面朝下** | `-INF` (无效) | `Val` (真实值) | 此时只能操作 Down 面 |

### 为什么这样做有效？

1.  **Add 操作**：只给“正面朝上”的盘子加值。
    - 我们只需要给整个区间的 `mx[1]` 加上 $X$。
    - 对于真正朝上的盘子：`Val + X` （正确更新）。
    - 对于朝下的盘子：`-INF + X` （依然是极小值，不影响最大值查询）。
    - **不需要判断哪些盘子朝上，直接全加！**

2.  **Flip 操作**：翻转盘子。
    - 只需要交换 `mx[1]` 和 `mx[0]` 的值。
    - 原本 `mx[1]` 是真实值，交换后 `mx[0]` 变成真实值（代表它转到了背面），`mx[1]` 变成 `-INF`（代表正面现在不可用）。

---

## 3. 线段树节点设计与 Lazy 标记

为了支持区间操作，我们需要三种 Lazy Tag，并且要注意它们的**优先级**。

### 结构体定义
```cpp
struct node {
    ll l, r;
    ll mx[2];   // mx[1]: 正面值, mx[0]: 背面值
    ll add[2];  // 对应两个面的加法 Tag
    ll rev;     // 翻转 Tag (0 或 1)
    bool clean; // 清空 Tag (吃掉章鱼烧)
} tr[N << 2];
```
### Pushdown 优先级 (非常重要)

由于一个节点可能积压了多种操作，下放标记时必须遵循逻辑顺序：
**先吃 (Clean) $\to$ 再翻 (Rev) $\to$ 最后加 (Add)**

1.  **Clean (吃掉)**：
    - 将所有 **有效值**（$> -INF$ 的值）归零。
    - `-INF` 保持不变（因为那个面本来就不存在）。
    - *注意：吃完后，盘子上的章鱼烧变为 0，但朝向不变。*

2.  **Rev (翻转)**：
    - 交换 `mx[0]` 和 `mx[1]`。
    - 交换 `add[0]` 和 `add[1]`（因为累积的加法操作也随之换了面）。

3.  **Add (加法)**：
    - 仅对 > -INF 的状态进行数值累加。

---

## 4. AC 代码实现

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
#define lc p << 1
#define rc p << 1 | 1
#define INF 0x3f3f3f3f3f3f3f3f
#define endl '\n'

const int N = 2e5 + 10;

struct node {
    ll l, r;
    ll mx[2];   // mx[1] 始终代表"朝上面"的值(若当前朝下则为-INF)
    ll add[2];
    ll rev;
    bool clean;
} tr[N << 2];

// 辅助函数：给 ch 状态增加 v
void lazy_add(ll p, int ch, ll v) {
    // 关键：只更新有效状态，-INF 永远保持 -INF
    if (tr[p].mx[ch] > -INF)
        tr[p].mx[ch] += v;
    tr[p].add[ch] += v;
}

// 辅助函数：翻转状态
void lazy_rev(ll p) {
    tr[p].rev ^= 1;
    swap(tr[p].mx[0], tr[p].mx[1]);    // 交换数值
    swap(tr[p].add[0], tr[p].add[1]);  // 交换加法标记
}

// 辅助函数：清空（吃掉）
void lazy_clean(ll p) {
    tr[p].clean = 1;
    tr[p].add[0] = tr[p].add[1] = 0; // 之前的加法作废
    // 只把真实存在的数值归零
    if (tr[p].mx[0] > -INF) tr[p].mx[0] = 0;
    if (tr[p].mx[1] > -INF) tr[p].mx[1] = 0;
}

void pushup(ll p) {
    tr[p].mx[0] = max(tr[lc].mx[0], tr[rc].mx[0]);
    tr[p].mx[1] = max(tr[lc].mx[1], tr[rc].mx[1]);
}

void pushdown(ll p) {
    // 优先级 1: Clean
    if (tr[p].clean) {
        lazy_clean(lc);
        lazy_clean(rc);
        tr[p].clean = 0;
    }
    // 优先级 2: Rev
    if (tr[p].rev) {
        lazy_rev(lc);
        lazy_rev(rc);
        tr[p].rev = 0;
    }
    // 优先级 3: Add
    if (tr[p].add[0]) {
        lazy_add(lc, 0, tr[p].add[0]);
        lazy_add(rc, 0, tr[p].add[0]);
        tr[p].add[0] = 0;
    }
    if (tr[p].add[1]) {
        lazy_add(lc, 1, tr[p].add[1]);
        lazy_add(rc, 1, tr[p].add[1]);
        tr[p].add[1] = 0;
    }
}

void build(ll p, ll l, ll r) {
    tr[p].l = l; tr[p].r = r;
    tr[p].clean = 0; tr[p].rev = 0;
    tr[p].add[0] = tr[p].add[1] = 0;

    if (l == r) {
        // 初始状态：全部正面朝上(mx[1])，值为0
        // 背面(mx[0])是不存在的，设为 -INF
        tr[p].mx[1] = 0;
        tr[p].mx[0] = -INF;
        return;
    }
    ll mid = (l + r) >> 1;
    build(lc, l, mid);
    build(rc, mid + 1, r);
    pushup(p);
}

// Type 1: Add (只加到 mx[1])
void modify1(ll p, ll x, ll y, ll c) {
    if (x <= tr[p].l && tr[p].r <= y) {
        lazy_add(p, 1, c);
        return;
    }
    pushdown(p);
    ll mid = (tr[p].l + tr[p].r) >> 1;
    if (x <= mid) modify1(lc, x, y, c);
    if (y > mid) modify1(rc, x, y, c);
    pushup(p);
}

// Type 2: Eat & Flip
void modify2(ll p, ll x, ll y) {
    if (x <= tr[p].l && tr[p].r <= y) {
        lazy_clean(p); // 先吃
        lazy_rev(p);   // 后翻
        return;
    }
    pushdown(p);
    ll mid = (tr[p].l + tr[p].r) >> 1;
    if (x <= mid) modify2(lc, x, y);
    if (y > mid) modify2(rc, x, y);
    pushup(p);
}

ll query(ll p, ll x, ll y) {
    if (x <= tr[p].l && tr[p].r <= y) {
        // 因为我们一直在维护 mx[1] 为"当前朝上面"
        // 即使盘子翻转了，swap 操作也保证了 mx[1] 存的是可视面的值
        return tr[p].mx[1];
    }
    pushdown(p);
    ll mid = (tr[p].l + tr[p].r) >> 1;
    ll res = -INF;
    if (x <= mid) res = max(res, query(lc, x, y));
    if (y > mid) res = max(res, query(rc, x, y));
    return res;
}

void solve() {
    int n, q;
    cin >> n >> q;
    build(1, 1, n);
    while (q--) {
        ll op, x, y, c;
        cin >> op >> x >> y;
        if (op == 1) {
            cin >> c;
            modify1(1, x, y, c);
        } else if (op == 2) {
            modify2(1, x, y);
        } else {
            ll ans = query(1, x, y);
            // 如果 ans 是 -INF，说明盘子可能正面朝下(且正面无效)，输出 0
            cout << max(0LL, ans) << endl;
        }
    }
}

int main() {
    ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    solve();
    return 0;
}
```