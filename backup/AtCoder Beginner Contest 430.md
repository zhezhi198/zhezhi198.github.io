[点这里进入比赛界面](https://atcoder.jp/contests/abc430)

### C - Truck Driver
> 题意:
已知长度为n的字符串s，区间内的限制条件：A个‘a’字符，B个'b'字符，求有多少个不同的(l,r)区间满足'a'的数量>=A且'b'的数量<B。

> 思路:
问题要求统计所有满足条件的连续子串（即子串中 'a'的数量 ≥ A，且 'b'的数量 < B）。这类问题通常涉及对大量重叠子串的检查，暴力枚举所有子串（O(n²)）在 N最大为 3×10⁵ 时会严重超时。且当子串的起点 i向右移动时，其有效终点的范围也具单调性（即终点 j只能向右移动，不会回退）。这是因为：起点 i右移后，窗口缩小，'a'和 'b'的计数减少，但为了重新满足条件，终点 j可能需要向右扩展以纳入更多字符。这种单调性使得双指针可以高效跟踪变化，避免重复计算。所以这题可以用滑动窗口来优化暴力求法.
我们用i,l,r三个指针来维护滑动窗口，分工如下:

>i(起点指针):表示字串可能的起点，每次右移动后计数中移除对s[i]的影响。

>l(满足'a'条件的指针):对于当前起点i，向右移动l，直到窗口[i,l-1]中'a'的数量>=A.此时l指向的第一个满足'a'条件的位置之后(实际有效终点从l-1开始)。

>r(满足'b'条件的指针):向右移动 r，直到窗口 [i, r-1]中 'b'的数量严格<B此时 r指向第一个可能使 'b'数量超标的位置（实际有效终点到 r-1为止）。

>框架如下：
 ```cpp
for (int i = 1, j = 1; j <= n; j++) {
    // ... 更新窗口状态（如 cntb++）
    while (i <= j && 窗口条件不满足) {
        // ... 移除 s[i] 的影响（如 if (s[i]=='b') cntb--;）
        i++; // i 右移，收缩窗口！
    }
    // 此时，所有以 i 到 j 为起止点的子串都是潜在解
    if (条件满足) {
        ans += (j - i + 1); // 统计有效子串数
    }
}
```
（不知道这个放进来为什么是这样的格式）

所以我们只需要填入条件加上细心的边界处理就可以完成这个题目

>代码如下:

```cpp
#include <bits/stdc++.h>
using namespace std;
//CJX__//
typedef long long ll; // 不开long long 见祖宗
typedef unsigned long long ull;
typedef __int128 i128;
typedef pair<int, int> PII;
typedef pair<ll, ll> PLL;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef vector<double> vd;
typedef vector<PII> vPII;
#define IOS ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
#define out(x) cout << ((x) ? "YES" : "NO") << endl
#define mod(x, P) (((x) % (P) + (P)) % (P))
#define endl '\n'
#define gcd __gcd
#define lc p<<1
#define rc p<<1|1
#define INF 0x3f3f3f3f3f3f3f3f
#define inf 0x3f3f3f3f
#define fi first
#define se second
#define all(x) x.begin(), x.end()
#define lowbit(x) ((x)&(-x))
#define rep(i, x, n) for (ll i = x; i <= n; i++)
#define dep(i, x, n) for (ll i = x; i >= n; i--)
#define mem(a, x) memset(a, x, sizeof a)
const double eps=1e-5;
const int N = 1e5 + 10,M=2*N,K=26;
const ll MOD = 1e9 + 7,Md3 = 998244353, Md7 = 1e9 + 7, Md9 = 1e9 + 9;
const int dx[8] = {-1, 0, 1, 0, -1, -1, 1, 1}, dy[8] = {0, 1, 0, -1, -1, 1, -1, 1};
const int ddx[8] = {1, 1, 2, 2, -1, -1, -2, -2}, ddy[8] = {2, -2, 1, -1, 2, -2, 1, -1};
template<typename T> bool cmin(T &a, const T &b) { return b < a ? a = b, 1 : 0; }
template<typename T> bool cmax(T &a, const T &b) { return b > a ? a = b, 1 : 0; }
template<typename T> void sort_range(vector<T> &v, int l, int r) { sort(v.begin() + l, v.begin() + r + 1); }
struct Random { mt19937_64 rng; Random() : rng(chrono::steady_clock::now().time_since_epoch().count()) {} ull rand_ull(ull max_val = -1) { return rng() % (max_val + 1); } ll rand_ll(ll l, ll r) { return uniform_int_distribution<ll>(l, r)(rng); } int rand_int(int l, int r) { return uniform_int_distribution<int>(l, r)(rng); } double rand_db(double l, double r) { return uniform_real_distribution<double>(l, r)(rng); } bool rand_bool(double p = 0.5) { return bernoulli_distribution(p)(rng); } template<typename T> void shuffle(vector<T> &v) { std::shuffle(v.begin(), v.end(), rng); } };
ll qmi(ll a, ll b, ll p) { ll res = 1 % p; a %= p; while (b) { if (b & 1) res = res * a % p; a = a * a % p; b >>= 1; } return res; }
/*

}
*/
	   
       
void solve()
{
	ll n,na,nb; cin>>n>>na>>nb;
	string s; cin>>s;
	s=" "+s;
	ll cnta=0,cntb=0,ans=0;//记录区间内 a b字符的数量 ans记录合法的区间数
	for(int i = 1, l = 1, r = 1; i <= n; i++)
	{
		while(l<=n&&cnta<na)
		{
			cnta+=s[l]=='a';
			l++;
		}
		while(r<=n&&cntb+(s[r]=='b')<nb)
		{
			cntb += ((s[r]=='b'));
			r++;
		}
		if(cnta>=na&&cntb<nb&&l<=r){
			ans+=r-l+1;
		}
		 /**
         * 准备处理下一个起点(i+1)：从当前计数中移除起点i处的字符
         * 这是因为下一轮循环i会递增，窗口起点变为i+1
         * 需要从计数中移除不再属于新窗口的字符s[i]
         */
		cnta-=(s[i]=='a');
		cntb-=(s[i]=='b');
	}
	cout<<ans<<endl;
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


