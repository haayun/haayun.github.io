---
emoji: π
title: γλ°±μ€γ 1717λ² μ§ν©μ νν
date: '2022-12-17 04:00:00'
author: νμ°
tags: μ½λ©νμ€νΈ λ°±μ€ BOJ μ λμ¨νμΈλ λΆλ¦¬μ§ν©
categories: μκ³ λ¦¬μ¦
---

## β λ¬Έμ 

### [λ¬Έμ  λ°λ‘κ°κΈ°](https://www.acmicpc.net/problem/1717)

#### μ ν : μ λμ¨ νμΈλ (λΆλ¦¬μ§ν©)

#### ν°μ΄ : Gold4

## β νμ΄

μ λμ¨ νμΈλ(λΆλ¦¬ μ§ν©) νμ©νλ λ¬Έμ μλ€.
μ£Όμ΄μ§λ μμλ₯Ό ν©μ§ν© μ°μ°νκ±°λ κ°μ μ§ν©μ ν¬ν¨λμ΄μλμ§ νμΈνλ μ°μ°μ μννλ κ²μ΄ μ£Όμ΄μ‘λ€.
μ λμ¨νμΈλμ μκ°λ³΅μ‘λλ O(1)μ κ°κΉμ΄ λΉ λ₯Έ μκ³ λ¦¬μ¦μ΄λ€.
λμ€μ κ°λ μ λ¦¬λ₯Ό λ€μ νλ©΄ μ’μ κ² κ°μ§λ§ κ°λ¨ν νμ΄νλ€.
μ λμ¨ νμΈλλ₯Ό κ΅¬ννλ 2κ°μ§ λ°©μμ΄ μλλ° λ ν¨μ¨μ μΈ 2λ²μ§Έ λ°©μμΌλ‘ κ΅¬ννλ€.

1. parent λ°°μ΄μ μκΈ° μμ μ μμ κ°μΌλ‘ μ΄κΈ°νν΄μ μ λμ¨ μ°μ°μ νλ©΄μ λΆλͺ¨ λΈλμ μΈλ±μ€λ₯Ό μ μ₯νλ λ°©μ
   β μλ μ μ μ΄ λ§μλ μ§ν©μ λ£¨νΈκ° μλ‘μ΄ μ§ν©μ λ£¨νΈκ° λλ κ²μ΄ λ ν¨μ¨μ μ΄λ€. (μ§ν©μ ν¬κΈ°λ₯Ό μ μ₯ν΄μΌ νλ€!)
2. parent λ°°μ΄μ -1λ‘ μ΄κΈ°νν΄μ μ λμ¨ μ°μ°μ νλ©΄μ λ£¨νΈλ μ§ν©μ ν¬κΈ°λ₯Ό μμλ‘, λλ¨Έμ§ λΈλλ€μ λΆλͺ¨ λΈλμ μΈλ±μ€λ₯Ό μ μ₯νλ λ°©μ
   β λ©λͺ¨λ¦¬λ₯Ό μ μ½νκ³  ν¨μ¨μ μ΄λ€.

μ λμ¨νμΈλ μκ³ λ¦¬μ¦μμ λ΄κ° μμ£Ό λΉ λ¨λ¦¬μ§λ§, μ€μν ν¬μΈνΈλ
Find μ°μ°μ νλ©΄μ κ° μ μ μ λΆλͺ¨λ₯Ό λ£¨νΈ μ μ μΌλ‘ μ€μ νλ κ²μ΄λ€. = κ·Έλν μμΆ
μ²λ¦¬νμ§ μμΌλ©΄ μ΅μμ κ²½μ° Find μ°μ°μμ O(N)μ μκ°λ³΅μ‘λλ₯Ό κ°μ§λ€.

### π μ½λ

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main_1717_μ§ν©μ_νν {
    // μ λμ¨ νμΈλ (λΆλ¦¬ μ§ν©) : μλ‘ λ€λ₯Έ λ μμκ° κ°μ μ§ν©μ μν΄ μλμ§ νλ³νλ μκ³ λ¦¬μ¦
    // μκ°λ³΅μ‘λ O(a(N))μΌλ‘ O(1)μ κ°κΉλ€
    // λ°©μ 1) parent λ°°μ΄μ μκΈ° μμ μΌλ‘ μ΄κΈ°ν
    // λ°©μ 2) parent λ°°μ΄μ -1λ‘ μ΄κΈ°ννμ¬ μ§ν©μ ν¬κΈ°λ νμνλλ‘ νλ€
    static int N, M;
    static int[] parent;

    public static int findParent(int a) { // μ μ  aκ° μν μ§ν©μ λ£¨νΈ μ μ μ λ°ννλ€.
        if(parent[a] < 0) { // λ£¨νΈ μ μ μ parent κ°μ μμμΈ μ§ν©μ ν¬κΈ°λ₯Ό λνλΈλ€.
            return a;
        }
        return parent[a] = findParent(parent[a]); // κ° μ μ μ λΆλͺ¨λ₯Ό λ£¨νΈ μ μ μΌλ‘ μ€μ νμ¬ κ·Έλν μμΆμ νλ€. (μμΆνμ§ μμΌλ©΄ μ΅μμ κ²½μ° μκ°λ³΅μ‘λ O(N))
    }

    public static void union(int a, int b) { // μ μ  aμ bμ μ§ν©μ ν©μ°μ°νλ ν¨μ, μ μ μ΄ λ λ§μ μ§ν©μ λ£¨νΈκ° μλ‘μ΄ μ§ν©μ λ£¨νΈκ° λλ κ²μ΄ ν¨μ¨μ μ΄λ€.
        int ap = findParent(a);
        int bp = findParent(b);
        if(ap == bp)    // μ΄λ―Έ κ°μ μ§ν©μ μλ€λ©΄
            return;

        if(parent[ap] < parent[bp]) {   // aκ° μν μ§ν©μ ν¬κΈ°κ° λ ν¬λ€λ©΄ ν΄λΉ μ§ν©μ λ£¨νΈ μλμ bκ° μ°κ²°λλ€. ν¬κΈ°κ° μμμ΄κΈ° λλ¬Έμ < μ°μ°μ νμ©
            parent[ap] += parent[bp];   // μ§ν©μ ν¬κΈ°λ₯Ό κ°±μ νλ€.
            parent[bp] = ap;            // bpμ λΆλͺ¨λ₯Ό apλ‘ μ€μ νλ€. = apκ° μλ‘μ΄ λ£¨νΈκ° λλ€
        } else {                        // bκ° μν μ§ν©μ ν¬κΈ°κ° λ ν¬λ€λ©΄
            parent[bp] += parent[ap];
            parent[ap] = bp;            // bpκ° μλ‘μ΄ λ£¨νΈκ° λλ€.
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        parent = new int[N + 1];
        for (int i = 0; i <= N; i++) {  // parent λ°°μ΄ μ΄κΈ°κ°μ -1λ‘ μ€μ νλ€, μ§ν©μ ν¬κΈ°λ₯Ό λνλΈλ€
            parent[i] = -1;
        }
        while (M-- > 0) {
            st = new StringTokenizer(br.readLine());
            int cmd = Integer.parseInt(st.nextToken());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            if (cmd == 0) {     // μ λμ¨
                union(a, b);
            } else {            // νμΈλ
                if(findParent(a) == findParent(b)) {
                    System.out.println("YES");
                } else {
                    System.out.println("NO");
                }
            }
        }
    }
}

```

### π£ κ²°κ³Ό

μμ μκ° : 1 h
![1717](./result.png)

```toc

```
