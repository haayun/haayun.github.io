---
emoji: ๐
title: ใํ๋ก๊ทธ๋๋จธ์คใ ๋ถ๋๋ณต๊ท
date: '2023-03-02 00:00:00'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ํ๋ก๊ทธ๋๋จธ์ค BOJ GRAPH DIJKSTRA
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://school.programmers.co.kr/learn/courses/30/lessons/132266)

#### ์ ํ : BFS

## โ ํ์ด

์ฃผ์ด์ง destination์ source๋ก ํด์ ๋ค์ต์คํธ๋ผ๋ก ํ์๋ค

### ๐ ์ฝ๋

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
