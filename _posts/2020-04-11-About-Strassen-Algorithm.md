---
layout: single
title:  "About Strassen Algorithm"
date:   2020-04-11 20:30:00 +0900
categories: jekyll update
---

스트라센 알고리즘은 분할 정복을 이용한 알고리즘으로,

$O(n^3)$ 으로 알려진 행렬 곱셈을 약 $O(n^{2.807})$ 으로 더 빠르게 구하는 알고리즘입니다.

스트라센 알고리즘에 대한 이해를 돕기 위해, 일반적인 행렬 곱셈 방법부터 알아봅시다.

<br />

---

### 1.일반적인 행렬 곱셈

$A*B = C$ 를 만족하는 $n*n$크기의 행렬 $A, B, C$ 에서, 일반적인 행렬 곱셈 방법은 다음과 같습니다.
$$
AB = C =\begin{bmatrix}
\sum_{k=1}^nA_{1k}B_{k1} & \sum_{k=1}^nA_{1k}B_{k2} & \cdots & \sum_{k=1}^nA_{1k}B_{kn}
\\\sum_{k=1}^nA_{2k}B_{k1} & \sum_{k=1}^nA_{2k}B_{k2} & \cdots & \sum_{k=1}^nA_{2k}B_{kn}
\\\vdots & \vdots & \ddots & \vdots
\\\sum_{k=1}^nA_{nk}B_{k1} & \sum_{k=1}^nA_{nk}B_{k2} & \cdots & \sum_{k=1}^nA_{nk}B_{kn}
\end{bmatrix}
$$
이를 코드로 나타내면 아래와 같습니다.

```c++
void normal_mult(int n, int A[][], int B[][], int C[][])
{
	for (int i = 1; i <= n; i++)
		for (int j = 1; j <= n; j++)
		{
			C[i][j] = 0; //초기화. 미리 해두었다면 생략 가능.
			for (int k = 1; k <= n; k++)
				C[i][j] += A[i][k] * B[k][j];
		}
}
```

#### 시간복잡도

n번의 반복이 3중으로 일어나므로, 시간복잡도는 $O(n^3)$ 입니다.

<br />

---

### 2. 분할정복을 이용한 행렬곱셈

$A*B = C$ 를 만족하는 $n = 2^k$ 크기의 행렬을 $2^{k-1}$ 크기의 4개의 부분행렬(submatrix)로 쪼개어, C의 값을 다음과 같이 구할 수 있습니다.
$$
C = \begin{bmatrix}C_{11}&C_{12}\\C_{21}&C_{22}\end{bmatrix},
A = \begin{bmatrix}A_{11}&A_{12}\\A_{21}&A_{22}\end{bmatrix},
B = \begin{bmatrix}B_{11}&B_{12}\\B_{21}&B_{22}\end{bmatrix}
$$

$$
C_{11}=A_{11}B_{11}+A_{12}B_{21}
\\C_{12}=A_{11}B_{12}+A_{12}B_{22}
\\C_{21}=A_{21}B_{11}+A_{22}B_{21}
\\C_{22}=A_{21}B_{12}+A_{22}B_{22}
$$

#### 시간복잡도

매 과정마다 __부분행렬끼리의 <span style="color:red">8번의 곱셈</span>과 __ <span style="color:blue">4번의 덧셈</span>이, 재귀적으로 위의 과정이 $k (=log_2n)$ 번 반복됩니다. 이를 통해 시간복잡도를 증명해봅시다.  _(여기서 c는 덧셈, 대입 등의 상수복잡도입니다.)_
$$
T(n)=8T(\frac{n}{2})+c
\\=8[8T(\frac{n}{4})+c]+c
\\=8[8^2T(\frac{n}{8})+8c+c]+c
\\=8[8^3T(\frac{n}{16})+8^2c+8c+c]+c
\\\vdots
\\=8^{log_2n}T(1)+\frac{8^{log_2n}-1}{8-1}c
\\\approx 8^{log_2n}(T(1)+c)
\\=n^{log_28}(T(1)+c)=n^3(T(1)+c)
\\\implies O(n^3)
$$
이 방법으로도, 시간복잡도는 그대로 $O(n^3)$ 임을 알 수 있습니다. 

