875. Koko Eating Bananas

https://leetcode.com/problems/koko-eating-bananas/description/

二分查找，寻找能满足的最小速度

所以每次是total>H 因为当 不大于H的时候走 high=m,即low不变，最终返回一个low即可，即为最小的速度。



```c++
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int H) {
        int low=1,high=1000000000;
        while(low<high)
        {
            int total=0,m=low+(high-low)/2;
            for(int p:piles)
                total+=(p+m-1)/m;
            if(total>H)
                low=m+1;
            else
                high=m;
        }
        return low;
    }
};
```

