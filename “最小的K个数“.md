---
title: 最小的K个数
date: 2016-05-02 22:24:15
tags:
---

    #include <iostream>
    #include<algorithm>
    #include<set>
    #include<vector>
    
    using namespace std;
    //0(n)时间找到最小的K个数，而且这K个数是排好序的，但是会修改原始数组
    //借鉴快排的划分
    
    //int Partition(int *a, int start ,int ent){
    //    if(a==NULL||start<0||ent<0)
    //        throw new exception();
    //    int temp=a[ent];//最后一个值作为基准
    //    int i=start-1;
    //    for(int j=start;j<ent;j++){
    //        if(a[j]<=temp){
    //            i++;
    //            swap(a[i],a[j]);
    //        }
    //    }
    //    swap(a[i+1],a[ent]);
    //    return i+1;
    //}
    //void GetLeastNumber(int *input,int n,int k){
    //   // int output[k]={0};
    //    if(input==NULL||n<=0||k<=0||k>n)
    //        return;
    //    int start=0;
    //    int endt=n-1;
    //    int index=Partition(input,start,endt);
    //    while(index!=k-1){
    //        if(index<k-1){
    //            start=index+1;
    //           index=Partition(input,start,endt);
    //        }
    //        else{
    //            endt=index-1;
    //            index=Partition(input,start,endt);
    //        }
    //    }
    //    for(int i=0;i<=index;i++){
    //
    //        cout<<input[i]<<" ";
    //    }
    //    cout<<endl;
    //
    //}
    //int main()
    //{
    //    int a[]={4,5,1,6,2,7,3,8};
    //
    //    GetLeastNumber(a,8,6);
    //    return 0;
    //}
    
    //****************方法二********************************
    //上面的时间很快，但是会改变原始数据
    //所以用一个k大的容器 来装k个最小值，容器没有满那就直接插入。如果满了，那就做三件事：1.找到容器中最大值；2.删除最大值；3.插入新的数据
    //找到最大值，最快的是最大堆，基于红黑树结构实现的set and multiset
    typedef multiset<int,greater<int> > intSet;//greater作用实现降序排列
    typedef multiset<int ,greater<int> >::iterator setItertor;
    void GetLeastNumbers(const vector<int>& data, intSet& leastNumber,int k){
        leastNumber.clear();
        if(k<1||data.size()<k)
            return;
        vector<int>::const_iterator iter=data.begin();
        for(;iter!=data.end();++iter){
    
            if(leastNumber.size()<k)
                leastNumber.insert(*iter);
            else{
                setItertor iterGreatest=leastNumber.begin();
                if(*iter<*(leastNumber.begin())){
                    leastNumber.erase(iterGreatest);
                    leastNumber.insert(*iter);
                }
            }
        }
    }
    int main(){
        int a[8]={4,5,1,6,2,7,3,8};
    
        vector<int> data(a,a+8);
        intSet leastNumber;
        GetLeastNumbers(data,leastNumber,8);
        cout<<"the actual output numbers are:"<<endl;
        for(setItertor iter=leastNumber.begin();iter!=leastNumber.end();iter++)
            cout<<*iter<<" ";
        cout<<endl;
        return 0;
    }

