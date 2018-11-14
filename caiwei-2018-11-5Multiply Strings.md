43. Multiply Strings

https://leetcode.com/problems/multiply-strings/description/

按照计算的累加性质，

```
int tempt=(num1[i]-'0')*(num2[j]-'0');
int a=i+j;
int b=i+j+1;
tempt+=result[b];
result[b]=tempt%10;
result[a]+=tempt/10;
```

知识点：vector<char>  answer转 string

string(answer.begin(),answer.end())

```c++
class Solution {
public:
    string multiply(string num1, string num2) {
        int m=num1.size();
        int n=num2.size();
        vector<int> result(m+n,0);
        for(int i=m-1;i>=0;i--)
            for(int j=n-1;j>=0;j--)
            {
                int tempt=(num1[i]-'0')*(num2[j]-'0');
                int a=i+j;
                int b=i+j+1;
                tempt+=result[b];
                result[b]=tempt%10;
                result[a]+=tempt/10;
            }
        
        vector<char> answer;
        for(int i=0;i<m+n;i++)
        {
            if(result[i]!=0||answer.size()!=0)
                answer.push_back(result[i]+'0');
        }
        if(answer.size()==0)
            return "0";
        return string(answer.begin(),answer.end());
    }
};
```

