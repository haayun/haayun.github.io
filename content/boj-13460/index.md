---
emoji: ð
title: ãë°±ì¤ã 13460ë² êµ¬ì¬ íì¶ 2
date: '2022-12-14 02:00:00'
author: íì°
tags: ì½ë©íì¤í¸ ë°±ì¤ BOJ DP ì­ì¶ì 
categories: ìê³ ë¦¬ì¦
---

## â ë¬¸ì 

### [ë¬¸ì  ë°ë¡ê°ê¸°](https://www.acmicpc.net/problem/14002)

#### ì í : DP ì­ì¶ì 

#### í°ì´ : Gold4

## â íì´

[11053 ê°ì¥ ê¸´ ì¦ê°íë ë¶ë¶ ìì´](https://haayun.github.io/boj-9251) ë¬¸ì ì ëì¼íê² LISì ê¸¸ì´ë¥¼ ì¶ë ¥íê³  ìì´ì ì¶ë ¥íë ë¬¸ì ì´ë¤.
ì¦, ê²½ë¡ë¥¼ ì­ì¶ì í´ì ëµì ì°¾ëë¤.  
â ê²½ë¡ë¥¼ ì ì¥íë ë°°ì´ì´ ì¶ê°ë¡ íìíë¤.

answer ë³ì ì´ê¸°ê° ì¤ì ì ì£¼ìí´ì¼íë¤. (ì¸ë±ì¤ë 0ì¼ë¡, ê¸¸ì´ë 1ì¼ë¡, ìëë©´ ê°ìíë ë°°ì´ì¼ ìë ìê¸° ëë¬¸ì!)

### ð ì½ë

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main_14002_ê°ì¥_ê¸´_ì¦ê°íë_ë¶ë¶ìì´_4 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int[] arr = new int[N];
        int[] dp = new int[N];
        int[] path = new int[N];
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
            dp[i] = 1;
            path[i] = -1;
        }

        int[] answer = new int[]{0, 1};

        for (int i = 1; i < N; i++) {
            for (int j = 0; j < i; j++) {
                if (arr[i] > arr[j] && dp[i] < dp[j] + 1) {
                    dp[i] = dp[j] + 1;
                    path[i] = j;
                }
            }
            if (dp[i] > answer[1]) {
                answer[0] = i;
                answer[1] = dp[i];
            }
        }

        int x = answer[0];
        int size = answer[1];
        int[] result = new int[size];

        for (int i = size - 1; i >= 0; i--) {
            result[i] = arr[x];
            x = path[x];
        }

        sb.append(size).append("\n");
        for (int i = 0; i < size; i++) {
            sb.append(result[i]).append(' ');
        }

        System.out.println(sb.toString());

    }

}
```

### ð£ ê²°ê³¼

ìì ìê° : 1 h
![result](./result.png)

```toc

```
