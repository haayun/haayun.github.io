---
emoji: ๐
title: ใํ๋ก๊ทธ๋๋จธ์คใ ๋ง์น ํ๊ธฐ
date: '2023-03-07 00:00:00'
author: ํ์ฐ
tags: ์ฝ๋ฉํ์คํธ ํ๋ก๊ทธ๋๋จธ์ค
categories: ์๊ณ ๋ฆฌ์ฆ
---

## โ ๋ฌธ์ 

### [๋ฌธ์  ๋ฐ๋ก๊ฐ๊ธฐ](https://school.programmers.co.kr/learn/courses/30/lessons/161989)

## โ ํ์ด

๊ทธ๋ฅ ์ ์น ํด์ง ๊ณณ์ด ๋ฐ๊ฒฌ๋๋ฉด ์น ํจ.
์ ํ์ผ๋ก ํ์ํ๋ฉด ๋์ธ ๋ฌธ์ ์๋ค.
๋ฉ๋ชจ๋ฆฌ ๋ ์๋ ์ ์์ ๊ฒ ๊ฐ๊ธด ํ๋ฐ ๊ทธ๋ฅ ์ฒ์ ํผ ๋๋ก ์ ์ถ..

### ๐ ์ฝ๋

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
