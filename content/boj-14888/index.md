---
emoji: ๐
title: ใ๋ฐฑ์คใ 14888๋ฒ ์ฐ์ฐ์ ๋ผ์๋ฃ๊ธฐ
date: '2022-12-12'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ๋ฐฑ์ค BOJ ๋ธ๋ฃจํธํฌ์ค ๋ฐฑํธ๋ํน
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/14888)

#### ์ ํ : ๋ธ๋ฃจํธํฌ์ค ๋ฐฑํธ๋ํน

#### ํฐ์ด : Silver1

## โ ํ์ด

๋ธ๋ฃจํธํฌ์ค + ๋ฐฑํธ๋ํน

DFS๋ก ๋ชจ๋  ๊ฒฝ์ฐ์ ์๋ฅผ ๋ค ํด๋ณธ๋ค.

์์ด ์๊ฐํ๋ฉด์ ์ฐ์ฐ์ ๊ฐ์๊ฐ ๋จ์์์ผ๋ฉด ๊ณ์ฐํ๊ณ  ์ฌ๊ท ํธ์ถํ๋ค.

์ข๋ฃ ์กฐ๊ฑด์ ๋ง์ง๋ง ํผ์ฐ์ฐ์๊น์ง ๊ณ์ฐํ์ ๋, ๊ทธ๋ฆฌ๊ณ  min, max ๊ฐ๊ฐ ํ์ธํ๋ค.

์ฐ์ฐ์ ๊ฐ์๋ฅผ ๋ฑ ๋ง๊ฒ ์ ๊ณตํด์ ์์ธ ์ฒ๋ฆฌ(out of bound)๊ฐ ํ์์์๋ค. ๊ตณ.

### ๐ ์ฝ๋

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main_3055_ํ์ถ {
    static int R, C;
    static char[][] map;
    static int[][] check;
    static Queue<int[]> queue, water;
    static int[] S, D;
    static int[] dr = {-1, 0, 1, 0};
    static int[] dc = {0, -1, 0, 1};
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());
        map = new char[R][];
        check = new int[R][C];
        queue = new LinkedList<>();
        water = new LinkedList<>();
        for(int i = 0; i < R; i++){
            String s = br.readLine();
            map[i] = s.toCharArray();
            for(int j = 0; j < C; j++){
                if(map[i][j] == 'S'){
                    S = new int[]{i, j};
                    check[i][j] = 1;
                }
                if(map[i][j] == 'D'){
                    D = new int[]{i, j};
                }
                if(map[i][j] == '*'){
                    water.offer(new int[]{i, j});
                }
            }
        }

        int result = bfs();
        if(result == 0)
            System.out.println("KAKTUS");
        else
            System.out.println(result);

    }

    static int bfs(){
        int[] cur, next;
        int size;
        queue.offer(S);
        while(!queue.isEmpty()){
            // ๋ฌผ ํ์ฅ
            size = water.size();
            for(int w = 0; w < size; w++){
                cur = water.poll();
                for(int i = 0; i < 4; i++){
                    next = new int[]{cur[0] + dr[i], cur[1] + dc[i]};
                    if (next[0] < 0 || next[0] >= R || next[1] < 0 || next[1] >= C) continue;
                    if (map[next[0]][next[1]] == '.') {
                        water.offer(next);
                        map[next[0]][next[1]] = '*';
                    }
                }
            }

            // ๊ณ ์ด๋์น ์ด๋
            size = queue.size();
            for(int s = 0; s < size; s++) {
                cur = queue.poll();
                if(map[cur[0]][cur[1]] == 'D'){
                    return check[cur[0]][cur[1]] - 1;
                }
                for (int i = 0; i < 4; i++) {
                    next = new int[]{cur[0] + dr[i], cur[1] + dc[i]};
                    if (next[0] < 0 || next[0] >= R || next[1] < 0 || next[1] >= C) continue;
                    if (check[next[0]][next[1]] > 0 || map[next[0]][next[1]] == '*' || map[next[0]][next[1]] == 'X') continue;

                    queue.offer(next);
                    check[next[0]][next[1]] = check[cur[0]][cur[1]] + 1;
                }
            }
        }
        return 0;
    }
}
```

### ๐ฃ ๊ฒฐ๊ณผ

์์ ์๊ฐ : 30 m
![14888](./result.png)

ํ๊ธฐ :
ํ๋ฉด ์ ์ด๋ ค์ด๋ฐ ์์ด, ์กฐํฉ ์ด๋ฐ ๊ฑฐ ๋ค์ ๊ธฐ์ตํด๋ณผ๋ผ๋๊น ์ข ๋ง๋งํ๋ค.
์์ธ ์๊ธฐ์ง ์๊ฒ ์ฐ์ฐ์ ๊ฐ์ ๋ฑ ๋ง๊ฒ ์คฌ๋๋ฐ ๊ทธ๋ ์ง ์์ ๊ฐ์ ์ผ๋ก ํ์ด๋ ์ข์ ๋ฏ? (์ฐ์ฐ์๊ฐ ์ ๋ถ 0๊ฐ์ด๋ฉด ์ฌ๊ท ํธ์ถํ์ง ์๊ฒ ์งฐ์)

```toc

```
