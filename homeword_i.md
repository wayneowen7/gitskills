k_th max number o(log n)

1.获取一个随机数，把随机数当做索引pivot，对前后进行left,right 分割

2.对result 进行遍历，每个值，如果小于随机数的索引所对应的值，放在left，否则（等于或者大于）放在right，遍历的flag==随机数时跳过，即随机数所对应的值不考虑，留给后面考虑

3.如果left.size()==k-1 则说明随机索引指向的值就是我们的目标值return result[pivot]即可

4.如果left.size()> k-1 k 为指定排名的数字，则递归 left 当做result,k继续当成k

5.如果left.size()<k-1 则说明 我们要找的数字在right,则递归 right 当做result，k=k-left.size()-1(-1是因为pivot也不是目标值，所以还要减去一个pivot指向的那个数字)
```
#include<iostream>
#include<algorithm>
#include <bits/stdc++.h>
using namespace std;
int helper(vector<int> &result,int k);


int main()
{
    int len,k_th;
    vector<int> result;
    cin>>len>>k_th;
    int temp;
    for(int i=0;i<len;i++)
    {
        int temp;
        scanf("%d",temp);
        result.push_back(temp);
        //cout<<result[i]<<endl;
    }

    cout<<helper(result,len-k_th+1);
    //cout<<res;
    return 0;

}
int helper(vector<int> &result,int k)
{

    vector<int> left;
    vector<int> right;
    srand(time(NULL));

    int temp_pivot=rand()%result.size();
    int j=0;
    for(int i=0;i<result.size();i++)
    {
        if(i==temp_pivot)
            continue;
        if(result[i]<result[temp_pivot])
            left.push_back(result[i]);
        else
            right.push_back(result[i]);
        j+=i;
    }
    if(left.size()==k-1)
        return result[temp_pivot];
    else if(left.size()>k-1)
        return helper(left,k);
    else
        return helper(right,k-left.size()-1);

}
```

最近点距离

1.先将输入的点按照X进行排序

2.以个数的中位数的索引，作为分界点，分为左团跟右团

3.分别计算左团的最短 点距离，右团最短 点距离（递归）

4.比较两团各自最短距离，获取综合最短距离

5.从分界点两侧，向左走最短距离，寻找点，把在最短距离之内点的存进sub array  output[] ,再向右走最短距离，把路程上的点存进sub array

6.将sub array 按照y的升序排序

7.对sub array进行双循环，找到每个点 的后面 dis_min距离（按照y计算）的点，计算距离，如果距离小于dis_min,更新dis_min；

8.返回dis_min
```
#include<cstdio>

#include<algorithm>

#include<cmath>

using namespace std;

double MAX=1e10;
int a,b;
struct Node{
    double x,y;
};
Node input[100000],output[100000];
bool cmpx(Node a ,Node b)
{
    return a.x<b.x;
}
bool cmpy(Node a,Node b)
{
    return a.y<b.y;
}
double min_value(double a,double b)
{
    return a<b? a:b;
}
double dis(Node a,Node b)
{
    return sqrt(pow(a.x-b.x,2)+pow(a.y-b.y,2));
}
double helper(int left,int right);
int main()
{
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++)
    {
        scanf("%lf %lf",&input[i].x,&input[i].y);
    }
    sort(input,input+n,cmpx);

    double result=helper(0,n);
    printf("%.2lf",result);
}
double helper(int left,int right)
{
    int mid,i,j,sub_array=0;
    double min_dis;
    if(left==right)
    {
        return MAX;
    }

    mid=(left+right)/2;
    min_dis=min_value(helper(left,mid),helper(mid+1,right));
    //printf("\n*****%lf *****\n",min_dis);
    int count=5;
    for(int i=mid;i>=left&&input[mid].x-input[i].x<min_dis;i--)
    {
        output[sub_array++]=input[i];
        count--;
    }
    if(count >5)
        count++;
    for(int i=mid+1;i<right&&input[i].x-input[mid].x<min_dis;i++)
    {

        output[sub_array++]=input[i];
        count++;
    }
    if(count <5)
        count--;
    sort(output,output+sub_array,cmpy);
    for(int i=0;i<sub_array;i++)
        for(int j=i+1;j<sub_array&&output[j].y-output[i].y<min_dis;j++)
        {
            if(min_dis>dis(output[j],output[i]))
                min_dis=dis(output[j],output[i]);
        }
    return min_dis;
}

```
