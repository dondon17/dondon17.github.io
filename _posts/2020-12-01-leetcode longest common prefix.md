---
layout: post
title: leet code - Longest Common Prefix
category: leetcode
tags: [leetcode, python]
---

# leet code 문제 풀기 > [leetcode](https://leetcode.com/)  

## [leetcode - Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)  

```python
def longestCommonPrefix(self, strs):
    """
    :type strs: List[str]
    :rtype: str
    """
    res = ""
    strs.sort(key=len)
    flag = 0
    if len(strs)==0:
        return res
    for j in range(0, len(strs[0])):
        for i in range(0, len(strs)):
            if strs[0][j] == strs[i][j]:
                flag=1
            else:
                flag=0
                return res
            if(i==len(strs)-1 and flag==1):
                res+=strs[0][j]
    return res

```

---

배열 요소들의 공통 prefix를 찾는 문제이다. 모든 문제가 그러하듯 solution부터 보는 것은 좋지 않은 습관이니 참고용도로만 보는 것을 추천한다.

📌풀이 방법  
> 먼저 매개변수로 전달받은 배열을 요소의 길이별로 정렬한다. 예를 들어, aaaaaa, bbb, cccc가 저장된 배열은 bbb, cccc, aaaaaa 순으로 정렬된다. 이 때, 요소의 길이가 같은 것은 상관할 필요가 없다. 어짜피 prefix의 최대 길이는 길이가 가장 작은 요소의 길이이기 때문이다.  
> 정렬을 했다면 배열의 가장 첫번째 요소의 문자를 차례대로 다른 요소들의 문자들과 처음부터 비교해본다.
>
> 즉, 예를들면 strs = [flow, flower, flipper]인 경우 flow의 f부터 flower, flipper의 앞 문자부터 비교한다.  
>
> 만약 prefix가 달라지는 요소가 하나라도 있으면 flag를 0으로 만들고 바로 return 하고, 배열의 마지막 요소와 비교했을 때도 flag비트가 1로 켜져있다면, 중간에 return되지 않은 것이므로 res에 더해준다.  
>
> 여기서 주의할 점은 배열의 길이가 0인 경우와, 요소가 한개인 경우인데, 길이가 0인 경우 바로 return하도록 지정하였고, 길이가 1인 경우는 strs[0][j]를 strs[i][j]와 비교할 떄, i를 0부터 시작함으로써 자기 자신과도 비교시킴으로써 해결하였다.
  
📌변수 설명  
> res  : 결과를 저장할 변수  
> flag : 달라진 prefix가 있는 경우를 판별할 플래그 비트  
