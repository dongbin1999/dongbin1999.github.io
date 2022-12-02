---
title: "Greedy Algorithm"
date: 2020-04-16 15:50:00 +0900
categories:
- PS
- university
tags:
- codeforces
- assignment
- review
---

<!-- more -->

## [Codeforces Round #635 (Div. 2) #C 문제](https://codeforces.com/contest/1337/problem/C)

오늘은 4/15 어제밤에 치뤘던 대회의 `greedy algorithm` 문제에 대해 소개드리겠습니다.



![C](/assets/images/2020-04-16/C.JPG)

### 문제

* 왕국에는 <span style="color:blue">`n`</span>개의 도시와 <span style="color:blue">`n-1`</span>개의 양방향 도로가 있다.
* 어느 도시에서든, 다른 도시로 가는 길이 존재한다.
* 도시는 `1`부터 `n`까지 번호가 매겨져 있고, __도시 `1`은 왕국의 <span style="color:green">수도</span>이다. <span style="color:red">=> (트리 구조)</span>__
* Linova는 정확히 <span style="color:blue">`k`</span>개의 도시를 선택하여, <span style="color:purple">산업도시</span>로 만들것이다.
* 1년에 한번  <span style="color:green">수도</span>에서 회의가 열린다. 회의에 참석하기 위해 각 <span style="color:purple">산업도시</span>에서 <span style="color:skyblue">사절</span>을 보낸다. 모든 <span style="color:skyblue">사절</span>들은 <span style="color:red">가장 짧은 경로</span>로 <span style="color:green">수도</span>로 향한다.
* <span style="color:green">수도</span>로 가는 길에, 각 <span style="color:skyblue">사절</span>은 그가 가는 길의 <span style="color:purple">관광도시</span> 수 만큼 <span style="color:blue">행복함</span>을 느낀다.
* Linova는 모든 <span style="color:skyblue">사절</span>들의 <span style="color:blue">행복함</span>의 합이 최대가 되도록 <span style="color:blue">`k`</span>개의 도시를 선택하고 싶어한다.

<br />

### 입력

* 첫 번째 줄에 두 개의 정수 <span style="color:blue">`n`(도시의 수)</span>과 <span style="color:purple">`k`(산업도시 수)</span> $(2≤n≤2⋅10^5, 1≤k<n)$ 가 주어진다.
* 다음 n-1개의 줄에 각각 두 개의 정수 <span style="color:blue">`u`</span>와 <span style="color:blue">`v`</span> $(1≤u,v≤n)$ 가 주어지며, 이는 <span style="color:blue">도시 `u`</span>와<span style="color:blue">도시 `v`</span>를 연결하는 도로가 있음을 나타낸다.

<br />

### 출력

* 모든 <span style="color:skyblue">사절</span>들의 <span style="color:blue">행복함</span>의 최대 합계를 출력한다.



<br />

<br />

<br />

---

## 풀이

우선, 수도(루트 노드)로 가는 사절들의 최단 경로의 길이는, 해당 산업도시의 레벨의 값과 같습니다.

다음의 예제를 트리로 그려봅시다.

![Example](/assets/images/2020-04-16/Example.JPG)



![tree](/assets/images/2020-04-16/tree.png)

이 상태에서, 각 노드의 레벨은 __`DFS`__ 로 구현할 수 있습니다.

<br />

그 코드입니다.

```c++
vector<int> tree[200001];
int lv[200001];

void go(int node, int level, int parent)
{
	lv[node] = level; //현재 자신의 레벨값 저장.
	int size = tree[node].size(); //각 도시와 인접한 도시의 수
	for (int i = 0; i < size; i++)
		if (parent != tree[node][i]) //부모가 아닌 모든 인접 노드(자식 노드)를 방문하면서,
			go(tree[node][i], level + 1, node); //자식 노드이므로 level+1. 그 부모는 현재 자신.
}
```

<br />

이렇게 모든 노드의 레벨을 `lv`배열에 저장해놓고, 값을 출력해보면 다음과 같습니다.

```c++
for (int i = 1; i <= N; i++)
		printf("lv[%d] = %d\n", i, lv[i]);
```

```c++
lv[1] = 0
lv[2] = 1
lv[3] = 2
lv[4] = 3
lv[5] = 2
lv[6] = 1
lv[7] = 1
lv[8] = 3
```

<br />

우리가 원하는 값은 모든 <span style="color:skyblue">사절</span>들의 <span style="color:blue">행복함</span>의 최대 합계이므로, __매 순간마다 `lv`값이 가장 큰 도시를 <span style="color:blue">`k`</span>번 선택합니다. (greedy)__ 지난시간에 배운 `분할정복`을 이용한 `merge sort` 또는 `quick sort`로 레벨값을 내림차순 정렬한 후 <span style="color:blue">`k`</span>개 만큼의 합을 구하면 될 듯 합니다. `nlogn`의 시간복잡도입니다.

<br />

`C++` 에는`nlogn` 시간복잡도로 정렬해주는 `sort`함수가 `#include <algorithm>` 헤더 파일에 있으므로, 그걸 사용하겠습니다.

