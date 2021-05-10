# abc
第一个（演示）
三个进程P1、P2、P3互斥使用一个包含N个单元的缓冲区
semaphore odd=0;
even=0;
empty=N;
mutex=1;
P1(){
x=produce();
P(empty);
P(mutex);
Put();
V(mutex);
if(x%2==0)
V(even);
else
V(odd);
}
P2(){
P(odd);
getodd();
V(mutex);
V(empty);
countodd();
}
P3(){
P(even);
p(mutex);
geteven();
V(mutex);
V(empty);
counteven();
}
--------------------------------------
某银行提供1个服务窗口和10个供顾客等待的座位。
semaphore seets=10;//有十个座位
mutex=1;//取号机互斥信号量
haveCustom=0;//顾客与营业员同步，无顾客时营业员休息
process 顾客{
P(seets);
P(mutex);
取号机取号;
V(mutex);
v(haveCustom);
等待营业员叫号;
V(seets);
接受服务;
}
process 营业员{
P(haveCustom);
叫号;
为顾客服务;
}
--------------------------------------
某博物馆最多可容纳500人同时参观，有一个出入口;
semaphore empty=500;
semaphore mutex=1;
参观者进程i{
P(empty);
P(mutex);
进门;
V(mutex);
参观;
P(mutex);
出门;
V(mutex);
V(empty);
}
-----------------------------
系统中有多个生产者进程和多个消费者今晨俄国，共享一个能存放1000件产品的环形缓冲区;
semaphore mutex1=1;
semaphore mutex2=1;
semaphore empty=n;
semaphore full=0;
producer(){
while(1){
生产一个产品;
P(empty);
P(mutex2);
把产品放入缓冲区;
V(mutex2);
V(full);
}
}
consumer(){
while(1){
P(mutex1)
for(int i=0;i<=10;++i){
P(full);
P(mutex2);
从缓冲区取出一件产品;
V(mutex2);
V(empty);
消费者件产品;
}
V(mutex1)
}
}
-------------------------------
有A、B两人通过心想进行辩论；
semaphore Full_A=x;
semaphore Empty_A=M-x;
semaphore Full_B=y;
semaphore Empty_B=N-y;
semaphore mutex_A=1;
semaphore mutex_B=1;
A{
while(TRUE){
P(Full_A);
P(mutex_A);
从A的信箱中取出一个邮件;
V(mutex_A);
V(Empty_A);
回答问题并提出一个新问题；
P(Empty_B);
P(mutex_B);
将新邮件放入B的信箱;
V(mutex_B);
V(Full_B);
}
}
B{
while(TRUE){
P(Full_B);
p(mutex_B);
从B的信箱中取出一个邮件;
V(mutex_B);
V(Empty_B);
回答问题并提出一个新问题;
P(Empty_A);
P(mutex_A);
将新邮件放入A的信箱;
V(mutex_A);
V(Full_A);
}
}
----------------------------------
某进程有3个并发执行的线程thread1,thread2,thread3;
semaphore mutex_y1=1; //用于thread1与thread3对变量y的互斥访问
semaphore mutexe_y2=1; //用于thread2与thread3对变量y的互斥访问
semaphore mutex_z=1;//用于变量z的互斥访问
thread1{
cnum w;
wait(mutex_y1);
w=add(x,y);
signal(mutex_y1);
}
thread2{
cnum 2;
wait(mutex_y2);
wait(mutex_z);
w=add(y,z);
signal(mutex_z);
signal(mutex_y2);
}
thread3{
cnum 2;
w.a=1;
w.b=1;
wait(mutex_z);
z=add(z,w);
signal(mutex_z);
wait(mutex_y1);
wait(mutex_y2);
y=add(y,2);
signal(mutex_y1);
signal(mutex_y2);
}
