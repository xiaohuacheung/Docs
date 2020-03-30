# Command: SU

   su命令可切换至其他用户(超级用户或普通用户)执行命令。如果没有设置sudoers 如果您知道目标用户的密码，它允许Linux用户更改与正在运行的consol或shell的当前用户帐户。 语法如下：

 ## 使用说明：
   
   su [OPTION]... [-] [USER [ARG]...]

 - 参数：

    -, -l, --login

    给定执行shell环境的用户，如果没有给定参数，则表示使用的是root用户
 
     -c, --command=COMMAND
    执行的具体命令，执行完成后，并创建会话

    --session-command=COMMAND
    执行的具体命令，执行完成后，但是并不创建会话

     -f, --fast
     传递“-f” 给 shell 环境，启动 sell的fast模式（仅对 csh和 tcsh又用，fast模式下这两个shell启动的时候不会调用者主目录中的.cshrc文件并搜索和执行命令里面的初始化命令，常用的 bash、ksh 不用处理这个参数，甚至会报错）

     -m, --preserve-environment
      不重置环境变量，继续沿用当前的上下文环境变量,不可以与 “-”，“-l”,“--login” 同时使用

     -p
      与 -m 参数一致

     -s, --shell=SHELL
      如果/etc/shells里面罗列了的话，则运行给定的shell

      --help
      显示帮助信息并退出

      --version
      显示版本信息并退出

 

## 举例示范：