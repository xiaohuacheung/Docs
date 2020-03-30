# 构建Java 应用程序


## Gradle 概念

### Projects 和 tasks
Gradle 里的任何东西都是基于这两个基础概念:

    projects ( 项目 )
    tasks ( 任务 )
每一个构建都是由一个或多个 projects 构成的. 一个 project 到底代表什么取决于你想用 Gradle 做什么. 举个例子, 一个 project 可以代表一个 JAR 或者一个网页应用. 它也可能代表一个发布的 ZIP 压缩包, 这个 ZIP 可能是由许多其他项目的 JARs 构成的. 但是一个 project 不一定非要代表被构建的某个东西. 它可以代表一件**要做的事, 比如部署你的应用.

不要担心现在看不懂这些说明. Gradle 的合约构建可以让你来具体定义一个 project 到底该做什么.

每一个 project 是由一个或多个 tasks 构成的. 一个 task 代表一些更加细化的构建. 可能是编译一些 classes, 创建一个 JAR, 生成 javadoc, 或者生成某个目录的压缩文件.

目前, 我们先来看看定义构建里的一些简单的 task. 以后的章节会讲解多项目构建以及如何通过 projects 和 tasks 工作.








## Gradle 的守护进程
Gradle 守护进程是一个后台进程, 它运行着繁重的构建, 然后在构建等待下一次构建的之间保持自身存在. 这使得数据和代码在下一次构建前已经准备好,并存入内存中. 这显著的提高了后续构建的性能. 启用Gradle守护进程是一种节约构建时间的廉价方式.

强烈建议在所有开发机器上启用Gradle的守护进程.但是不推荐在持续集成和构建服务器环境下启用守护进程
