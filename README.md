# 151. Reverse Words - LeetCode (Medium)

## 🔗 Problem Link
[LeetCode - Reverse Words of a String](https://leetcode.com/problems/reverse-words-in-a-string/)

## Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The goal is to reverse the **order** of words, not the characters within them.  
First thought: use Python's built-in string handling to strip extra spaces, split the words, reverse the list, and join them with a single space.

## Approach
<!-- Describe your approach to solving the problem. -->
1. Use `strip()` to remove leading/trailing whitespace.
2. Use `split()` to break the string into words — this automatically handles multiple spaces.
3. Reverse the list of words using slicing (`[::-1]`).
4. Use `' '.join(...)` to combine the words into a single space-separated string.

## Complexity
- Time complexity:  
<!-- Add your time complexity here, e.g. $$O(n)$$ -->  
$$O(n)$$ — where *n* is the length of the input string. We traverse the string a few times: stripping, splitting, and joining.

- Space complexity:  
<!-- Add your space complexity here, e.g. $$O(n)$$ -->  
$$O(n)$$ — for storing the list of words and the final output string.

## Code
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = []
        s = s.strip()  # Remove leading/trailing spaces
        k = 0

        for i in range(len(s)):
            if s[i] == ' ':
                # Only add non-empty words (skip multiple spaces)
                if s[k:i] != '':
                    words.append(s[k:i])
                k = i + 1

        # Add the last word (after the loop ends)
        if s[k:] != '':
            words.append(s[k:])

        print("Before reversing:", words)
        words = words[::-1]
        print("After reversing:", words)

        # Join words with a single space
        return ' '.join(words)
```
## Or we can simply use the pythonic one liner: 
```python
class Solution:
    def reverseWords(self, s: str) -> str:
        return ' '.join(s.strip().split()[::-1])
```

---

# 238. Product of Array Except Self - LeetCode (Medium)

## 🔗 Problem Link
[LeetCode - Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

## 💡 Intuition

- The brute-force approach calculates the product for each index by multiplying all the other numbers in the array, but this takes O(n^2) time.
- The optimal solution avoids using division by using prefix and suffix arrays to hold the running product from the left and the right.

## 🧠 Approach

- Initialize an array `result` to hold the final products.
- Use two passes through the array: one to calculate the prefix product and one to calculate the suffix product.
- Multiply the prefix and suffix products for each index to get the final product except self for that index.

## ⏱ Time Complexity

- **Time:** O(n)
- **Space:** O(1) (excluding output array)

## 📦 Code

```python
from typing import List

class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        product = 1
        zero_count = 0

        for num in nums:
            if num == 0:
                zero_count += 1
            else:
                product *= num

        result = []
        for num in nums:
            if zero_count == 0:
                result.append(product // num)
            elif zero_count == 1:
                if num == 0:
                    result.append(product)
                else:
                    result.append(0)
            else:
                result.append(0)

        return result
```
---

# 345. Reverse Vowels of a String - LeetCode

## 🔗 Problem Link
[LeetCode - Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/)

## ✅ Intuition
My first thought was: “We only care about vowels — so let’s grab them, reverse them, and drop them back in like nothing happened.”

We don’t need to reverse the whole string or worry about consonants. Just treat the vowels like VIPs, reverse their order, and stitch them back while keeping all other characters in place.

## 🧠 Approach
1. Convert the string into a list so it's mutable.
2. Create a list of vowels (both lowercase and uppercase, 'cause equality).
3. Iterate through the string and store all vowels in a separate list.
4. Loop through the string again — when a vowel is encountered, replace it with the corresponding vowel from the reversed list.
5. Finally, join the list back into a string and return it.

## Complexity
- **Time complexity:**  $$O(n)$$  
  (One pass to collect vowels, one to replace them — linear time overall)

- **Space complexity:**  $$O(n)$$  
  (We're storing the string as a list and the vowels separately — both proportional to the size of the input.)

## 💻 Code

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        s = list(s)
        vowels = ['A', 'E', 'I', 'O', 'U', 'a', 'e', 'i', 'o', 'u']
        v = []
        for i in s:
            if i in vowels:
                v.append(i)
        j = 1
        for i in range(len(s)):
            if s[i] in vowels:
                s[i] = v[len(v) - j]
                j += 1
        return ''.join(s)
```

---

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

---

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
