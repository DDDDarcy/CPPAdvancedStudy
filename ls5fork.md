
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
