
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
