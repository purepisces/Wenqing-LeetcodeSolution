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
```
