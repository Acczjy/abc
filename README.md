abc
第一个（演示） 三个进程P1、P2、P3互斥使用一个包含N个单元的缓冲区 
semaphore odd=0;</br>
 even=0;</br>
 empty=N;</br>
 mutex=1;</br>
P1(){ x=produce();</br>
 P(empty);</br>
 P(mutex);</br>
 Put();</br>
 V(mutex);</br>
 if(x%2==0) V(even);</br>
 else V(odd);</br>
 } P2(){ P(odd);</br>
 getodd();</br>
 V(mutex);</br>
 V(empty);</br>
 countodd();</br>
 } P3(){ P(even);</br>
 p(mutex);</br>
 geteven();</br>
 V(mutex);</br>
 V(empty);</br>
 counteven();</br>
 }
 ————————————– 
某银行提供1个服务窗口和10个供顾客等待的座位。 semaphore seets=10;</br>
//有十个座位 mutex=1;</br>
//取号机互斥信号量 haveCustom=0;</br>
//顾客与营业员同步，无顾客时营业员休息 process 顾客{ P(seets);</br>
 P(mutex);</br>
 取号机取号;</br>
 V(mutex);</br>
 v(haveCustom);</br>
 等待营业员叫号;</br>
 V(seets);</br>
 接受服务;</br>
 } process 营业员{ P(haveCustom);</br>
 叫号;</br>
 为顾客服务;</br>
 } 
————————————– 
某博物馆最多可容纳500人同时参观，有一个出入口;</br>
 semaphore empty=500;</br>
 semaphore mutex=1;</br>
 参观者进程i{ P(empty);</br>
 P(mutex);</br>
 进门;</br>
 V(mutex);</br>
 参观;</br>
 P(mutex);</br>
 出门;</br>
 V(mutex);</br>
 V(empty);</br>
 } 
—————————– 
系统中有多个生产者进程和多个消费者今晨俄国，共享一个能存放1000件产品的环形缓冲区;</br>
 semaphore mutex1=1;</br>
 semaphore mutex2=1;</br>
 semaphore empty=n;</br>
 semaphore full=0;</br>
 producer(){ while(1){ 生产一个产品;</br>
 P(empty);</br>
 P(mutex2);</br>
 把产品放入缓冲区;</br>
 V(mutex2);</br>
 V(full);</br>
 } } consumer(){ while(1){ P(mutex1) for(int i=0;</br>
i<=10;</br>
++i){ P(full);</br>
 P(mutex2);</br>
 从缓冲区取出一件产品;</br>
 V(mutex2);</br>
 V(empty);</br>
 消费者件产品;</br>
 } V(mutex1) } } 
 有A、B两人通过心想进行辩论； semaphore Full_A=x;</br>
 semaphore Empty_A=M-x;</br>
 semaphore Full_B=y;</br>
 semaphore Empty_B=N-y;</br>
 semaphore mutex_A=1;</br>
 semaphore mutex_B=1;</br>
 A{ while(TRUE){ P(Full_A);</br>
 P(mutex_A);</br>
 从A的信箱中取出一个邮件;</br>
 V(mutex_A);</br>
 V(Empty_A);</br>
 回答问题并提出一个新问题； P(Empty_B);</br>
 P(mutex_B);</br>
 将新邮件放入B的信箱;</br>
 V(mutex_B);</br>
 V(Full_B);</br>
 } } B{ while(TRUE){ P(Full_B);</br>
 p(mutex_B);</br>
 从B的信箱中取出一个邮件;</br>
 V(mutex_B);</br>
 V(Empty_B);</br>
 回答问题并提出一个新问题;</br>
 P(Empty_A);</br>
 P(mutex_A);</br>
 将新邮件放入A的信箱;</br>
 V(mutex_A);</br>
 V(Full_A);</br>
 } }
 ———————————-
 某进程有3个并发执行的线程thread1,thread2,thread3;</br>
 semaphore mutex_y1=1;</br>
 //用于thread1与thread3对变量y的互斥访问 semaphore mutexe_y2=1;</br>
 //用于thread2与thread3对变量y的互斥访问 semaphore mutex_z=1;</br>
//用于变量z的互斥访问 thread1{ cnum w;</br>
 wait(mutex_y1);</br>
 w=add(x,y);</br>
 signal(mutex_y1);</br>
 } thread2{ cnum 2;</br>
 wait(mutex_y2);</br>
 wait(mutex_z);</br>
 w=add(y,z);</br>
 signal(mutex_z);</br>
 signal(mutex_y2);</br>
 } thread3{ cnum 2;</br>
 w.a=1;</br>
 w.b=1;</br>
 wait(mutex_z);</br>
 z=add(z,w);</br>
 signal(mutex_z);</br>
 wait(mutex_y1);</br>
 wait(mutex_y2);</br>
 y=add(y,2);</br>
 signal(mutex_y1);</br>
 signal(mutex_y2);</br>
 }
