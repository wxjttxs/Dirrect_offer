---
title: 找到第n个ugly number
date: 2016-05-06 16:15:23
tags:
---
//因子只包含2,3,5的数叫做丑数,
//找到第n个丑数，1是第一个

    #include <iostream>
    
    using namespace std;
    //***********************第一种方法***********************
    //bool IsUglyNumber(int n){
    //    while(n%2==0)
    //        n/=2;
    //    while(n%3==0)
    //        n/=3;
    //    while(n%5==0)
    //        n/=5;
    //    return (n==1)?true:false;
    //}
    //int GetUglyNumber(int index){
    //    if(index<0)
    //        return 0;
    //    int number=0;
    //    int uglyFound=0;
    //    while(uglyFound<index){
    //        ++number;
    //        if(IsUglyNumber(number))
    //            ++uglyFound;
    //    }
    //    return number;
    //
    //}
    //**********************第二种方法***********************
    //保存已经排好序的丑数
    int Min(int n1,int n2,int n3){
        int mint=(n1<n2)?n1:n2;
        mint=(mint<n3)?mint:n3;
        return mint;
    }
    int GetUglyNumber(int index){
        if(index<0)
            return 0;
        int *pUglyNumbers=new int[index];
        pUglyNumbers[0]=1;//保存已经排好序的丑数
        int nextUglyIndex=1;//第i个丑数的位置
        int *pMultiplu2=pUglyNumbers;
        int *pMultiplu3=pUglyNumbers;
        int *pMultiplu5=pUglyNumbers;
        while(nextUglyIndex<index){
            int mintt=Min(*pMultiplu2*2,*pMultiplu3*3,*pMultiplu5*5);//取比当前最大丑数大的最小值
            pUglyNumbers[nextUglyIndex]=mintt;
            while(*pMultiplu2*2<=pUglyNumbers[nextUglyIndex])
                ++pMultiplu2;//这个位置之前的数乘2都比当前丑数的最大值要小;退出时候均比当前最大丑数大的最小值
            while(*pMultiplu3*3<=pUglyNumbers[nextUglyIndex])
                ++pMultiplu3;
            while(*pMultiplu5*5<=pUglyNumbers[nextUglyIndex])
                ++pMultiplu5;
            ++nextUglyIndex;
    
        }
        int ugly=pUglyNumbers[nextUglyIndex-1];
        delete[] pUglyNumbers;
        return ugly;
    
    }
    int main()
    {
        cout <<GetUglyNumber(4) << endl;
        return 0;
    }

