# 2126. Asteroid Collision Solution

## Intuition
The idea is simple — if you can absorb a smaller or equal-sized asteroid, your mass increases by its size. To maximize survival chances, absorb smaller asteroids first. Sorting the list ensures you always encounter the smallest possible asteroid next.

## Approach
1. **Sort** the list of asteroids in ascending order.
2. Iterate over the sorted asteroids:
   - If the asteroid’s size is less than or equal to the current mass, absorb it and increase your mass.
   - If you encounter an asteroid larger than your current mass, you can't absorb it — return `False`.
3. If all asteroids are absorbed successfully, return `True`.

## Complexity
- **Time complexity:**  $$O(n \log n)$$  
  (because of sorting the list of `n` asteroids)

- **Space complexity:**  $$O(1)$$  
  (if sorting in-place — otherwise $$O(n)$$ depending on the language’s sorting implementation)

## Code
```python
class Solution:
    def asteroidsDestroyed(self, mass: int, asteroids: List[int]) -> bool:
        ast = sorted(asteroids)
        for a in ast:
            if a <= mass:
                mass += a
            else:
                return False
        return True
```

# 169. Majority Element - LeetCode

## 🔗 Problem Link
[LeetCode - Majority Element](https://leetcode.com/problems/majority-element/)

## 💡 Intuition
I needed to find the element that appears more than `n/2` times in a list. My initial thought was to count how often each element appears, and `collections.Counter` instantly came to mind—it’s built for this exact task.

## 🧠 Approach
1. I used `Counter` from Python’s `collections` module to count frequencies of all elements in the list.
2. Then I looped through the counted elements and returned the one that appears at least `n//2` times.

> Note: Technically, the majority element appears **more than** `n/2` times, not just `>=`, but the problem guarantees a majority exists, so this approach works.

## ✅ Code

```python
from collections import Counter
from typing import List

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count = Counter(nums)
        for i in count:
            if count[i] >= (len(nums) // 2):
                return i

```
