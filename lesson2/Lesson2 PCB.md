# PCB介绍

### /usr/src/linux-headers-3.16.0-30/include/linux/sched.h 文件中查看 PCB struct
### task_struct  是PCB结构体名称

#### 1、linux 下 使用 grep -r "task_struct {" /usr/src/linux-headers-3.16.0-30/include/linux/ 查找 该结构体

#### 2、进程id 系统中每个进程都有唯一的id，在C语言中pid_t 表示类型就是一个非负整数
#### 3、进程状态 有（初始化）就绪、运行、挂起、停止等状态。
#### 4、进程切换时需要保存和恢复一些CPU寄存器。
#### 5、描述虚拟地址空间信息。
#### 6、描述控制终端的信息。
#### 7、当前工作目录（current working directory）
#### 8、umask 掩码 保护文件创建修改。
#### 9、文件描述符，包含很多指向file结构体的指针。
#### 10、和信号量相关的信息
#### 11、用户id 和 组 id.
#### 12、会话（session）和进程组。
#### 13、进程可以使用的资源上限（Resource Limit）

####  ulimit -a 命令查看linux 运行资源上限限制的
