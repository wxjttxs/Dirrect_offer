---
title: 第一个只出现一次的字符
date: 2016-05-07 15:45:45
tags:
---
//考察哈希表；字符串
//第一个只出现一次

    #include <iostream>
    
    using namespace std;
    char FirstNotReaptingChar(char* pString){
        if(!pString)
            return '\0';
        const int tableSize=256;
        unsigned int hashTable[tableSize];
        for(int i=0;i<tableSize;i++)
            hashTable[i]=0;
        char* pHashKey=pString;//第一遍统计各个字符出现的次数，字符作为下标
        while(*pHashKey!='\0')
            hashTable[*(pHashKey++)]++;
        pHashKey=pString;//第二遍，从头开始找第一次只出现一遍的字符。
        while(*pHashKey!='\0'){
            if(hashTable[*pHashKey]==1)
                return *pHashKey;
            pHashKey++;
        }
        return '\0';
    
    }
    int main()
    {
        cout <<FirstNotReaptingChar("aaaccdeff")<< endl;
        return 0;
    }

