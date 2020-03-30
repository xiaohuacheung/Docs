# Command: SUDO

 ## Description
sudo allows a permitted user to execute a command as another user, according to specifications in the /etc/sudoers file. The real and effective uid and gid of the issuing user are then set to match those of the target user account as specified in the passwd file.

By default, sudo requires that users authenticate themselves with a password. By default, this is the user's password, not the root password itself.

Once a user has been authenticated, a timestamp is recorded and the user may use sudo without a password for a short period of time (5 minutes, unless configured differently in sudoers). This timestamp can be renewed if the user issues sudo with the -v flag.

If a user not listed in sudoers tries to run a command using sudo, it is considered an unsuccessful attempt to breach system security and mail is sent to the proper authorities, as defined at configure time or in the sudoers file. The default authority to be notified of unsuccessful sudo attempts is root. Note that the mail will not be sent if an unauthorized user tries to run sudo with the -l or -v flags; this allows users to determine for themselves whether or not they are allowed to use sudo.

sudo can log both successful and unsuccessful attempts (as well as errors) to syslog, a unique log file, or both. By default, sudo will log to syslog but this can be changed at configure time or in the sudoers file.

To edit the sudoers file, use the visudo command.

## Syntax
sudo -V | -h | -l | -L | -v | -k | -K | -s | [ -H ] [-P ] [-S ] [ -b ] | 
     [ -p prompt ] [ -c class|- ] [ -a auth_type ] [-r role ] [-t type ] 
     [ -u username|#uid ] command
## Options
   
    -V	
    
    The -V (version) option causes sudo to print the version number and exit. If the invoking user is already root, the -V option will print out a list of the defaults sudo was compiled with as well as the machine's local network addresses.
   
    -l	
    
    The -l (list) option will print out the commands allowed (and forbidden) the user on the current host.
   
    -L	
    
    The -L (list defaults) option will list out the parameters that may be set in a Defaults line along with a short description for each. This option is useful in conjunction with grep.
   
    -h	
    
    The -h (help) option causes sudo to print a usage message and exit.
  
    -v	
    
    If given the -v (validate) option, sudo will update the user's timestamp, prompting for the user's password if necessary. This extends the sudo timeout for another 5 minutes (or whatever the timeout is set to in sudoers) but does not run a command.
    
    -k	
    
    The -k (kill) option to sudo invalidates the user's timestamp by setting the time on it to the epoch. The next time sudo is run a password will be required. This option does not require a password and was added to allow a user to revoke sudo permissions from a .logout file.
    
    -K	
    
    The -K (sure kill) option to sudo removes the user's timestamp entirely. Likewise, this option does not require a password.
   
    -b	
    
    The -b (background) option tells sudo to run the given command in the background. Note that if you use the -b option you cannot use shell job control to manipulate the process.
   
    -p
    
    	The -p (prompt) option allows you to override the default password prompt and use a custom one. The following percent ('%') escapes are supported:

        %u is expanded to the invoking user's login name;

        %U is expanded to the login name of the user the command will be run as (which defaults to root);

        %h is expanded to the local hostname without the domain name;

        %H is expanded to the local hostname including the domain name (only if the machine's hostname is fully qualified or the "fqdn" sudoers option is set);

        %% (two consecutive % characters) are collapsed into a single % character.
   
    -c	
    
    The -c (class) option causes sudo to run the specified command with resources limited by the specified login class. The class argument can be either a class name as defined in /etc/login.conf, or a single '-' character. Specifying a class of - indicates that the command should be run restricted by the default login capabilities for the user running the command. If the class argument specifies an existing user class, the command must be run as root, or the sudo command must be run from a shell that is already root. This option is only available on systems with BSD login classes where sudo has been configured with the --with-logincap option.
   
    -a	
    
    The -a (authentication type) option causes sudo to use the specified authentication type when validating the user, as allowed by /etc/login.conf. The system administrator may specify a list of sudo-specific authentication methods by adding an "auth-sudo" entry in /etc/login.conf. This option is only available on systems that support BSD authentication where sudo has been configured with the --with-bsdauth option.
    
    -u	
    
    The -u (user) option causes sudo to run the specified command as a user other than root. To specify a uid instead of a username, use #uid.
    
    -s	
    
    The -s (shell) option runs the shell specified by the SHELL environment variable if it is set or the shell as specified in the file passwd.
    
    -H	
    
    The -H (HOME) option sets the HOME environment variable to the home directory of the target user (root by default) as specified in passwd. By default, sudo does not modify HOME.
   
    -P	
    
    The -P (preserve group vector) option causes sudo to preserve the user's group vector unaltered. By default, sudo will initialize the group vector to the list of groups of the target user. The real and effective group IDs, however, are still set to match the target user.
   
    -r	
    
    The -r (role) option causes the new (SELinux) security context to have the role specified by ROLE.
    -t	
    
    The -t (type) option causes the new (SELinux) security context to have the have the type (domain) specified by TYPE. If no type is specified, the default type is derived from the specified role.
    
    -S	
    
    The -S (stdin) option causes sudo to read the password from standard input instead of the terminal device.
   
    --	
    
    The -- flag indicates that sudo should stop processing command line arguments. It is most useful in conjunction with the -s flag.
## Return Values
Upon successful execution of a program, the return value from sudo will be the return value of the program that was executed.

Otherwise, sudo quits with an exit value of 1 if there is a configuration/permission problem or if sudo cannot execute the given command. In the latter case the error string is printed to stderr. If sudo cannot stat one or more entries in the user's PATH an error is printed on stderr. (If the directory does not exist or if it is not really a directory, the entry is ignored and no error is printed.) This should not happen under normal circumstances. The most common reason for stat to return "permission denied" is if you are running an auto-mounter and one of the directories in your PATH is on a machine that is currently unreachable.