<br />

---

### 3. 스트라센 알고리즘

위의 방법에서, __부분행렬끼리의 <span style="color:red">곱셈 횟수를 7번으로 줄인</span>__ 알고리즘이 바로 스트라센 알고리즘입니다.

그 방법은 다음과 같습니다.
$$
M_1=(A_{11}+A_{22})(B_{11}+B_{22})
\\M_2=(A_{21}+A_{22})B_{11}
\\M_3=A_{11}(B_{12}−B_{22})
\\M_4=A_{22}(B_{21}−B_{11})
\\M_5=(A_{11}+A_{12})B_{22}
\\M_6=(A_{21}-A_{11})(B_{11}+B_{12})
\\M_7=(A_{12}-A_{22})(B_{21}+B_{22})
$$
$$
C_{11}=M_1+M_4-M_5+M_7
\\C_{12}=M_3+M_5
\\C_{21}=M_2+M_4
\\C_{22}=M_1-M_2+M_3+M_6
$$

#### 시간복잡도

매 과정마다 __부분행렬끼리의 <span style="color:red">7번의 곱셈</span>과 __ <span style="color:blue">6+6번의 덧셈, 4+2번의 뺄셈</span>이, 재귀적으로 위의 과정이 $k(=log_2n)$ 번 반복됩니다. 마찬가지로 시간복잡도를 증명해봅시다.
$$
T(n)=7T(\frac{n}{2^1})+c
\\=7[7T(\frac{n}{2^2})+c]+c
\\=7[7^2T(\frac{n}{2^3})+7c+c]+c
\\=7[7^3T(\frac{n}{2^4})+7^2c+7c+c]+c
\\\vdots
\\=7^{log_2n}T(1)+\frac{7^{log_2n}-1}{7-1}c
\\\approx 7^{log_2n}(T(1)+c)
\\=n^{log_27}(T(1)+c) \approx n^{2.807}(T(1)+c)
\\\implies O(n^{2.807})
$$
이를 구현한 코드입니다. (A[0] = $A_{11}$, A[1] = $A_{12}$, A[2] = $A_{21}$, A[3] = $A_{22}$ 이고, M[0] = $M_1$, ..., M[6] = $M_7$ 입니다.) 

