## Basic installation
- [cuda][1]
	- sudo service lightdm stop
	- install cuda
	- sudo service lightdm start
- cudnn
	- \*.h -\> /usr/local/cuda/include
	- \*.so -\> /usr/local/cuda/lib64

## 变量相关
- 若变量需要在其他**子进程**执行，则需要以export来使变量变成环境变量，不妨以caffe路径为例：

		export CAFFE_ROOT=/home/lurui/tools/caffe 
		export PATH=$PATH:$CAFFE_ROOT/build/tools

- 子进程概念：在我**目前的shell**下打开另一个**新的shell**或者跑一个新的程序，新的shell就是子进程；在一般状态下，父进程的自定义变量是无法在子进程内使用的；但通过**export将变量变成环境变量**后，就能够在子进程下面应用了。总的来说，在这个bash下面所执行的任何命令都是由这个**bash所衍生出来**的，这些被执行的命令就被称为子进程。

- **declare**的使用

		declare -i randint=$RANDOM*10/23767; echo $randint
	- 上面的例子将**randint声明为一个整数**，然后调用环境变量RANDOM得到一个0到9的随机整数

- 变量删除

		path=${PATH}
		echo ${path#/*sbin:}
	- **\\\\#**表示**从头开始**，删除最短的介于**/**与**sbin:**之间的内容
	- **\#\#**表示**从头开始**删除**最长**的  

## 数据流重定向
- 基本概念：每个linux命令都有**标准输入**、**标准输出**以及**标准错误输出**：
	- 标准输入(stdin): 代码为0, 使用\<或\<\<
	- 标准输出(stdout): 代码为1, 使用\>或\>\>
	- 标准错误输出(stderr): 代码为2, 使用2\>或2\>\>
	- 其中，stdout与stderr**默认输出到屏幕**
	- **\>**表示覆盖，**\>\>**表示append
- 将stdout与stderr分别存到不同的文件中去：

		find /home -name .bashrc > list_right 2> list_err

- 将正确与错误数据写入一个文件的语法：

		find /home -name .bashrc > list 2>&1
	- 表示首先将**1(stdout)重定向到文件list**，然后将**2(stderr)重定向到1(stdout)**，这样**2(stderr)也被重定向到了文件list**。
- 上面例子的错误写法:

		find /home -name .bashrc 2>&1 > list
	- 这条命令表示**先将2(stderr)重定向到1(stdout)**，**再将1(stdout)重定向到文件list**，但此时**2(stderr)仍然是重定向到屏幕**上。

- **stdin**的用法:

		cat > catfile < ~/.bashrc
	- 上面的命令将**.bashrc文件作为cat命令的stdin**，然后将其**stdout重定向到文件catfile**，最后**相当于copy**的操作。

- &&与||

		command1 && command2 || command3
		ls /tmp/abc && echo "exist" || echo "not exist"
	- 执行command1，若成功执行则继续执行command2，否则执行command3 

## 管道命令(pipe)
管道命令仅能处理**前一个命令传来的正确信息**，也就是**standard output**的信息，对**standard error output**会**予以忽略**；管道后的命令必须能够接收**standard input**才行。
- cut的使用

		echo $PATH | cut -d ':' -f 3,5
	- 使用cut命令对$PATH的返回路径**按照’:’进行切割**并取出第3和第5个返回结果；注意，如果管道进来的是**多行**，那么该命令将**逐行分析stdin**。

- grep的使用
	grep可以解析一行文字，取得关键字，若该行存在关键字，就会整行显示出来。

		grep --color=auto 'MANPATH' /etc/man.config
		last | grep -v 'root' | cut -d ' ' -f 1
	- 在文件/etc/man.config中搜索关键字’MANPATH’，并用颜色显示出来。
	- 首先在last命令的返回中找到那些**没有关键字**’root’的行，然后对返回的每一行**用空格进行分割**，并取出其中的第一行作为最终返回。 

## 排序命令
- sort命令 

		cat /etc/passwd | sort -t ':' -k 3 -n 
		last | cut -d ' ' -f 1 | sort 
	- 第一条命令：将passwd文件的内容**逐行管道给sort**，用关**键字’:’对每一行进行分割**，然后根据每行的第3个字符串对所有行进行排序； -n 的含义是将**排序关键字**当作**纯数字**。
	- 第二条命令：将last命令的内容首先**逐行管道给cut命令**，用**空格进行分割**后将每一行的第1个字符串进行排序。

- uniq命令

		last | cut -d ' ' -f 1 | sort | uniq -c 
	- 将last管道给cut命令，用空格关键字分割后取出每一行的第1个字符串；将以上结果管道给sort命令后排序，最后管道给uniq命令使得每个**相同字符串仅显示一次**，用**-c**参数查询**每个字符串出现的次数**。 
	- 本命令查询所有用户的登录次数。

- wc命令

		last | grep "[a-zA-Z]" | grep -v 'wtmp' | wc 
	- 将last输出结果管道给grep命令，挑选出其中的**非空行**，并**去除**带有’wtmp’关键字的行，然后依次输出剩余内容的**行数**、**单词数**以及**字符数**。

[1]:	http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#cross-installation