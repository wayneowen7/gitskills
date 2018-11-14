#714. Best Time to Buy and Sell Stock with Transaction Fee#

- [https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```c++
class Solution {
public:
    int maxProfit(vector<int>& p, int fee) {
        int n = p.size();
        if (n < 2) return 0;
        vector<int> buy(n, 0), sell(n, 0);
        buy[0]=0-p[0];
        sell[0]=0;
        for (int i = 1; i < n; i++) {
            sell[i]=max(sell[i-1],buy[i-1]+p[i]-fee);
            buy[i]=max(buy[i-1],sell[i-1]-p[i]);
            
        }

        return sell[n - 1];
    }
};
```