```c++
#include <cstdio>
#include <cstdlib>
#include <ctime>
#define SIZE 1<<10 //행렬의 크기. (n == 2^k == 1<<k)
using namespace std;

//threshold : 임계값.(일정 크기 미만의 행렬은 일반적인 행렬곱 방식이 더 빠름.)
int size = SIZE, threshold = 5;

void normal_mult(int n, int** A, int** B, int*** C);
void strassen(int n, int** A, int** B, int*** C);
void sum(int n, int** A, int** B, int*** C);
void subtract(int n, int** A, int** B, int*** C);

int main()
{
    //실행시간 측정. 단위는 ms.
    clock_t start, end;
    double runtime;

    int** A, ** B, ** C;
    A = (int**)malloc(sizeof(int*) * size);
    B = (int**)malloc(sizeof(int*) * size);
    C = (int**)malloc(sizeof(int*) * size);
    for (int row = 0; row < size; row++)
    {
        A[row] = (int*)malloc(sizeof(int) * size);
        B[row] = (int*)malloc(sizeof(int) * size);
        C[row] = (int*)malloc(sizeof(int) * size);
    }

    //A,B의 값 랜덤 설정.
    srand((unsigned)time(NULL));
    for (int row = 0; row < SIZE; row++)
        for (int col = 0; col < SIZE; col++)
        {
            A[row][col] = rand() % 1000;
            B[row][col] = rand() % 1000;
            C[row][col] = 0; //미리 0으로 초기화.
        }

    printf("[A]\n");
    for (int row = 0; row < SIZE; row++)
    {
        for (int col = 0; col < SIZE; col++)
            printf("%3d ", A[row][col]);
        printf("\n");
    }
    printf("\n");

    printf("[B]\n");
    for (int row = 0; row < SIZE; row++)
    {
        for (int col = 0; col < SIZE; col++)
            printf("%3d ", B[row][col]);
        printf("\n");
    }
    printf("\n");

    //스트라센 알고리즘으로 행렬곱 구하기.
    start = clock();
    strassen(size, A, B, &C);
    end = clock();
    
    printf("[스트라센 알고리즘으로 구한 행렬 C]\n");
    for (int row = 0; row < SIZE; row++)
    {
        for (int col = 0; col < SIZE; col++)
            printf("%7d ", C[row][col]);
        printf("\n");
    }

    runtime = (double)(end - start);
    printf("\nruntime : %lf ms", runtime);
    return 0;
}

void strassen(int n, int** A, int** B, int*** C)
{
    if (n < threshold) //일반적인 행렬곱 방법이 더 빠르면, 그걸로 실행.
    {
        normal_mult(n, A, B, C);
        return;
    }

    //임시로 필요한 submatrix 동적 할당. 메모리 비용이 꽤 많이 들어감.
    int half = n / 2;
    int** subA[4], ** subB[4], ** subC[4], ** M[7];
    for (int num = 0; num < 4; num++)
    {
        subA[num] = (int**)malloc(sizeof(int*) * half);
        subB[num] = (int**)malloc(sizeof(int*) * half);
        subC[num] = (int**)malloc(sizeof(int*) * half);
    }
    for (int num = 0; num < 7; num++)
        M[num] = (int**)malloc(sizeof(int*) * half);

    //subC의 값과 M의 값을 저장할 때 행렬 연산이 여러번 요구되므로, 임시 배열이 필요함. 
    int** temp_A = (int**)malloc(sizeof(int*) * half);
    int** temp_B = (int**)malloc(sizeof(int*) * half);

    for (int row = 0; row < half; row++)
    {
        for (int num = 0; num < 4; num++)
        {
            subA[num][row] = (int*)malloc(sizeof(int) * half);
            subB[num][row] = (int*)malloc(sizeof(int) * half);
            subC[num][row] = (int*)malloc(sizeof(int) * half);
        }
        for (int num = 0; num < 7; num++)
            M[num][row] = (int*)malloc(sizeof(int) * half);

        temp_A[row] = (int*)malloc(sizeof(int) * half);
        temp_B[row] = (int*)malloc(sizeof(int) * half);
    }

    //submatrix에 각각 값 집어넣기.
    for (int row = 0; row < n; row++)
        for (int col = 0; col < n; col++)
        {
            //A_11, B_11, C_11부분.
            if (row < half && col < half)
            {
                subA[0][row][col] = A[row][col];
                subB[0][row][col] = B[row][col];
            }
            //A_12, B_12, C_12부분.
            else if (row < half && col >= half)
            {
                subA[1][row][col - half] = A[row][col];
                subB[1][row][col - half] = B[row][col];
            }
            //A_21, B_21, C_21부분.
            else if (row >= half && col < half)
            {
                subA[2][row - half][col] = A[row][col];
                subB[2][row - half][col] = B[row][col];
            }
            //A_22, B_22, C_22부분.
            else if (row >= half && col >= half)
            {
                subA[3][row - half][col - half] = A[row][col];
                subB[3][row - half][col - half] = B[row][col];
            }
        }

    //M_1, ... , M_7에 값 저장하기.

    //M_1.
    sum(half, subA[0], subA[3], &temp_A);
    sum(half, subB[0], subB[3], &temp_B);
    strassen(half, temp_A, temp_B, &M[0]);

    //M_2.
    sum(half, subA[2], subA[3], &temp_A);
    strassen(half, temp_A, subB[0], &M[1]);

    //M_3.
    subtract(half, subB[1], subB[3], &temp_B);
    strassen(half, subA[0], temp_B, &M[2]);

    //M_4.
    subtract(half, subB[2], subB[0], &temp_B);
    strassen(half, subA[3], temp_B, &M[3]);

    //M_5.
    sum(half, subA[0], subA[1], &temp_A);
    strassen(half, temp_A, subB[3], &M[4]);

    //M_6.
    subtract(half, subA[2], subA[0], &temp_A);
    sum(half, subB[0], subB[1], &temp_B);
    strassen(half, temp_A, temp_B, &M[5]);

    //M_7.
    subtract(half, subA[1], subA[3], &temp_A);
    sum(half, subB[2], subB[3], &temp_B);
    strassen(half, temp_A, temp_B, &M[6]);


    //C_1, ... , C_4에 값 저장하기.

    //C_1.
    sum(half, M[0], M[3], &temp_A);
    subtract(half, temp_A, M[4], &temp_B);
    sum(half, temp_B, M[6], &subC[0]);

    //C_2.
    sum(half, M[2], M[4], &subC[1]);

    //C_3.
    sum(half, M[1], M[3], &subC[2]);

    //C_4.
    sum(half, M[0], M[2], &temp_A);
    subtract(half, temp_A, M[1], &temp_B);
    sum(half, temp_B, M[5], &subC[3]);

    //submatrix C_1, ... , C_4에 저장한 값을 최종적으로 배열 C에 대입.
    for (int row = 0; row < n; row++)
        for (int col = 0; col < n; col++)
        {
            //A_11, B_11, C_11부분.
            if (row < half && col < half)
                (*C)[row][col] = subC[0][row][col];
            //A_12, B_12, C_12부분.
            else if (row < half && col >= half)
                (*C)[row][col] = subC[1][row][col - half];
            //A_21, B_21, C_21부분.
            else if (row >= half && col < half)
                (*C)[row][col] = subC[2][row - half][col];
            //A_22, B_22, C_22부분.
            else if (row >= half && col >= half)
                (*C)[row][col] = subC[3][row - half][col - half];
        }

    //너무 많은 메모리를 사용하게 되므로, 다 쓴 메모리 공간은 재사용할 수 있도록 free.
    for (int row = 0; row < half; row++)
    {
        for (int num = 0; num < 4; num++)
        {
            free(subA[num][row]);
            free(subB[num][row]);
            free(subC[num][row]);
        }
        free(temp_A[row]); free(temp_B[row]);
        for (int num = 0; num < 7; num++)
            free(M[num][row]);
    }
    for (int num = 0; num < 4; num++)
    {
        free(subA[num]);
        free(subB[num]);
        free(subC[num]);
    }
    free(temp_A); free(temp_B);
    for (int num = 0; num < 7; num++)
        free(M[num]);
}

void sum(int n, int** A, int** B, int*** C)
{
    for (int row = 0; row < n; row++)
        for (int col = 0; col < n; col++)
            (*C)[row][col] = A[row][col] + B[row][col];
}

void subtract(int n, int** A, int** B, int*** C)
{
    for (int row = 0; row < n; row++)
        for (int col = 0; col < n; col++)
            (*C)[row][col] = A[row][col] - B[row][col];
}

void normal_mult(int n, int** A, int** B, int*** C)
{
    for (int row = 0; row < n; row++)
        for (int col = 0; col < n; col++)
        {
            (*C)[row][col] = 0; //초기화.
            for (int k = 0; k < n; k++)
                (*C)[row][col] += A[row][k] * B[k][col];
        }
}
```

