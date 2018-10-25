### leetcode practice
- Best Time to Buy and Sell Stock with Cooldown
  https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/





  ####	思路

  dp

  buy[i]数组表示为在第i天买入，此时的收益，显然buy[0]=-prices[0]

  sell[i]数组表示为在第i天卖出，此时的收益，显然sell[0]=0

  buy数组的每一个值可以分为两种情况，即买入可以分为两种情况

  1.在两天之前是卖出，然后等一个空窗天，然后买入，即buy[i]=sell[i-2]-prices[i]

  2.间隔了很久很久，然后才买入，这种情况由于不知道怎么表示很久很久，DP的思想就是依赖前部，即buy[i]=buy[i-1]+prices[i-1]-prices[i]

  因为不买，有空窗，但是我想假设买了前一天，但是我卖掉了，然后我在今天买了，这样可以把前部依赖起来

  所以buy[i]=max(sell[i-2]-prices[i], buy[i-1]+prices[i-1]-prices[i]);

  那么sell也可以分成两个情况

  1.昨天买，今天卖，即sell[i]=buy[i-1]+prices[i]

  2.前几天买，今天卖，这个几天还是不好表示，用前部依赖 sell[i]=sell[i-1]-prices[i-1]+prices[i]

  因为我留着不卖，但是可以假装每天都卖，然后再买，收益还是按照第一天来算的，即买卖相抵

  所以sell[i]=max(buy[i-1]+prices[i], sell[i-1]-prices[i-1]+prices[i]);


```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        if(n==0)
            return 0;
        vector<int> sell(n,0);
        vector<int> buy(n,0);
        buy[0]=-prices[0];
        int res=0;
        sell[0]=0;
        for(int i=1;i<n;i++)
        {
            sell[i]=max(buy[i-1]+prices[i],sell[i-1]-prices[i-1]+prices[i]);
            res=max(res,sell[i]);
            if(i==1)
                buy[1]=buy[0]+prices[0]-prices[1];
            buy[i]=max(sell[i-2]-prices[i],buy[i-1]+prices[i-1]-prices[i]);
        }
        return res;
    }
};
```

