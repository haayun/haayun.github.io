---
emoji: π
title: γνλ‘κ·Έλλ¨Έμ€γ νμ  ν°λ¨λ¦¬κΈ°
date: '2023-03-09 00:00:00'
author: νμ°
tags: μ½λ©νμ€νΈ νλ‘κ·Έλλ¨Έμ€ BOJ
categories: μκ³ λ¦¬μ¦
---

## β λ¬Έμ 

### [λ¬Έμ  λ°λ‘κ°κΈ°](https://school.programmers.co.kr/learn/courses/30/lessons/68646)

## β νμ΄

κ° νμ μ κΈ°μ€μΌλ‘ μ’μΈ‘μ μ΅μκ°, μ°μΈ‘μ μ΅μκ°μ κ΅¬ν΄μ λ μ€ νλλΌλ μκ±°λ κ°μΌλ©΄ μ΅νμ νμ μ΄ λ  μ μλ€.

### π μ½λ

```java
class Solution {
    public int solution(int[] a) {
        int N = a.length;
        int[] fromLeft = new int[N];
        int[] fromRight = new int[N];
        fromLeft[0] = a[0];
        for(int i = 1; i < N; i++) {
            fromLeft[i] = Math.min(fromLeft[i-1], a[i-1]);
        }
        fromRight[N-1] = a[N-1];
        for(int i = N-2; i >= 0; i--) {
            fromRight[i] = Math.min(fromRight[i+1], a[i+1]);
        }
        int answer = 0;
        for(int i = 0; i < N; i++) {
            if(fromLeft[i] >= a[i] || fromRight[i] >= a[i]) answer++;
        }
        return answer;
    }
}
```

```toc

```
