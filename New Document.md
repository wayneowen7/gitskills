#insert sort 

after sorted ,return mid index 
```
int insertSort(int array[],int left,int right)
{
    int temp;
    int j;
    for(int i=left+1;i<=right;i++)
    {
        j=i-1;
        temp=array[i];
        while(array[j]>temp&&j>=left)
            array[j+1]=array[j--];
        array[j+1]=temp;
    }
    return (left+right)>>1+left;
}
```

```
#include <iostream>
#include <vector>
using namespace std;
void QuickSort(vector<int> &iArray,int left, int right);
int main()
{
    int len,k_th;
    vector<int> result;
    cin>>len>>k_th;
    //cout<<len<<endl;
    //cout<<k_th;
    for(int i=0;i<len;i++)
    {
        int temp;
        cin>>temp;
        result.push_back(temp);
    }
    QuickSort(result,0,result.size()-1);
    cout<<result[len-k_th];
    return 0;
}
void QuickSort(vector<int> &iArray,int left, int right)
{
    if(left>right)
        return ;
    int piovt=iArray[left];
    int LeftIndex=left;
    int RightIndex=right;

    while(LeftIndex<RightIndex)
    {

        while(LeftIndex<=RightIndex)
        {

            if(iArray[RightIndex]>=piovt)

            {
                RightIndex--;
            }
            else
            {
                iArray[LeftIndex]=iArray[RightIndex];
                break;
            }
        }
        while(LeftIndex<RightIndex)
        {
            if(iArray[LeftIndex]<=piovt)
            {

                LeftIndex++;
            }
            else
            {
                iArray[RightIndex]=iArray[LeftIndex];
                RightIndex--;
                break;
            }
        }

    }
    iArray[LeftIndex]=piovt;
    QuickSort(iArray,left,LeftIndex-1);
    QuickSort(iArray,LeftIndex+1,right);

}

```