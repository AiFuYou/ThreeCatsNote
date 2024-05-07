要在Jenkins流水线中编写脚本来获取所有节点信息，包括节点名称、节点可执行的任务数量以及最大可执行的任务数量，可以使用Jenkins的Groovy脚本功能来实现。以下的流水线脚本演示了如何获取这些信息：

```groovy
pipeline {
    agent any
    stages {
        stage('Get Nodes Info') {
            steps {
                script {
                    // 获取所有节点，包括master节点
                    def allNodes = Jenkins.instance.nodes
                    // 遍历每个节点
                    allNodes.each { node ->
                        // 获取节点的名称
                        def nodeName = node.nodeName == '' ? 'master' : node.nodeName
                        // 获取节点的计算器,这决定了节点能并行执行多少个任务
                        def nodeExecutors = node.numExecutors
                        // 获取总任务数 (当前节点上的构建队列)
                        def totalTasks = node.queue.items.length
                        // 获取当前正在运行的任务数
                        def runningTasks = node.executors.findAll{!it.idle}.size()
                        // 打印信息
                        println("节点名称: ${nodeName}")
                        println("最大可执行任务数量: ${nodeExecutors}")
                        println("当前排队的任务数量: ${totalTasks}")
                        println("当前正在执行的任务数量: ${runningTasks}")
                        println("---------------------------------")
                    }
                }
            }
        }
    }
}
```

要运行这个脚本，请注意以下几点：

1. 这个脚本使用了Jenkins的内部API，这意味着需要Jenkins管理员权限才能正确执行。
2. 如果在沙盒环境中执行脚本，可能需要管理员批准相关的脚本方法使用。
3. `Jenkins.instance` 可能因为安全控制而不被允许直接使用，这就需要配置脚本安全插件，允许使用这些方法。

安装并配置好必要的权限和插件后，您可以将上述代码保存在Jenkins流水线的Jenkinsfile中或直接在流水线脚本内执行。

流水线脚本会遍历所有节点（包含master节点），并打印出每个节点的名字、最大可执行任务数量、当前排队的任务数量以及当前正在执行的任务数量。可能需要针对您的具体环境细节进行相应的调整。
