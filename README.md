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

void Input()
{
    system("cls");
    cout<<"请输入进程个数n（最多输入100个进程）：";
    cin >>n;
    if(n>100)
    {
        cout<<"超出最大进程数，请重新输入"<<endl;
        Input();
    }
    cout<<"请分别输入进程名、进程到达时间、进程服务时间："<<endl;
    for(int i=0; i<n; i++)
        cin>>pro[i].ID>>pro[i].arrtime>>pro[i].sertime;

    cout<<endl<<"------------------------------------"<<endl;
}

void Sortarrivetime()
{
    sort(pro, pro+n, cmp);
}

void Sortserivetime(int a)
{
    int i, j;
    for(i=a; i<n; i++)//记录在正在执行的进程服务时间内到达的进程
    {
        if(pro[i].arrtime<=pro[a-1].fintime)
            pro[i].sertime_SJF=pro[i].sertime;
    }
    for(i=a; i<n; i++)//对已到达的进程排序
    {
        for(j=i+1; j<n; j++)
        {
            if(pro[i].sertime_SJF>pro[j].sertime_SJF && pro[i].sertime_SJF!=0 && pro[j].sertime_SJF!=0)
            {
                temp=pro[i];
                pro[i]=pro[j];
                pro[j]=temp;
            }
        }
    }
}
