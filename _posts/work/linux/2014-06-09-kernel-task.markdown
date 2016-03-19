---
layout:     post
title:      "task"
subtitle:   " \"linux kernel task\""
date:       2015-01-29 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - linux kernel
---
全局变量

#define init_task	(init_task_union.task)	//【include/asm-i386/processor.h】
#define init_stack	(init_task_union.stack)

struct task_struct * init_tasks[NR_CPUS] = {&init_task, };	//【kernel/sched.c】

static LIST_HEAD(runqueue_head);	//runing task列表
wake_up_process
	-try_to_wake_up
		-add_to_runqueue
		


static struct task_struct *task_struct_head;
static unsigned int nr_task_struct;


task_struct
{
	... ...
	struct list_head *prev_task;	//link to init_task
	struct list_head *next_task;
	struct list_head *run_list;	//link to runqueue_head list
	... ...
	pid_t pid;
	struct list_head thread_group; //线程组
	... ...
	struct task_struct *pidhash_next;//解决pidhash表中的冲突
	struct task_struct **pidhash_pprev;
	... ...
	wait_queue_head_t wait_chldexit;	/* for wait4() */
	... ...
	struct rlimit rlim[RLIM_NLIMITS];

	struct thread_struct thread;		//保存硬件tss中相关数据
}

do_fork
	-alloc_task_struct		//分配2个页面做描述符和进程内核堆栈()


SET_LINK	//把描述符放入链表中
MOVE_LINK	//把描述符从链表中删除

for_each_task(p)	//遍历进程


可运行队列
-----------------------------------------------------------------------
struct list_head runqueue_head;		//全局，所有可运行进程的队列
add_to_runqueue(p);			//将进程加入可运行队列
del_from_runqueue(p);			//
move_first_runqueue();			//将进程描述符移动到可运行队列的开头
move_last_runqueue();			//将进程描述符移动到可运行队列的末尾




pidhash
-----------------------------------------------------------------------
struct task_struct *pidhash[PIDHASH_SZ];//全局，
pidhash[pid_hashfn(p->pid)];		
find_task_by_pid(int pid);		//从pid得到struct task_struct
hash_pid();				//在pidhash中插入进程
unhash_pid();				//在pidhash中删除进程




等待队列
-----------------------------------------------------------------------
struct wait_queue_head_t;	//等待队列头，每个等待队列一个队列头
struct wait_queue_t		//等待队列中的元素，每个元素一个睡眠进程
{
	unsigned int flags;
	struct *task_struct;
	struct list_head task_list;
}






进程切换
-----------------------------------------------------------------------
进程切换只发生在内核态，执行进程切换之前，用户态进程使用的所有寄存器内容都已保存，如用户态堆栈指针ss和esp。
Linux不是哦那个硬件文境切换，但强制为系统中每个不同的CPU创建一个TSS
	cpu从用户态切换到内核态是，从tss中获取内核态堆栈地址
	用户态访问I/O端口时，cpu访问tss中的I/O许可权位图
struct tss_struct{}	描述tss结构
task_struct->thread	保存进程的tss



switch_to










进程创建
-----------------------------------------------------------------------
