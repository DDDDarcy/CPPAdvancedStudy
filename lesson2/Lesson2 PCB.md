# PCB介绍

### /usr/src/linux-headers-3.16.0-30/include/linux/sched.h 文件中查看 PCB struct
### task_struct  是PCB结构体名称

#### linux 下 使用 grep -r "task_struct {" /usr/src/linux-headers-3.16.0-30/include/linux/ 查找 该结构体

#### 进程id 系统中每个进程都有唯一的id，在C语言中pid_t 表示类型就是一个非负整数
#### 进程状态 有就绪、运行、挂起、停止等状态。
#### 进程切换时需要保存和恢复一些CPU寄存器。
#### 描述虚拟地址空间信息。
#### 描述控制终端的信息。
#### 当前工作目录（current working directory）
#### umask 掩码
#### 文件描述符，包含很多指向file结构体的指针。
