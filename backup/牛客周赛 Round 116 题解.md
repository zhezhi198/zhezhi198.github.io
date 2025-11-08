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