```c++
#include <cstdio>
#include <vector>
#include <algorithm> // sort()
#include <functional> //greater<>()
#define ll long long
using namespace std;

vector<int> tree[200001];
int lv[200001];

void go(int node, int level, int parent)
{
	lv[node] = level;
	int size = tree[node].size();
	for (int i = 0; i < size; i++)
		if (parent != tree[node][i])
			go(tree[node][i], level + 1, node);
}

int main()
{
	int N, k, u, v;
	scanf("%d %d", &N, &k);
	for (int i = 1; i < N; i++)
	{
		scanf("%d %d", &u, &v);
		//양방향 도로
		tree[u].push_back(v);
		tree[v].push_back(u);
	}

	go(1, 0, 1);
	sort(lv + 1, lv + 1 + N, greater<>()); //내림차순 정렬

	ll ans = 0; //값이 int형 범위를 넘어갈 수 있습니다.
	for (int i = 1; i <= k; i++)
		ans += (ll)lv[i];
	printf("%lld", ans);
	return 0;
}

//출력결과 : 11.
```

값이 `11`이 나옵니다. 예제의 답 `9`와 다르네요.

그 이유에 대해 생각해봅시다.

<br />

---

위의 `lv`배열을 내림차순으로 정렬하면, `{3,3,2,2,1,1,1,0}` 이 됩니다. 따라서 <span style="color:blue">`k`</span> 가 `5`로 주어졌으므로, `3+3+2+2+1 = 11`을 출력한 것입니다. 이 경우를 그림으로 나타내봅시다.



![wrong example](/assets/images/2020-04-16/wrong-example.png)

위의 그림에서 <span style="color:green">`4번 도시`</span>, <span style="color:green">`8번 도시`</span>를 고를때까진 문제가 없습니다. 하지만 <span style="color:skyblue">`5번 도시`</span>와 <span style="color:skyblue">`3번 도시`</span>를 고를때,

__이 도시들이 <span style="color:purple">관광도시</span>에서 <span style="color:purple">산업도시</span>로 바뀌는 과정에서 <span style="color:green">`4번 사절`</span>과 <span style="color:green">`8번 사절`</span>의 <span style="color:blue">행복함</span>이 1씩 감소하게됩니다.__ 

그렇다면, `x`번 도시가 <span style="color:purple">산업도시</span>로 선택됨으로 인해  <span style="color:blue">행복함</span>이 감소되는 사절의 수는 어떻게 구할까요?

그 답은 __`x`번 도시의 <span style="color:blue">`자손 노드의 수`</span>__ 입니다. 왜냐하면 우리는 레벨이 높은 도시부터 우선적으로 골라왔기때문에, 어떤 노드를 고를 때 그 자손 노드들은 이미 다 선택되어있을 것입니다. 따라서 다음과 같은 상황이 됩니다.

![corrected example](/assets/images/2020-04-16/corrected-example.png)

따라서 `2+2+2+2+1 = 9`로 정확한 답이 됩니다. _(위의 그림에서 `7`을 고른다면 답보다 값이 작아집니다.)_

답을 출력하기 위한 과정은 다음과 같습니다.

* __`DFS`__ 과정에서 각 노드의 <span style="color:blue">`자손 노드`</span>의 수를 저장하는 `descendant`배열을 만듭니다.
* 도시 `x`를 선택할 때 발생하는 <span style="color:blue">행복함</span>의 값은, __`lv[x]` - `descendant[x]`__ 입니다. (자손 노드의 수만큼 총 <span style="color:blue">행복함</span> 값이 감소하고, 자신의 `lv`값 만큼 <span style="color:blue">행복함</span>이 증가하므로)
* __위의 값이 큰것부터 <span style="color:blue">`k`</span>개를 뽑아 더한 값을 출력하면 됩니다.(greedy)__

<br />

그 코드입니다.

```c++
#include <cstdio>
#include <vector>
#include <algorithm>
#include <functional>
#define ll long long
using namespace std;

vector<int> tree[200001];
int lv[200001];
int descendant[200001];

int go(int node, int level, int parent)
{
	lv[node] = level;
	int size = tree[node].size(), d = 0;

	for (int i = 0; i < size; i++)
		if (parent != tree[node][i])
		//[현재 자식의 자손 수 + 현재 자식노드(1)]을 모든 자식에 대해 반복 => 현재 노드의 총 자손 수
			d += go(tree[node][i], level + 1, node) + 1;

	return descendant[node] = d;
}

int main()
{
	int N, k, u, v;
	scanf("%d %d", &N, &k);
	for (int i = 1; i < N; i++)
	{
		scanf("%d %d", &u, &v);
		tree[u].push_back(v);
		tree[v].push_back(u);
	}

	go(1, 0, 1);
	for (int i = 1; i <= N; i++)
		lv[i] -= descendant[i];
	sort(lv + 1, lv + 1 + N, greater<>());

	ll ans = 0;
	for (int i = 1; i <= k; i++)
		ans += (ll)lv[i];
	printf("%lld", ans);
	return 0;
}
```

