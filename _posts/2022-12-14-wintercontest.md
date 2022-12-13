---
title: "겨울 숲의 초대 후기"
date: 2022-12-14 02:42:00
categories:
- PS
tags:
- review
---

![scoreboard](C:\Users\leedongbin\dongbin1999.github.io\assets\images\2022-12-14\scoreboard.JPG)

망했다.

<!-- more -->

![badge](C:\Users\leedongbin\dongbin1999.github.io\assets\images\2022-12-14\badge.JPG)

![background](C:\Users\leedongbin\dongbin1999.github.io\assets\images\2022-12-14\background.JPG)

귀여운 프로필 뱃지와 배경을 모두 받을 수 있는 대회였다. 실력 테스트 겸 컬렉션 수집하려고 참여했는데, B번에서 머리가 마구마구 꼬여버렸다.

### A.[눈 치우기](https://www.acmicpc.net/problem/26215)

동시에 두 집 앞의 눈을 치우는 행동을 최대한 많이 해야 한다.

그런데 아무렇게나 두 집을 골라서 치우면, 나중에 눈이 많이 쌓인 집 하나만 남아서 비효율적이게 된다.

따라서 크기순으로 정렬한 뒤 눈이 많은 집 두 개를 골라 치우는 작업을 반복해주면 된다.

```c++
#include <bits/stdc++.h>
using namespace std;

int a[100001];

int main(){
    int n;scanf("%d",&n);
    int ans=0;
    priority_queue<int> pq;
    for(int i=1;i<=n;i++)
        scanf("%d",&a[i]),pq.push(a[i]);
    while(pq.size()>1){
        int x=pq.top();pq.pop();
        int y=pq.top();pq.pop();
        ans+=y;
        pq.push(x-y);
    }
    ans+=pq.top();
    if(ans>1440)ans=-1;
    printf("%d",ans);
    return 0;
}
```

### B.[은나무](https://www.acmicpc.net/problem/26216)

먼저, 만들어지는 노드의 총 개수를 생각해보자.

* 모든 흰색 노드가 가지는 파란색 자식은 K개 이다.

* 높이가 H일 때, 흰색 노드의 개수는 아래와 같다.
$$
  1+(K+1)+(K+1)^2 + ... + (K+1)^{H-1} = \frac{(K+1)^{H}-1}{(K+1)-1} = \frac{(K+1)^{H}-1}{K}
$$


따라서 파란색 노드의 개수는 $(K+1)^{H}-1$ 개이고, 이는 **길이가 H 이하인 (K+1) 진법의 수들**로 표현할 수 있다.

파란색 노드가 은나무 내에 존재하는지 여부는 주어진 키값이 $(K+1)^{H}$보다 작은지 확인해 주면 된다.

두 파란색 노드를 연결하는 경로의 길이를 알려면 두 노드의 LCA(Lowest Common Ancestor)를 알아야 한다.

이 때 LCA란, 동시에 두 노드의 부모이면서 깊이가 가장 깊은 노드를 말한다.

두 노드 중 깊이가 더 깊은 노드를 한 단계씩 부모 노드로 올려가면서, 두 노드가 만날 때까지 반복해주면 된다.

하지만 총 노드의 수가 너무 많아서 직접 트리를 구현하는 것은 안 되고, 나는 아래 그림처럼 흰색 노드에 적절한 키값을 대입하는 방식으로 풀었다.

![example](C:\Users\leedongbin\dongbin1999.github.io\assets\images\2022-12-14\example.png)

흰색 노드에 대입해준 키값은, 흰색 노드의 깊이를 h라고 했을 때, **$(K+1)^{H+1-h}$ 의 배수이면서, 자기 자식들의 키값보다 큰 수 중 가장 작은 수...** 로 정했다. 지금 생각해봐도 좋은 접근은 아닌 것 같다. 꼬여버린 머리로 어떻게든 꾸역꾸역 푼 문제였다.

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<int,int> pii;
typedef pair<ll,ll> pll;
const ll mod=1000000007;
#define UNIQUE(v) sort(v.begin(),v.end()),v.erase(unique(v.begin(),v.end()),v.end());
ll GCD(ll a,ll b){return b?GCD(b,a%b):a;}
ll power(ll a,ll b){ll ret=1;while(b){if(b%2)ret=ret*a%mod;a=a*a%mod;b/=2;}return ret;}

bool exist(ll a,ll k,ll h){
    while(h--)a/=k;
    return !a;
}

