# Write a System V init script

Init is the program on Unix and Linux systems which spawns all other processes. It runs as a daemon and typically has PID 1. It is the parent of all processes. Its primary role is to create processes from a script stored in the file /etc/inittab file. The main advantages is flexibility and scalability provided by SysV.
The Runlevels in System V describe certain states. For example:

* Runlevel 0: Halt
* Runlevel 1: Single user mode
* Runlevel 6: Reboot

All System V init scripts are stored in /etc/rc.d/init.d/ or /etc/init.d directory. These scripts are used to control system startup and shutdown. Usually you will find scripts to start a web server or networking. For example you type the command:

    # /etc/init.d/httpd start

OR

    # /etc/init.d/network restart

In above example httpd or network are System V scripts written in bash or sh shell. Here is a sample shell script:

    #!/bin/bash
    #
    # chkconfig: 35 90 12
    # description: Foo server
    #

    # Get function from functions library
    . /etc/init.d/functions

    # Start the service FOO
    start() {
            initlog -c "echo -n Starting FOO server: "
            /path/to/FOO &
            ### Create the lock file ###
            touch /var/lock/subsys/FOO
            success $"FOO server startup"
            echo
    }

    # Restart the service FOO
    stop() {
            initlog -c "echo -n Stopping FOO server: "
            killproc FOO
            ### Now, delete the lock file ###
            rm -f /var/lock/subsys/FOO
            echo
    }

    ### main logic ###
    case "$1" in
    start)
            start
            ;;
    stop)
            stop
            ;;
    status)
            status FOO
            ;;
    restart|reload|condrestart)
            stop
            start
            ;;
    *)
            echo $"Usage: $0 {start|stop|restart|reload|status}"
            exit 1
    esac

    exit 0

Above script is specific to Cent OS or Fedora Core/Red Hat Linux. But it should work on all other Linux distro as well. Make sure you replace the FOO name (word/path start with FOO) with actual application name.