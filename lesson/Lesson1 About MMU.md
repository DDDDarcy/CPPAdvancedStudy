# 介绍MMU工作原理


#### 0-3G是用户区
#### .test  .rodata 是ro 只读区
#### .bss（为初始化区 跟初始化为0的区域）   .data  是rw  读写区
#### heap 堆（地址由低到高）  stack 栈（地址由高到低）
#### stack 上边是环境变量跟命令行参数
#### 3-4G是内核区，其中存有PCB（（process control block）进程控制块），存有描述进程的信息


## MMU 映射到物理地址 不足 4k的都是 每个page都是4k


![MMU](https://github.com/DDDDarcy/CPPAdvancedStudy/blob/main/mmu.jpg)

##
##
##
## 同一程序打开两次 两个进程相互独立 除了内核区映射到相同区域不同地址以外 其余都是每个进程另开辟新区域去映射 ，因为物理地址内核区就一块
## 如图
## 

![MMU](https://github.com/DDDDarcy/CPPAdvancedStudy/blob/main/mmu2.jpg)
