### 870. Advantage Shuffle
- https://leetcode.com/problems/advantage-shuffle/
- 田忌赛马
- 每次将比B中对应数字大的最小数字拿出来，如果找不到，就找最小的
- 这个A的最大最小就用map实现,把A中的数字当做key，重复次数当做value
- 知识点：



```c++
- map<int,int>::iterator it;
- it=m.upper_bound(B[i]);
  int index=  it!=m.end()?it->first:m.begin()->first;
    if(--m[index]==0)
        m.erase(index);
```





```c++
class Solution {
public:
    vector<int> advantageCount(vector<int>& A, vector<int>& B) {
        map<int,int> m;
        for(int i:A)
            m[i]++;
        vector<int> result;
        map<int,int>::iterator it;
        for(int i=0;i<B.size();i++)
        {
            it=m.upper_bound(B[i]);
            int index=  it!=m.end()?it->first:m.begin()->first;
            if(--m[index]==0)
                m.erase(index);
            
            result.push_back(index);
        }
        return result;
    }
};
```

