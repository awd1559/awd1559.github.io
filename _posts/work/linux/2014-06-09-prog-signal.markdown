---
layout:     post
title:      "signal"
subtitle:   " \"Linux signal program\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux prog
---
信号集的处理

int sigemptyset(sigset_t *set); //创建set并且情况信号集
int sigfillset(sigset_t *set); //创建set并使set包含所有linux的信号
int addset(sigset_t *set,int signo);      //给set信号集增加一个signo信号
int sigdelset(sigset_t*set,int signo); //将set信号集中的signo定义的信号剔除

以上四个函数成功调用返回0,失败返回1

int sigismember(const sigset_t *set,int signo); //判断set信号集中是否已经包含signo所指向的信号,真返回1,假返回0
int sigprocmask(int how,const sigset_t *set,sigset_t *oset);    //设置信号集的屏蔽位,如果oset不为NULL,则oset返回当前修改之前的屏蔽字
how的参数定义
SIG_BLOCK : 屏蔽set所包含的所有信号
SIG_UNBLOCK : 解除set所包含的所有信号
SIG_SETMASK : 直接设置屏蔽信号所指向的值给set信号集

int sigaction(int signo,const struct sigction *act,struct sigaction *oact);
sigaction函数的功能是检测或者修改signo信号关联的处理动作
signo是要检测或者修改具体动作的信号编号数,若act非NULL,则修改它的动作,如果oact非NULL,则返回该信号的原先动作
struct sigaction{
void (*sa_handler)(int signo); //用户自定义处理函数,或者SIG_DFL或者 SIG_IGN
sigset_t sa_mask;       //信号集,用来指导在信号处理指向过程中哪些信号要被阻塞
int sa_flags;   //信号选项,包括是否则色,是否忽略SIGSTOP,SIGSTP,SIGTTIN,SIGTTOU信号,是否自定义信号只执行一次等等
void (*as_restore);       
}

int sigpending(sigset_t *set); //用于检测set信号集中是否为未决的信号,比如在信号集阻塞时的信号


sa_restorer已过时，POSIX不支持它，不应再使用。

当你的信号需要接收附加信息的时候，你必须给sa_sigaction赋信号处理函数指针，同时还要给sa_flags赋SA_SIGINFO, 如下：

              sigemptyset(&sig_act.sa_mask);
              sig_act.sa_sigaction=sig_handler_with_arg;
              sig_act.sa_flags=SA_SIGINFO;
如果你的应用程序只需要接收信号，而不需要接收额外信息，那你需要的设置的是sa_handler,而不是sa_sigaction，如下：
              sigemptyset(&sig_act.sa_mask);
              sig_act.sa_handler=sig_handler;
              sig_act.sa_flags=0;


新版本
信号发送函数sigqueue()及信号安装函数sigaction()


信号值位于SIGRTMIN和SIGRTMAX之间的信号都是可靠信号，可靠信号克服了信号可能丢失的问题。
这些信号支持排队，不会丢失。 

信号阻塞：当信号发生而无法处理的时候，不要忽略该信号，在进程准备好时再通知它
信号产生到在进程上标记标志之间，信号未决(pending)

三个函数改变信号屏蔽字
sigpending将制定的哦信号设置为阻塞和pending
sigprocmask查询和设置当前进程的信号屏蔽字
sigsuspend在原子操作中实现恢复信号屏蔽字,并且使进程睡眠