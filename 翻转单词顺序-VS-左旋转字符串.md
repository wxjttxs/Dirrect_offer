---
title: 翻转单词顺序 VS 左旋转字符串
date: 2016-05-09 11:01:09
tags:
---
//一个字符串。要求翻转单词顺序，但是单词内部字符顺序不变

    #include <iostream>
    #include<string.h>
    using namespace std;
    //翻转一个单词
    void Reverse(char* pBegin,char* pEnd){
        if(pBegin==NULL || pEnd==NULL)
            return;
        while(pBegin<pEnd){
            char temp=*pBegin;
            *pBegin=*pEnd;
            *pEnd=temp;
            pBegin++;
            pEnd--;
        }
    }
    char* ReverseSentence(char *pData)
    {
        if(pData == NULL)
            return NULL;
    
        char *pBegin = pData;
    
        char *pEnd = pData+strlen(pData)-1;
    
        // 翻转整个句子
        Reverse(pBegin, pEnd);
    
        // 翻转句子中的每个单词
        pBegin = pEnd = pData;
        while(*pEnd!='\0'){
            if(*pEnd!=' ')
                pEnd++;
            else{
                Reverse(pBegin,pEnd-1);//空格前一个
                pBegin=++pEnd;//pBegin指向空格后一个
            }
        }
        Reverse(pBegin,pEnd-1);//最后一个单词，pEnd指向'\0'
        return pData;
    }
    
    //********************左旋转n位字符**************************
    //前n位看做空格前字母，比如“hello world”
    char* LeftRotateString(char* pStr,int n){
        if(pStr!=NULL){
            int length=static_cast<int>(strlen(pStr));
            if(length>0 && n>0 &&n<length){//输入是有效的
                char* pFirstBegin=pStr;
                char* pFirstEnd=pStr+n-1;
                char* pSecondBegin=pStr+n;
                char* pSecondEnd=pStr+length-1;
                Reverse(pFirstBegin,pFirstEnd);//旋转第一段
                Reverse(pSecondBegin,pSecondEnd);//旋转第二段
                Reverse(pFirstBegin,pSecondEnd);//旋转整个单词
            }
        }
        return pStr;
    }
    int main()
    {
          char sentence[]="stu dent!";
          char *reverced=ReverseSentence(sentence);
          cout<<reverced<<endl;
    
          char sentence1[]="abcdefg";
          char *reverced1=LeftRotateString(sentence1,7);
         // char *reverced1=LeftRotateString(“abcdef”,2);不承认这样的赋值方式
          cout<<reverced1<<endl;
          return 0;
    }

