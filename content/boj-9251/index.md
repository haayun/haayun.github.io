---
emoji: ๐
title: ใ๋ฐฑ์คใ 9251๋ฒ LCS
date: '2022-12-14 03:00:00'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ๋ฐฑ์ค BOJ DP
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/9251)

#### ์ ํ : DP ์ญ์ถ์ 

#### ํฐ์ด : Gold5

## โ ํ์ด

[๋์  ๊ณํ๋ฒ](https://haayun.github.io/dynamic-programming/#9251-lcs) ํฌ์คํธ ์์ฑํ๋ฉด์ ํผ ๋ฌธ์ 

- 2์ฐจ์ ํ์ด๋ธ์ ์์ฑํด์ ๊ฐ๋ฅํ ๋ฌธ์์ด๋ค์ ์กฐํฉ์ ๋ํ ๊ณตํต ๋ถ๋ถ ์์ด์ ์ต๋ ๊ธธ์ด๋ฅผ ์ ์ฅํ๋ค.
- ๋ ๋ฌธ์๊ฐ ์๋ก **๋ค๋ฅธ ๊ณณ**์ ๊ณตํต ๋ถ๋ถ ๋ฌธ์์ด์ ์ํ์ง ์์ผ๋ฏ๋ก **๊ทธ ์ ์ ๊ธธ์ด ์ต๋๊ฐ** ๊ทธ๋๋ก ๊ฐ์ ธ์ด  
  โ ์์ชฝ or ์ผ์ชฝ
- ๋ ๋ฌธ์๊ฐ ์๋ก **๊ฐ์ ๊ณณ**์ ๊ณตํต ๋ถ๋ถ ๋ฌธ์์ด์ ์ถ๊ฐ๋๋ฏ๋ก **ํด๋น ๋ฌธ์๋ค์ด ํฌํจ๋๊ธฐ ์ ์ ๊ธธ์ด + 1**  
  โ ์ข์ํฅ ๋๊ฐ์ 

### ๐ ์ฝ๋

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main_9251_LCS {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char[] arr1 = br.readLine().toCharArray();
        char[] arr2 = br.readLine().toCharArray();
        int n1 = arr1.length;
        int n2 = arr2.length;

        // ๋ฐฐ์ด์ ํฌ๊ธฐ๋ฅผ +1 ํ๋ ์ด์ : (1, 1)๋ถํฐ ์ธ๋ฑ์ค๋ฅผ ๊ด๋ฆฌํ๊ธฐ ์ํด
        int[][] dp = new int[n1 + 1][n2 + 1];   // LCS์ ๊ธธ์ด๋ฅผ ์ ์ฅํ๋ ๋ฐฐ์ด

        for (int i = 1; i <= n1; i++) {
            for (int j = 1; j <= n2; j++) {
                if (arr1[i - 1] == arr2[j - 1]) {       // ๋ ๋ฌธ์๊ฐ ๊ฐ์ผ๋ฉด CS์ ํฌํจํด์ผ ๋๋๊น
                    dp[i][j] = dp[i - 1][j - 1] + 1;    // ๋ฌธ์๋ค์ด ํฌํจ๋๊ธฐ ์ ์ ๊ธธ์ด + 1
                } else {                        // ๋ ๋ฌธ์๊ฐ ๋ค๋ฅธ ๊ฒฝ์ฐ
                    dp[i][j] = dp[i - 1][j];    // ์์ชฝ์ ๊ฐ์ ๊ฐ์ ธ์ ์ ์ฅ
                }
                if (dp[i][j] < dp[i][j - 1]) {  // ์ผ์ชฝ์ ๊ฐ์ด ๋ ํฌ๋ค๋ฉด ๊ฐฑ์ 
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }

        System.out.println(dp[n1][n2]);   // LCS์ ๊ธธ์ด๋ฅผ ์ถ๋ ฅํ๋ค.
    }
}

```

### ๐ฃ ๊ฒฐ๊ณผ

์์ ์๊ฐ : 30 m
![9251](./result.png)

```toc

```
