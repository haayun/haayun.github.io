---
emoji: ๐
title: ใ๋ฐฑ์คใ 9252๋ฒ LCS 2
date: '2022-12-14 04:00:00'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ๋ฐฑ์ค BOJ DP ์ญ์ถ์ 
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/9252)

#### ์ ํ : DP ์ญ์ถ์ 

#### ํฐ์ด : Gold4

## โ ํ์ด

[9251 LCS](https://haayun.github.io/boj-9251) ๋ฌธ์ ์ ๋์ผํ๊ฒ ๊ณตํต ๋ถ๋ถ ์์ด์ ์ต๋ ๊ธธ์ด๋ฅผ ์ถ๋ ฅํ๊ณ  ๊ทธ ๋ฌธ์์ด๊น์ง ์ถ๋ ฅํ๋ ๋ฌธ์ ์ด๋ค.
์ฆ, ๊ฒฝ๋ก๋ฅผ ์ญ์ถ์ ํด์ ๋ต์ ์ฐพ๋๋ค.  
โ ๊ฒฝ๋ก๋ฅผ ์ ์ฅํ๋ 2์ฐจ์ ๋ฐฐ์ด์ด ์ถ๊ฐ๋ก ํ์ํ๋ค. ์ด๋ ๋ฐฉํฅ์์ ์๋์ง ์ ์ฅํ๋ค. (0: ์์์, 1: ์ผ์ชฝ์์, 2: ์ข์ํฅ์์)

### ๐ ์ฝ๋

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main_9252_LCS_2 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char[] arr1 = br.readLine().toCharArray();
        char[] arr2 = br.readLine().toCharArray();
        int n1 = arr1.length;
        int n2 = arr2.length;

        // ๋ฐฐ์ด์ ํฌ๊ธฐ๋ฅผ +1 ํ๋ ์ด์ : (1, 1)๋ถํฐ ์ธ๋ฑ์ค๋ฅผ ๊ด๋ฆฌํ๊ธฐ ์ํด
        int[][] dp = new int[n1 + 1][n2 + 1];   // LCS์ ๊ธธ์ด๋ฅผ ์ ์ฅํ๋ ๋ฐฐ์ด
        int[][] path = new int[n1 + 1][n2 + 1]; // ์ด๋ ๊ฒฝ๋ก๋ฅผ ํํ๋์ง ์ ์ฅํ๋ ๋ฐฐ์ด (0: ์์์, 1: ์ผ์ชฝ์์, 2: ์ข์ํฅ์์)
        for (int i = 0; i <= n1; i++) {
            for (int j = 0; j <= n2; j++) {
                path[i][j] = -1;
            }
        }
        for (int i = 1; i <= n1; i++) {
            for (int j = 1; j <= n2; j++) {
                if (arr1[i - 1] == arr2[j - 1]) {       // ๋ ๋ฌธ์๊ฐ ๊ฐ์ผ๋ฉด CS์ ํฌํจํด์ผ ๋๋๊น
                    dp[i][j] = dp[i - 1][j - 1] + 1;    // ๋ฌธ์๋ค์ด ํฌํจ๋๊ธฐ ์ ์ ๊ธธ์ด + 1
                    path[i][j] = 2;
                } else {                        // ๋ ๋ฌธ์๊ฐ ๋ค๋ฅธ ๊ฒฝ์ฐ
                    dp[i][j] = dp[i - 1][j];    // ์์ชฝ์ ๊ฐ์ ๊ฐ์ ธ์ ์ ์ฅ
                    path[i][j] = 0;
                }
                if (dp[i][j] < dp[i][j - 1]) {  // ์ผ์ชฝ์ ๊ฐ์ด ๋ ํฌ๋ค๋ฉด ๊ฐฑ์ 
                    dp[i][j] = dp[i][j - 1];
                    path[i][j] = 1;
                }
            }
        }

        // ์ญ์ถ์ ํ๊ธฐ
        StringBuilder sb = new StringBuilder();
        int[] dr = {-1, 0, -1};         // ์์ชฝ, ์ผ์ชฝ, ์ข์ํฅ
        int[] dc = {0, -1, -1};
        int r = n1, c = n2;             // ์ต์ฐํ๋จ์์ ์ถ๋ฐ (์์ฑ๋ ๊ฒฝ๋ก)
        System.out.println(dp[r][c]);   // LCS์ ๊ธธ์ด๋ฅผ ์ถ๋ ฅํ๋ค.

        while (path[r][c] != -1) {      // ์ข์๋จ ๊ฒฝ๊ณ๋ฅผ ๋ง๋  ๋๊น์ง
            int d = path[r][c];
            if (d == 2) {               // LCS์ ํฌํจ๋๋ ๋จ์ด์ธ ๊ฒฝ์ฐ
                sb.append(arr1[r - 1]);
            }
            r += dr[d];
            c += dc[d];
        }
        System.out.println(sb.reverse());   // ๊ฐํธํ๊ฒ ์ญ๋ฐฉํฅ์ผ๋ก ์ถ๋ ฅํ  ์ ์๋ค.
    }
}

```

### ๐ฃ ๊ฒฐ๊ณผ

์์ ์๊ฐ : 1 h
![9252](./result.png)

```toc

```
