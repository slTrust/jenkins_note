
> 示例1

- 声明式

```
pipeline{
    agent any
    stages{
        stage("get code"){
           steps{
               echo "get code from scm"
           }
        }
        stage("package"){
            steps{
                echo "packge code"
            }
        }
        stage("deploy"){
            steps{
                echo "deploy packge to node1"
            }
        }
    }
}
```

> 脚本式 groovy 语法

```
node {
    stage('Build'){

    }
    stage('Test'){

    }
    stage('Deploy'){

    }
}
```

#### 实战001

- jenkins 新建 My-pipeline-job
- 选择Pipeline
- General 勾选 丢弃旧的构建
    - 保持构建的天数	5
 	- 保持构建的最大个数 5
- Pipeline
    - 脚本里输入
    ```
    pipeline{
        agent any
        stages{
            stage("Build"){
                steps{
                    echo "build"
                }
            }
            stage("Test"){
                steps{
                    echo "test"
                }
            }
            stage("deploy"){
                steps{
                    echo "deploy"
                }
            }
        }
    }
    ```
- 点击保存
- 立刻构建

### 使用 Pipeline 脚本完善 005的功能

- 创建一个 pipeline 的构建
- 选择 你的代码仓库
- 你的git仓库创建 Jenkinsfile 文件放在项目根目录

```
pipeline{
    agent any
    stages{
        stage("get code"){
           steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '06ac7536-b4d0-400f-ae10-fb71cdb266dc', url: 'git@192.168.56.11:oldboy/monitor.git']]])
           }
        }
        stage("package"){
            steps{
                sh 'cd /var/lib/jenkins/workspace/pipeline-job && tar czf /opt/web-$(date +%F).tar.gz .'
            }
        }
        stage("deploy"){
            steps{
                sh 'scp /opt/web-$(date +%F).tar.gz 192.168.56.11:/var/www/html'
                sh 'ssh 192.168.56.11 "cd /var/www/html/&&tar xf web-$(date +%F).tar.gz"'
            }
        }
    }
}
```

#### 不懂里面的语法怎么办

- 你的构建 左侧 Pipeline Syntax 
- 点击 Snippet Generate
- 右侧选择例子 选择 sh Shell Script
- Shell Script 里输入
    ```
    pwd
    ```
- 点击生成  =》 就会得到代码 `sh 'pwd'`
