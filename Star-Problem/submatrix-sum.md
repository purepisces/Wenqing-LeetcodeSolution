Refer to this blog: https://medium.com/@syphaxp/sum-of-sub-matrices-using-dynamic-programming-317bb26bd481

```python
def dynamic_sum_submatrices(mat):
    # n and m represent dimensions of the matrix
    n = len(mat)
    m = len(mat[0])
    
    # Declaring a (n*m) matrix initialized with zeros
    sum_mat = [[0] * m for _ in range(n)]
    
    # Part 1: Base case
    sum_mat[0][0] = mat[0][0]
    
    # Part 2: Fill the first row
    for i in range(1, m):
        sum_mat[0][i] = mat[0][i] + sum_mat[0][i - 1]
    
    # Part 3: Fill the first column
    for i in range(1, n):
        sum_mat[i][0] = mat[i][0] + sum_mat[i - 1][0]
    
    # Part 4: Fill the rest of the matrix
    for i in range(1, n):
        for j in range(1, m):
            sum_mat[i][j] = (
                mat[i][j]
                + sum_mat[i - 1][j]
                + sum_mat[i][j - 1]
                - sum_mat[i - 1][j - 1]
            )
    
    return sum_mat

def get_submatrix_sum(sum_mat, r1, c1, r2, c2):
    # Start with the total sum from the top-left corner to (r2, c2)
    total = sum_mat[r2][c2]
    
    # Subtract rows above r1
    if r1 > 0:
        total -= sum_mat[r1 - 1][c2]
    
    # Subtract columns to the left of c1
    if c1 > 0:
        total -= sum_mat[r2][c1 - 1]
    
    # Add back the overlapping region
    if r1 > 0 and c1 > 0:
        total += sum_mat[r1 - 1][c1 - 1]
    
    return total
```
Time Comlexity: $O(n \times m)$
Space Complexity: $O(n \times m)$


### **Example**

#### Input
```python
mat = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
sum_mat = dynamic_sum_submatrices(mat)
result = get_submatrix_sum(sum_mat, 1, 1, 2, 2)
```

#### Steps

1.  **Preprocessing (`dynamic_sum_submatrices`)**:
```python
sum_mat = [
    [1,  3,  6],
    [5, 12, 21],
    [12, 27, 45]
]
```
2. **Query (`get_submatrix_sum`)**:

   - Submatrix bounds: `(1, 1)` to `(2, 2)` corresponds to:
```python
[5, 6]
[8, 9]
```

-   Start with `sum_mat[2][2] = 45`
-   Subtract rows above: `sum_mat[0][2] = 6` 
   $$45 - 6 = 39$$
   -   Subtract columns left: `sum_mat[2][0] = 12` 
   $$39 − 12 = 27$$
   -   Add back overlap: `sum_mat[0][0] = 1` 
   $$27 + 1 = 28$$

#### Output

-   `result = 28`
