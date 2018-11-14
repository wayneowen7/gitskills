71. Simplify Path

https://leetcode.com/problems/simplify-path/description/

每次碰见/就进行判断

​	如果此时，name里面是空的，就继续

​	如果name里面是..，就把nameVect 里面的东西吐出来一个nameVect.pop_back(); vector

​	如果name里面是“.”，就不做操作

​	除了上述情况，就把name里面的东西压入nameVect里面 nameVect.push_back(name);

​	

​	上述左右操作做完了之后，进行name空间清理，name.clear()



没碰见/就往name 里面塞东西



```c++
class Solution {
public:
    string simplifyPath(string path) {
       
        vector<string> nameVect;
        string name;
        path.push_back('/');
        for(int i=0;i<path.size();i++)
        {
            if(path[i]=='/')
            {
                if(name.size()==0)
                    continue;
                else if(name=="..")
                {
                    if(!nameVect.empty())
                        nameVect.pop_back();
                    
                }
                else if(name==".")
                {
                    
                }
                else
                {
                    nameVect.push_back(name);
                }
                name.clear();
                
            }
            else
            {
                name.push_back(path[i]);
            }
        }
        if(nameVect.size()==0)
            return "/";
        string res;
        for(auto subss:nameVect)
        {
            res+="/"+subss;
        }
        return res;
        
        
    }
};
```

答案：

```c++
class Solution {
public:
    string simplifyPath(string path) {
        int p1 = 0, p2 = 0;
        while (p2 < path.length()) {
            int st = p2;
            while (p2 < path.length() && path[p2] != '/') p2++;
            string tmp = path.substr(st, p2 - st);
            if (tmp == "..") {
                if (p1 != 0) {
                    while(p1-- >= 0 && path[p1] != '/');
                } 
            } else if (tmp.length() != 0 && tmp != ".") {
                path[p1++] = '/';
                for (int i = 0; i < tmp.length(); i++) {
                    path[p1++] = tmp[i];
                }
            }
            p2++;
        }
        path = path.substr(0, p1).empty() ? "/" : path.substr(0, p1);
        return path;
    }
};
```

