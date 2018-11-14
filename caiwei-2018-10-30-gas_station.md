#134.Gas Station#

- [https://leetcode.com/problems/gas-station/](https://leetcode.com/problems/gas-station/)

  ####	思路

  1.站点 A如果不能到B，那么AB中间的点也不能到B，

  证明

  diff[i]=gas[i]=cost[i]

  diff[i]+diff[i+1]+diff[i+2]+......diff[k]<0

  因为从i,走到k，才没油了，所以

  可以走到k-1

  即：

  diff[i]+diff[i+1]+diff[i+2]+......diff[k-1]>0

  极限思考

  k-1可以走，

  k-2可以走

  .

  .

  .i+1可以走

  i可以走

  说明diff[i]>0

  那么diff[i+1]+diff[i+2]+......diff[k]<0肯定成立，

  因为diff[i]+diff[i+1]+diff[i+2]+......diff[k]<0 其中diff[i]>0

  所以中间的点都不能走到加油站

  2.总油数大于总油耗数量，则必定有解

  a. 最开始，站点0是始发站，假设车开出站点p后，油箱空了，假设sum1 = diff[0] +diff[1] + ... + diff[p]，可知sum1 < 0；

  b. 根据上面的论述，我们将p+1作为始发站，开出q站后，油箱又空了，设sum2 = diff[p+1] +diff[p+2] + ... + diff[q]，可知sum2 < 0。

  c. 将q+1作为始发站，假设一直开到了未循环的最末站，油箱没见底儿，设sum3 = diff[q+1] +diff[q+2] + ... + diff[size-1]，可知sum3 >= 0。

  那么想要开回q点，

  首先得开回p点，即必须sum3+sum1>0

  然后再sum3+sum1+sum2>0

  因为sum2<0,所以由sum3+sum1+sum2>0，必定可以得出sum3+sum1>0

  故只需要证明sum3+sum1+sum2>0即可

  所以需要一个total记录所有的diff，最后加起来如果>0则必定有解

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int tank=0;
        int total=0;
        int start=0;
        for(int i=0;i<gas.size();i++)
        {
            if((tank=tank+gas[i]-cost[i])<0)
               {
                   start=i+1;
                   total+=tank;
                   tank=0;
               }
        }
        return total+tank<0?-1:start;
    }
};
```

