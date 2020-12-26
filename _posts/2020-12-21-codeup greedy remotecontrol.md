---
layout: post
title: codeup - 3301 거스름돈
category: codeup
tags: [codeup, python]
---

# codeup 문제 풀기 > [codeup](https://codeup.kr/)

## [codeup - 3031 거스름돈](https://codeup.kr/problem.php?id=3301)

```python
# 정답 소스코드
price = int(input())
money = [50000, 10000, 5000, 1000, 500, 100, 50, 10]
total = 0
for cash in money:
    total += (price//cash)
    price %= cash

print(total)
```

---
📌풀이방법  
> 그리디 알고리즘의 기본적인 문제인 거스름돈 문제이다. 주어진 금액을 어떻게 거슬러 주는 것이 가장 적은 개수의 지폐 또는 동전을 사용하는지를 구하는 문제이다.  
> 시간복잡도는 for 반복문에서 거슬러 줄 화폐의 종류 N개만큼 반복하기 때문에 <b>O(n)</b>이 된다.  
> 이 때, 가장 큰 거스름돈부터 진행되는 이유는, 나머지 화폐들이 모두 약수이기 때문이다. 즉, 50000원 밑의 액수들은 전부 50000의 약수이고, 10000원 밑의 액수들은 전부 10000의 약수이다.  
> 거슬러 줄 값인 <b>price</b>를 money 리스트의 거스름돈으로 나눈 몫을 total에 더해주고, 거스름돈으로 나눈 나머지로 price를 초기화한다. 이 과정을 money리스트의 모든 거스름돈을 사용할 때까지 진행한다.  

📌변수 설명  
> <b>total</b>은 거슬러 줄 지폐(화폐)의 개수이고, money 리스트는 거슬러줄 금액을 큰 순서대로 나열해 둔 배열이다.