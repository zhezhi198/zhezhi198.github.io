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
const int N = 1e6 + 10, M = 1e7 + 10, K = 26;
const ll MOD = 1e9 + 7, Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
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
/*      题目 要求 ai>=2  然后问满足任意(i,j)使得数组中gcd(a[i],a[j])==1
    但是你可以删去 数组中的元素 问最少删除多长 使得满足上面条件
    获得硬币 ai-1  支付硬币 ai+1
    3
  5 5 5   -> 4 5 5 -> 3 5 5 -> 3 4 5  out 0

  4
  2 3 2 4   -> 凑不出 ->  2 3  out 2

  3
  2 100 2 -> 2 3 97  out 0

   5
2 4 2 11 2   ->2 3 4 10 ->2 3 5 7 out 1
*/

ll prime[N], cnt = 0;
bool st[M];
ll sum[N];
void init()
{
    for (ll i = 2; i < M; i++)
    {
        if (!st[i])
            prime[cnt++] = i;
        for (ll j = 0; prime[j] * i < M && j < cnt; j++)
        {
            st[prime[j] * i] = true;
            if (i % prime[j] == 0)
                break;
        }
    }
    rep(i, 0, cnt - 1)
    {
        sum[i + 1] = sum[i] + prime[i];
    }
}

void solve()
{
    ll n;
    cin >> n;
    vll a(n + 1, 0);
    ll summ = 0, num = 0;
    rep(i, 1, n) cin >> a[i], summ += a[i];
    sort_range(a, 1, n);
    rep(k, 0, n)
    {
        if (summ - num >= sum[n - k])
        {
            cout << k << endl;
            return;
        }
        if (k < n)
            num += a[k + 1];
    }
}

int main()
{
    IOS;
    int _ = 1;
    cin >> _; // 如果是多组数据
    init();
    while (_--)
    {
        solve();
    }
    return 0;
}
```