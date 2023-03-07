---
emoji: 🐜
title: 〈프로그래머스〉 인사고과
date: '2023-03-08 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스 BOJ
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/152995)

## ❕ 풀이

꽤나 헤맸다...ㅎㅎ  
근무태도 내림차순, 같다면 동료평가 오름차순으로 정렬한다. (다른 임의의 사원보다 두 점수가 모두 낮으면 인센티브를 받지 못함.)

풀다가 틀린 이유...

1. 완호 점수가 나오면 무조건 리턴했는데 뒤의 사원들의 점수 합이 완호보다 높을 수도 있으므로 끝까지 탐색해야함.
2. 이전 동료평가와 비교할 것이 아니라 앞선 동료평가 점수 중 max와 비교해야함. (근무태도는 작거나 같으니까 동료평가는 크거나 같아야함)
   완호 점수라면 인센티브를 받을 수 있는지 확인하고 continue
   완호 점수가 아니라면 완호보다 석차가 높은지 확인한다. (인센티브를 받으면서 두 점수 합이 완호 점수 합보다 커야한다.)

도움이 되는 문제였다...

### 👀 코드

```java
import java.util.*;
class Solution {
    public int solution(int[][] scores) {

        int[] wanho = scores[0];
        int sum = wanho[0] + wanho[1];

        // 근무태도 내림차순, 동료평가 오름차순
        Arrays.sort(scores, (s1, s2) -> s1[0] == s2[0] ? s1[1] - s2[1] : s2[0] - s1[0]);

        int maxPeer = scores[0][1];
        int answer = 1;
        for(int i = 0; i < scores.length; i++) {
            int[] score = scores[i];

            // 완호 스코어
            if(wanho.equals(score)) {
                // 인센티브 못 받는지 체크
                if(maxPeer > score[1]) return -1;
            }

            // answer = 완호보다 석차가 높은 사람 수
            // 인센티브를 받으면서 (maxPeer보다 peer점수가 크거나 같아야함)
            // sum이 wanhoSum보다 커야함
            else if(maxPeer <= score[1] && score[0] + score[1] > sum) {
                maxPeer = Math.max(maxPeer, score[1]);
                answer++;
            }
        }

        return answer;
    }
}
```

```toc

```
