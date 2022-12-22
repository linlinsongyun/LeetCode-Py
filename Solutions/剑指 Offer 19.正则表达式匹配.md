##[题目](https://leetcode.cn/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。
在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。


## [思路](https://leetcode.cn/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solutions/494128/jian-zhi-offer-19-zheng-ze-biao-da-shi-pi-pei-dong/?orderBy=most_votes)


```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        m, n = len(s) + 1, len(p) + 1
        dp = [[False] * n for _ in range(m)]
        dp[0][0] = True
        for j in range(2, n, 2):
            dp[0][j] = dp[0][j - 2] and p[j - 1] == '*'
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i][j - 2] or dp[i - 1][j] and (s[i - 1] == p[j - 2] or p[j - 2] == '.') \
                           if p[j - 1] == '*' else \
                           dp[i - 1][j - 1] and (p[j - 1] == '.' or s[i - 1] == p[j - 1])
        return dp[-1][-1]
```

