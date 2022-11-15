实现 pow(x, n) ，即计算 x 的整数 n 次幂函数（即，$x^n$ ）。


可以逐级拆分成 x = x^2, n=n//2 
               x = (x^2)^2, n = (n//2)//2
每次都要考虑 n//2之后是奇数or偶数的问题


```Python

class Solution:
    def myPow(self, x: float, n: int) -> float:
    
        if n==0:   ## 中止条件
            return 1
        elif n<0:
            return  self.myPow(1/x, abs(n)) 
        # 拆分子问题
        res = 1
        while n:
            if n%2==1:
                res = res * x
               
            x = x * x
            n >> 1
        return res
        
        
```
