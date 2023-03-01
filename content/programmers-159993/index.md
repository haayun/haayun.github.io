---
emoji: 🐜
title: 〈프로그래머스〉 미로 탈출
date: '2023-03-01 00:00:00'
author: 하연
tags: 코딩테스트 프로그래머스 BOJ BFS
categories: 알고리즘
---

## ❔ 문제

### [문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/159993)

#### 유형 : BFS

## ❕ 풀이

단순히 BFS 문제
프로그래머스로 코테를 보는 경우가 많으니까... IDE 없이 푸는 연습을 하고 있음

### 👀 코드

```java
import java.util.*;

class Solution {
    public int solution(String[] maps) {

        char[][] map = new char[maps.length][];
        int sr = 0, sc = 0, lr = 0, lc = 0, er = 0, ec = 0;
        for(int i = 0; i < maps.length; i++) {
            map[i] = maps[i].toCharArray();
            for(int j = 0; j < map[i].length; j++) {
                if(map[i][j] == 'S') {
                    sr = i; sc = j;
                    map[i][j] = 'O';
                } else if(map[i][j] == 'L') {
                    lr = i; lc = j;
                    map[i][j] = 'O';
                } else if(map[i][j] == 'E') {
                    er = i; ec = j;
                    map[i][j] = 'O';
                }
            }
        }

        int toL = bfs(map, sr, sc, lr, lc);
        int toE = bfs(map, lr, lc, er, ec);

        if(toL == -1 || toE == -1) return -1;
        return toL + toE;
    }

    int[] dr = {-1, 1, 0, 0};
    int[] dc = {0, 0, -1, 1};

    int bfs(char[][] map, int sr, int sc, int er, int ec) {
        int N = map.length, M = map[0].length;
        int[][] visited = new int[map.length][map[0].length];
        Queue<int[]> queue = new LinkedList<>();

        visited[sr][sc] = 1;
        queue.offer(new int[]{sr, sc});

        while(!queue.isEmpty()) {
            int r = queue.peek()[0];
            int c = queue.peek()[1];
            queue.poll();

            if(r == er && c == ec) {
                return visited[r][c] - 1;
            }

            for(int i = 0; i < 4; i++) {
                int nr = r + dr[i];
                int nc = c + dc[i];
                if(nr < 0 || nr >= N || nc < 0 || nc >= M || visited[nr][nc] != 0 || map[nr][nc] == 'X') continue;
                queue.offer(new int[]{nr, nc});
                visited[nr][nc] = visited[r][c] + 1;
            }

        }
        return -1;
    }
}
```

```toc

```
