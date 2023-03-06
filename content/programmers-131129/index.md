---
emoji: 🐜
title: 〈프로그래머스〉 카운트 다운
date: '2023-03-06 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스 DP
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/131129)

#### 유형 : DP

## ❕ 풀이

2차원 DP 배열 활용한 문제.
dp[0] → 0점을 만드는 최소한의 다트 수
dp[1] → 최선의 경우의 "싱글" 또는 "불"을 맞춘 횟수 (최대한 많이 던지는 방법)
코드가 깔끔하진 않지만... 암튼 간단한 DP 문제였다.

### 👀 코드

```java
class Solution {
    public int[] solution(int target) {
        int INF = 100000;
        int[][] dp = new int[100001][2];
        for(int i = 0; i <= 100000; i++) {
            dp[i][0] = INF;
        }
        for(int i = 1; i <= 20; i++) {
            dp[i][0] = 1; dp[i][1] = 1;
            if(dp[i * 2][0] == INF) {
                dp[i * 2][0] = 1; dp[i * 2][1] = 0;
            }
            if(dp[i * 3][0] == INF) {
                dp[i * 3][0] = 1; dp[i * 3][1] = 0;
            }
        }

        dp[50][0] = 1; dp[50][1] = 1;

        for(int i = 21; i <= target; i++) {
            for(int j = 1; j <= 20; j++) {
                if(dp[i - j][0] + 1 < dp[i][0]) {
                    dp[i][0] = dp[i - j][0] + 1;
                    dp[i][1] = dp[i - j][1] + 1;
                } else if ((dp[i - j][0] + 1 == dp[i][0]) && (dp[i - j][1] + 1 > dp[i][1])) {
                    dp[i][0] = dp[i - j][0] + 1;
                    dp[i][1] = dp[i - j][1] + 1;
                }

                if(i - j * 2 > 0) {
                    if(dp[i - j * 2][0] + 1 < dp[i][0]) {
                        dp[i][0] = dp[i - j * 2][0] + 1;
                        dp[i][1] = dp[i - j * 2][1];
                    }
                }

                if(i - j * 3 > 0) {
                    if(dp[i - j * 3][0] + 1 < dp[i][0]) {
                        dp[i][0] = dp[i - j * 3][0] + 1;
                        dp[i][1] = dp[i - j * 3][1];
                    }
                }

                if(i > 50) {
                    if(dp[i - 50][0] + 1 < dp[i][0]) {
                        dp[i][0] = dp[i - 50][0] + 1;
                        dp[i][1] = dp[i - 50][1] + 1;
                    } else if ((dp[i - 50][0] + 1 == dp[i][0]) && (dp[i - 50][1] + 1 > dp[i][1])) {
                        dp[i][0] = dp[i - 50][0] + 1;
                        dp[i][1] = dp[i - 50][1] + 1;
                    }
                }
            }
        }

        return dp[target];
    }
}
```

```toc

```
