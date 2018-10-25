#213. House Robber II#
- [https://leetcode.com/problems/house-robber-ii/](https://leetcode.com/problems/house-robber-ii/)

  ####	思路

  做过第一个版本的打家劫舍，所以这里就是多了一个环，那么就把0-->n-2 1-->n-1这两种情况比较一下，得出最大的结果就行

  那么小问题就是上个版本的打家劫舍，

  当前打劫的条件是上一次不打，所以

  dp[i]=max(dp[i-2]+nums[i],dp[i-1])

  成了

  不使用数组的方法

  用a 存储i-2，用b 存储i-1，但是本次更新到b，

  b=max(a+nums[i],b)

  这里需要把尾部的b保存，因为在下一次循环里面，这个b就是i-2，所以

  b要变成下一次的a

  ​	    int temp=b;
  ​            b=max(a+nums[i],b);
  ​            a=temp;

  ```c++
  class Solution {
  public:
      int rob(vector<int>& nums) {
          if(nums.size()==0)
              return 0;
          if(nums.size()==1)
              return nums[0];
          if(nums.size()==2)
              return max(nums[0],nums[1]);
          return max(helper(nums,0),helper(nums,1));
      }
      int helper(vector<int> &nums,int start)
      {
          int n=nums.size();
          int a=nums[start];
          int b=max(nums[start],nums[start+1]);
          for(int i=start+2;i<=n-2+start;i++)
          {
              int temp=b;
              b=max(a+nums[i],b);
              a=temp;
          }
          return b;
      }
  };
  
  ```
