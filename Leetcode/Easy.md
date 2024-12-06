
# 69. Sqrt(x)

## Newton-Raphson method

$$
x_{k+1} = x_{k} - \frac{f(x_{\text{k}})}{f'(x_{\text{k}})}
$$

 $f(x) = x^2 - N = 0$, $f'(x) = 2x$. We want to find $sqrt(N)$.
 **Iterative method**
 
$$
x_{k+1} = x_{k} - \frac{1}{2}\left( x_k + \frac{N}{x_k} \right)
$$


# [112. Path Sum](https://leetcode.com/problems/path-sum/)

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def hasPathSum(self, root, targetSum):
        """
        :type root: Optional[TreeNode]
        :type targetSum: int
        :rtype: bool
        """
        if not root:
            return False

        def reachLeaf(current, sum, target):
            if not current:
                return
            sum += current.val
            # Valida si el nodo actual es una hoja y alcanzo la suma
            if sum == target and not (current.left or current.right):
                return True
            if reachLeaf(current.left, sum, target):
                return True
            if reachLeaf(current.right, sum, target):
                return True
            return False    
        return reachLeaf(root, 0, targetSum)
```

