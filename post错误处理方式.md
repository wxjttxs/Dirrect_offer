---
title: post错误处理方式
date: 2016-04-21 22:22:15
tags:
---
##三种处理错误异常的方式
                       
    返回值     优:和系统API一致;     
              缺：不能方便的使用结算结果;
    全局变量   优：能够方便的使用结算结果;   
              缺：用户可能会检查全局变量;                                                                         
    异常      优：可以为不同的出错原因定义不同异常类型，逻辑清晰明了；     
              缺：有些语言（C）不支持异常，抛出异常可能对性能有负面影响
##实现阶乘陷阱多多
```
#include <iostream>
using namespace std;
//以为pow(x,n)很简单，但是好多陷阱,比如指数为负，底数为0，所以需要错误处理(全局变量)
//基本而且完整的代码
bool flag_error=false;
//double PowerUnsignedExp(double base,unsigned int exp){
//    double result=1.0;
//    if(exp==0)
//        return 1;
//    for(int i=0;i<exp;i++){
//        result*=base;
//    }
//    return result;
//}
//下面联系一下效率更高的一种。首先 x^n=x^(n/2)*x^(n/2)(n为偶数)；n为奇数（x^n=x^((n-1)/2)*...*x）
double PowerUnsignedExp(double base,unsigned int exp){
    if(exp==0)
        return 1;
    double result=PowerUnsignedExp(base,exp>>1);//右移一位除以2

    result*=result;
    if(exp&0x1==1)//这个数为奇数
        result*=base;
    return result;

}
bool equalt(double a,double b){
    return ((a-b<0.0000001)&&(b-a)<0.0000001)?1:0;
}
double Power(double base, int exponent){
    flag_error=false;

    if(equalt(base,0.0)){//底数W为0
        flag_error=true;
        return 0;//因为底数为0造成的返回结果为0，
    }
    unsigned int absExp=(exponent<0)?(-exponent):exponent;
    double result=PowerUnsignedExp(base,absExp);
    if(exponent<0)
        result=1.0/result;
    return result;
}
int main()
{
    cout <<Power(10,3) << endl;
    return 0;
}
```
    