행렬곱의 실행 시간을 구하는 방법은 아래의 방법으로 구현했습니다. (위의 코드에도 포함되어 있습니다.)

```c++
#include <ctime>
using namespace std;

int main()
{
    clock_t start, end;
    double runtime;
    start = clock();
    strassen(size, A, B, &C);
    end = clock();
    runtime = (double)(end - start);
    printf("\nruntime : %lf ms", runtime);
}
```



### 4. 실행 결과

1. 행렬곱 결과

```c++
//n=8일 때
[A]
764 935 140 625 515 727 977 937
173 110 930 875 997 587 370 392
655 865 321 844 414 470 147 425
735 693 815 386 419 397 705 130
241 920 905 691 745 846 370  23
466  23 483 834 526  68 105 133
505  39  92 957 933 662 533 874
728 508 935 441 732 728 875 826

[B]
540 552 810  98 930  10 185 812
593 473 439 948 740 577 636 527
212 283 455 383 762 187 942 315
278 616 978 732 956 280 913 624
937 858 530 474  58 626 268 648
766 152 288 268 823 809 738 492
261 893 556 115 202 631 924 501
  7 889 257 382 286 205 857  52

[스트라센 알고리즘으로 구한 행렬 C]
2471438 3546431 2970602 2381607 3200127 2467420 3818808 2776818
2082205 2573264 2471250 1940112 2515229 1896945 3155126 2178010
1958609 2317200 2427509 2126412 2862782 1621278 2702134 2210745
1969557 2366911 2409706 1759428 2717039 1722668 2864979 2286421
2502490 2368622 2536792 2379399 3075922 2284934 3298697 2482349
1172813 1592190 1813899 1193378 1761470  819580 1719419 1496899
2107921 3066848 2610089 1837043 2440076 1947826 3058744 2299530
2492871 3432802 2965821 2192074 3241612 2367360 3990993 2742400

runtime : 0.000000 ms
```

