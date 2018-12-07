435. Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/description/

思路，按照从小到大排序

之后按照新的start 跟旧的end进行大小比较，如果start小于end，则重叠

重叠：result++，并且 需要对后续的旧的情况进行判断，度过新的end比旧的end小，则说明需要更新，把新的当作旧的，进行下一次循环，如果不是的话，则需要保留旧的，即不更新旧的数据。

```c++
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    int eraseOverlapIntervals(vector<Interval>& intervals) {
        auto compared=[](Interval &a,Interval &b){return a.start<b.start;};
        sort(intervals.begin(),intervals.end(),compared);
        int result=0,pre=0;
        for(int i=1;i<intervals.size();i++)
        {
            if(intervals[i].start<intervals[pre].end)
            {
                result++;
                if(intervals[i].end<intervals[pre].end)
                    pre=i;
            }
            else
                pre=i;
        }
        return result;
    }
};
```

