---
emoji: π
title: γνλ‘κ·Έλλ¨Έμ€γ νΌλ‘λ
date: '2023-03-03 00:00:00'
author: νμ°
tags: μ½λ©νμ€νΈ νλ‘κ·Έλλ¨Έμ€ BOJ
categories: μκ³ λ¦¬μ¦
---

## β λ¬Έμ 

### [λ¬Έμ  λ°λ‘κ°κΈ°](https://school.programmers.co.kr/learn/courses/30/lessons/87946)

#### μ ν : μμ νμ

## β νμ΄

μμ νμ λ¬Έμ . μμ΄λ‘ νν μμλ₯Ό μ νκ³  νν ν΄λ³΄λ©΄μ μ΅λ λμ  μλ₯Ό μ°Ύλλ€.

### π μ½λ

```java
import java.util.*;
class Solution {
    int[] result;
    boolean[] visited;
    int size, K;
    int[][] dgs;
    int max = 0;

    public int solution(int k, int[][] dungeons) {
        size = dungeons.length;
        K = k;
        result = new int[size];
        visited = new boolean[size];
        dgs = dungeons;
        perm(0);

        return max;
    }

    // μμ΄ : νν μμλ₯Ό μ νκΈ°
    void perm(int cnt){
        if(cnt == size) {
            // ννν΄λ³΄κΈ°
            int result = adventure();
            // μ΅λ λμ  μ κ°±μ 
            max = Math.max(result, max);
            return;
        }

        for(int i = 0; i < size; i++) {
            if(!visited[i]){
                visited[i] = true;
                result[cnt] = i;
                perm(cnt + 1);
                visited[i] = false;
            }
        }

    }

    int adventure() {
        int health = K;
        int cnt = 0;
        for(int i = 0; i < size; i++) {
            int idx = result[i];
            // μ΅μ νμ νΌλ‘λ λΉκ΅
            if(health >= dgs[idx][0]) {
                health -= dgs[idx][1];
                cnt++;
            } else {
                break;
            }
        }
        return cnt;
    }
}
```

```toc

```
