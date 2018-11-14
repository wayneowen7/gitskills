### Lemonade Change
- https://leetcode.com/problems/lemonade-change/

```c++
static int x = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    bool lemonadeChange(vector<int>& bills) {
        std::map<int, int> mp;
        int n=bills.size();
        int five=0;
        int ten=0;
        for(int i: bills)
        {
            if(i==5) five++;
            else if(i==10) five--,ten++;
            else if(ten>0) ten--,five--;
            else
                five-=3;
            if(five<0)
                return false;
        }
        return true;
    }
};
```

