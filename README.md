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

void Input();//输入数据
void Sortarrivetime();//对到达时间排序
void Sortserivetime();//对服务时间排序，在短作业优先算法中使用
void Sortpriority(int a, int falg);//对优先权排序
void Calculationtime(int i);//计算进程的各个时间
void Calculationaverage();
void display();//输出
void Outtimestate();//输出个各时间状态
void Choose();//选择算法
void FCFS();//先来先服务算法
void SJF();//短作业优先算法
void HRRN();//高响应比算法
void PSA();//静态优先权算法
int cmp(PCB a, PCB b)//sort排序
{
    if(a.arrtime < b.arrtime)
        return 1;
    return 0;
}

int main()
{
    int s;
    while(1)
    {
        memset(&pro[0], 0, sizeof(PCB));
        Input();//调用输入函数
        Choose();//调用选择算法函数
        cout<<endl<<"请输入：1-继续，2-退出"<<endl;
        cin>>s;
        if(s==2)
            break;
    }
    return 0;
}
