```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        # 0  1  2  3  4  5
        #            one two
        one, two = 1, 1
        for i in range(n-1):
            temp = one
            one = one + two
            two = temp
        return one
```
Time Complexity: O(n)

Space Complexity: O(1)

___
___

Explanation:

Example 1:

stating at step0 and want to get step2.

step0 step1 step2

<img src="step2.png" alt="step2" width="400" height="300"/>

Consider we want to reach step 2, then from 0 we can take 1 step which reach 1 or take 2 step which reach 2(**completed**),  then from 1, we can take 1 step which reach 2(**completed**) or take 2 steps which reach 3(too far).

There are 2 ways total.

Example2:
stating at step0 and want to get step3.

step0 step1 step2 step3

<img src="step3.png" alt="step3" width="400" height="300"/>

Consider we want to reach step 3, then from 0 we can take 1 step which reach 1 or take 2 step which reach 2.

Then from 1, we can take 1 step which reach 2 or take 2 steps which reach 3(**completed**). From 2, we can take 1 step which reach 3(**completed**) or take 2 steps which reach 4(too far).

From 2, we can take 1 step which reach 3(**completed**) or take 2 steps which reach 4(too far).

There are 3 ways total.
___
Now I have an inituition now, that if we reach step 4, and our final goal is step 10, then we maybe have different ways to reach step4, but after that, step4 to step10 the way don't need to recalculate again and again. So we can cache the result, which is the inherent nature of dynamic programming.  And in the previous example, I see that in each step I'm making a decison, so I will use decision tree to illustrate it.

🌟🌟🌟🌟🌟 Base Case: At every given point, we have 2 decisions to make, either climb one or two. **When we reach 5**, it is our base case, we're gonna solve this recursively. When reach 5, **return 1**, this is when we find one way. And if this number of steps ever **exceeds five**, this is also the base case, we're going to **return 0**.

<img src="decisoin-tree.png" alt="decisoin-tree" width="400" height="300"/>

In the above image, the green circle 5 will return 1, the red ❌ will return 0. We can tell from the image total is 8 ways to reach step 5.

Now remember since we start at step0, we were asking how many different ways starting at step0 can we get to step5. Then we got to a subproblem starting at step1, how many ways can we reach step5, from this decison tree along, we can see there are 5 ways, and if the subproblem is starting at step2, we will have 3 ways to reach step5. So if solve the problem like this, basically using recursion and you could probably do it with dfs, because it is basically a tree. Time complexity is $2^n$, in this approach. Since we have two decisons each time, so it's goting to be 2 to the power of the height of this tree. And the height of the tree it's going to be roughly n equals 5, if you see the longest path is the most left path and that's roughly the height. So the overall time complexity is $2^n$. That's inefficient. 

```python
# inefficient solution
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        def dfs(i):
            if i >= n:
                return i == n
            return dfs(i + 1) + dfs(i + 2)
        return dfs(0)
```
Time Complexity: O($2^n$) 
Space Complexity: O(n)

> 🌟🌟🌟🌟🌟🌟🌟🌟🌟🌟 Time Complexity: When analyzing recursion, **time complexity** accounts for the **total number of calls** made to the function. In this case, the total number of recursive calls is proportional to the **total number of nodes in the recursion tree**. 
> - At each call to `dfs(i)`, the function does work in the form of making **two recursive calls**: `dfs(i + 1)` and `dfs(i + 2)`.
> -   These recursive calls are **new computations** — they explore different paths in the recursion tree and **add to the total number of operations performed**.
> -   Therefore, the total number of recursive calls is proportional to the **total number of nodes in the recursion tree**, which grows exponentially as $O(2^n)$.
> 
> Space Complexity: Each recursive call pushes the current state of the function onto the stack. The maximum depth of the recursion stack is equal to the **depth of the recursion tree**, which is O(n) in this case.
___
🌟🌟🌟🌟🌟 When look back at decision tree graph, we are repeating the same problem multiple times.  These two purple blocks is the same decision tree which calculate the way from step2 to step5. Because in both cases, we're solving the exact same subproblems. And since we are doing dfs, the left purple will be solved first, which calculated the way from step2 to step5. So when we get to right purple, we don't we just take that result store it in memory? We can store it in dp or basically this is a cache. We're storing it in memory so then when we get here we can just say we already  know the result of this meaning, we don't need to draw out the entire deciosn tree, we 're just going to skip that all together we're not going to draw right purple block. So I can eliminating all that repeated work by saving the left purple's solution.

<img src="purple.png" alt="purple" width="400" height="300"/> <img src="eliminate.png" alt="eliminate" width="400" height="300"/>

🌟🌟🌟🌟🌟 Similarly, staring from step3 to reach step5, these two blue blocks also the same, because we are aking that same question. My inituition here is that if the subproblem is same, we can just use a cache to store it, so we don't need to calculate it again, which elimate the repeated work.  Similar for the two orange block, which start from step 4 to reach step 5. The left decision tree the orange block is going to be computed first since we're doing dfs, so once again let's elimante the right orange block, elimanate the repeated work.

