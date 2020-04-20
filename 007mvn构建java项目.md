> 首先安装 maven

1. 下载Maven 3安装包
	官网：http://maven.apache.org/download.cgi
	清华镜像：https://mirrors.tuna.tsinghua.edu.cn/apache/maven/
2. 安装Maven

```
tar xf apache-maven-3.3.9-bin.tar.gz 
mv apache-maven-3.3.9 /usr/local/
ln -s /usr/local/apache-maven-3.3.9/ /usr/local/maven
/usr/local/maven/bin/mvn -v
```

3. 编辑/etc/profile文件，在末尾添加

```
export PATH=/usr/local/apache-maven-3.3.9/bin/:$PATH
```

> 配置好 maven后

- 上传 hello-world.tar.gz 至 用户根目录 并解压
- `sudo yum -y install tree` 安装 tree命令

```
cd~/hello-world

# 打包命令，它会下载 依赖的jar包 在 .m2 目录里 如果 .m2已经存在就不再下载
mvn package
# 打包后 会生成 target文件夹 里面有对面的jar包

# 清除上次打包的内容重新打包
mvn clean package
```

#### maven 相关概念参考

- https://github.com/slTrust/javaweb/


