---
emoji: 🐜
title: 〈프로그래머스〉 덧칠하기
date: '2023-03-07 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/161989)

## ❕ 풀이

그냥 안 칠해진 곳이 발견되면 칠함.
선형으로 탐색하면 끝인 문제였다.
메모리 더 아낄 수 있을 것 같긴 한데 그냥 처음 푼 대로 제출..

### 👀 코드

```java
class Solution {
    public int solution(int n, int m, int[] section) {
        boolean[] notPainted = new boolean[n + 1];
        for(int i = 0; i < section.length; i++) {
            notPainted[section[i]] = true;
        }
        int answer = 0;
        for(int i = 1; i <= n; i++) {
            if(notPainted[i]) {
                answer++;
                for(int j = 0; j < m; j++) {
                    if(i + j > n) continue;
                    notPainted[i + j] = false;
                }
            }
        }
        return answer;
    }
}
```

```toc

```
