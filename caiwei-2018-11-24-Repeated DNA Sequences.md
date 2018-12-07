187. Repeated DNA Sequences

https://leetcode.com/problems/repeated-dna-sequences/description/

遍历，i,i+9，用set放进去，重复的就放进set,然后遍历set，做出一个result

知识点：

1.遍历set，

做迭代器

set<string>::iterator it

for(it=s.begin();it<begin.end();i++)

​	result.push_back(*it);



2.substr

两个参数

s.substr(开始索引点，子串长度)

```c++
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        set<string> set1;
        set<string> set2;
        vector<string> result;
        if(s.size()<10)
            return result;
        for(int i=0;i<=s.size()-10;i++)
        {
            string tempt=s.substr(i,10);
            if(set1.count(tempt))
            {
                set2.insert(tempt);
            }
            else
            {
                set1.insert(tempt);
            }
        }
        set<string>::iterator it;
        for( it=set2.begin();it!=set2.end();it++)
            result.push_back(*it);
        return result;
               }
};
```

抄答案：

A is 0101, C is 0103, G is 0107, T is 0124. 

因为二进制不同，就直接将每次字符弄成ASCII码转成数字，取10位当成map的key，如果重复说明字符串重复

怎么转换

每次取9位()，压入新的一位，拼成10位，做成index

start=start<<3 & 0x3FFFFFFF|s[end]&7

<<3是为了将溢出的头一个数字吐出去（做成33位，&3FFFFFFF之后就是30位，低3位待赋值，全为1，即为111）

之后 |s[end]&7 是将新的三位进行或操作，与111或操作即为新的赋值，组成新的30位数字。

知识点：

if(m[start=start<<3 & 0x3FFFFFFF|s[end]&7]++==1)

start=startXXXX一大堆操作，返回的是 start本身的值，所以能作为m的索引 

```c++
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        
        unordered_map<int,int> m;
        vector<string> result;
        int start=0,end=0;
        while(end<9)
        {
            start=start<<3|s[end++]&7;
        }
        for(;end<s.size();end++)
        {
            if(m[start=start<<3 & 0x3FFFFFFF|s[end]&7]++==1)
                result.push_back(s.substr(end-9,10));
        }
        
        return result;
        }
};
```

