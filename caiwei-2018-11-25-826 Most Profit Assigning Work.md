826. Most Profit Assigning Work

https://leetcode.com/problems/most-profit-assigning-work/



做difficulty 跟profit 的 pair 之后进行排序job，并且把工人也排序

按照每个工人，从job,中寻找符合难度的，并且进行max profit存储，之后选中最大的收益

由于工人的能力是升序，所以之前遍历的job不需要遍历了，max profilt已经得到了，再这个max proflt的基础上继续遍历job,

```c++
class Solution {
public:
    int maxProfitAssignment(vector<int>& difficulty, vector<int>& profit, vector<int>& worker) {
        vector<pair<int,int>> job;
        for(int i=0;i<profit.size();i++)
            job.push_back(make_pair(difficulty[i],profit[i]));
        sort(job.begin(),job.end()),sort(worker.begin(),worker.end());
        int i=0,max_out=0,N=worker.size(),result=0;
        for(int & limit:worker)
        {
            while(i<N&&limit>=job[i].first)
                max_out=max(max_out,job[i++].second);
            
            result+=max_out;
            
        }
        return result;
    }
};
```

甚至更快

首先是进行对每个任务，只保存对应的最大收益，

之后索引就是任务难度，指向的内容就是其最大收益，由于难度向下兼容，所以收益也向下兼容，用一个循环加一个表达式record[i]=max(record[i],record[i-1]);可以实现最大收益的向下兼容。

最后按照工人的能力，寻找对应的难度索引，因为可能工人能力太大，没有那么大的任务难度，所以当能力大于最大难度的时候，就选择最大难度的任务。

正常的话，工人能力就应当匹配对应的任务难度。

```c++
class Solution {
public:
    int maxProfitAssignment(vector<int>& difficulty, vector<int>& profit, vector<int>& worker) {
        int result=0,max_ability=0;
        for(int i=0;i<difficulty.size();i++)
            max_ability=max(max_ability,difficulty[i]);
        
        
        vector<int> record(max_ability+1,0);
        for(int i=0;i<difficulty.size();i++)
        {
            record[difficulty[i]]=max(profit[i],record[difficulty[i]]);
        }
        for(int i=1;i<record.size();i++)
            record[i]=max(record[i],record[i-1]);
        for(int &a:worker)
        {
            if(a>max_ability)
                result+=record[max_ability];
            else
                result+=record[a];
        }
        return result;
        /*vector<int> dp(100001,0);
        for (int i = 0; i < difficulty.size(); i++) {
            dp[difficulty[i]] = max(dp[difficulty[i]], profit[i]);
        }
        for (int i = 0; i < dp.size(); i++) {
            if (i > 0) {
                dp[i] = max(dp[i - 1], dp[i]);
            }
        }
        int sum = 0;
        for (int i : worker) {
            sum += dp[i];
        }
        return sum;*/
    }
};
```

