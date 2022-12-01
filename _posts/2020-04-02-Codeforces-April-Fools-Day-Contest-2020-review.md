---
title: "Codeforces April Fools Day Contest 2020 review"
date: 2020-04-02 14:30:00 +0900
categories:
- PS
- university
tags:
- codeforces
- assignment
- review
---

<!-- more -->

# Codeforces April Fools Day Contest 2020 review

<br />

---

<br />

# 1. 대회 소개

[대회 링크](https://codeforces.com/contest/1331)

![출처 : https://codeforces.com/contest/1331](/images/2020-04-02/April_Fools_Day_Contest_2020_introduction.JPG)

4/1일에 진행된다.. 레이팅에 반영되지 않는다[^1].. 출제자와 유머 코드가 맞아야 한다..? 등의 내용입니다.



![출처 : https://codeforces.com/contests](/images/2020-04-02/participants.JPG)

세계 각국에서 __19470__ 분이나 참가하셨습니다.

<br />

---

<br />

# 2. 목차

![출처 : https://codeforces.com/contest/1331](/images/2020-04-02/Problems_list.JPG)

문제 목차입니다. <span style="color:green">초록색</span>은 제가 맞힌 문제, <span style="color:red">빨간색</span>은 제가 시도했지만 틀린 문제입니다.

총 8문제로 구성되었고, [우리나라 시계 기준 4/1 밤 11시 35분](https://www.timeanddate.com/worldclock/fixedtime.html?day=1&month=4&year=2020&hour=17&min=35&sec=0&p1=166)부터 2시간 동안 진행되었습니다. 

<br />

---

<br />

# 3. 문제 풀이

![출처 : https://codeforces.com/contest/1331/problem/A](/images/2020-04-02/A.JPG)

[`A번 문제`](https://codeforces.com/contest/1331/problem/A)입니다. 첫 문제부터 입출력 예제와 문제에 대한 설명이 하나도 없습니다...

<br />

### 풀이

문제 이름이 __"Is it rated?"__ 입니다.

대회 소개에서 `"... and it will be unrated."` 라 했으므로, NO를 출력하면 되는 문제였습니다.

```c++
#include <cstdio>
using namespace std;
 
int main()
{
    printf("NO");
    return 0;
}
```

<br />

---

<br />

![출처 : https://codeforces.com/contest/1331/problem/B](/images/2020-04-02/B.JPG)

[`B번 문제`](https://codeforces.com/contest/1331/problem/B)입니다. 문제 설명은 풀이와 아무 관련이 없는듯합니다..

<br />

### 풀이

`input`과 `output`간의 규칙을 보면, 

| Test case | input | output        |
| --------- | ----- | ------------- |
| #1        | 35    | 57  (5*7)     |
| #2        | 57    | 319  (3*19)   |
| #3        | 391   | 1723  (17*23) |

output은 소수의 오름차순 곱으로 이루어져 있다는 것을 알 수 있습니다!

```c++
#include <cstdio>
using namespace std;
 
int prime[12] = { 2,3,5,7,11,13,17,19,23,29,31 };
 
int main(void)
{
    int a;
    scanf("%d", &a);
    for (int i = 0; i <= 10; i++)
    {
        if (a % prime[i] == 0)
            while (a % prime[i] == 0)
            {
                printf("%d", prime[i]);
                a /= prime[i];
            }
        if (a == 1)
            break;
    }
    if (a != 1)
        printf("%d", a);
    return 0;
}
```

<br />

---

<br />

![출처 : https://codeforces.com/contest/1331/problem/C](/images/2020-04-02/C.JPG)

[`C번 문제`](https://codeforces.com/contest/1331/problem/C)입니다. 풀이를 생각해내는 데 한참 걸렸습니다.

문제 이름을 해석하면 "... 그리고 그들은 행복하게 살았답니다." 정도인 것 같습니다.

동화의 마무리 멘트 같은 느낌이네요.

<br />

### 풀이

__a의 범위가 0~63__ 인 것에 착안하여, `input`과 `output`을 **6개의 2진수 비트** 로 나타내면 다음과 같습니다.

| Test case | input(binary) | output(binary) | 비트 이동        |
| --------- | ------------- | -------------- | ---------------- |
| #1        | 000010        | 000010         | 2->2             |
| #2        | 000101        | 011000         | 1->5, 3->4       |
| #3        | 100011        | 110010         | 1->5, 2->2, 6->6 |

표의 `비트 이동`과 같은 규칙으로 비트가 이동했음을 알 수 있습니다.

예시만으로는 4번째 비트와 5번째 비트가 어디로 이동하는지 알 수 없으므로, ~~운으로 찍었습니다.~~

>  (더 정확한 풀이를 아시는 분은 <dongbin1999@inu.ac.kr> 로 알려주세요!)

```c++
#include <cstdio>
using namespace std;
 
int main(void)
{
    int a;
    scanf("%d", &a);
    int b[6] = { 0 };
    for (int i = 0; i < 6; i++)
        if ((a & (1 << i)) != 0)
            b[i] = 1;
    int ans = 0;
    if (b[0])
        ans += 16;
    if (b[1])
        ans += 2;
    if (b[2])
        ans += 8;
    if (b[3])
        ans += 4;
    if (b[4])
        ans += 1;
    if (b[5])
        ans += 32;
    printf("%d", ans);
    
    return 0;
}
```

<br />

---

<br />

![출처 : https://codeforces.com/contest/1331/problem/D](/images/2020-04-02/D.JPG)

[`D번 문제`](https://codeforces.com/contest/1331/problem/D)입니다. 오른쪽 아래`Problem tags`에 `chinese remainder theorem`[^2]라고 나와있는데, 저게 왜 필요한지 잘 모르겠습니다. 만우절 디테일에 신경 쓴 듯합니다.

<br />

### 풀이

A 뒤에 나오는 숫자를 2로 나눈 나머지를 출력하면 됩니다.

```c++
#include <cstdio>
using namespace std;
 
int main(void)
{
    int a;
    char c;
    scanf("%c", &c);
    scanf("%d", &a);
    printf("%d", a % 2 == 0 ? 0 : 1);
    return 0;
}
```

<br />

---

<br />

__여기서부터는 제가 풀지 못한 문제들이라 짧게 리뷰하고 넘어가겠습니다.__

![출처 : https://codeforces.com/contest/1331/problem/E](/images/2020-04-02/E1.JPG)

![출처 : https://codeforces.com/contest/1331/problem/E](/images/2020-04-02/E2.JPG)

[`E번 문제`](https://codeforces.com/contest/1331/problem/E)입니다. 푸는 데 상당히 많은 시간이 걸릴 것 같은 문제입니다.

<br />

### 풀이

`input`좌표가 그림 속 얼굴 안쪽이면 IN을, 바깥쪽이면 OUT을 출력하는 문제 같습니다.

저는 주어진 시간인 2시간 내에 풀지 못할 것 같아 넘겼습니다.  __~~귀찮아서~~__

<br />

---

<br />

![출처 : https://codeforces.com/contest/1331/problem/F](/images/2020-04-02/F.JPG)

[`F번 문제`](https://codeforces.com/contest/1331/problem/F)입니다. 풀이가 너무 궁금하여 다른 분들의 코드를 참고했는데, 저는 대회 시간이 10시간이었더라도 못 풀었을 문제입니다. 풀이를 보시기 전에 한 번 고민해보세요!

<br />

### 풀이

<details><summary>풀이 보기</summary>주기율표의 원소기호만 사용하여 `input`의 단어를 만들 수 있으면 `YES`를, 아니면 `NO`를 출력하는 문제입니다.
예를 들어, GENIUS -> 'Ge(저마늄)' + 'N(질소)' + 'I(아이오딘)' + 'U(우라늄)' + 'S(황)'으로 표현이 가능하므로 'YES'입니다.</details>

<br />

---

<br />

[`G번 문제`](https://codeforces.com/contest/1331/problem/G), [`H번 문제`](https://codeforces.com/contest/1331/problem/H)는 코드를 참고해도 모르겠습니다..

특히 H번 문제는 `UnknownX`라는 언어로 제출 언어 제한이 걸려있습니다.

H번 문제의 풀이 자체는 `n`의 [double factorial](https://en.wikipedia.org/wiki/Double_factorial)을 `mod`로 나눈 나머지를 구하라는 문제인데, C++ 코드를 그대로 제출하니 <span style="color:blue">`Compilation error`</span>를 받았습니다.

제출했던 코드는 아래와 같습니다.

```c++
#include <cstdio>
using namespace std;
 
int main(void)
{
    int temp;
    scanf("%d", &temp);
    int n = temp / 1000;
    int mod = temp % 1000;
    int ans = 1;
    for (int i = n; i > 0; i -= 2)
        ans = (ans * i) % mod;
    
    printf("%d", ans);
    return 0;
}
```

<br />

---

<br />

# 4. 결과

![출처 : https://codeforces.com/contest/1331/standings](/images/2020-04-02/standing.JPG)

제 성적입니다.

+ __<span style="color:green">초록색 +</span>__ 는 맞힌 문제, __<span style="color:green">+</span>__ 뒤의 숫자는 틀린 횟수를 나타냅니다.
+ __틀린 횟수 당 10분의 패널티가 주어집니다.__
+ __<span style="color:blue">`-2`</span>__ 는 2번 틀리고 풀지 못했음을 나타냅니다.
+ `Tried`는 각 문제당 제출된 코드 수, __<span style="color:green">`Accepted`</span>__ 는 그중 맞힌 사람의 수를 나타냅니다.

<br /><br /><br />

혹시 코딩에 관심 있으신 분은 코드포스 대회에 참여해보시는 걸 추천합니다!

여기까지 후기였습니다. 긴 글 봐주셔서 감사합니다!

<br />

[^1]: Codeforces는 대회 성적을 반영한 rating시스템이 있습니다.
[^2]: [중국인의 나머지 정리]([https://namu.wiki/w/%EC%A4%91%EA%B5%AD%EC%9D%B8%EC%9D%98%20%EB%82%98%EB%A8%B8%EC%A7%80%20%EC%A0%95%EB%A6%AC](https://namu.wiki/w/중국인의 나머지 정리))