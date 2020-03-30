# Command: RUNUSER

runuser命令使用指定的用户或在用户组运行Shell。一般情况下仅root用户可以使用（其它用户使用此命令的时候，需要设置 setuid，否则运行失败），使用 runuser命令不需要进行用户身份认证，因此系统开销比su低。

 ## 使用说明：
   
   runuser [OPTION]... [-] [USER [ARG]...]

 - 参数：

    -, -l, --login

    给定执行shell环境的用户，如果没有给定参数，则表示使用的是root用户

    -g --group=group
    给定执行sell环境的主用户组 

    -G --supp-group=group
给定执行sell环境的补充用户组 

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

1. 非root用户执行会报错

     [Anson@workstation ~]$ runuser - -c ls 
     
     runuser: may not be used by non-root users
2. 不提供用户名的时候缺省表示 root用户，反之是给定用户

     [root@workstation ~]# runuser - -c whoami
      
      root

     [root@workstation ~]# runuser -l Anson -c whoami

      Anson
 


