---
emoji: ๐
title: ใ๋ฐฑ์คใ 1520๋ฒ ๋ด๋ฆฌ๋ง ๊ธธ
date: '2022-12-15 04:00:00'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ๋ฐฑ์ค BOJ DP DFS
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/1520)

#### ์ ํ : DP DFS

#### ํฐ์ด : Gold3

## โ ํ์ด

๋จ์ํ BFS, DFS๋ก ํ๋ฉด ์์ ํ์์ ๊ฐ๊น๊ธฐ ๋๋ฌธ์ ๋ชจ๋ ์๊ฐ์ด๊ณผ๊ฐ ๋๋ค.
๋ฐ๋ผ์ DP๋ฅผ ํ์ฉํด์ ์ค๋ณต์ผ๋ก ๊ฒฝ์ฐ์ ์๋ฅผ ์ธ๋ ์ฐ์ฐ์ ์ค์ฌ์ผ ํ๋ค.
์ข์๋จ์์ ์ฐํ๋จ๊น์ง ๊ฒฝ๋ก๋ฅผ ์ฐพ์ ๋๋ง๋ค ํด๋น ๊ฒฝ๋ก์ ๊ฒฝ์ฐ์ ์๋ฅผ ์ ์ฅํ๊ณ  ์ด๋ฏธ ๊ฐ์ด ์กด์ฌํ๋ค๋ฉด ํ์ํ์ง ์๋ ๋ฐฉ์์ด๋ค.
DFS์ DP๋ฅผ ์ ์ฉํ๋ ๋ถ๋ถ์ด ์ด๋ ค์ ๋ ๋ฌธ์ ์๋ค.

### ๐ ์ฝ๋

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main_1520_๋ด๋ฆฌ๋ง๊ธธ {
    // DFS + DP
    // DFS๋ง ํ์ฉํ๋ฉด ์๊ฐ์ด๊ณผ
    // ๊ฒฝ๋ก์ ๊ฒฝ์ฐ์ ์๋ฅผ ์ ์ฅํ๋ฉด์ ํ์ํด์ผํ๋ค.

    static int N, M, answer = 0;
    static int[][] map, dp;
    static int[] dr = {-1, 0, 1, 0};
    static int[] dc = {0, -1, 0, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new int[N][M];
        dp = new int[N][M];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                dp[i][j] = -1;
            }
        }
        System.out.println(dfs(0, 0));
    }

    static int dfs(int r, int c) {
        if (r == N - 1 && c == M - 1) { // ์ต์ฐํ๋จ์ ๋๋ฌํจ = ๊ฒฝ๋ก ํ๋ ์๊ธด ๊ฒ์ด๋ฏ๋ก dp๊ฐ์ 1๋ก ์ด๊ธฐํํ ํ ๋ฆฌํด
            return dp[r][c] = 1;
        }

        if (dp[r][c] != -1) {    // ์ด๋ฏธ ๊ฐ(ํ์ฌ ์ ์ ์์ ์ต์ฐํ๋จ๊น์ง ๊ฐ๋ ๊ฒฝ๋ก์ ์)์ด ์กด์ฌํ๋ค๋ฉด
            return dp[r][c];
        }

        dp[r][c] = 0;           // ํ์ ์์์ ์ํด์ 0์ผ๋ก ์ด๊ธฐํ
        for (int i = 0; i < 4; i++) {
            int nr = r + dr[i], nc = c + dc[i];
            if (nr < 0 || nr >= N || nc < 0 || nc >= M) continue;    // ๋ฒ์ ์ฒดํฌ
            if (map[nr][nc] < map[r][c]) {
                dp[r][c] += dfs(nr, nc);    // ๋ค์ ์ ์ ์ ๊ฐ์ ํ์ฌ ์ ์ ์ ๋ํ๋ค.
            }
        }

        return dp[r][c];    // ์์  ๋ธ๋ ๋ชจ๋ ํ์ ์๋ฃ ํ ํ์ฌ ์ ์ ์ ๊ฐ์ ๋ฆฌํดํด์ ๋ถ๋ชจ ๋ธ๋๋ก ๋์๊ฐ๋ค.
    }
}
```

### ๐ฃ ๊ฒฐ๊ณผ

์์ ์๊ฐ : 2 h
![1520](./result.png)

```toc

```
