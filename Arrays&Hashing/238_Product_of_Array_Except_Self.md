# Link:
- [238_Product_of_Array_Except_Self](https://leetcode.com/problems/product-of-array-except-self/description/)

# Intuition

This problem is a little bit tricky, and I watched Neetcode's explanation. Neetcode is very clever.

Given the input: $nums = [1,2,3,4]$

The expected output is: $[24,12,8,6]$

First, we need to construct a result array to store each product value. The array's length is the same as `nums`. For example:
- For `1`, the product is $2 \times 3 \times 4$
- For `2`, the product is $1 \times 3 \times 4$
- For `3`, the product is $1 \times 2 \times 4$
- For `4`, the product is $1 \times 2 \times 3$

We can notice that the array is split into two parts based on the value for which we want to know its product. So, we can calculate the prefix product and the postfix product, then multiply them together.

For the prefix product, we can initialize it to be 1 and update its value as we loop through the entire array. We will calculate each position's prefix product value. How do we do it? `res[i] = prefix`, and then `prefix *= nums[i]`. That means each time we reach `nums[i]`, the prefix is already the prefix product value that we can simply use and then update.

For the postfix product, we can also initialize it to be 1, and it should be calculated in reverse order. By this time, `res` is already filled with the prefix product value. Then, for the postfix product, we will update `res[i] *= postfix`, then update `postfix *= nums[i]`.

# Approach

Construct a result array, which is `[1] * len(nums)`, to store the product value for each number. The product is divided into prefix and postfix. In this case, the prefix will be initialized to 1, and we will loop through the entire array to update the result array and the prefix value. Similarly, the postfix will be initialized to 1, and we will loop through the entire array in reverse order to update the result array and the postfix value.


# Complexity
- Time complexity:
$$O(n)$$

    - The time complexity is $O(n)$ because we iterate through the array twice: once to calculate the prefix products and once to calculate the postfix products. Each iteration is linear in terms of the number of elements in the array.

- Space complexity:
$$O(n)$$

    - The space complexity is $O(n)$ because we use an additional array res of the same length as the input array nums to store the results. The space used by prefix and postfix variables is constant, but the additional result array makes the space complexity linear.

# Code
```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = [1] * len(nums)
        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(len(nums)-1,-1,-1):
            res[i]*=postfix  
            postfix*=nums[i]
        return res
```
