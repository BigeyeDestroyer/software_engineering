## 代码阅读
- [知乎][1]
- [源码解析][2]
- [教程合集][3]

## Ubuntu + QT
### 需要注意的地方：
- 在QT中打开**CMakeLists.txt**后会报找不到**CMAKE\_C\_COMPILER**的错，打开相应的build目录下的**CMakeCache.txt**文件后为CMAKE\_C\_COMPILER添加gcc路径即可：

	CMAKE_C_COMPILER:STRING=/usr/bin/gcc

[1]:	https://www.zhihu.com/question/27982282
[2]:	https://zhuanlan.zhihu.com/p/24343706?refer=dlclass
[3]:	https://absentm.github.io/2016/05/14/%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0Caffe%E7%B3%BB%E5%88%97%E6%95%99%E7%A8%8B%E9%9B%86%E5%90%88/