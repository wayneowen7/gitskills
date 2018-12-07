201. Bitwise AND of Numbers Range

https://leetcode.com/problems/bitwise-and-of-numbers-range/

按位与范围之内的数字

那么只有相邻数之间与一下，肯定就最后一位是0，只要范围不是只有一个属，只要大于等于两个数

那么就转换成子问题 抛去最后一位的范围之内数字之间的相与

借鉴：

```c++

class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
        return n>m? rangeBitwiseAnd(m>>=1,n>>=1)<<1:m;
    }
};
```

这里的count 表示有最终的结果，屁股后面有多少个0,因为我们知道肯定是后面全0的情况。

```c++
class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
        int count=0;
        while(m!=n)
        {
            m/=2;
            n/=2;
            count++;
        }
        return m<<count;
    }
};
```

