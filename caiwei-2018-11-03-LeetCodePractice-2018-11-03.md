#406. Queue Reconstruction by Height#

-  [https://leetcode.com/problems/queue-reconstruction-by-height/](https://leetcode.com/problems/queue-reconstruction-by-height/)

首先按照身高进行降序排序，second作为第二选择项，降序排序

之后按照身高降序进行插入，按照second第二选择项进行插入

因为第二选择项只在乎比他大的，即比他高的人，而比他高的人的相互顺序已经站定了，

所以可以迭代计算。

后续比他小的人的插入，并不会影响之前比他高的人的rank,即第二选择项。

```c++
class Solution {
public:
    vector<pair<int, int>> reconstructQueue(vector<pair<int, int>>& people) {
        sort(people.begin(),people.end(),[](pair<int,int>& a,pair<int,int>&b){
            return a.first>b.first||(a.first==b.first&&a.second<b.second);
            
        });
        //vector<pair<int,int>>&result;
        for(int i=0;i<people.size();i++)
        {
            pair<int,int> temp=people[i];
            if(temp.second!=i)
            {
                people.erase(people.begin()+i);
                people.insert(people.begin()+temp.second,temp);
            }
            
        }
        return people;
    }
};
```

