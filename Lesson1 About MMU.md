# 介绍MMU工作原理


#### 0-3G是用户区
#### .test  .rodata 是ro 只读区
#### .bss（为初始化区 跟初始化为0的区域）   .data  是rw  读写区
#### heap 堆（地址由低到高）  stack 栈（地址由高到低）
#### stack 上边是环境变量跟命令行参数
#### 3-4G是内核区，其中存有PCB（（process control block）进程控制块），存有描述进程的信息





![MMU](https://github.com/DDDDarcy/CPPAdvancedStudy/blob/main/mmu.jpg)
