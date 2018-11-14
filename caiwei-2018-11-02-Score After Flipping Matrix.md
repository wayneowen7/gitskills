861. Score After Flipping Matrix

https://leetcode.com/problems/score-after-flipping-matrix/description/

贪心

每层就是一个数字

每层的首个位置应当为1，不是1的话进行行翻转

每一列的每个位置权重相同，计数之后如果小于一般，就翻转（计数之后，拿总数减去）

```c++
class Solution {
public:
    int matrixScore(vector<vector<int>>& A) {
        int m=A.size();
        int n=A[0].size();
        for(int i=0;i<m;i++)
        {
            if(A[i][0]==0)
                for(int j=0;j<n;j++)
                    A[i][j]^=1;
        }
        int sum=m;
        for(int j=1;j<n;j++)
        {
            int count=0;
            for(int i=0;i<m;i++)
            {
                    count+=A[i][j];
            }
            if(count<=(m/2))
                count=m-count;
            sum=sum*2+count;
        }
        return sum;
    }
};
```

