环境变量



操作系统中用来指定操作系统运行环境二队一些参数通常具备以下特征：

字符串本质 有统一的格式： 名=值[:值] 

shell 命令 是命令解析器

echo $PATH 查看linux下path环境变量

echo $SHELL 查看当前命令解析器是哪个

echo $LANG 查看语言编码

echo $TERM 当前终端类型 决定一些程序输出显示方式

echo $HOME 当前用户主目录的路径





加载位置 与 命令行参数类似 位于用户区 高于stack

引入环境变量表：须声明环境变量。extern char **environ 

environ是以NULL结尾的

引入当前进程的环境变量表


#include<stdio.h>

extern char** environ;

int main(void){

int i;

for(i=0;extern[i];i++)

printf("%s",extern[i]);

return 0;

}

环境变量函数：

getenv函数：

获取环境变量值

char*getenv(const char *name);

成功：返回环境变量值。

失败：NULL（name不存在）

setenv函数：

设置环境变量的值

int setenv(const char*name,const char*value,int overwrite);

成功：返回0.

失败：返回-1

参数overwrite 取值：1：覆盖原环境变量

​									0：不覆盖（该参数常用于设置新环境变量，如：PATH=das/ds/dsd）

unsetenv函数

删除环境变量name的定义

int unsetenv(const char*name); 

成功：0

失败：-1

name不存在时仍然返回0（成功） 当name命名为“PATH=”则会出错







学习所有的函数 用 man page入手 （Manual）

