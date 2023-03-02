---
emoji: 🐜
title: 〈프로그래머스〉 부대복귀
date: '2023-03-02 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스 BOJ GRAPH DIJKSTRA
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/132266)

#### 유형 : BFS

## ❕ 풀이

주어진 destination을 source로 해서 다익스트라로 풀었다

### 👀 코드

```java
import java.util.*;
class Solution {
    int N;
    public int[] solution(int n, int[][] roads, int[] sources, int destination) {
        N = n;

        ArrayList<Integer>[] map = new ArrayList[n + 1];
        for(int i = 1; i < N + 1; i++) map[i] = new ArrayList<>();

        for(int i = 0; i < roads.length; i++) {
            int a = roads[i][0], b = roads[i][1];
            map[a].add(b);
            map[b].add(a);
        }

        int[] dist = dijkstra(map, destination);

        int[] answer = new int[sources.length];
        for(int i = 0; i < sources.length; i++) {
            answer[i] = dist[sources[i]] == Integer.MAX_VALUE ? -1 : dist[sources[i]];
        }
        return answer;
    }

    int[] dijkstra(ArrayList<Integer>[] map, int destination){
        int[] dist = new int[N + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        boolean[] visited = new boolean[N + 1];

        dist[destination] = 0;
        visited[destination] = true;

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(destination);

        while(!queue.isEmpty()) {
            int cur = queue.poll();
            for(int next : map[cur]) {
                if(!visited[next]) {
                    if(dist[cur] + 1 < dist[next]) {
                        dist[next] = dist[cur] + 1;
                        queue.offer(next);
                        visited[next] = true;
                    }
                }
            }
        }
        return dist;
    }

}
```

```toc

```
