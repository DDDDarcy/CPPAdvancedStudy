
``` 
#include<stdio.h>
#include<stdlib.h>
#inlcude<unistd.h>



int main(void){

pid_t = pid;

printf("xxxxxxxxxx");

pid = fork();

if(pid ==-1){

  perror("fork error:");

  exit(1);

}else if (pid==0){    //子进程

  printf(" I m child,pid = %u, ppid = %u\n",getpid(),getppid());

}else{                //父进程

  printf("I m parent,pid = %u,ppid = %u\n",getpid(),getppid());
  sleep(1);

}

printf("YYYYYYYYYYY");      //父子进程都会执行这句，谁先谁后后边再讨论

}
```

### 运行结果:
![fork2](https://github.com/DDDDarcy/CPPAdvancedStudy/blob/main/fork1.jpg)

printf("YYYYYYYYYYYY");会执行两次，而XXXXXXX行执行了一次，说明父进程用fork创建了子进程之后，fork之后的代码，父子进程都有各自的一份相同的代码，所以后边的代码都会执行。具体是先执行父进程的还是子进程的以后讨论。



### 正确创建五个子进程方法 代码如下： 
```
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>


int main(){

pid_t  pid;

printf("XXXXXXXXXXXXX");

for(int i = 0; i<5; i++){

	pid = fork();
	if(pid == 0)	//注意 子进程里的pid 为0 所以每个子进程 此句为真退出循环 

	break;		//父进程 pid 不等于0 等于子进程ID 所以将继续循环。
						// 而且还要注意 每个进程剥夺系统资源无优先级，
            //所以不存在父进程先生成5个子进程之后，这五个子进程才能继续执行，
            //并不是这样的，而是当第一个子进程创建之时，
            //他便与后续生成的子进程以及父进程在并发执行。
}
}

```

## fork调用后，子进程与父进程是否共享变量?

### 这里引用一篇博客：地址：https://blog.csdn.net/weixin_39578364/article/details/78995433 
### 作者：浅浅的i
### 先贴代码：
```
#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<unistd.h>
int main(){
    pid_t pid;
    int num=0;
    pid=fork();
    if(pid==0){
        num+=10;
        printf("child %d\n",num);
        printf("child %d\n",&num);
    }
    if(pid>0){
        num+=20;
        printf("parent %d\n",num);
        printf("parent %d\n",&num);
    }

    return 0;
}
```
运行结果：
```
parent 20
parent -948260088
child 10
child -948260088
```
根据顺序可以得出 假如共享一个内存单元的话，父进程先执行了num自加20之后，子进程在自加10，num应该为30，但是子进程num值为10，也就是说明不共享一个内存单元，但是父子进程打印的num地址是一样的，这就矛盾了，与此根据原博主博客，了解到，是因为liunx 自己的虚拟地址跟物理地址的映射关系造成这一原因，我们打印的并不是num的真实物理地址，而是linux给类似程序的虚拟地址，再由操作系统完成映射，到物理地址上，实际的父子进程的num物理地址不一样。
###  共享问题解决以后，之前碰到的以下问题也就可以解释清楚了：
``` 
#include<stdio.h>
#include<stdlib.h>
#inlcude<unistd.h>



int main(void){

int i;
pid_t = pid;

printf("xxxxxxxxxx");
for(i = 0; i < 5; i++){

pid = fork();

if(pid ==-1){

  perror("fork error:");

  exit(1);

}else if (pid==0){    //子进程

  printf(" I m child,pid = %u, ppid = %u\n",getpid(),getppid());

}else{                //父进程

  printf("I m parent,pid = %u,ppid = %u\n",getpid(),getppid());
  sleep(1);

}
}

printf("YYYYYYYYYYY");      //父子进程都会执行这句，谁先谁后后边再讨论

}
```
运行结果就不展示了，运行结果会产生多个子进程，并不只有五个，而且，子进程 依然有 父进程的i、 pid等变量，变量值跟 父进程创建他们的时候一样。但是并不会共享一块内存，类似于函数调用中的值传参方式，不像引用也非指针传参，所以父子进程i的变化，并不会互相影响其i的值，所以父进程自己会创建5个等低位的子进程，与此同时，i=0的时候创建的第一个子进程，会延续i=0的时候，但是i=0的时候，但是i=0的时候子进程不会创建新的子进程，是走下一个循环，i=1的时候创建新的子进程，就是第一个父进程创建了5个子进程，第一个子进程又创建了4个子进程，第一个父进程的第二个子进程有创建了3个子进程，以此类推，他的第4个子进程又创建了1个子进程才完毕，但是第一个子进程创建的四个子进程又会分别去创建，整个过程类似于一棵二叉树的形状。所以 该方法行不通。
