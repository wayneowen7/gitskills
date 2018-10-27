322.Coin Change

https://leetcode.com/problems/coin-change/

####	递归

遍历所有 1 2 5  11

11= 10+1

11=9+1

11=5+1

取最小的

普通递归会超时，需要加个备忘录

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        /*if(find(coins.begin(),coins.end(),1)==coins.end())
            return -1;*/
        vector<int> count(amount,0);
        return helper(coins,amount,count);
    }
    int helper(vector<int>& coins, int amount,vector<int> &count)
    {
        if(amount<0)
            return -1;
        if(amount==0)
            return 0;
        if(count[amount-1]!=0)
            return count[amount-1];
        int n=coins.size();
        int min_cmp=0x7fffffff;
        
        for(int i=0;i<n;i++)
        {
            int res=helper(coins,amount-coins[i],count);
            if(res>=0&&res<min_cmp)
                min_cmp=res+1;
            
                
        }
        
        count[amount-1]=min_cmp==0x7fffffff? -1:min_cmp;
        return count[amount-1];
                    
    }
};
```

####	DP

这里的DP从底向上，计算dp[1]=1

dp[2]=1/2=1

dp[3]=3/2=2

.....

从1-amount遍历

每次就是从dp[amount - coins[j]] +1 里面找个最小的方案

初始化，自然的就是dp[1],dp[2],dp[5] 都是1

不过这里初始其实是，将全部都置为0，

dp[0]=0 这就是初始化

即相等的数字，因为后面都+1，dp[5]=dp[5-5]+1=d[0]+1=1

注意点：最小值的比较，因为又要最小值，但是特殊情况-1，会影响最小值的判断，所以一开始设置为0x7fffffff

因为这里用的0x7fffffff，所以可能会有不一样的情况，(对程序之外的环境太过于依赖，例如操作系统等)

所以可以用一个高级条件判断

假设我们就是要找最小值，那么就是min(min_cmp,dp)

但是min_cmp=-1（将特殊情况直接带入初值，即当不更新时，就是意外情况，直接返回-1）

所以在 更新时，我们就需要放弃-1.即

min_cmp=   min_cmp==-1? tempt:(tempt<min_cmp? tempt:min_cmp);

​			异常情况，进行直接从-1跨入正值		

​								正常情况，判断是否比最小值小，更新最小值

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if(amount<0)
            return -1;
        
        vector<int> dp(amount+1,0);
        for(int i=1;i<=amount;i++)
        {
            int min_cmp=0x7fffffff;
            for(int j=0;j<coins.size();j++)
            {
                if(i>=coins[j]&&dp[i-coins[j]]!=-1)
                {
                    int tempt=dp[i-coins[j]]+1;
                    min_cmp=min(min_cmp,tempt);
                }
            }
            
            dp[i]=min_cmp==0x7fffffff? -1:min_cmp;
        }
        return dp[amount];
    }
};
```





```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if(amount<0)
            return -1;
        
        vector<int> dp(amount+1,0);
        for(int i=1;i<=amount;i++)
        {
            int min_cmp=-1;
            for(int j=0;j<coins.size();j++)
            {
                if(i>=coins[j]&&dp[i-coins[j]]!=-1)
                {
                    int tempt=dp[i-coins[j]]+1;
                    min_cmp=min_cmp<0?tempt:(tempt<min_cmp?tempt:min_cmp);
                    
                }
            }
            
            dp[i]=min_cmp;
        }
        return dp[amount];
    }
};
```

##	cs224n

assignment1

def softmax(x)

sigmoid derivative==> =σ(x)×(1–σ(x))

softmax derivative==>∂CE∂θi=Si–yi

![1540659473865](C:\Users\caiwei\AppData\Roaming\Typora\typora-user-images\1540659473865.png)

def sigmoid(x)

def sigmoid_grad(s)

def gradcheck_naive(f,x)

def forward_backward_prop(data,labels,params,dimensions)