<img src="blue.png" alt="blue" width="400" height="300"/> <img src="orange.png" alt="orange" width="400" height="300"/>


🌟🌟🌟🌟🌟 So this is what our decion tree ends up looking like when we elimanate all the repeated work. And the time complexity is roughly O(n). This is linear time solution, since we're only solving each sub problem once. So we know the first subproblem, the original problem is starting at 0, then we get a subproblem of 1, 2, 3,4 all the way to 5 which is our base case. So each of these sub problems is just being solved once and n is 5, so overall the time complexity is O(n). And this is **basically the dynamic programming solution where we are caching the result aka memorization.**

<img src="eliminate-decision-tree.png" alt="eliminate-decision-tree" width="400" height="300"/>

___
🌟🌟🌟🌟🌟 But this problem can actually be solved with a true dynamic programming. The result of step0 depends on the subproblem which is the result of step1, step1 depends on its subproblem which is the result of step2,..., the result of step4 depends on its subproblem which is the basecase. So **why don't we start at the bottom solve the base case and then work our way up to the original problem at 0? This is called a bottom up dynamic programming.** Start at the base case, and work our way up.

<img src="bottom-up.png" alt="bottom-up" width="400" height="300"/>

Remember we are starting at position 0 and our goal is to get to the 5th step, each time we can take one step or 2 step.

<img src="question.png" alt="question" width="400" height="300"/>

So I'm going to **storing our result in an array called dp.** So we're going to have a position in dp all the way from index 0 all the way up to index n which is going to be our input value. **Each position in dp represents how many different ways from here to reach the goal.** So remember we're at the base case initially. At the last step if we start here, there just gonna be 1 way to reach here, 1 is our default value.

<img src="start-step5-1.png" alt="start-step5-1" width="400" height="300"/> <img src="start-step5-2.png" alt="start-step5-2" width="400" height="300"/>

Then we're able to solve starting from step4,  because it depends on the subproblem which is starting from step5. So starting from step4 we can take one step which will reach 5, or we can take two steops which lans us out of bounds. So starting from step4 and reach the goal, the way we can choose is 1.

<img src="start-step4-1.png" alt="start-step5-1" width="400" height="300"/> <img src="start-step4-2.png" alt="start-step5-2" width="400" height="300"/>

And what's interesting here is that, if change n to be 100, then you can see in position 100 and position 99, the value will also be 1. So no matter how to change the value of n, the value remains 0 for position n and position n-1. Since n-1 could only take one step to reach n, if take 2 steps, it will be out of bounds.

<img src="remain-1-1.png" alt="remain-1-1" width="400" height="300"/>

🌟🌟🌟🌟🌟 Now we want to know how many different ways from step3 to reach step5. **This depends on two sub problems which come after it.** From 4, we don't need to continue to figure out how many different ways from 4 can we get to 5, because we just computed that, that's why we're using dynamic programming! that's why we have this array because we already computed starting at 4 how many different ways can we reach 5. And we also know stariting at 5 how many different ways can we reach 5, that's also 1. So in position3's value, is basically **take  these next two values and add them together**, which is 1+1 = 2.

<img src="start-step3-1.png" alt="start-step5-1" width="400" height="300"/> <img src="start-step3-2.png" alt="start-step5-2" width="400" height="300"/>

Do the same for position2 and repeat it, then we can get the final result, which is 8. In graph, the orange part is related to orange square, the green part is related to green square, and the purple part is related to purple square. If you're familiar with what the fibonacci sequence, it is exactly the fibonacci numbers.

<img src="final-result.png" alt="final-result" width="400" height="300"/>

**So we're starting at the base case of 1, 1, adding these two values to get the next result then repeating it.** And we're using extra memory, we're having an entire array size equals n that's going to be O(n) extra memory. 
___
🌟🌟🌟🌟🌟 But actually we don't needed an entire array, notive each value only depends on the two values that come after it, so we just need two different variables. **We can make it named to "one, two", which one is gonna be position 4, and two is gonna be position 5. Because in position3, if we take one step we reach position4, so that's why we let one to be position4, and if we take two step we reach position5, so that's why we let two to be position5.** And once we computed position3, we will shift one and two variables to the left. And repeating it until we get to the result. 

<img src="one-two.png" alt="one-two" width="400" height="300"/>

And if we initialize two variables one and two as values 1, how many values do we have to compute that come after? In this case, we have to compute 4 values, which from position0 to position3. So **basically we compute n-1 values, we have to loop n-1 times. And the ONE variable will finally get to position0, and we're going to return it.** The one and two variables gonna shift n-1 times.

<img src="compute-n-1-final-one.png" alt="compute-n-1-final-one" width="400" height="300"/>

```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        # 0  1  2  3  4  5
        #            one two
        one, two = 1, 1
        for i in range(n-1):
            temp = one
            one = one + two
            two = temp
        return one
```
___
___
