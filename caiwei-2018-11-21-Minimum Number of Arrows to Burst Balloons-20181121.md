#452.Minimum Number of Arrows to Burst Balloons#

- [https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)

题目思路类似于2018-11-18

只不过那里是相同的进行删减，这里是相同的不rest++,即每次出现不重合气球时，result++

11-18是出现重合的时候，result++，因为题目要求是统计需要删减的冗余元素

```c++
class Solution {
public:
    int findMinArrowShots(vector<pair<int, int>>& points) {
        auto compared=[](pair<int, int> &a,pair<int, int> &b){return a.first<b.first||a.first==b.first&&a.second<b.second;};
        if(points.size()==0)
            return 0;
        sort(points.begin(),points.end(),compared);
        int result=1,pre=0;
        for(int i=1;i<points.size();i++)
        {
            if(points[i].first<=points[pre].second)
            {
                
                if(points[i].second<=points[pre].second)
                {
                    pre=i;
                }
            }
            else
            {
                result++;
                pre=i;
            }
            
        }
        return result;
    }
};
```

