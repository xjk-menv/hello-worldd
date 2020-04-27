#include <bits/stdc++.h>
using namespace std;

#define MaxNum 100

typedef struct
{
    char ID;//进程名字
    int order;//处理次序
    int arrtime;//到达时间
    int sertime;//服务时间
    int sertime_SJF;//SJF排序时间
    double priority;//优先权
    double prioritytime;//优先权时间
    int fintime;//结束时间
    int starttime;//执行时间
    int wholetime;//周转时间
    double weightwholetime;//带权周转时间
} PCB;


int n=0;
PCB pro[100];//进程结构体
PCB temp;//临时进程结构

int choose;
double Averagewt=0;//平均周转时间
double Averagewwt=0;//平均带权周转时间
int sumwt=0;//周转时间总和
double sumwwt=0;//带权周转时间总和

