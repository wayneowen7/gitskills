#376.Wiggle Subsequence#

- [https://leetcode.com/problems/wiggle-subsequence/](https://leetcode.com/problems/wiggle-subsequence/)

  ####	思路

  记录当前节点最大wiggle 的substring 的结尾以 大结尾的长度 big

  以小 结尾的长度small

  小结尾碰到大的 big=small+1 更新

  大结尾碰见小的 small=big+1 更新

  其余值不变

  最终返回max

```c++
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int big=1;
        int small=1;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]<nums[i-1])
            {
                
                small=big+1;
            }
            else if(nums[i]>nums[i-1])
            {
                big=small+1;
                
            }
            
        }
        
        return nums.size()>0? max(big,small):0;
    }
};
```

