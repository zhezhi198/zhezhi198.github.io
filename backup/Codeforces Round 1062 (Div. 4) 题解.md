 ### Codeforces Round 1062
[点这里进入比赛页面](https://codeforces.com/contest/2167)
## A Square?
题意:
>题目意思很简单，给定四个数大小的边，分别为a,b,c,d。判断是否可以构成正方形。
>显然四个数都相等必然可以构成一个正方形。
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
    set<ll> st;
    rep(i, 1, 4)
    {
        ll x;
        cin >> x;
        st.insert(x);
    }
    if (st.size() == 1)
    {
        out(1);
    }
    else
        out(0);
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
## B Your Name
题意:
>Khba正在写他女朋友的名字。他有几个立方体，每个上面都写着一个小写的拉丁字母。它们排成一行，形成一个字符串 s 。他女朋友的名字也是一个字符串 t ，由 n个小写拉丁字母组成。为了证明他的爱，他必须检查是否有可能重新排列字符串 s 的字母，使它成为她的名字 t 。

>也很简单，排序后判断即可。
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
	ll n;
	cin >> n;
	string s, t;
	cin >> s >> t;
	sort(all(s));
	sort(all(t));
	if (s == t)
		out(1);
	else
		out(0);
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
## C  Isamatdin and His Magic Wand!
题意:
>Isamatdin把玩具排成一排。 i \第一个玩具有一个整数 ai 。他想把它们分类，否则他妈妈会骂他。然而，Isamatdin从来不喜欢整理玩具，所以他的朋友JahonaliX给了他一根魔杖来帮助他。不幸的是，贾奥纳利克斯在制作魔杖时犯了一个小错误。但是伊萨马特丁不能再等了，他决定使用那根断了的魔杖。魔棒只能交换两个玩具，如果它们的整数有不同的奇偶性（一个是偶数，另一个是奇数）。换句话说，只有当 aimod2≠ajmod2 ，其中 mod-是整数除法的余数时，你才能交换位置为 (i,j) 的玩具。现在他想知道用这根断了的魔杖能得到的最小的字典排列。∗ 如果存在一个索引 i 使得 pj=qj 对于所有 j<i 和 pi<qi ，那么序列 p 在字典序上小于序列 q 。

这题我在分析样例的时候大概就看出一个结论，只要题目给出的这组数中同时出现奇数和偶数的情况下，我们就可以直接按照字典序排列，如果不同时存在就不行，我也没有严格证明了，一发就过了。
不信服的话可以看看官方的解释，如下图:

<img width="1278" height="530" alt="Image" src="https://github.com/user-attachments/assets/7d2519e1-5723-4808-895f-2e26afc04733" />

其实和我想的一样，也没证明啥的，大概就是猜结论吧。

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
    ll n;
    cin >> n;
    bool odd = false, even = false;
    vll a(n + 1, 0);
    rep(i, 1, n)
    {
        cin >> a[i];
        if (a[i] & 1)
            odd = true;
        else
            even = true;
    }
    if (odd && even)
    {
        sort_range(a, 1, n);
    }
    rep(i, 1, n) cout << a[i] << " ";
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
## D Yet Another Array Problem
题意：
>你得到一个整数 n 和一个长度为 n 的数组 a 。求最小的整数 x ( 2≤x≤1018 )，使得存在一个索引 i ( 1≤i≤n )，索引 gcd ∗ (ai,x)=1 。如果在 [2,1018] 范围内不存在 x ，则输出 −1 。∗ gcd(x,y) 表示整数 x和 y 的最大公约数[GCD]
没啥好说的，题目数据很小，按着题目的意思暴力就好了。
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
    ll n;
    cin >> n;
    vll a(n + 1, 0);
    rep(i, 1, n) cin >> a[i];
    ll ans = INF;
    rep(i, 1, n)
    {
        rep(j, 2, 200)
        {
            if (gcd(j, a[i]) == 1)
                cmin(ans, j);
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
## E khba Loves to Sleep!
>题意如下图所示:

<img width="1967" height="5173" alt="Image" src="https://github.com/user-attachments/assets/d6979712-f3c6-4e18-8b50-06b6270d4ccc" />

思路:
>想象一下，你的朋友khba是个瞌睡虫，他只想尽可能多睡一会儿。他的n个朋友分布在一条数轴上，准备通过你设置的k个传送门来找他。一旦朋友到达任何一个传送门，khba就会被吵醒。你的任务，就是合理地安放这k个传送门，让‘最快到达’的那个朋友所花的时间尽可能长。换句话说，我们要最大化所有朋友中，到达最近传送门所需时间的最小值。我们在求最大值最小的问题上，很容易想到二分，但题目的难点就在于如何设计二分答案的check呢,而且此题是不是一定满足二分的条件呢?“直接去想‘如何放置才能让时间最大’，就像大海捞针。我们不妨换个角度思考。让我们来玩一个猜谜游戏。我问你：‘我们能不能做到，让所有朋友到达传送门的时间都不少于 T 秒？’这个问题是不是比原问题简单多了？它变成了一个‘Yes/No’的判断题。
>*如果答案是‘Yes’，说明 T 这个时间是可能达成的。那我们是不是可以更大胆一点，试试能不能达成 T+1 秒？
>*如果答案是‘No’，说明 T 这个时间太长了，根本办不到。那我们只能放低要求，试试能不能达成 T-1 秒。
发现了吗？这个答案 T 具有非常漂亮的单调性！随着我们要求的时间 T 变大，实现的难度也单调递增（从‘Yes’变成‘No’）。这种性质，完美地契合了二分查找的适用场景。于是，我们的思路豁然开朗：我们不再直接求解那个最大时间，而是去二分枚举这个最大时间 T，然后写一个函数来check(T)，判断这个时间是否可行。”
>check(T) 函数的使命，就是回答：‘我们能否只用 k 个传送门，就让所有朋友到传送门的距离都 ≥ T？’为了方便处理，我们首先将所有朋友的位置 a[i] 进行排序。这样，朋友们就从左到右整齐排列了，我们可以清晰地看到他们之间的‘空隙’。现在，对于任何一个朋友 p，为了让他到达传送门的时间不小于 T，传送门 t 必须满足 |p - t| >= T。也就是说，传送门必须放在 p 的 T 距离之外。基于这个原则，我们来看看哪里可以安放传送门：
1.在两个相邻朋友 a[i-1] 和 a[i] 之间：
>传送门 t 必须同时满足 t >= a[i-1] + T 且 t <= a[i] - T。所以，我们可以在 [a[i-1] + T, a[i] - T] 这个闭区间内放置传送门。这个区间能放的传送门数量就是 (a[i] - T) - (a[i-1] + T) + 1，前提是这个区间得存在，即 a[i] - a[i-1] >= 2 * T。
2.在第一个朋友 a[0] 的左边：
>我们可以在 [0, a[0] - T] 这个区间放置传送门。能放的数量是 (a[0] - T) - 0 + 1。
3.在最后一个朋友 a[n-1] 的右边：
>我们可以在 [a[n-1] + T, x] 这个区间放置传送门。能放的数量是 x - (a[n-1] + T) + 1。

>我们的 check(T) 函数，就是把所有这些‘空隙’里能放置的传送门数量加起来，看看总数够不够 k 个。如果 总数 >= k，就返回 true，否则返回 false。”
之后就是简单的二分板子书写了
下面给出AC代码:
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
    ll n, k, x;
    cin >> n >> k >> x;
    vll a(n, 0);
    rep(i, 0, n - 1) cin >> a[i];
    sort(all(a));
    auto check = [&](ll d, bool out = false) -> bool
    {
        ll res = 0;
        vll ans;
        if (a[0] >= d)
        {
            res += a[0] - d + 1;
            if (out)
            {
                for (ll i = 0; a[0] - i >= d; i++)
                {
                    if (ans.size() < k)
                        ans.push_back(i);
                    else
                        break;
                }
            }
        }
        if (x - a[n - 1] >= d)
        {
            res += x - a[n - 1] - d + 1;
            if (out)
            {
                for (ll i = x; i - a[n - 1] >= d; i--)
                {
                    if (ans.size() < k)
                        ans.push_back(i);
                    else
                        break;
                }
            }
        }
        for (int i = 1; i < n; i++)
        {
            int len = a[i] - a[i - 1];
            if (len >= d * 2)
            {
                res += len - d * 2 + 1;
                if (out)
                {
                    for (int j = a[i - 1] + d; j + d <= a[i]; j++)
                    {
                        if (ans.size() < k)
                            ans.push_back(j);
                        else
                            break;
                    }
                }
            }
        }
        if (out)
        {
            for (auto t : ans)
                cout << t << " ";
            cout << endl;
        }
        return res >= k;
    };
    ll l = -1, r = x + 1;
    while (l + 1 < r)
    {
        ll mid = l + (r - l) / 2;
        if (check(mid))
            l = mid;
        else
            r = mid;
    }
    if (l == 0)
    {
        for (int i = 0; i < k; i++)
            cout << i << " ";
        cout << endl;
        return;
    }
    check(l, true);
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
>值得一提的是代码中的check函数传入了两个参数，一个是变量参数，一个是bool类型的判断参数，由于题目不仅要求距离最大值最小，而且想要知道这些传输器应该放在什么位置，所以我们可以在传统的一个参数的check函数中新增一个bool的变量参数，这样我们就可以控制输出同时可以作为二分的条件判断。

### F. Tree, TREE!!!
题目如下面图所示:

<img width="2090" height="3802" alt="Image" src="https://github.com/user-attachments/assets/2948f50f-e755-48c0-a33d-ac798c437d1f" />

题目解读:
>题目要我们计算一个叫做 "Kawaiiness" 的值。这个值是把树上每一个节点都当一次根节点（Root），分别计算其 "Cuteness"，然后把所有这些 "Cuteness" 加起来。Kawaiiness = |S₁| + |S₂| + ... + |Sₙ|那 "Cuteness" 又是什么呢？对于一个固定的根 r，我们从树上任意挑选 k 个不同的节点。这 k 个节点的“最低公共祖先”（LCA）是哪个节点？我们把所有可能的 k 个节点的组合都试一遍，会得到一堆LCA。把这些LCA节点收集起来，去掉重复的，得到一个集合 Sr。这个集合的大小 |Sr| 就是以 r 为根时的 "Cuteness"。举个栗子：想象一棵家族树，你（根节点 r）是族长。现在要从整个家族里随便挑 k 个人开会，开会地点必须是这 k 个人共同的、辈分最低的祖先（LCA）。我们把所有可能的 k 人小组都召集一遍，看看哪些祖先当过开会地点。当过开会地点的祖先总共有多少个，这就是 "Cuteness"。

思路:
>如果按照题目的定义直接计算，那简直是场灾难：
>1.我们要枚举 n 个节点作为根。
>2.对每个根，我们要枚举 C(n, k) 种 k 个节点的组合.
>3.对每个组合，我们还要计算一次LCA。
这绝对会超时。所以我们需要换个思路。这种求总和的问题，一个经典的技巧是改变统计对象。
>原来的思路是：对于每一个根 r，我们去计算有多少个节点 u 可以成为LCA？
>总和 = ∑ (对于每个根 r) (能成为LCA的节点 u 的数量)
>现在我们换一下：对于每一个节点 u，我们去计算它在多少种根 r 的情况下，可以成为LCA？
>总和 = ∑ (对于每个节点 u) (u 能成为LCA时，根 r 的数量)

>其实我们不难发现:
以 r 为根时，节点 u 能成为LCA的充要条件是：在以 r 为根的树中，u 的子树大小（包括u自己）大于等于 k。
所以我们只需计算计算 ∑_{u=1 to n} (使 u 的子树大小 >= k 的根 r 的数量)即可。
下面给出附带注释的AC代码:
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

int h[N], e[M], ne[M], idx;

void add(int a, int b)
{
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

void solve()
{
    ll n, k;
    cin >> n >> k;
    idx = 0;
    rep(i, 0, n) h[i] = -1;
    rep(i, 1, n - 1)
    {
        int x, y;
        cin >> x >> y;
        add(x, y);
        add(y, x);
    }
    vll c(n + 1, 0);
    auto dfs = [&](auto &&self, int u, int pa) -> void
    {
        c[u] = 1;// c[u] 表示以1为根时，u的子树大小。先把自己算上。
        for (int i = h[u]; ~i; i = ne[i])
        {
            int j = e[i];
            if (j == pa)
                continue;
            self(self, j, u);
            c[u] += c[j];// 把孩子j的子树大小，加到自己头上
        }
    };
    dfs(dfs, 1, -1);
    ll r1 = 0;//统计有多少个节点的子树大小 >= k
    rep(i, 1, n) if (c[i] >= k) r1++;
    auto modify = [&](int x, int v) -> void
    {
        if (c[x] >= k)
            r1--;
        c[x] = v;
        if (c[x] >= k)
            r1++;
    };
    ll res = 0;
    auto dfs2 = [&](auto &&self, int u, int pa = -1) -> void
    {
		// 1. 到达新首都u，记录此地的Cuteness
        res += r1;
		// 2. 准备迁都到邻近的城市j
        for (int i = h[u]; ~i; i = ne[i])
        {
            int j = e[i];
            if (j == pa)
                continue;
				// 迁都前的准备：保存现场
				// 3. 开始迁都！从 u 迁到 j，世界观变了！
        //    a. 对于旧首都u，它现在是j的孩子了。
        //       它的新子树是“整个世界”去掉“j原来的子树”。
        //       所以u的新子树大小是 n - cj。
            int cu = c[u], cj = c[j];
            modify(u, cu - cj);
	    //    b. 对于新首都j，它的子树现在是“整个世界”。
        //       所以j的新子st大小是 n
            modify(j, n);// modify函数更新c[j]和r1
			 // 4. 国王去新的首都j巡视
            self(self, j, u);
		 // 5. 巡视完毕，国王回到u，一切复原（回溯）
        //    这样才能公平地去下一个邻居城市k巡视
            modify(u, cu);
            modify(j, cj);
        }
    };
    dfs2(dfs2, 1);
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
>注意一下这种dfs写法即可。
### G. Mukhammadali and the Smooth Array
题意如下图:

<img width="2261" height="4423" alt="Image" src="https://github.com/user-attachments/assets/b38235c2-7929-4de0-8b24-f1b605f152d6" />

思路:
>想象一下，你有一列积木，每个积木上写着一个数字，比如 [4, 3, 2, 1]。我们的目标是重新搭这列积木，让它们从左到右不再变矮（可以一样高或者变高），也就是形成一个“非递减”的序列。
>规则:
>1.你可以替换掉任何一块积木，换成你想要的任何数字，但这需要支付一笔“成本”（比如 c[i]）。
>2.你不替换的积木，就必须保持原样。
>最终目标是：花最少的钱（总成本最小），让整列积木没有“变矮”的地方。

>花最少的钱去修改” 这个问题，其实可以等价地看成 “省下最多的钱不去修改”。
>*总成本：如果你决定把所有的积木都换掉，那总成本就是所有 c[i]的和，我们记为 tot。这显然是最差的情况，花了最多的钱。

>*保留的成本：反之，如果你能保留一部分积木不动，那么你就不需要为这些保留的积木花钱。这些“省下来”的钱，就是这些被保留的积木的成本之和。
>所以：
>最小修改成本 = 总成本 (tot) - 最大保留成本
>现在，问题的核心变成了：我们应该保留哪些积木，才能让“保留成本”尽可能的大？
>对“保留的积木”有什么要求？
你绝对不能随便保留积木。你选择保留的积木，它们自身的数字必须已经是从左到右“不下降”的。
>为什么呢？我们用上面的例子 [4, 3, 2, 1]来说明：
>*假如你决定保留第一块积木 4和最后一块积木 1。
>*由于保留的积木不能改，所以最左边永远是 4，最右边永远是 1。
>*无论你怎么修改中间的积木，4和 1之间都必然会出现一个“下降”（因为 4 > 1），这个“drop”是无法通过修改其他积木来消除的。

>所以，一个重要结论是：所有被保留的、不修改的积木，它们在原数组中的位置和数值，必须自然地构成一个“非递减子序列”。也就是说，如果你保留了一个位置 j和它后面的一个位置 i（j < i），那么必须有 a[j] <= a[i]。
明白了这个我们设计dp即可

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
    cin >> n;
    ll tot = 0;
    vll a(n + 1), c(n + 1);
    vll dp(n + 1, 0ll);
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++)
    {
        cin >> c[i];
        tot += c[i];
    }

    for (int i = 1; i <= n; i++)
    {
        dp[i] = c[i];
        for (int j = 1; j < i; j++)
        {
            if (a[j] <= a[i])
            {
                dp[i] = max(dp[i], c[i] + dp[j]);
            }
        }
    }
    ll mx = 0;
    for (int i = 1; i <= n; i++)
    {
        mx = max(mx, dp[i]);
    }
    cout << tot - mx << endl;
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