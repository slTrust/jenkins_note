### jenkins 核心目录，jenkins一切皆文件

用 `rpm -ql jenkins` 查看相关的文件目录

```
/etc/init.d/jenkins
/etc/logrotate.d/jenkins
# 配置文件目录
/etc/sysconfig/jenkins
/usr/lib/jenkins  
# jenkins 的程序文件，你升级的时候 替换这个 war包即可
/usr/lib/jenkins/jenkins.war
/usr/sbin/rcjenkins
/var/cache/jenkins
/var/lib/jenkins
# 日志
/var/log/jenkins
```

- `/etc/sysconfig/jenkins`  配置文件目录

```
# jenkins的主目录 ，jenkins一切皆文件，所有文件都在这
JENKINS_HOME
# 默认监听端口
JENKINS_PORT 
```