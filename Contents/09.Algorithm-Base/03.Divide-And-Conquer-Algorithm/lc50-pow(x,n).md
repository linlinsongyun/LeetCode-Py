实现 pow(x, n) ，即计算 x 的整数 n 次幂函数（即，$x^n$ ）。



```Python

class Solution:
    def myPow(self, x: float, n: int) -> float:
    
        if n==0:   ## 中止条件
            res = 1
        elif n==1:
            res =  x
        elif n<0:
            res =  self.myPow(1/x, abs(n)) 
        # 拆分子问题
        while n:
            if n%2==1:
                res = self.myPow(x, n//2) * self.myPow(x, n//2) * x
            else:
                res = self.myPow(x, n//2) * self.myPow(x, n//2)    
            n >> 1
        return res
        
        
```
