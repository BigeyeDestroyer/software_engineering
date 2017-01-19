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
- 若变量需要在其他子进程执行，则需要以export来使变量变成环境变量，不妨以caffe路径为例：

	export CAFFE_ROOT=/home/lurui/tools/caffe 
	export PATH=$PATH:$CAFFE_ROOT/build/tools

[1]:	http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#cross-installation