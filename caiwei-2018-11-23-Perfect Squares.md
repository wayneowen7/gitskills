### 279. Perfect Squares
- https://leetcode.com/problems/perfect-squares/
- 大循环，双重，每次依赖一下最大的 square数，等于减去最大square对应的索引+1，这个1就是最大square需要的个数，就这一个数。

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> result(n+1,INT_MAX);
        result[0]=0;
        for(int j=1;j<=n;j++)
        {
            
            for(int i=1;i*i<=j;i++)
            {
                result[j]=min(result[j],result[j-i*i]+1);
                
            }
            
        }
        return result[n];
    }
};
```

小循环

```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> result={0};
        int m=0;
        while(result.size()<=n)
        {
            m=result.size();
            int tempt=INT_MAX;
            for(int i=1;i*i<=m;i++)
            {
                tempt=min(tempt,result[m-i*i]+1);
                
            }
            result.push_back(tempt);
        }
        return result.back();
    }
};
```

