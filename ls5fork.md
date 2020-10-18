
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

}else if (pid==0){

  printf(" I m child,pid = %u, ppid = %u\n",getpid(),getppid());

}else{

  printf("I m parent,pid = %u,ppid = %u\n",getpid(),getppid());
  sleep(1);

}

printf("YYYYYYYYYYY");

}
```

### 运行结果:
![fork2](https://github.com/DDDDarcy/CPPAdvancedStudy/blob/main/fork1.jpg)

printf("YYYYYYYYYYYY");会执行两次，而XXXXXXX行执行了一次，说明父进程用fork创建了子进程之后，fork之后的代码，父子进程都有各自的一份相同的代码，所以后边的代码都会执行。具体是先执行父进程的还是子进程的以后讨论。
