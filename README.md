# software\_engineering
This is the repo for software engineering related to deep learning.

## 时间安排
预计四个课时讲完所有内容，每个课时+QA时长2\～3h，安排如下：
1. 预备和编译链接运行：2016.7.9 13:00 已完成
2. Linux命令行：2016.7.13 19:30 已完成
3. 代码风格和工程设计：2016.7.16 9:00 补export/source,stdin/pipe
4. 高效的工具链：2016.7.20 19:30 已完成

## 技能目录
### 预备：
- zsh相对bash的好处
	1. 箭头颜色表示返回值
	2. Tab补全方向键可选
	3. Tab模糊补全
	4. 前缀查找历史命令
- 选择oh-my-zsh主题
- 选择vim主题

### 欲学习的技能分为三类：Linux理论和操作，软件工程，高效工具链。目录如下：
1. Linux理论和操作
	- Linux命令行
		- 前后台调度：fg/jobs/nohup/&
		- 管道和输出重定向：pipe/&1/&2/\>/\>\>/tee/tail
		- 文件查找和正则表达式：which/locate/updatedb/find/grep/wc/sed
		- 循环：while/for in/xargs/find -exec
		- 监测系统：w/bmon/iostat/iotop
		- misc：ln/export/实时设置变量/source/chmod/chown/#!/sshpass/crontab
		- 例子：简单监测程序：while/variables/wc
	- 编译链接运行
		- 编译：\*.cpp-\>\*.o, cc/gcc/g++/c++/-I
		- 链接：\*.o-\>{\*.so, \*.a, exec}, -L\*
		- 运行：PATH/LD\_LIBRARY\_PATH
		- misc：ldd/ldconfig/libxxx-dev/{python, matlab}可执行文件
		- 例子：caffe编译：CMakeLists/Makefile/cmake/make
		- 例子：cudnn安装
		- 例子：matcaffe找不到\*.so

2. 软件工程
	- caffe python代码风格/PEP8/Google python代码风格
		- 最最重要的：与已有代码保持一致；最重要的：看PyCharm提示
		- 命名规范：类名大写，其余小写，下划线分隔，不camel，不匈牙利
		- 不import \*
		- 列表和字典用默认迭代器
		- 括号前后没空格；冒号逗号前没后有空格；索引冒号加减号前后没空格；参数列表没空格
		- 顶层函数间空两行，类内函数间空一行
		- @ 悬挂缩进和垂直对齐
	- caffe工程目录结构设计
	- fast-rcnn
		- fast-rcnn工程目录结构设计
		- log系统实现：set x/e/u, exec/&\>/process subtitution
	- python-glog
3. 高效的工具链
	- 3.1  vim
		- 3.1.1 两种主要模式：命令/插入/Esc/i/:w/:wq
		- 3.1.2 上下左右，跳转翻页：k/j/h/l/w/e/b/g/gg/G/0/$/%
		- 3.1.3 选择/块选择：v/Ctrl+V/Shift+I
		- 3.1.4 复制粘贴删除：y/yy/p/d/dd
		- 3.1.5 查找替换：//%s/n/N
		- 3.1.6 命令重复：数字+命令
		- 3.1.7 编辑多个文件：vim -O/Ctrl+ww
		- 3.1.8 固定搭配：ves/10dd/gg0vG$y
		- 3.1.9 misc：o/O/A/c
	- 3.2 cmake
		- 3.2.1 一个较为复杂的工程：roadSign2015
	- 3.3 git
		- 3.3.1 工作区/暂存区/版本库
		- 3.3.2 git clone
		- 3.3.3 git add
		- 3.3.4 git commit
		- 3.3.5 git push
		- 3.3.6 git pull
		- 3.3.7 git diff
		- 3.3.8 版本回退：git reset/git branch/git checkout
		- 3.3.9 zsh git快捷键
	- 3.4 pip
		- 3.4.1 pip install/pip uninstall
		- 3.4.2 从文件安装：pip install -r
		- 3.4.3 精确调控版本：pip install —upgrade/pip install xxx==vvv
		- 3.4.4 pip和apt-get：/usr/local/lib和/usr/lib

## 练习题
### 故障诊断类
1. matconvnet某一版和cudnn5配合不畅（可能是matconvnet或者matlab本身的bug）。系统本身在/usr/local/cuda-7.5下装了cudnn5，另外cudnn4已下载好，在/home/yanziang/tools/cudnn/v4。已知cudnn4和cuda7.5没有问题，求方案使matconvnet用cudnn4
2. 胡文政在hawk上的python cv2模块无法读入图像，我的可以，求诊断思路（开放性问题）
3. hawk上ssd(Single Shot Detector)编译报numpy/arrayobject.h找不到，求诊断思路（开放性问题）

## 技艺类
1. caffe可以同时兼容cudnn4和cudnn5。卸载系统已有的caffe，并安装不同版本的cudnn，重新编译caffe，使mnist样例运行无误。再卸载新装好的cudnn，安装原有版本的cudnn，重新编译caffe，使其运行无误
