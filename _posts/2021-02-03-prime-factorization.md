---
title: "prime-factorization"
date: 2021-02-03 05:02:00 +0900
categories:
- algorithm
tags:
- prime-factorization
- sieve-of-Eratosthenes
- under-prime
---

<!-- more -->

# 1. 에라토스테네스의 체 (sqrt(n))

```c++
#include <bits/stdc++.h>
using namespace std;
//n<=sz^2이 되도록 sz 적당히 크게 잡기. n은 소인수분해 할 가장 큰 수.
//고쳐야 할 부분 (1)~(2)
const int sz=3163;//(1)
bool no_prime[sz+1]={true,true};
vector<int> prime;

int main()
{
    int n; scanf("%d",&n);
    
    for(int i=2;i*i<=n;i++)//(2)
        if(!no_prime[i])
        {
            prime.push_back(i);
            for(int j=i*2;j<=sz;j+=i)
                no_prime[j]=true;
        }

    for(int i:prime)
        while(n%i==0)
        {
            printf("%d\n",i);
            n/=i;
        }
    //prime 벡터에 없는 큰 소수가 남았다면 직접 출력.
    if(n!=1) printf("%d",n);
    return 0;
}
```



# 관련문제

[백준11653 : 소인수분해](https://www.acmicpc.net/problem/11653)











# 2. 언더 프라임 (log(n))

```c++
#include <bits/stdc++.h>
using namespace std;
//n<=sz이 되도록. n은 소인수분해 할 가장 큰 수.
const int sz=5000000;
int under_prime[sz+1];//under_prime[i] : i을 나누는 가장 작은 소수.

void logsieve()
{
    under_prime[1]=1;
    //1+(1/2)+(1/3)+...+(1/sz) 는 log sz로 수렴.
    for(int i=2;i<=sz;i++)
        if(!under_prime[i])
            for(int j=i;j<=sz;j+=i)
                if(!under_prime[j])
                    under_prime[j]=i;
}

int main()
{
    //메인에서 함수 실행하기.
    logsieve();
    int n; scanf("%d",&n);
    while(n--)
    {
        int k; scanf("%d",&k);
        vector<int> factor;
        while(k>1)
        {
            factor.push_back(under_prime[k]);
            k/=under_prime[k];
        }
        for(int i:factor)
            printf("%d ",i);
        printf("\n");
    }
    return 0;
}
```



# 관련문제

[백준16563 : 어려운 소인수분해](https://www.acmicpc.net/problem/16563)