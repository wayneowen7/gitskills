416. Partition Equal Subset Sum

https://leetcode.com/problems/partition-equal-subset-sum/

用dp，是否能组成索引值所对应的数，

dp[5]说明nums里面能加起来等于5，

那么最终只要让nums,能加起来组成sum/2,就自然是 砍成一半的两个相等数字

for(int num:nums)
​            for(int j=target;j>=num;j--)
​                dp[j]=dp[j]||dp[j-num];

dp[j-num] 就是实现的条件，因为dp[0]=true，那么只要有num数字，dp[num]就是true，

dp[num1+num2+num3+......=target]=true，这样nums1,2,3+......=target,答案就得到了

```c++
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int sum=accumulate(nums.begin(),nums.end(),0);
        if(sum%2!=0)
            return false;
        int target=sum/2;
        vector<bool> dp(target+1,false);
        dp[0]=true;
        for(int num:nums)
            for(int j=target;j>=num;j--)
                dp[j]=dp[j]||dp[j-num];
        return dp[target];
    }
};
```

