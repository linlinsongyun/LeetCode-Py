# [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

- 标签：递归、数学
- 难度：简单

## 题目大意

`0`、`1`、…、`n - 1` 这 `n` 个数字排成一个圆圈，从数字 `0` 开始，每次从圆圈里删除第 `m` 个数字。现在给定整数 `n` 和 `m`。

要求：求出这个圆圈中剩下的最后一个数字。 

## [解题思路](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solutions/177639/javajie-jue-yue-se-fu-huan-wen-ti-gao-su-ni-wei-sh/)
- 数学上的约瑟夫环问题
```pythhon

class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        idx = 0
        i = 1
        while i <= n:
            idx = (idx + m) %i
            i += 1
        return idx
```

模拟循环删除，需要进行 `n - 1` 轮，每轮需要对节点进行 `m` 次访问操作。总体时间复杂度为 `O(nm)`。

可以通过找规律来做，以 `n = 5`、`m = 3` 为例。

- 刚开始为 `0`、`1`、`2`、`3`、`4`。
- 第一次从 `0` 开始数，数 `3` 个数，于是 `2` 出圈，变为 `3`、`4`、`0`、`1`。
- 第二次从 `3` 开始数，数 `3` 个数，于是 `0` 出圈，变为 `1`、`3`、`4`。
- 第三次从 `1` 开始数，数 `3` 个数，于是 `4` 出圈，变为 `1`、`3`。
- 第四次从 `1` 开始数，数 `3` 个数，于是 `1` 出圈，变为 `3`。
- 所以最终为 `3`。

通过上面的流程可以发现：每隔 `m` 个数就要删除一个数，那么被删除的这个数的下一个数就会成为新的起点。就相当于数组进行左移了 `m` 位。反过来思考的话，从最后一步向前推，则每一步都向右移动了 `m` 位（包括胜利者）。

如果用 `f(n, m)` 表示： `n` 个数构成环没删除 `m` 个数后，最终胜利者的位置，则 `f(n, m) = f(n - 1, m) + m`。

即等于 `n - 1` 个数构成的环没删除 `m` 个数后最终胜利者的位置，像右移动 `m` 次。

问题是现在并不是真的进行了右移，因为当前数组右移后超过数组容量的部分应该重新放到数组头部位置。所以公式应为：`f(n, m) = [f(n - 1, m) + m] % n`，`n` 为反过来向前推的时候，每一步剩余的数字个数（比如第二步推回第一步，n `4`），则反过来递推公式为：

- `f(1, m) = 0`。
- `f(2, m) = [f(1, m) + m] % 2`。
- `f(3, m) = [f(2, m) + m] % 3`。
- 。。。。。。

- `f(n, m) = [f(n - 1, m) + m] % n `。

接下来就是递推求解了。

## 代码

```Python
class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        ans = 0
        for i in range(2, n + 1):
            ans = (m + ans) % i
        return ans
```

## 参考资料：

- [字节题库 - #剑62 - 简单 - 圆圈中最后剩下的数字 - 1刷](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/zi-jie-ti-ku-jian-62-jian-dan-yuan-quan-3hlji/)

