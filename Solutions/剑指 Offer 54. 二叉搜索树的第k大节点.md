# [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

- 标签：树、深度优先搜索、二叉搜索树、二叉树
- 难度：简单

## 题目大意

给定一棵二叉搜索树的根节点 `root`，以及一个整数 `k`。

要求：找出二叉搜索树书第 `k` 大的节点。

## 解题思路

解题思路：https://leetcode.cn/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/solutions/184216/mian-shi-ti-54-er-cha-sou-suo-shu-de-di-k-da-jie-d/

已知中序遍历「左 -> 根 -> 右」能得到递增序列。逆中序遍历「右 -> 根 -> 左」可以得到递减序列。

```python
# 打印中序遍历倒序
def dfs(root):
    if not root: return
    dfs(root.right) # 右
    print(root.val) # 根
    dfs(root.left)  # 左
 ```


则根据「右 -> 根 -> 左」递归遍历 k 次，找到第 `k` 个节点位置，并记录答案。

递归解析：
- 终止条件： 当节点 root 为空（越过叶节点），则直接返回；
- 递归右子树： 即 dfs(root.right) ；
- 三项工作：
    提前返回： 若 k=0 ，代表已找到目标节点，无需继续遍历，因此直接返回；
    统计序号： 执行 k=k−1 （即从 k 减至 0）；
    记录结果： 若 k=0，代表当前节点为第 k大的节点，因此记录 res=root.val ；
- 递归左子树： 即 dfs(root.left) ；




## 代码

```Python
class Solution:
    res = 0
    k = 0
    def dfs(self, root):
        if not root:
            return
        self.dfs(root.right)
        if self.k == 0:
            return
        self.k -= 1
        if self.k == 0:
            self.res = root.val
            return
        self.dfs(root.left)

    def kthLargest(self, root: TreeNode, k: int) -> int:
        self.res = 0
        self.k = k
        self.dfs(root)
        return self.res
```

