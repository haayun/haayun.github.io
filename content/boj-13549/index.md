---
emoji: π
title: γλ°±μ€γ 13549λ² μ¨λ°κΌ­μ§ 3
date: '2022-12-13'
author: νμ°
tags: μ½λ©νμ€νΈ λ°±μ€ BOJ λ€μ΅μ€νΈλΌ
categories: μκ³ λ¦¬μ¦
---

## β λ¬Έμ 

### [λ¬Έμ  λ°λ‘κ°κΈ°](https://www.acmicpc.net/problem/13549)

#### μ ν : λ€μ΅μ€νΈλΌ

#### ν°μ΄ : Gold5

## β νμ΄

μ€μν λ¬Έμ  μ‘°κ±΄ : **μκ°μ΄λμ νλ κ²½μ°μλ 0μ΄ νμ 2\*Xμ μμΉλ‘ μ΄λνκ² λλ€.**

μ²μμ BFSλ‘λ§ νμ΄λ³΄λ €κ³  νλ€. β κ²°κ³Ό : νλ Έμ΅λλ€.

μ΄μ  : BFSλ **λͺ¨λ  κ°μ μ κ°μ€μΉκ° λμΌν΄μΌ νλ€λ**Β μ μ  μ‘°κ±΄μ΄ νμνλ€.

κ·Έλμ μ§λ¬Έ κ²μνκ³Ό μ νμ μ°Έκ³ ν΄λ³΄λ νμ΄ λ°©μμ 3κ°μ§ μ λλ‘ λλ μ μλ€κ³  νλ€.

- λ€μ΅μ€νΈλΌ μκ³ λ¦¬μ¦
- 0-1 BFS: κ°μ€μΉκ° 0μΈ κ°μ μ μ°κ²°λ μ μ μ νμ λ§¨ λ€κ° μλ λ§¨ μμ λ£λ λ°©λ²
- 2λ₯Ό λ³λμ κ°μ μΌλ‘ μκ°νμ§ μκ³ , +1μ΄λ -1μ μν μ’νλ₯Ό νμ λ£μ λ κ·Έ μ’νμ 2μ κ±°λ­μ κ³± λ°°μΈ μ’νλ€μ μ λΆ νμ λ£λ λ°©λ²

μ΄ μ€ λ€μ΅μ€νΈλΌ μκ³ λ¦¬μ¦(+ μ°μ μμ ν) νμ©ν΄μ νμλ€.

λμ€μ 0-1 BFSμ λν΄μλ κ³΅λΆν΄λ³΄λ©΄μ λ€μ νλ©΄ μ’μ κ² κ°λ€.

### π μ½λ

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main_13549_μ¨λ°κΌ­μ§_3 {
    static int MAX = 100000;
    static class Node {
        int v;
        int cost;

        public Node(int v, int cost) {
            this.v = v;
            this.cost = cost;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> o1.cost - o2.cost);
        int[] dist = new int[MAX + 1];
        boolean[] visited = new boolean[MAX + 1];
        for (int i = 0; i <= MAX; i++) {
            dist[i] = Integer.MAX_VALUE;
        }
        dist[N] = 0;
        visited[N] = true;
        pq.offer(new Node(N, 0));
        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            if(cur.v == K) break;
            if(!visited[cur.v]) visited[cur.v] = true;
            ArrayList<Node> nextNodes = new ArrayList<>();
            if(cur.v - 1 >= 0) nextNodes.add(new Node(cur.v - 1, 1));
            if(cur.v + 1 <= MAX) nextNodes.add(new Node(cur.v + 1, 1));
            if(cur.v * 2 <= MAX) nextNodes.add(new Node(cur.v * 2, 0));

            for(Node next : nextNodes) {
                if(!visited[next.v] && dist[next.v] > cur.cost + next.cost) {
                    dist[next.v] = cur.cost + next.cost;
                    pq.add(new Node(next.v, dist[next.v]));
                }
            }
        }
        System.out.println(dist[K]);

    }
}
```

### π£ κ²°κ³Ό

μμ μκ° : 1 h
![13549](./result.png)

```toc

```
