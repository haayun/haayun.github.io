---
emoji: ๐
title: ใ๋ฐฑ์คใ 3055๋ฒ ํ์ถ
date: '2022-12-12'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ๋ฐฑ์ค BOJ BFS
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/3055)

#### ์ ํ : BFS

#### ํฐ์ด : Gold3

## โ ํ์ด

์ฌํํ BFS ํ์ฉ ๋ฌธ์  : ๋ ๊ทธ๋ ๋ฏ check ๋ฐฐ์ด์ int๋ก ๋ง๋ค์ด์ ์ด๋์๊ฐ๊ณผ ์ค๋ณต ํ์ธ์ ๋์์ ํจ

ํ ๋จ์ ์๊ฐ๋ง๋ค

1. ๋ฌผ ํ์ฅ (โ๊ณ ์ด๋์น๋ ๋ฌผ์ด ์ฐฐ ์์ ์ธ ์นธ์ผ๋ก ์ด๋ํ  ์ ์๋คโ โ **๋ฌผ์ ๋จผ์  ํ์ฅํ๋ค**)
   1. ๋ฌผ์ ๋น ์นธ์ผ๋ก๋ง ํ์ฅ ๊ฐ๋ฅ
2. ๊ณ ์ด๋์น ์ด๋
   1. ๋น๋ฒ์ ์๊ตด์ด๋ ๋น ์นธ์ผ๋ก ์ด๋ ๊ฐ๋ฅ

๋ด๊ฐ ์๊ฐํ๊ธฐ์ ์ค์ํ ํฌ์ธํธ๋

- ๋จ์ ์๊ฐ๋ง๋ค queue์ ํฌ๊ธฐ๋งํผ๋ง ๋์์ผํ๋ค๋ ์ 
- ๋ฌผ๋, ๊ณ ์ด๋์น๋!

### ๐ ์ฝ๋

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main_14888_์ฐ์ฐ์_๋ผ์๋ฃ๊ธฐ {
    static int N, min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
    static int[] arr, op;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        arr = new int[N];
        op = new int[4];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for(int i = 0; i < N; i++){
            arr[i] = Integer.parseInt(st.nextToken());
        }
        st = new StringTokenizer(br.readLine());
        for(int i = 0; i < 4; i++){
            op[i] = Integer.parseInt(st.nextToken());
        }

        dfs(0, arr[0]);
        System.out.println(max);
        System.out.println(min);
    }

    static void dfs(int r, int value){
        if(r == N - 1){
            if(value < min) min = value;
            if(value > max) max = value;
        }
        for(int i = 0; i < 4; i++){
            if(op[i] <= 0) continue;
            op[i] -= 1;
            dfs(r + 1, calc(i, value, arr[r + 1]));
            op[i] += 1;
        }
    }

    static int calc(int op, int a, int b){
        switch (op){
            case 0:
                return a + b;
            case 1:
                return a - b;
            case 2:
                return a * b;
            case 3:
                return a / b;
        }
        return 0;
    }
}
```

### ๐ฃ ๊ฒฐ๊ณผ

์์ ์๊ฐ : 30 m
![3055](./result.png)

```toc

```
