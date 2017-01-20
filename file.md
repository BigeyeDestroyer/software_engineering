## Linux常见压缩命令
- \*.gz : gzip程序**压缩**的文件
- \*.bz2 : bzip2程序**压缩**的文件
- \*.tar : tar程序**打包**的文件，并**没有经过压缩**
- \*.tar.gz : tar程序**打包**的文件, 并**经过gzip的压缩**
- \*.tar.bz2 : tar程序**打包**的文件, 并**经过bzip2的压缩**

### gzip
以压缩文件man.config为例：

	gzip -v man.config 
	zcat man.config.gz
	gzip -d man.config.gz
	gzip -9 -c man.config > man.config.gz
- 第一条命令：打包文件man.config并**输出压缩比**；此时**原来的文件man.config会被删除**。
- 第二条命令：类似于cat，适用于压缩文件。
- 第三条命令：解压缩文件man.config.gz；此时**解压前的文件man.config.gz会被删除**。
- 第四条命令：以**最高压缩比（-9）**压缩后通过-c重定向到文件man.config.gz；-c参数**默认**将压缩后的结果**输出到屏幕**。

### bzip2
同样以压缩文件man.config为例：

	bzip2 -z man.config
	bzcat man.config.bz2
	bzip2 -d man.config.bz2 
	bzip2 -9 -c man.config > man.config.bz2
 - 第一条命令：打包文件man.config，此时**原来的文件man.config会被删除**。
- 第二条命令：类似于cat，适用于压缩文件。
- 第三条命令：解压缩文件man.config.gz；此时**解压前的文件man.config.bz2会被删除**。
- 第四条命令：以**最高压缩比（-9）**压缩后通过-c重定向到文件man.config.bz2；-c参数**默认**将压缩后的结果**输出到屏幕**。

### tar
- 压缩

		tar -zpcv -f /root/etc.tar.gz /etc
		tar -jpcv -f /root/etc.tar.bz2 /etc
	- 第一条命令：**-z**表示**gzip支持**，可以压缩或解压.gz文件；**-p**表示**保留原来文件的权限与属性**；**-c**表示**新建打包文件**；**-f**后面**单独接一个被处理的文件名**。
	- 第二条命令：与第一条命令的区别在于**-j**表示**bzip2支持**。

