---
title: n个骰子和为S的次数以及相应的概率
date: 2016-05-09 17:10:41
tags:
---

> //把n个骰子扔地上，所有骰子朝上一面的点数之和为 S。输入n,打印出S中所有可能出现的值的概率。
> //动态规划.找到最优子结构。采用备忘录的方法避免重复计算。
> //最优子结构：f(n,s)表示n个骰子点数和为S的种类，N表示骰子个数，S表示N个骰子的点数和
> //F(n,s)=F(n-1,s-1)+F(n-1,s-2)+F(n-1,s-3)+F(n-1,s-4)+F(n-1,s-5)+F(n-1,s-6)
> n>0,n<=S<=6*n //      =0  n>S  or  S>6*k

    #include <iostream>
    #include<cmath>
    using namespace std;
    const int FACE_NUM=6;//骰子的面数
    //函数功能：N个骰子的向上一面的和
    //函数参数：骰子数目
    
    void PrintSumProbabilityOfDices(int n){
        if(n<=0)
            return;
        int *pSum=new int[n*FACE_NUM+1];//和的种类
        double total=pow(6.0,n);//和的所有可能性
        int sizee=n*FACE_NUM;
        int i,j,k;
        //初始化
        pSum[0]=0;//没有骰子
        for(i=1;i<=FACE_NUM;i++)
            pSum[i]=1;//只有一个骰子,和的可能性为1~6，只可能出现一次
        for(;i<=sizee;i++)
            pSum[i]=0;//数组初始化0
        for(i=2;i<=n;i++){//骰子数目从2~n
            for(j=i*FACE_NUM;j>=i;j--){//i个骰子和的范围是i~i*FACE_NUM，j代表的是可能的和的种类
                pSum[j]=0;//每次要清零
                for(k=1;k<=6 && j>=k;k++){//这个就是F(n,s)=F(n-1,s-1)+F(n-1,s-2)+F(n-1,s-3)+F(n-1,s-4)+F(n-1,s-5)+F(n-1,s-6)
                    pSum[j]+=pSum[j-k];
                }
            }
            //不可能的情况
            for(j=i-1;j>=0;j--)
                pSum[j]=0;
        }
       //打印结果
       for(i=0;i<=sizee;i++){
            cout<<"sum= "<<i<<", p= "<<pSum[i]/total<<endl;
       }
    }
    int main()
    {
        PrintSumProbabilityOfDices(3);
        return 0;
    }

