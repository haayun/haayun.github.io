---
emoji: ๐
title: ใ๋ฐฑ์คใ 13913๋ฒ ์จ๋ฐ๊ผญ์ง 4
date: '2022-12-13 23:00:00'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ๋ฐฑ์ค BOJ BFS ์ญ์ถ์ 
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://www.acmicpc.net/problem/13913)

#### ์ ํ: BFS ์ญ์ถ์ 

#### ํฐ์ด : Gold4

## โ ํ์ด

์ญ์ถ์ ์ ํ์ฉํ๋ BFS ๋ฌธ์ 

PQ์ visited ๋ฐฐ์ด์ ํ์ฉํด์ ์ต๋จ๊ฑฐ๋ฆฌ๋ฅผ ์ฐพ๊ณ  path ๋ฐฐ์ด์ ์ด๋ ์ด์ ์ ์ธ๋ฑ์ค๋ฅผ ์ ์ฅํ์๋ค.

๊ทธ๋์ ๋์ ์์น์์๋ถํฐ ์๋น์ด๊น์ง ๋๋ฌํ๋ ๊ฒฝ๋ก๋ฅผ ๊ฑฐ๊พธ๋ก ์ถ๋ ฅํด์ฃผ๋ฉด ํ๋ฆฌ๋ ๋ฌธ์ ์๋ค.

์๊ฐ์ ๋ ์ด๋ป๊ฒ ์ค์ฌ์ผํ ์ง๋ ๋ชจ๋ฅด๊ฒ ๋คโฆ (insert๊ฐ ์ค๋ ๊ฑธ๋ฆฌ๋ ๊ฒ ๊ฐ๊ธฐ๋ ํ๊ณ ?)

### ๐ ์ฝ๋

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main_13913_์จ๋ฐ๊ผญ์ง_4 {
    static int MAX = 100000;
    static PriorityQueue<Node> pq;
    static int[] path;
    static boolean[] visited;
    static class Node implements Comparable<Node>{
        int v;
        int cost;
        public Node(int v, int cost){
            this.v = v;
            this.cost = cost;
        }

        @Override
        public int compareTo(Node o) {
            return this.cost - o.cost;
        }
    }
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        visited = new boolean[MAX + 1];
        path = new int[MAX + 1];

        pq = new PriorityQueue<>();
        pq.offer(new Node(N, 0));
        visited[N] = true;
        path[N] = -1;
        Node cur = null;

        while(!pq.isEmpty()){
            cur = pq.poll();
            if(cur.v == K) {
                break;
            }

            move(cur, cur.v - 1);
            move(cur, cur.v + 1);
            move(cur, cur.v * 2);
        }
        System.out.println(cur.cost);
        do {
            sb.insert(0, K + " ");
            K = path[K];
        } while(K != -1);

        System.out.println(sb.toString());

    }

    static void move(Node c, int n) {
        if(n >= 0 && n <= MAX && !visited[n]) {
            visited[n] = true;
            path[n] = c.v;
            pq.offer(new Node(n, c.cost + 1));
        }
    }

}
```

### ๐ฃ ๊ฒฐ๊ณผ

์์ ์๊ฐ : 1 h
![result](./result.png)

```toc

```
