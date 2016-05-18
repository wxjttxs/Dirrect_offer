---
title: 排序给定人数的年龄o(n)
date: 2016-04-21 21:01:26
tags:
---
```
//实现上万个人的年龄的排序
#include<iostream>
using namespace std;
void ageSort(int *a,int n){
    if(a==NULL||n<=0)
        return;
    const  int Maxage=99;
    int countAge[Maxage+1];//0~99,一共100个数
    for(int i=0;i<Maxage+1;i++){//每种年龄出现的次数
        countAge[i]=0;
    }
    for(int i=0;i<n;i++){
        int age=a[i];
        if(age<0||age>Maxage)
            return;//输入不合法
        countAge[age]++;
    }
    int index=0;//排好序的下标
   for(int i=0;i<Maxage;i++){
     for(int j=0;j<countAge[i];j++){//,来控制每个年龄出现的次数
        a[index++]=i;
     }
   }
}
int main(){
    int a[9]={3,4,5,6,7,5,4,3,2};
    ageSort(a,9);
    for(int i=0;i<9;i++){
        cout<<a[i]<<" ";
    }
    return 0;
}
```