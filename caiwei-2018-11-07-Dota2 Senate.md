- 649.Dota2 Senate
  https://leetcode.com/problems/dota2-senate/

  ###	思路

  比较靠前的能ban掉后面的位置

  那就放两个队列，存放的是每个人的index，

  每次从队列各突出一个，比较index大小，小的index就保留到下一次（存入index+n，用以表示第二次循环的index，再保留的话就是index+n+n，也是index  新的 +n）


```c++
class Solution {
public:
    string predictPartyVictory(string senate) {
        queue<int> q1,q2;
        int n=senate.size();
        for(int i=0;i<n;i++)
            senate[i]=='R'? q1.push(i):q2.push(i);
        
        while(!q1.empty()&&!q2.empty())
        {
            int radient=q1.front(),dire=q2.front();
            q1.pop(),q2.pop();
            radient<dire? q1.push(radient+n):q2.push(dire+n);
            
        }
        return q1.size()>q2.size()? "Radiant":"Dire";
        
    }
};

```

