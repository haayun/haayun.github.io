---
emoji: π
title: γλ°±μ€γ 11053λ² κ°μ₯ κΈ΄ μ¦κ°νλ λΆλΆ μμ΄
date: '2022-12-14 01:00:00'
author: νμ°
tags: μ½λ©νμ€νΈ λ°±μ€ BOJ BFS μ­μΆμ 
categories: μκ³ λ¦¬μ¦
---

## β λ¬Έμ 

### [λ¬Έμ  λ°λ‘κ°κΈ°](https://www.acmicpc.net/problem/11053)

#### μ ν : DP

#### ν°μ΄ : Silver2

## β νμ΄

[λμ  κ³νλ²](https://haayun.github.io/dynamic-programming/#11053-κ°μ₯-κΈ΄-μ¦κ°νλ-λΆλΆ-μμ΄) ν¬μ€νΈ μμ±νλ©΄μ νΌ λ¬Έμ 
0λ² μΈλ±μ€λΆν° νμνλ©° ν΄λΉ μΈλ±μ€λ‘ λλλ λΆλΆ μμ΄μ μ΅λκ°μ κ³μ°νλ λ°©μμΌλ‘ νμλ€.

### π μ½λ

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main_11053_κ°μ₯_κΈ΄_μ¦κ°νλ_λΆλΆ_μμ΄ {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[] A = new int[N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(st.nextToken());
        }

        int[] dp = new int[N];
        int ans = 0;
        for (int i = 0; i < N; i++) {
            int prev = 0;
            for (int j = 0; j < i; j++) {
                if (A[i] > A[j])
                    prev = Math.max(prev, dp[j]);
            }
            dp[i] = prev + 1;
            ans = Math.max(ans, dp[i]);
        }
        System.out.println(ans);

    }
}

```

### π£ κ²°κ³Ό

μμ μκ° : 30 m
![11053](./result.png)

```toc

```
