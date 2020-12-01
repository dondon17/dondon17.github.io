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
            sum = nums[i]+nums[l]+nums[r]
            if sum < 0:
                l += 1
            elif sum > 0:
                r -= 1
            else:
                res.append([nums[i], nums[l], nums[r]])
                l += 1
                while l<r and nums[l] == nums[l-1]:
                    l += 1
    return res

```

---
주어진 배열에서 3개 요소의 합이 0이 되는 부분 집합을 찾는 문제이다. 중복된 3개의 쌍은 제외하되 출력해야하며, 정렬된 상태로 출력되어야 한다.  
📌풀이방법  
> 맨 처음에 떠오르는 방법은 3중 for문을 돌려 합이 0이되는 3개의 요소들을 찾아내는 방법이었다. 다만 테스트 케이스들을 모두 통과하기는 하지만 time over되는 문제가 발생하여 새로운 방법으로 다시 시도해보았다.  
> 두 번째 방법은 바로 한 요소를 양 끝에서 얻은 두 요소와 기준 값을 더한 값이 0이되는 방법이다. 즉, 정렬된 nums 배열에서 i번째 요소를 기준으로 i번째부터 배열의 남은 요소들의 구간에서 가장 작은 값과 큰 값을 더하는 방법이다.
>
