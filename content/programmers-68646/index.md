---
emoji: 🐜
title: 〈프로그래머스〉 풍선 터뜨리기
date: '2023-03-09 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스 BOJ
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/68646)

## ❕ 풀이

각 풍선을 기준으로 좌측의 최솟값, 우측의 최솟값을 구해서 둘 중 하나라도 작거나 같으면 최후의 풍선이 될 수 있다.

### 👀 코드

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
