---
title: post打印1~n的最大
date: 2016-04-22 09:28:32
tags:
---
##字符串表示大树问题
```
#include <iostream>
#include<string>
#include<memory.h>
using namespace std;
//判断什么到达最大的n位数是重中之重,第一位进1时候一定达到最大位

//bool Increment(char* number){
//    int n=strlen(number);
//    bool isOverflow=false;//最低位是否进位
//    int nTakeOver=0;//每一位上的进位
//    for(int i=n-1;i>=0;i--){
//        int ithNum=number[i]-'0'+nTakeOver;//第i位上的数字,这个地方是“-”，由字符转换成数字是“-”，而由数字转换成字符是“+”
//        if(i==n-1)//最高位那么就加1
//            ithNum++;
//        if(ithNum>=10){//第i位有进位
//                if(i==0)
//                    isOverflow=true;
//                else{
//                    ithNum-=10;
//                    nTakeOver=1;
//                    number[i]='0'+ithNum;
//                }
//        }
//        else{
//            number[i]='0'+ithNum;//没有进位，还没到最大
//            break;
//        }
//    }
//    return isOverflow;
//}
//
//void PrintNumber(char* number){
//    bool isBegin0=true;//从第一个不是0开头的数字开始打印
//    int n=strlen(number);
//    for(int i=0;i<n;i++){
//        if(isBegin0 && number[i]!='0')//不是以0开头
//            isBegin0=false;
//        if(!isBegin0)//开头不是0就输出
//            cout<<number[i];
//
//
//    }
//    cout<<" ";
//
//}
//void Print1ToMaxofNdigits(int n){
//    if(n<=0)
//        return;
//    char* number=new char[n+1];
//    memset(number,'0',n);
//    number[n]='\0';
//    while(!Increment(number))
//        PrintNumber(number);
//    delete []number;
//}
//int main()
//{
//    Print1ToMaxofNdigits(2);
//    return 0;
//}

void PrintNumber(char* number){
    bool isBegin0=true;
    int n=strlen(number);
    for(int i=0;i<n;i++){
        if(isBegin0&&number[i]!='0')
            isBegin0=false;
        if(!isBegin0)
            cout<<number[i];
    }
    cout<<" ";

}
void Print1ToMaxofNdigitsRecursively(char* number,int n, int index){//把每一位都值成0~9
    if(index==n-1){
        PrintNumber(number);
        return;
    }
    for(int i=0;i<10;i++){
        number[index+1]=i+'0';
        Print1ToMaxofNdigitsRecursively(number,n,index+1);//递归打印下一位
    }
}
void Print1ToMaxofNdigits(int n){
    char* number=new char(n+1);
    number[n]='\0';

    if(n<=0)
        return;
    for(int i=0;i<10;i++){
        number[0]=i+'0';
        Print1ToMaxofNdigitsRecursively(number,n,0);//从第一位开始打印
    }
}
int main(){
    Print1ToMaxofNdigits(-1);
    return 0;
}


```