2. 실행시간 비교 (strassen VS normal mult)

```c++
//n=16
strassen runtime : 0.000000 ms
normal runtime : 0.000000 ms
//n=32
strassen runtime : 2.000000 ms
normal runtime : 0.000000 ms
//n=64
strassen runtime : 15.000000 ms
normal runtime : 1.000000 ms
//n=128
strassen runtime : 104.000000 ms
normal runtime : 7.000000 ms
//n=256
strassen runtime : 712.000000 ms
normal runtime : 62.000000 ms
//n=512
strassen runtime : 5008.000000 ms
normal runtime : 586.000000 ms
//n=1024
strassen runtime : 34959.000000 ms
normal runtime : 6009.000000 ms
//n=2048
strassen runtime : 245181.000000 ms
normal runtime : 79973.000000 ms
```

clock함수의 리턴값이 정수인가봅니다. 소수점은 표현되지 않았습니다.

visual studio 2019의 debug모드에서 실행한 결과인데, release모드에선 조금 더 빠르게 동작합니다.

코드에서는 임계값을 5로 설정했는데, 실제 실행시간을 보니 임계값이 더 높아야겠습니다.

(코드가 최적화[^1]되지 않아서인지도 모르겠습니다. 더 자세한 이유를 아시는 분은 댓글 남겨주세요!)

(실험중에 임계값을 높이면 실험의 의미가 없으므로 코드는 그대로 놔두겠습니다.)

아무튼 중요한 사실은, __n의 값이 2배가 될 때마다 strassen의 실행시간 증가폭은 <span style="color:red">x7</span>정도로 유지되는 반면,  normal mult 방식의 실행시간 증가폭은 <span style="color:red">x8</span>(혹은 그 이상)이라는 것입니다.__ 위에서 증명한 시간복잡도와 비슷한 결과입니다.

<br />

이것으로 스트라센 알고리즘의 소개를 마치겠습니다. 감사합니다!

[^1]: 예를 들어, M_6, M_7은 subC를 구할 때 중복 사용되지 않으므로 따로 할당하지 않고 구하는 방법을 생각해 볼 수 있습니다.

