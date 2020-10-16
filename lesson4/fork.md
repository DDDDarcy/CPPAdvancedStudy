进程控制原语

fork函数 -create a child process

创建一个当前进程的子进程

pid_t fork(void)

返回一个进程ID



返回值有两个 一个进程--->两个进程--->fork返回值大于0 是父进程返回子进程ID

​						fork函数返回值等于0，说明是子进程且创建成功。 
