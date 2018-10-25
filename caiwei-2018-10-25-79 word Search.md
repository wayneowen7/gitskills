79 word Search

https://leetcode.com/problems/word-search/

###	思路

回溯，每次往上下左右走，

注意点：走之前，记得把当前值，因为走过，所以需要置空，这里我换成了'*' 

这样会避免走回路，避免aa 走出了aaaaaaaa



```
class Solution {
public:
    
    bool exist(vector<vector<char>>& board, string word) {
        int m=board.size();
        int n=board[0].size();
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++)
                if(helper(board,word, 0, i, j))
                    return true;
        return false;
    }
    bool helper(vector<vector<char>> &board,string &word,int start,int a,int b)
    {
        
        if(a<0||a>=board.size()||b<0||b>=board[0].size()||board[a][b]!=word[start])
            return false;
        
        if(start==word.size()-1)
            return true;
            
        bool result=false;
        vector<int> move={0,1,0,-1,0};
        char temp='*';
        temp=board[a][b];
        board[a][b]='*';
        for(int i=0;i<4;i++)
        {
            result=result||helper(board,word,start+1,a+move[i],b+move[i+1]);
        }
        board[a][b]=temp;
        return result;
        
    }
};
```

##	cs224n

笔记 4-7

rnn，语言翻译可以用五点进行优化

梯度消失梯度爆炸可以用jacob矩阵进行分析

爆炸可以用一个阈值进行限制，即反复跳跃，不让梯度爆炸

梯度消失：：

可以尝试初始化的时候不用随机初始化，用的单位矩阵，并且加上relu激活函数