---
layout: post
title: leet code - 3sum
category: leetcode
tags: [leetcode, python]
---

# leet code 문제 풀기 > [leetcode]("https://leetcode.com/")

## [leetcode - 3sum]("https://leetcode.com/problems/3sum/")  

```python
def threeSum(self, nums):
    """
    :type nums: List[int]
    :rtype: List[List[int]]
    """
    nums.sort()
    n, res = len(nums), []
    if n<3:
        return res
    for i in range(n):
        l, r = i+1, n-1
        if i > 0 and nums[i]==nums[i-1]:
            continue
        while l < r:
            if nums[i]+nums[l]+nums[r] < 0:
                l += 1
            elif nums[i]+nums[l]+nums[r] > 0:
                r -= 1
            else:
                res.append([nums[i], nums[l], nums[r]])
                l += 1
                while l<r and nums[l] == nums[l-1]:
                    l += 1
    return res

```

---
제목을 자꾸 반복해서 말하면 조금 이상하게 들린다..🔞  

주어진 배열에서 3개 요소의 합이 0이 되는 부분 집합을 찾는 문제이다. 중복된 3개의 쌍은 제외하되 출력해야하며, 정렬된 상태로 출력되어야 한다.

📌풀이방법  
> 맨 처음에 떠오르는 방법은 3중 for문을 돌려 합이 0이되는 3개의 요소들을 찾아내는 방법이었다. 다만 테스트 케이스들을 모두 통과하기는 하지만 time over되는 문제가 발생하여 새로운 방법으로 다시 시도해보았다.  
>
> 두 번째 방법은 바로 한 요소를 양 끝에서 얻은 두 요소와 기준 값을 더한 값이 0이되는 방법이다. 즉, 정렬된 nums 배열에서 i번째 요소를 기준으로 i번째부터 배열의 남은 요소들의 구간에서 가장 작은 값과 큰 값을 더하는 방법이다.  
>  
> l 값이 r값보다 커지면 반복문을 중단하며, ``` if i > 0 and nums[i]==nums[i-1]: continue ```  부분은 중복된 triplet을 허용하지 않기 위해 추가해준 조건문이다.  
>  
> 만약 sum = nums[i]+nums[l]+nums[r] 값이 0보다 작다는 것은 nums[l] 값이 너무 작기 때문이므로 l 값을 증가시킨다. 정렬되있으므로 l값이 증가시키면 이전의 nums[l]값 보다는 큰 수가 저장된다. 반대로 sum 값이 0보다 크다는 것은 nums[r] 값이 너무 크기 때문이므로 r 값을 1 감소 시켜준다.
>  
> 만약 0이 되는 세 개의 값을 찾으면 res 배열에 list형태로 추가하고, 마찬가지로 중복값을 추가하지 않기 위해 l 값을 중복값이 나타나지 않을 때까지 증가시킨다.  
   
📌변수 설명  
> l과 r은 각각 left, right 라고 보면 된다. 배열에서 nums[i] 이후 값들 중에서 left는 가장 작은 값, right는 가장 큰 값에서 시작한다.  
> sum은 세 수의 합을 나타내며, 만약 두 수의 값으로 나타내고 싶다면 nums[l]+nums[r]=-nums[i]로 생각하고 풀면 된다.(좌변이 3항인 등식에서 하나를 우변으로 옮긴것으로 그냥 똑같다고 보면 된다.)  
>
