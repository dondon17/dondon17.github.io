---
layout: post
title: leet code - Add Two Numbers
category: leetcode
tags: [leetcode, python]
---

# leet code 문제 풀기 > [leetcode]("https://leetcode.com/")

## [leetcode - 3sum]("https://leetcode.com/problems/add-two-numbers/")  

```python
def addTwoNumbers(self, l1, l2, c=0):  
    """
    :type l1: ListNode
    :type l2: ListNode
    :rtype: ListNode
    """

    val = l1.val + l2.val + c
    c = val//10

    result = ListNode(val%10)

    if l1.next != None or l2.next != None or c != 0:
        if l1.next == None:
            l1.next = ListNode(0)
        if l2.next == None:
            l2.next = ListNode(0)

        result.next = self.addTwoNumbers(l1.next, l2.next, c)

    return result  
```

---
연결 리스트의 노드끼리 더하는 함수를 구현하는 문제이다. 조금 구체적으로 말하면 두 수의 LSB부터 계산하는 문제이다.  

📌풀이방법  
> 먼저 기존의  ```addTwoNumbers```함수의 파라미터에 carry(c) 값을 추가하였다. carry는 두 노드의 합이 10을 넘어갈 경우 발생하는 올림수를 의미하는데, 재귀 호출로 문제를 풀 때, 이 전 노드에서 발생한 carry값을 다음 노드의 계산에 사용하려면 파라미터로 넘겨줘야한다.  
> 다음으로 리턴할 listnode의 val값에 파라미터로 전달받은 두 listnode의 val값을 더하고 carry값을 더한다. LSB 노드를 계산할 때에는 default c값인 0이 더해진다. 이후 val값을 10으로 나눈 몫을 c에 초기화하고, val값을 10으로 나눈 나머지를 ListNode에 추가한다.  
> 다음으로 나오는 ```if``` 서로 다른 개수의 노드를 가진 listnode끼리의 합을 처리하기 위함이다. c값이 0이 아니거나, listnode의 next val이 null이 아닌 경우 모두 조건문을 거치게 되며, 조건문 안에서는 null이되는 listnode의 next val값을 0으로 초기화해줌으로써 덧셈을 가능하도록 해준다.  
> 이 때, 주의할 점은 ```l2.next=0```으로 초기화하면 안되고 next도 node value값이므로 ```l2.next=ListNode(0)```으로 초기화해주어야 한다.
> 그 다음으로 c값을 포함하여 재귀호출하여 다음 노드의 덧셈을 실행하고, 모든 계산이 끝나면 반환하도록 한다.  
>  
📌변수 설명  
> val은 노드에 들어가는 값이라고 보면 된다. next와 val을 헷갈릴 수 있지만, 둘 다 node에 들어가는 값으로 동일하며, 단지 val은 현재 node의 값, next는 다음 node의 값이라고 보면 된다.  
> c값은 carry를 의미하는 변수로, 올림수를 처리하기 위한 변수이다.  
>