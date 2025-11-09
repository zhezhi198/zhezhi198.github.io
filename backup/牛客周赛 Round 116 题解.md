### 牛客周赛 Round 116
[点这里进入比赛](https://ac.nowcoder.com/acm/contest/120553#question)

### A-小红的区间

<img width="940" height="757" alt="Image" src="https://github.com/user-attachments/assets/0a7c960c-0bf3-4cd0-98cd-f87c95de8901" />

>A题不多说，弄清楚相交，包含，相离的定义通过条件判断就可以解决这个题目

>AC代码:
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
    ll a, b, c, d;
    cin >> a >> b >> c >> d;
    if (c < a && d > b)
    {
        cout << "A" << endl;
    }
    else
        cout << "B" << endl;
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

### B-小红的区间判断

<img width="945" height="953" alt="Image" src="https://github.com/user-attachments/assets/a382e77b-7512-4484-9b15-b1af61a2e25a" />

>B题和A题一样在这里直接给出代码

>AC代码:
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
	ll l1, r1, l2, r2;
	cin >> l1 >> r1 >> l2 >> r2;
	if ((l2 < l1 && r1 < r2) || (l1 < l2 && r2 < r1))
	{
		cout << "A" << endl;
	}
	else if (r1 < l2 || l1 > r2)
	{
		cout << "B" << endl;
	}
	else
	{
		cout << "C" << endl;
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
### C-小红的区间查询

<img width="954" height="913" alt="Image" src="https://github.com/user-attachments/assets/5724a7c1-4c61-4c1d-b4f8-b7076f289c53" />

>朴素的思路:
>已知题目给出n个区间，然后q次询问，问我们每次询问的这个数是在第几个区间内，我们首先一个最朴素的想法就是，我们知道每个区间的l,r，我们可以利用差分数组在两个区间之间打上他们是第几个区间的值，比如他们是第一个区间。那么我们就在这个区间的两端赋值为1，使得[l,r]区间内的值都为1，其他的区间依次类推，最后没有赋值过的值肯定为0，那输出-1即可，有值的输出值即为题目要求的答案。为什么可以这样呢，因为题目保证了区间互不相交，所以每一段赋值都不会被其他的值覆盖掉，所以保证每个区间内的值都是单一的。这是最朴素的想法，但是1e9的数据范围让此方法不可行，所以我们必须想到优化的方法。
> 常见的优化方法就是二分，但是二分优化需要满足一定的单调性，我们发现将区间按照左端点排列，由于每个区间不会相互覆盖，我们就保证了区间始终是递增的，这样便具有了单调性，于是我们尝试有二分的方法完成这个题目，我们只需要创建结构体把区间的信息维护起来，然后用二分查找，合法的找到的就输出即可，找不到就输出-1.思路比较简单，二分注意细节即可。

>AC代码:
```cpp#include <bits/stdc++.h>
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

struct node
{
    ll l, r, id;
};
bool cmp(node a, node b)
{
    return a.l < b.l;
}
void solve()
{
    ll n, q;
    cin >> n >> q;
    vector<node> a;
    rep(i, 1, n)
    {
        ll l, r;
        cin >> l >> r;
        a.push_back({l, r, i});
    }
    sort(a.begin(), a.end(), cmp);
    while (q--)
    {
        ll x;
        cin >> x;
        ll lo = -1, hi = a.size();
        while (lo + 1 < hi)
        {
            ll mid = lo + (hi - lo) / 2;
            if (a[mid].r < x)
                lo = mid;
            else
                hi = mid;
        }
        if (hi != a.size() && a[hi].l <= x && x <= a[hi].r)
        {
            cout << a[hi].id << endl;
        }
        else
            cout << -1 << endl;
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
>这是我写的二分，读者可以想想为什么在输出答案的时候我的if条件为什么还如此复杂呢，为什么是这样，可以思考思考。但也许也有更好的二分技巧，我以为这个if条件wa了一发! -_-.

### 小红的区间相交

<img width="938" height="955" alt="Image" src="https://github.com/user-attachments/assets/96969b25-0785-4bbc-83c2-e1cda2354be7" />

>题目意思很简单，问我们区间是否满足任意两个两两相交,我们想什么时候一定可以保证两两相交呢，那么就是按区间的左右端点从小到大排列后，第一个区间和最后一个区间依然满足相交的关系就说明其他的都满足这个关系，想到这个就非常简单了。这题有一个启发我们的地方，在某一个条件难以写出它的条件判断时，我们可以写出其他与他互斥的关系，在用else就可以简单的把这个条件表示出来了。
>AC代码:
```cpp#include <bits/stdc++.h>
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
    vector<PLL> a(n);
    for (int i = 0; i < n; i++)
        cin >> a[i].fi >> a[i].se;
    sort(all(a));
    auto check = [&](auto &p1, auto &p2) -> bool
    {
        ll l1 = p1.fi, r1 = p1.se;
        ll l2 = p2.fi, r2 = p2.se;
        if (l2 < l1 && r1 < r2)
            return false;
        if (l1 < l2 && r2 < r1)
            return false;
        if (r2 < l1 || r1 < l2)
            return false;
        return true;
    };
    if (check(a[0], a.back()))
    {
        cout << "Yes" << endl;
    }
    else
        cout << "No" << endl;
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
###  小红的区间构造

<img width="1256" height="1414" alt="Image" src="https://github.com/user-attachments/assets/1f04ca5e-8c3e-4e5d-8a83-7805f7e4df28" />

>这个题目我一开始没写出来，慢慢看别人的代码才逐渐明白，最后自己又敲了一遍，才决定把题解奉上。

>这道题的核心任务是：给我们一片由不同高度建筑构成的“城市天际线”和一个预算 m，要求我们通过一系列“填平”操作，将整个天际线变为平地。我们需要计算出最基础的成本，并用剩余的预算给出一种具体的、最节省操作次数的“填平”方案。

### Step 1: 最初的幻想 —— “一层一层削平”
>面对一片高低不平的山脉，最符合直觉的想法是什么？当然是像切蛋糕一样，从最高的那一层开始，一刀切下去，把它削平！比如，对于 [2, 5, 3, 6, 2] 这样的高度，我们自然会想：
1.找到最高点 6.
2.把它削平成和第二高的 5 一样高。记录下成本.
3.现在地形变成了 [2, 5, 3, 5, 2].
4.找到最高点 5 和 5.
5.把它们削平成和下一个高度 3 一样高。记录成本...
这个思路清晰、朴素。但我们很快就会发现一个致命问题：太慢了！ 每次削平一层，我们都可能需要遍历整个数组来寻找新的最高点，或者用优先队列来维护。如果山峰极高，数组极长，这种 O(N * H) 的复杂度（H是最大高度）会让我们在时间限制面前“灰飞烟灭”。

### 视角的转变 —— 从“削平”到“填谷”
>既然从上往下“削”太慢，我们能不能换个角度？想象一下，我们不是在移山，而是在填海。任何一个可以被“填平”的区域，本质上都是一个凹槽或者说山谷。一个山谷由什么构成？左边的山峰，右边的山峰，以及中间的谷底。我们能填多少土，取决于两边山峰中较矮的那个，也就是“水桶效应”。那么问题转化了：我们不再关心全局最高点，而是去寻找每一个独立的“山谷”结构，并计算填平它的成本。怎么高效地找到每一个“山峰”以及它两侧的“边界”呢？这正是我们今天主角——单调栈——大显神通的舞台！
### Step 3: 神兵天降 —— “单调栈”的建筑美学
>想象我们有一个“勘探机器人” i，它从左到右沿着城市天际线行走。同时，我们还有一个“瞭望塔”序列，这就是我们的单调栈。这个栈有一个铁律：从栈底到栈顶，瞭望塔的高度必须是严格递增的。 也就是说，新来的建筑如果比栈顶的瞭望塔矮，就说明我们找到了一个“山峰”的右边界！让我们用一个例子 [0, 2, 5, 3, 6, 2, 0] 来走一遍这个神奇的过程。（注意，我们在数组前后各加一个0，这像是两堵无限矮的墙，它们是整个故事的关键！）
1.i = 1 (高度2): 栈里只有 0 (高度0)。2 > 0，满足递增！1号位置建立瞭望塔。stk = {0, 1}。
2.i = 2 (高度5): 5 > a[1]=2，满足递增！2号位置建立瞭望塔。stk = {0, 1, 2}。
3.i = 3 (高度3): 高能预警！ 3 < a[2]=5。铁律被打破！这说明：
*我们找到了一个山峰！ 就是栈顶的 2号位置，高度为5。
*它的左边界是栈里的前一个元素，即 1号位置 (高度2)
*它的右边界就是我们机器人当前的位置 i=3 (高度3)。
*这个山谷的“水面高度”是 max(左边界高度, 右边界高度) = max(2, 3) = 3。
*所以，我们可以从 5 号山峰上削掉 a[2] - 3 = 2 的厚度。
*【核心操作】 我们在概念上将 a[2] 的高度“削”为 3。现在，地形变成了 [0, 2, 3, 3, 6, 2, 0]。因为 a[3] 和削平后的 a[2] 一样高了，形成了一个平顶。我们继续前进。
这个过程反复进行，单调栈就像一个精密的仪器，每当一个新来的矮个子打破它的队形，它就能立刻识别出一个完整的“山峰-山谷”结构，并计算出“削平”它的成本。
### Step 4: 终极奥义 —— n+1 的“强制清算”
>在我的探索过程中，我曾犯过一个致命的错误：我的机器人只走到了 n。考虑 [0, 1, 2, 3, 4, 5] 这样的序列。我的机器人 i 从1走到5，因为高度一直在增加，瞭望塔 stk 不断建立，变成了 {0, 1, 2, 3, 4, 5}。然后... 循环结束了！栈里辛辛苦苦建立的瞭望塔，全都没有被处理！成本为0，大错特错！问题出在哪？因为这些山峰的右边没有更矮的建筑来“终结”它们。解决方案，也是这个算法最精妙的一笔，就是引入“天涯海角”的概念。 我们让机器人多走一步，走到 i = n+1 的位置。我们规定，这个位置的高度是 0这个 a[n+1] = 0 就像一道万丈深渊，它比任何存在于栈中的瞭望塔都要矮。当机器人 i 走到这里时，它会触发一个“清算雪崩”：
*a[n+1]=0 比栈顶的 5 矮？处理山峰 5！
*处理完后，栈顶是 4。a[n+1]=0 比 4 矮？处理山峰 4！
*...
这个 i = n+1 的“强制清算人”，会确保栈里所有待处理的山峰，在旅程的最后被一一结算，一个不留。这就是为什么循环必须是 rep(i, 1, n + 1)。
### Step 5: 预算的艺术 —— 如何花钱
>通过单调栈，我们已经得到了一个 cost 列表和一个对应的 qj (区间) 列表。这就像一份“工程报价单”。
1.核算总价： 我们先把所有 cost 加起来，从总预算 m 中扣除。如果此时 m < 0，说明预算连基础建设都不够，直接宣告失败 -1。
2.精打细算花余钱： 剩下的 m 是我们可以用来“优化操作”的。我们的目标是操作次数最少。
*一次 (L, R) 的操作，可以填平 [L, R] 区间的一层。
*一次 (l, l) 的操作，只能填平 l 位置的一层。
*显然，区间操作比单点操作更有效率。
3.贪心策略： 我们遍历每一笔“工程”(cost[i], qj[i])。对于该工程的 cnt 层，我们：
*优先使用单点操作 (l, l) 来消耗剩余预算 m。我们从左到右 *l++，直到 m 用完或者 l 追上 r。
剩下的部分，用一次最高效的区间操作 (l, r) 来完成。
4.最后的检查： 所有工程都安排完后，如果预算 m 还有剩余 (m > 0)，说明给的钱太多，花不完，也算任务失败（题目要求必须正好花完或者通过基础建设后为0），输出 -1。
至此，我们不仅高效地计算出了成本，还给出了一套最省操作次数的施工方案！

最后附上我的AC代码:
```cpp#include <bits/stdc++.h>
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
	ll n, m;
	cin >> n >> m;
	vll a(n + 2, 0); // 在两边设置“哨兵”
	rep(i, 1, n) cin >> a[i];

	vll stk(1, 0);	// 单调栈，初始有0号哨兵
	vector<PLL> qj; // 记录每个成本对应的区间
	vll cost;		// 记录每个被削平的山峰层的成本

	// 勘探机器人从1走到n+1，“清算人”出动！
	rep(i, 1, n + 1)
	{
		// 发现当前建筑比栈顶矮，找到了一个山峰！
		while (a[stk.back()] > a[i])
		{
			ll bk = stk.back(); // 山峰的位置
			stk.pop_back();
			ll bk2 = stk.back(); // 山峰的左肩
			// 水平面高度 = max(左肩, 右肩(即当前i))
			ll mx = max(a[bk2], a[i]);
			ll cnt = a[bk] - mx; // 计算出可削平的厚度(成本)

			if (cnt > 0)
			{ // 只记录有意义的成本
				cost.push_back(cnt);
				qj.push_back({bk, i - 1});
			}

			// 这是最精妙的“重塑地形”
			// 如果右肩比左肩高，说明削平后的bk可以作为i的基石
			if (a[i] > a[bk2])
			{
				stk.push_back(bk);
			}
			// 概念上将山峰削平
			a[bk] = mx;
		}
		// 如果当前建筑更高，建立新的瞭望塔
		if (a[i] > a[stk.back()])
			stk.push_back(i);
	}

	// 开始计算和分配预算
	for (int i = 0; i < cost.size(); i++)
	{
		m -= cost[i];
	}
	if (m < 0)
	{
		cout << -1 << endl;
		return;
	}

	vector<PLL> ans; // 最终施工方案
	for (int i = 0; i < cost.size(); i++)
	{
		ll cnt = cost[i];
		auto [L, R] = qj[i];
		for (int j = 0; j < cnt; j++)
		{
			ll l = L, r = R;
			// 贪心使用剩余预算m，用单点操作填补
			while (m > 0 && l < r)
			{
				ans.push_back({l, l});
				l++;
				m--;
			}
			// 剩下的用一个最高效的区间操作
			ans.push_back({l, r});
		}
	}

	if (m > 0) // 钱没花完
	{
		cout << -1 << endl;
		return;
	}

	cout << ans.size() << endl; // 输出操作总数
	for (auto &[L, R] : ans)
	{
		cout << L << " " << R << endl;
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
## 总结
>从这道题里，我学到的不仅是一个单调栈的模板，更是一种解决问题的思维跃迁：
1.当一种思路走到“复杂度”的死胡同时，果断放弃，转换视角。
2.学会用精巧的数据结构（如单调栈）来解决“寻找左右边界”这类经典问题。
3.永远不要忘记边界条件，那小小的 n+1，是算法鲁棒性的最后一块拼图。
