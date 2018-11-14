787. Cheapest Flights Within K Stops

https://leetcode.com/problems/cheapest-flights-within-k-stops/description/

fellmonde



```c+
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int K) {
        vector<int> results(n+1,1e9);
        results[src]=0;
        for(int i=0;i<K+1;i++)
        {
            vector<int> result(results);
            for(int j=0;j<flights.size();j++)
            {
                result[flights[j][1]]=min(result[flights[j][1]],results[flights[j][0]]+flights[j][2]);
            }
            results=result;
        }
        return results[dst]==1e9? -1:results[dst];
    }
};
```

