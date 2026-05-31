[Codeforces Round 1101 (Div. 2)](https://codeforces.com/contest/2232)

<img width="954" height="1190" alt="Image" src="https://github.com/user-attachments/assets/548d0409-47be-4bb1-a061-b28ef42e19d7" />

## 思考:看到题的时候我在想，选择一个中点作为一个固定的点，让左边和右边的过来，贡献就是min(l,r)+abs(r-l)，合起来其实就是取决于多的那边，可以这样写max(l,r)，虽然我这么想但是我还是认为这个固定的点就是出现最多的那个点，哈哈哈也是搞笑，不过马上发现不可行，于是乎枚举固定点位置，找到答案最小的值，过了。
 不过这里产生了一个思考：在经典的考题中，中位数，众数，平均数这些的常见的考法分别有什么呢，涉及到这些概念的题目可以尝试往什么方面想或者转换呢? ? ? 先抛一个疑问，下文在接着说。

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
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
        cnt[a[i]]++;
    }
    sort(a.begin() + 1, a.end());
    a.erase(unique(a.begin() + 1, a.end()), a.end());
    ll m = a.size();
    ll l = 0, r = 0, ans = INF;
    for (int i = 1; i <= m; i++)
    {
        ll x = cnt[a[i]];
        r = n - x - l;
        cmin(ans, max(l, r));
        l += x;
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

<img width="995" height="1354" alt="Image" src="https://github.com/user-attachments/assets/839da756-5ba4-4a1a-bc4c-8dad2e7abb10" />

### 思考：我们只关系前缀是不是能保持一个高度，且希望这个高度最大，那么我们简单假设一下情况 假设前几个高度是 1 2 3 ，那么答案对应的应该是 1 1 1，诶，在一段单调增的情况下我们的答案是否被前面的min限制住了，我们推测这个答案具有单调不增的性质，那么另外一种情况呢，3 2 1，答案应该是 3 2 1，诶，这样对吗，貌似第三个答案是2，因为题目说前面大于高度的像滚雪球一样滚到这边来，这个过程有些像在找平均数，但是在前面的样例我们发现，1 2 3 这样如果是找平均数 那么对应的 大概是 1 1 2 显然第三个只能是1，首先是因为这个不存在高处的雪球推过来失效，另外一方面是这个求前缀答案本来就是单调不增的，所以存在一个限制，所以我们考虑是对于当前的sum/i和上一个答案取一个min，这样作为正确的答案，尝试了一发，过了。

当然我依然觉得我的想法不够严谨，有些凭感觉，有些道理但是依然不严谨，可以参考官方题解，如下图。

<img width="854" height="220" alt="Image" src="https://github.com/user-attachments/assets/b3346473-c591-451b-9ef4-a741f93386cc" />



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
    ll n;
    cin >> n;
    vll a(n + 1, 0);
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    ll ans = INF, sum = 0;
    for (int i = 1; i <= n; i++)
    {
        sum += a[i];
        cmin(ans, sum / i);
        cout << ans << " ";
    }
    cout << endl;
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

<img width="967" height="1864" alt="Image" src="https://github.com/user-attachments/assets/31ef9557-3c22-4c6f-afb4-6fa5105e49cd" />

C1和C2本质是同一道题目，只是数据范围不同，一个可以用带点朴素的贪心解决，一个要像办法优化，当解法本质相同，我们在这里直接讲C2
### 思考:题意大概是说n个人，字符I, E ,A表示三类人的性格，I类人由于比较社恐，所以只能坐在空桌子上，E类人相反，必需坐在有人坐的桌子上，
A类比较随性有位置就能坐，现在有a张桌子，每张桌子只能坐b个人，现在求我们最多让多少人坐下。
首先我想的是E和I显然坐法几乎是固定的，我一开始还开了一个cnt数组表示第i张桌子目前坐了多少人，我对I的考虑是找一个空桌子坐就行，E的考虑是让他在已知不空的桌子中选最少人数的位置坐下，A的分配我想了挺久，貌似我们又要考虑后续的E和I，觉得当前位置是新占一个空位好，还是先把某些有人的位置坐满就好，本想接着贪心，后来在一次次的模拟中难以过全部的样例，于是我尝试了一发dp[j]表示在占用j个位置的前提下坐下的最多人数，尝试转移，过了样例但是Wa2。在沉默了一段时间后，真没招了，放弃了dp，于是又转向贪心，对A的分配进行深度思考，于是又是经典的假设论证，先不考虑除A之外的人，我们假设有EIEIEIEIEIIEIE 或者IEIEIEIEIEEIEI这种几乎交替的填法，我们发现如果一开始把E填好，会不会导致后续填的E毫无意义呢，显然这种交替解在某种E饱和之后的E并意义，不如与之前的I交换，这样还可能产生更多的贡献，于是启发我们可能是某种分割线，前面是E后面是I，或者前面是I后面是E??? 显然我们发现在前面的情况相当占位有限，如果全是E的话，比较容易饱和，倒不如先占一个空位，让后面的E的饱和值更高，当然有人会像，如果占位置已经占满了，还有I在占位置呢，显然既然是分割线的话，我们会让前面的I在达到某个最优的情况下就停下来让E来填后续的贡献，似乎更有道理。 那么我们的思路就是把A分为先I后E，这样在某个位置一定存在一个最大值。
另外在知道这个思路的时候我用写了一个wk函数来表示当前分割线在前pos个A是I后面是E的一个贡献，可能是我依然用了cnt模拟桌子的缘故，过了样例在第19个测试点的时候Time limit exceeded on test 19了，于是乎我们应该摒弃掉cnt，似乎我们并不在乎坐在哪个桌子上，因为每次放I的时候我们考虑当前是不是把所有桌子占领了，在考虑E的时候我们似乎也只是考虑我们占领的桌子是否完全桌面，于是我简化了一下过了。 这是简单版本，困难版本面临一个问题，我们无法在o(n2)的情况下算出答案，比较wk函数本身就是o(n)的，那么我们尝试分析单调性，我们发现这个wk随着pos的增大大概是一个先增后减的凸函数，这样启发我们二分或者三分，我尝试了二分求最值的写法，优化完过了。

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
    ll n, a, b;
    cin >> n >> a >> b;
    string s;
    cin >> s;
    s = " " + s;
    ll suma = 0;
    for (int i = 1; i <= n; i++)
    {
        if (s[i] == 'A')
            suma++;
    }
    auto wk = [&](ll pos) -> ll
    {
        ll op = 0, res = 0, cnta = 0;
        for (int i = 1; i <= n; i++)
        {
            char ch = s[i];
            if (ch == 'A')
            {
                cnta++;
                if (cnta <= pos)
                {
                    ch = 'I';
                }
                else
                {
                    ch = 'E';
                }
            }
            if (ch == 'I')
            {
                if (op < a)
                {
                    op++;
                    res++;
                }
            }
            if (ch == 'E')
            {
                if (op > 0 && res < op * b)
                {
                    res++;
                }
            }
        }
        return res;
    };
    ll l = -1, r = suma + 1;
    while (l + 1 < r)
    {
        ll mid = (l + r) >> 1;
        if (wk(mid) <= wk(mid + 1))
            l = mid;
        else
            r = mid;
    }
    cout << wk(r) << endl;
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

附带对贪心猜测的证明：

<img width="914" height="1743" alt="Image" src="https://github.com/user-attachments/assets/6ac9092e-d3d2-496c-b58b-c16d9f783fd7" />


-------------------------------------------------------------------------分割线----------------------------------------------------------------------------------
目前先写了前面四个题目，后面的题目难度较大，慢慢补。

另外我想说说中位数，平均数，众数的常见考法和一些思考。
# 经典统计学概念在算法中的思维转化：中位数、平均数与众数

## 一、 中位数 (Median)：绝对值距离与 1/-1 降维打击

### 思考与常见考法
中位数在算法题里是最“难搞”的，因为它不具备区间可加性（左半边的中位数加上右半边的中位数，跟全局中位数毫无关系）。它的常见考法主要集中在三个方向：

* **几何/物理意义考法：距离之和最小。**
  只要题目要求找一个点 $x$，使得 $\sum |a_i - x|$ 最小，想都不要想，这个点一定是这组数的中位数。如果是二维网格里的曼哈顿距离，就分别求 $X$ 轴和 $Y$ 轴的中位数。
* **动态维护考法：对顶堆/权值树状数组。**
  数据流不断进出，随时问你当前的中位数。经典的对顶堆模型：一个大根堆存较小的一半，一个小根堆存较大的一半，保证两个堆的大小差不超过 1。
* **进阶考法：二分答案 + 1/-1 变身。**
  这是最容易拉开差距的考点。题目往往要求“某个复杂区间的最大中位数”。处理中位数的终极杀招是**二分答案**。假设二分的值为 $mid$，我们把数组中 $\ge mid$ 的数统统视作 $1$，$ < mid$ 的数视作 $-1$。此时，只要这个区间的总和 $> 0$，就说明大于等于 $mid$ 的数比小的数多，真正的中位数必然 $\ge mid$。这个转化直接把不可加的中位数，变成了极其好维护的区间前缀和！

### 推荐题目与理由
* **题目链接：** [Codeforces 1486D - Max Median](https://codeforces.com/problemset/problem/1486/D)
* **推荐理由：** 这是一道将“二分 + 1/-1 转化”体现得淋漓尽致的经典神题。题目要求找一个长度至少为 $k$ 的子段，使其中位数最大。如果不用这个转化，面对 $2 \cdot 10^5$ 的数据规模绝对会陷入死胡同；一旦想到二分答案并将数组变成 $1$ 和 $-1$，配合维护一个前缀和的最小值，逻辑瞬间豁然开朗。

---

## 二、 平均数 (Mean)：除法转减法与 0/1 分数规划

### 思考与常见考法
涉及到平均数，最大的忌讳就是“直接除”，因为精度问题和浮点数比较会让你在 WA 的边缘疯狂试探。平均数的考点几乎都指向同一个方向：**不等式移项**。

* **最值转化考法：子段平均数 $\ge mid$。**
  题目让你求最大连续子段平均数。我们同样二分答案 $mid$，那么目标就是寻找是否存在一个区间满足：
  $$\frac{\sum a_i}{len} \ge mid$$
  把分母乘过去并移项，就变成了：
  $$\sum (a_i - mid) \ge 0$$
  这意味着，只要把原数组的每个元素都减去 $mid$，问题就退化成了寻找“是否存在一个和 $\ge 0$ 的子段”。
* **0/1 分数规划考法。**
  给你两组属性 $A$ 和 $B$，让你选出若干个物品，使得总收益的平均比值 $\frac{\sum A_i}{\sum B_i}$ 最大。套路完全一样，二分 $mid$，将每个物品的权重重新定义为 $A_i - mid \times B_i$，然后在这个新权重下跑贪心或者背包即可。

### 推荐题目与理由
* **题目链接：** [Codeforces 1003C - Intense Heat](https://codeforces.com/problemset/problem/1003/C)
* **推荐理由：** 这题虽然用暴力 $O(N^2)$ 前缀和也能过，但它却是练习“二分平均数”最完美的试金石。当你尝试不用暴力，而是强制自己用二分答案加上 $\sum(a_i - mid) \ge 0$ 的思想去通过它时，你就彻底掌握了 0/1 分数规划的核心降维原理。

---

## 三、 众数 (Mode)：极限一换一与局部优势

### 思考与常见考法
众数的考法通常偏向数据结构或者脑筋急转弯（思维 Trick）。

* **思维考法：绝对众数与摩尔投票。**
  寻找出现次数超过一半的数。核心思想是“极限一换一”：每次删掉两个不同的数，最后留下来的必定是那个超过一半的众数。这在空间被限制为 $O(1)$ 时是唯一解法。
* **数据结构考法：区间频繁查询。**
  因为众数不具备可加性，遇到多次查询区间 $[L, R]$ 的众数，通常是莫队算法（Mo's Algorithm）的绝对主场，或者需要用到分块技术预处理。
* **构造考法：抽屉原理的限制。**
  题目问能不能把数组重新排列，使得相邻元素不相等。这种题只需要看出现次数最多的那个众数即可。只要众数的频率没有超过总数的一半（向上取整），就一定能构造出来；排法就是把众数隔一个放一个。

### 推荐题目与理由
* **题目链接：** [Codeforces 1692H - Gambling](https://codeforces.com/problemset/problem/1692/H)
* **推荐理由：** 这题并没有让你求全局的众数，而是让你找一个“局部优势最大”的数字。它巧妙地把众数的频率统计，转化成了某种特定数字视作 $1$、其他数字视作 $-1$ 的最大子段和问题。这道题能很好地打破“遇到频率统计就想上线段树或莫队”的思维定势。

还有一些我遇到的题目： 
 [维护中位数](https://atcoder.jp/contests/abc458/tasks/abc458_d)
 [中位数的转换](https://codeforces.com/contest/2103/problem/C)