ll f(pll a,ll k){
    ll d=k;while(a.second--)d*=k;
    return (a.first-1+d)/d*d;
}

int main(){
    ll k,h,q;scanf("%lld %lld %lld",&k,&h,&q);
    k++;
    while(q--){
        ll a,b;scanf("%lld %lld",&a,&b);
        if(!exist(a,k,h)||!exist(b,k,h)) printf("-1\n");
        else if(a==b) printf("0\n");
        else{
            ll ans=2;
            pair<ll,ll> x={a,0},y={b,0};
            ll aa=a,bb=b;
            while(aa%k==0)x.second++,aa/=k;
            while(bb%k==0)y.second++,bb/=k;
            x={f(x,k),x.second+1},y={f(y,k),y.second+1};
            while(x!=y){
                if(x.second>y.second) swap(x,y);
                x={f(x,k),x.second+1};
                ans++;
            }
            printf("%lld\n",ans);
        }
    }
    return 0;
}
```

이 문제에서 시간을 다 써버렸다. 꼬였던 머리만큼이나 코드도 더러워진 모습.

### C.[별꽃의 세레나데 (Easy)](https://www.acmicpc.net/problem/26217)

예제 설명에서 준 힌트가 큰 도움이 된 문제다.

$N$ 이 입력으로 들어올 때, $N + N/2 + N/3  + ... +N/N$ 을 출력하면 되는 문제이다.

```c++
#include <bits/stdc++.h>
using namespace std;

int main(){
    int n;scanf("%d",&n);
    double ans=0.0;
    for(int i=1;i<=n;i++)ans+=(double)n/(double)(i);
    printf("%.10lf",ans);
    return 0;
}
```

### D. [생산 시스템 관리](https://www.acmicpc.net/problem/26218) / Upsolving

dp[i]\[j] : 추가로 구매해야 하는 기계의 개수를 1~i번째 까지 확정지었고,지금까지 쓴 총 비용이 j일때,
{($10^{2i}$ * P)의 최댓값, {추가 구매한 i번째 기계,j}} 를 저장하면서 knapsack을 돌리면 된다.

출력에서 $P*10^{2N}$만 물어봤다면, dp배열에 ($10^{2i}$ * P)의 최댓값만 있으면 된다. pair의 second 부분은 단순히 백트래킹을 위해 가지고 있는 정보이다.

백트래킹을 더 쉽게 할 수 있는 방법이 있을 것 같은데, PS가 너무 오랜만이라 방법을 잘 모르겠다.

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<ll,pair<ll,ll>> plll;

plll dp[10][30001];
ll p[10],a[10],c[10];

int main(){
    int n,b;scanf("%d%d",&n,&b);
    dp[0][0]={1,{0,0}};
    for(int i=1;i<=n;i++){
        scanf("%lld%lld%lld",&p[i],&a[i],&c[i]);
        for(ll buy=0,mx=(100-p[i]+a[i]-1)/a[i];buy<=mx;buy++){
            ll percent=min(100ll,p[i]+buy*a[i]),price=buy*c[i];
            for(int cost=0;cost<=b-price;cost++)
                dp[i][cost+price]=max(dp[i][cost+price],{dp[i-1][cost].first*percent,{buy,cost+price}});
        }
    }
    plll back={0,{0,0}};
    vector<ll> ans;
    for(int cost=0;cost<=b;cost++)
        back=max(back,dp[n][cost]);
    printf("%lld\n",back.first);
    while(ans.size()<n){
        ans.push_back(back.second.first);
        back=dp[n-ans.size()][back.second.second-back.second.first*c[n-ans.size()+1]];
    }
    reverse(ans.begin(),ans.end());
    for(auto i:ans)printf("%lld ",i);
    return 0;
}
```

이 문제는 B번 문제에서 멘탈과 시간이 모두 날아가버려서 못풀었다. ㅠㅠ



## 후기

전체적으로 수학 문제가 엄청 많다고 느껴졌던 대회였다. 평소에 수학 문제에 자신 있는 편이였는데, 내가 모르는 수학 문제는 아직도 많았다.

내년에 UCPC, ICPC에서 예선을 뚫으려면 플래티넘 하위 문제까지는 막힘없이 풀어야 하는데, 아직 플래티넘4 E번 문제도 어떻게 푸는지 모르겠다.

복학하기 전까지 PS 감을 되찾아야겠다.

