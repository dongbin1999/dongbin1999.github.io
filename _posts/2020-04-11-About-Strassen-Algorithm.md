---
layout: single
title:  "About Strassen Algorithm"
date:   2020-04-11 20:30:00 +0900
categories: jekyll update
---

# #1. 알고리즘 소개





```c++
void normal_mult(int n, int A[][], int B[][], int C[][])
{
	for (int i = 0; i < n; i++)
		for (int j = 0; j < n; j++)
		{
			C[i][j] = 0;
			for (int k = 0; k < n; k++)
				C[i][j] += A[i][k] * B[k][j];
		}
}
```

