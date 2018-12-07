#881.Boats to Save People#

- [https://leetcode.com/problems/boats-to-save-people/](https://leetcode.com/problems/boats-to-save-people/)

排序后进行前后双指针搜索，从小到大

如果两个人不能放进去，则只能放大的，即第一个指针不变，后面一个指针减一

如果两个人都能放进去，则两个指针都变 小的加一，大的减一

```c++
class Solution {
public:
    int numRescueBoats(vector<int>& people, int limit) {
        sort(people.begin(),people.end());
        int nums=0;
        for(int i=0,j=people.size()-1;i<=j;j--,nums++)
            if((people[i]+people[j])<=limit)
                i++;
        return nums;
    }
};
```

