## Basic installation
- [cuda][1]
	- sudo service lightdm stop
	- install cuda
	- sudo service lightdm start
- cudnn
	- \*.h -\> /usr/local/cuda/include
	- \*.so -\> /usr/local/cuda/lib64

## Bash
### 变量相关
- 若变量需要在其他**子进程**执行，则需要以export来使变量变成环境变量，不妨以caffe路径为例：

		export CAFFE_ROOT=/home/lurui/tools/caffe 
		export PATH=$PATH:$CAFFE_ROOT/build/tools

- 子进程概念：在我**目前的shell**下打开另一个**新的shell**或者跑一个新的程序，新的shell就是子进程；在一般状态下，父进程的自定义变量是无法在子进程内使用的；但通过**export将变量变成环境变量**后，就能够在子进程下面应用了。总的来说，在这个bash下面所执行的任何命令都是由这个**bash所衍生出来**的，这些被执行的命令就被称为子进程。

[1]:	http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#cross-installation