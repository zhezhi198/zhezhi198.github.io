[Codeforces Round 1103 (Div. 3) ](https://codeforces.com/contest/2236)

### A

A.火车上的游戏



每次测试时间限制：1秒



每个测试的内存限制：256兆字节



输入：标准输入



输出：标准输出

Dabir， Egor和Arseniy刚上了火车，决定玩个游戏。Dabir的背包里有无数个立方体。他用它们建造了 $n$ 座塔，其中第 $i$ 座塔的高度为 $h_i$ 立方。



Egor和Arseniy必须为每座塔楼 $i$ 选择一个整数 $x_i$ ，并将其高度增加 $x_i$ **，正好一次**。例如，如果 $h$ = {}\[ $1, 3, 2, 2$ \], $x$ = \[ $3, 2, 2, 8$ \]，那么增加 $h$ 后将得到\[ $4, 5, 4, 10$ \]。他们的目标是使所有塔的高度相等。



为了使游戏更有趣，Dabir想要选择一个整数 $k$ 并添加一个限制：每个 $x_i$ 必须满足 $1 \le x_i \le k$ 。帮助他找到最小的 $k$ ，有可能完成游戏。

输入* * * *



第一行包含单个整数 $t$ （ $1 \le t \le 10^4$ ）—测试用例的数量。



然后是 $t$ 测试用例。



每个测试用例的第一行包含一个整数 $n$ （ $1 \le n \le 5$ ）。



第二行包含 $n$ 整数 $h_1, h_2, \dots, h_n$ （ $1 \le h_i \le 6$ ）。

* * * *输出



对于每个测试用例，输出一个整数——最小值 $k$ ，使得所有塔都有相同的高度。

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
    ll mx = -1, mn = INF;
    for (int i = 1; i <= n; i++)
    {
        ll x;
        cin >> x;
        cmax(mx, x);
        cmin(mn, x);
    }
    cout << mx + 1 - mn << endl;
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

### B
B.鞑靼电视节目



每次测试的时间限制：2秒



每个测试的内存限制：256兆字节



输入：标准输入



输出：标准输出

假期期间，伊戈尔来喀山市看望他的朋友达比尔。出于无聊，Dabir和Egor想出了一个新的商业点子：制作他们自己的电视节目。



节目的形式非常简单：每一集他们邀请一位嘉宾，并与他们在二进制字符串上玩一个游戏。



在今天的节目中，Egor和Dabir邀请了鄂木斯克的主要名人Arseniy（又名MAKAN）。对于这个游戏，他们选择了一个长度为 $n$ 的二进制字符串 $s$ 和一个整数 $k$ 。



Arseniy可以无限次移动。在一次移动中，他可以选择一个整数 $i$ ( $1 \le i \le n - k$ )，并将位置 $i$ 和 $i + k$ 的字符反转，即将 $0$ 变为 $1$ ，将 $1$ 变为 $0$ 。



例如，如果 $s = 10110$ 和 $k = 2$ ，那么通过选择 $i = 2$ ，Arseniy将反转位置上的字符 $2$ 和 $4$ : $[ 10110 \rightarrow 11100 ]$



阿尔塞尼想要获得大奖——图格里克。要做到这一点，他需要使整个字符串 $s$ 等于零。



帮助阿尔谢尼决定他是否能得到他的奖品，或者他是否将一无所有地返回鄂木斯克。

输入* * * *



第一行包含一个整数 $t$ （ $1 \le t \le 10^4$ ）——测试用例的数量。



每个测试用例的第一行包含两个整数 $n$ 和 $k$ （ $1 \le k \le n \le 2 \cdot 10^5$ ）。



每个测试用例的第二行包含一个长度为 $n$ 的二进制字符串 $s$ 。



保证所有测试用例 $n$ 的和不超过 $2 \cdot 10^5$ 。

* * * *输出



对于每个测试用例，如果Arseniy可以使字符串完全为零，则输出“YES”，否则输出“NO”。



您可以在任何情况下输出“YES”和“NO”（例如，可以接受“YES”、“YES”和“YES”）。

思路：题目要求的操作只会改变i和i+k这两个位置，我们简单假设一下，如果当前位置要变，是不是只能被迫改变i+k，否则我们无法改变，因此我们得出只要从前向后扫一遍，如果最后能变成全0，意味着可行。

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
    ll n, k;
    cin >> n >> k;
    string s;
    cin >> s;
    s = " " + s;
    for (int i = 1; i <= n; i++)
    {
        if (s[i] == '1')
        {
            if (i + k <= n)
            {
                s[i] = '0';
                s[i + k] = (s[i + k] - '0') ^ 1 + '0';
            }
            else
            {
                cout << "NO" << endl;
                return;
            }
        }
    }
    cout << "YES" << endl;
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
思考：如果题目的操作改成区间呢，[i,i+k-1]区间取反呢，似乎暴力依然可以这样写，但是不足以AC。
如何实现在o1时间内实现区间的取反呢，我们想到了差分，在i的位置打上一个修改标记，在i+k-1的时候打上一个标记，用now记录一下当前的翻转操作。
变式代码：
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
    ll n, k;
    cin >> n >> k;
    string s;
    cin >> s;
    s = " " + s;
    vll d(n + 2, 0);
    ll now = 0;
    for (int i = 1; i <= n; i++)
    {
        now ^= d[i];
        ll v = (s[i] - '0') ^ now;
        if (v == 1)
        {
            if (i + k - 1 <= n)
            {
                now ^= 1;
                d[i + k] ^= 1;
            }
            else
            {
                cout << "NO" << endl;
                return;
            }
        }
    }
    cout << "YES" << endl;
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
### C
C. Omsk程序员



每次测试时间限制：1秒



每个测试的内存限制：256兆字节



输入：标准输入



输出：标准输出

一年一度的程序员博览会正在鄂木斯克的主要广场举行。你，作为鄂木斯克的主要程序员，决定参加这个精彩的活动并去了那里。在入口处，一名警卫决定检查你的技能，并给了你一个问题：



给你三个整数 $a$ ， $b$ , $x$ 。你想让 $a$ 和 $b$ 相等。为此，您可以应用以下操作：



1.  从整数 $a$ 或 $b$ 中选择一个，然后加上 $1$ 。

2.  选择一个整数 $a$ 或 $b$ ，然后除以 $x$ ，四舍五入。



您需要找到使 $a$ 等于 $b$ 的最小操作次数。你能证明你的技能吗，还是你必须回家？

输入* * * *



第一行包含单个整数 $t$ $(1 \le t \le 10^4)$ —测试用例的数量。



然后是 $t$ 测试用例。



每个测试用例由一行组成，其中包含三个整数 $a$ ， $b$ , $x$ （ $1 \le a, b \le 10^9$ , $2 \le x \le 10^9$ ）。

* * * *输出


对于每个测试用例，输出一个整数—使 $a$ 和 $b$ 相等所需的最小操作数。

思路：由于数据很大，显然不能简单的考虑BFS的类似方法求最小步数，那我们不得不重新考虑一下操作的两个问题，是先除后加优些，还是先加后除优，显然在除一个大因数前提下，我们改变因数得话更大的代价，所以可以尝试证明先除后加这种趋近相等的操作，证明即可。
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
    ll a, b, x;
    cin >> a >> b >> x;
    vector<PLL> pa, pb;
    ll cnta = 0, cntb = 0;
    while (a != 0)
    {
        pa.push_back({a, cnta});
        a /= x;
        cnta++;
    }
    pa.push_back({0, cnta});
    while (b != 0)
    {
        pb.push_back({b, cntb});
        b /= x;
        cntb++;
    }
    pb.push_back({0, cntb});
    ll ans = INF;
    for (auto [nx, cntx] : pa)
    {
        for (auto [ny, cnty] : pb)
        {
            cmin(ans, cntx + cnty + abs(nx - ny));
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

D.全新的鞑靼电视节目



每次测试的时间限制：2秒



每个测试的内存限制：256兆字节



输入：标准输入



输出：标准输出

Dabir和Egor并不满足于上一集的名气，所以他们决定制作另一个电视节目：这两个家伙在一个数组 $$$a$$$ 上玩他们最喜欢的游戏，数组中有他们最喜欢的整数 $$$k$$$ 。



达比尔先行动。在第一次移动时，可以选择和删除数组中的任何元素。让前面选择的元素等于 $$$x$$$ 。然后在当前的移动中，除了第一个，玩家必须从数组中选择一个元素 $$$y$$$ ，这样 $$$0 \leq y - x \leq k$$$ 并将其从数组中移除。不能移动的玩家输了。



但由于这不仅仅是一场比赛，而是一场真正的表演比赛，鄂木斯克的主要名人Arseniy （aka MAKAN）再次被邀请。作为嘉宾名人，Arseniy有机会在这场比赛中迈出第一步，也就是说，他代替Dabir**在比赛中迈出第一步。然而，事实证明阿尔塞尼是埃戈尔的粉丝，所以他希望自己的第一步能保证埃戈尔在面对达比尔的任何回应时都能取得胜利。



决定阿尔塞尼是否可以先为达比尔采取行动，这样，无论达比尔如何发挥，伊戈尔都会获胜。


输入** **



每个测试由多个测试用例组成。第一行包含一个整数 $$$t$$$ （ $$$1 \leq t \leq 10^4$$$ ）——测试用例的数量。



每个测试用例的第一行包含两个整数 $$$n$$$ 和 $$$k$$$ （ $$$1 \leq n, k \leq 2 \cdot 10^5$$$ ）——数组的长度和Dabir和Egor最喜欢的整数。



第二行包含 $$$n$$$ 个整数 $$$a &#95; 1, a &#95; 2, \ldots, a &#95; n$$$ （ $$$1 \leq a &#95; i \leq n$$$ ）。



保证所有测试用例的 $$$n$$$ 之和不超过 $$$2 \cdot 10^5$$$ 。

** **输出



对于每个测试用例，如果存在这样的第一步，即双方玩家Egor获胜，则输出“YES”，否则输出“NO”。



您可以在任何情况下输出“YES”和“NO”（例如，可以接受“YES”、“YES”和“YES”）。


思路：操作的限制大概是我们必须选择比之前大的数，且差值在[0,k]之间，那我们不得不先思考一个最极端的情况，假设我们第一个选的就是最大值，那么剩下的操作就被迫只能选最大值了，那是不是意味着，这种必败态的转化取决于当前最大元素数量，那如果我们一开始选的是次大值，且最大值依然可以在此基础上选择，那是不是可以通过次小值过渡一下状态的转变，所以代码思路也显然了。

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
    ll n, k;
    cin >> n >> k;
    vll a(n + 1, 0), cnt(n + 2, 0);
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
        cnt[a[i]]++;
    }
    sort(a.begin() + 1, a.end());
    a.erase(unique(a.begin() + 1, a.end()), a.end());
    n = a.size() - 1;
    bool ck = false;
    for (int i = n; i >= 1; i--)
    {
        ll x = a[i];
        if (cnt[x] % 2 == 0)
        {
            ck = true;
            break;
        }
        if (i > 1 && a[i] - a[i - 1] <= k)
        {
            ck = true;
            break;
        }
    }
    cout << (ck ? "YES" : "NO") << endl;
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
### E
E.友好的礼物



每次测试的时间限制：3秒



每个测试的内存限制：512兆字节



输入：标准输入



输出：标准输出

阿尔谢尼决定让他的朋友达比尔和伊戈尔高兴。为此，他决定给他们每个人一个长度相同的数字数组。如果数组 $b$ 的元素可以重新排列，使得所有 $i \gt 1$ 的条件 $b_i - b_{i - 1} = 1$ 都成立，则称为好数组。



Arseniy希望Dabir和Egor能够使用这些阵列。为此，必须满足以下条件：



1.  每个给定的数组都是好的。

2.  如果将一个数组写在另一个数组之后（换句话说，将它们连接起来），得到的数组也很好。



Arseniy已经有一个长度为 $n$ 的数组 $a$ 。他计划从 $a$ 切割两个数组，即选择两个相同长度的不重叠的子段**。帮助Arseniy确定结果数组的最大可能长度。

输入* * * *



第一行包含一个整数 $t$ $(1 \le t \le 1000)$ —测试用例的数量。



然后是 $t$ 测试用例。



每个测试用例的第一行包含一个整数 $n$ $(1 \le n \le 6000)$ 。



第二行包含 $n$ 整数 $a_1, a_2, \dots, a_n$ $(1 \le a_i \le n)$ 。



保证所有测试用例的 $n$ 之和不超过 $6000$ 。

* * * *输出



对于每个测试用例，输出单个整数—数组的最大可能长度。

思路：注意到题目数据很小，我们可以考虑把所有mx-mn=r-l的存在的连续数组打算标记，考虑到题目要求找到两段且拼接后依然是一样能拼接的，那么我们找到的这两段不存在重叠的可能，所有可以大胆的双层循环去找。
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
    int n;
    cin >> n;
    vll a(n + 1, 0);
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    vector<vector<bool>> st(n + 2, vector<bool>(n + 2, false));
    vll cnt(n + 2, 0);
    for (int l = 1; l <= n; l++)
    {
        ll mn = a[l], mx = a[l];
        int r;
        for (r = l; r <= n; r++)
        {
            cnt[a[r]]++;
            if (cnt[a[r]] >= 2)
                break;
            cmax(mx, a[r]);
            cmin(mn, a[r]);
            if (r - l == mx - mn)
            {
                st[mn][mx] = true;
            }
        }
        for (int k = l; k <= min(n, r); k++)
            cnt[a[k]] = 0;
    }
    int ans = 0;
    for (int len = n / 2; len >= 1; len--)
    {
        for (int x = 1; x + 2 * len - 1 <= n; x++)
        {
            if (st[x][x + len - 1] && st[x + len][x + 2 * len - 1])
            {
                cout << len << endl;
                return;
            }
        }
    }
    cout << 0 << endl;
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

###  F1
F1。萨兰斯克选举（简易版）



每次测试的时间限制：4秒



每个测试的内存限制：256兆字节



输入：标准输入



输出：标准输出

这是这个问题的简单版本。唯一的区别是 $x = 1$ **



在买完他最喜欢的苏打水“Zola Cero”回家的路上，Egor看到萨兰斯克正在举行“最佳数字”的选举。



投票站有许多人。每个人都带了一个号码 $a_i$ 。当第39624636人进入投票站时，他们选择的候选人是数字 $a_i$ 的约数。让选定的候选人为 $p_i$ 。



在每个人都投票之后，我们得到一个投票数组 $[p_1, p_2, \ldots, p_n]$ 。



Egor非常喜欢数字 $x$ ，并认为理想的投票是 $x \cdot {lcm}(p_1, p_2, \ldots, p_n)$ $^{\text{∗}}$ = $p_1 \cdot p_2 \cdot \ldots \cdot p_n$ 。帮助他找出 $p$ 模 $10^9 + 7$ 的不同 $^{\text{†}}$ 数组中最理想的个数。



$^{\text{∗}}$ $lcm$ -[最小公倍数]（https://codeforces.com/r/lcm-wiki）。



$^{\text{†}}$ 如果存在一个索引 $i$ ，其中两个数组具有不同的元素，则认为两个投票数组**不同**。

输入* * * *



第一行包含单个整数 $t$ （ $1 \leq t \leq 10^4$ ）—测试用例的数量。



然后是 $t$ 测试用例。



每个测试用例的第一行包含两个整数 $n$ 和 $x$ （ $1 \leq n \leq 10^5$ , $x = 1$ ）——投票站的选民人数和Egor最喜欢的数字。



每个测试用例的第二行包含 $n$ 个整数： $a_1, a_2, \dots, a_n$ （ $1 \leq a_i \leq 5 \cdot 10^5$ ）—选民带来的数字。



保证所有测试用例 $n$ 的和不超过 $10^5$ 。

* * * *输出



对于每个测试用例，输出对 $10^9 + 7$ 取模的投票方式数，以使结果的投票数组满足条件。

思路：首先我们必须先转化一下条件，一些数的最大公因数等于他们的累积和，当且仅当这些数互质的时候成立，那么题目转化为我们需要找到这些数的质因数，从中挑选n个互质的数，当然也可以选1，当然从这个视角来统计比较困难，我们可以转换一下视角，从位置选数到给质数分配归宿，既然最终选出来n个数必须两两互质，这意味着任意一个具体的质因数最多只能被这n个人中的某一个独占，绝不能被两个同时分配到，顺着这个思路，我们可以把每个出现的质数单独来算，对于某个质数z，我们统计出在所有数的质因数中他出现了多少次，记作sum[z]，现在我们要为质数 z 寻找归宿，它究竟有多少种合法的分配方式呢？其实只有两大类情况：第一种归宿是分配到具体的某个人，第二种归宿是大家都不拿，第一种用sum[z]种分配法，第二种只要一种，所以我们最后的答案就是(sum[z]+1)累积取模Md7。

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
ll cnt = 0;
ll p[N];
bool st[N];
ll mp[N];
ll sum[N];

void init()
{
    for (int i = 2; i < N; i++)
    {
        if (!st[i])
        {
            p[++cnt] = i;
            st[i] = true;
            mp[i] = i;
        }
        for (int j = 1; j <= cnt && i * p[j] < N; j++)
        {
            st[i * p[j]] = true;
            mp[i * p[j]] = p[j];
            if (i % p[j] == 0)
                break;
        }
    }
}

void solve()
{
    ll n, x;
    cin >> n >> x;
    vll a(n + 1, 0);
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    vll vis;
    for (int i = 1; i <= n; i++)
    {
        ll x = a[i];
        while (x > 1)
        {
            int z = mp[x];
            int c = 0;
            while (x % z == 0)
            {
                c++;
                x /= z;
            }
            if (sum[z] == 0)
            {
                vis.push_back(z);
            }
            sum[z] = (sum[z] + c) % Md7;
        }
    }
    ll ans = 1;
    for (auto x : vis)
    {
        ans = ans * (sum[x] + 1) % Md7;
        sum[x] = 0;
    }
    cout << ans << endl;
}

int main()
{
    IOS;
    init();
    int _ = 1;
    cin >> _; // 如果是多组数据
    while (_--)
    {
        solve();
    }
    return 0;
}
```
