385 Mini Parser

https://leetcode.com/problems/mini-parser/

####	思路

每次碰见数字，就用find_if_not 直接把数字部分的索引 t,t2 收尾指针找出来

然后取stack里面的top,将该字符串string(t,t2)加入stack的top里面

碰见[ 的话，就往stack里面压入新的空的nestedinteger

碰见]的话，就讲顶层的top取出，加入新的顶层的top，实现嵌套

```c++

  class Solution {
  public:
  NestedInteger deserialize(string s) {
      function<bool(char)> isnumber=[](char c){return c=='-'||isdigit(c);};
      stack<NestedInteger> stk;
      stk.push(NestedInteger());
      for(auto t=s.begin();t!=s.end();)
      {
          char &c=(*t);
          if(isnumber(c))
          {
              auto t2=find_if_not(t,s.end(),isnumber);
              int tempt=stoi(string(t,t2));
              stk.top().add(NestedInteger(tempt));
              t=t2;
          }
          else
          {
              if(c=='[')
              {
                  stk.push(NestedInteger());
              }
              else if(c==']')
              {
                  NestedInteger tp=stk.top();
                  stk.pop();
                  stk.top().add(tp);
              }
              t++;
          }
      }
      return stk.top().getList().front();
  }
  };
```

