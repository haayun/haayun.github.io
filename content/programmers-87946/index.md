---
emoji: 🐜
title: 〈프로그래머스〉 피로도
date: '2023-03-03 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스 BOJ
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/87946)

#### 유형 : 완전탐색

## ❕ 풀이

완전탐색 문제. 순열로 탐험 순서를 정하고 탐험 해보면서 최대 던전 수를 찾는다.

### 👀 코드

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

    // 순열 : 탐험 순서를 정하기
    void perm(int cnt){
        if(cnt == size) {
            // 탐험해보기
            int result = adventure();
            // 최대 던전 수 갱신
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
            // 최소 필요 피로도 비교
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
