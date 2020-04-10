 # clone 

## NAME

git-clone - Clone a repository into a new directory
>将存储库克隆到新目录

## SYNOPSIS  语法
       git clone [--template=<template_directory>]
                 [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
                 [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
                 [--dissociate] [--separate-git-dir <git dir>]
                 [--depth <depth>] [--[no-]single-branch] [--no-tags]
                 [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
                 [--jobs <n>] [--] <repository> [<directory>]

## DESCRIPTION
>Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository (visible using git branch -r), and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

>将存储库克隆到新创建的目录中，为克隆的存储库中的每个分支创建远程跟踪分支（使用git branch -r可见），并创建并签出初始从克隆的存储库的当前活动分支派生的分支。

>After the clone, a plain git fetch without arguments will update all the remote-tracking branches, and a git pull without arguments will in addition merge the remote master branch into the current master branch, if any (this is untrue when "--single-branch" is given; see below).

>克隆之后，不带参数的纯git fetch将更新所有远程跟踪分支，并且不带参数的git pull将另外将远程master分支合并到当前的master分支中（如果有的话，这是不正确的（当“ --single -branch”；请参见下文）。


>This default configuration is achieved by creating references to the remote branch heads under refs/remotes/origin and by initializing remote.origin.url and remote.origin.fetch configuration variables.
 
>通过在refs / remotes / origin下创建对远程分支头的引用并初始化remote.origin.url和remote.origin.fetch配置变量来实现此默认配置。

## OPTIONS 参数

**--local, -l**

>When the repository to clone from is on a local machine, this flag bypasses the normal "Git aware" transport mechanism and clones the repository by making a copy of HEAD and everything under objects and refs directories. The files under .git/objects/ directory are hardlinked to save space when possible.

>当要从中进行克隆的存储库位于本地计算机上时，此标志将绕过常规的“ Git感知”传输机制，并通过在对象和引用目录下创建HEAD以及所有内容的副本来克隆存储库。 .git / objects /目录下的文件被硬链接以尽可能节省空间。

>If the repository is specified as a local path (e.g., /path/to/repo), this is the default, and --local is essentially a no-op. If the repository is specified as a URL, then this flag is ignored (and we never use the local optimizations). Specifying --no-local will override the default when /path/to/repo is given, using the regular Git transport instead.

>如果将存储库指定为本地路径（例如/ path / to / repo），则这是默认设置，而--local本质上是无操作的。 如果将存储库指定为URL，则将忽略此标志（并且我们永远不会使用本地优化）。 当给出/ path / to / repo时，指定--no-local将覆盖默认值，而使用常规Git传输。

**--no-hardlinks**

>Force the cloning process from a repository on a local filesystem to copy the files under the .git/objects directory instead of using hardlinks. This may be desirable if you are trying to make a back-up of your repository.

>强制从本地文件系统上的存储库进行克隆过程，以复制.git / objects目录下的文件，而不使用硬链接。 如果您要备份存储库，则可能需要这样做。

**--shared, -s**

>When the repository to clone is on the local machine, instead of using hard links, automatically setup .git/objects/info/alternates to share the objects with the source repository. The resulting repository starts out without any object of its own.

>当要克隆的存储库位于本地计算机上时，而不是使用硬链接，而是自动设置.git / objects / info / alternates与源存储库共享对象。 生成的存储库开始时没有其自己的任何对象。

>NOTE: this is a possibly dangerous operation; do not use it unless you understand what it does. If you clone your repository using this option and then delete branches (or use any other Git command that makes any existing commit unreferenced) in the source repository, some objects may become unreferenced (or dangling). These objects may be removed by normal Git operations (such as git commit) which automatically call git gc --auto. (See git-gc(1).) If these objects are removed and were referenced by the cloned repository, then the cloned repository will become corrupt.

>**注意**:这可能是危险的操作； 除非您了解它的功能，否则请勿使用它。 如果使用此选项克隆存储库，然后在源存储库中删除分支（或使用任何其他Git命令使所有现有提交变为未引用），则某些对象可能会变为未引用（或悬空）。 这些对象可以通过自动调用git gc --auto的常规Git操作（例如git commit）删除。 （请参见git-gc（1）。）如果删除了这些对象并由克隆的存储库引用了这些对象，则克隆的存储库将损坏。

>Note that running git repack without the -l option in a repository cloned with -s will copy objects from the source repository into a pack in the cloned repository, removing the disk space savings of clone -s. It is safe, however, to run git gc, which uses the -l option by default.

>**请注意**，在用-s克隆的存储库中运行不带-l选项的git repack会将对象从源存储库复制到克隆的存储库中的数据包中，从而节省了克隆-s的磁盘空间。 但是，运行git gc是安全的，默认情况下使用-l选项。

>If you want to break the dependency of a repository cloned with -s on its source repository, you can simply run git repack -a to copy all objects from the source repository into a pack in the cloned repository.

>如果要打破在源存储库中用-s克隆的存储库的依赖性，只需运行git repack -a即可将源存储库中的所有对象复制到克隆存储库中的包中。

**--reference[-if-able] \<repository\>**

>If the reference repository is on the local machine, automatically setup .git/objects/info/alternates to obtain objects from the reference repository. Using an already existing repository as an alternate will require fewer objects to be copied from the repository being cloned, reducing network and local storage costs. When using the --reference-if-able, a non existing directory is skipped with a warning instead of aborting the clone.

>如果参考存储库位于本地计算机上，则自动设置.git / objects / info / alternates从参考存储库获取对象。 使用现有的存储库作为备用存储库将需要从要克隆的存储库中复制较少的对象，从而降低了网络和本地存储成本。 使用--reference-if-able时，系统会通过警告跳过不存在的目录，而不是中止克隆。

>NOTE: see the NOTE for the --shared option, and also the --dissociate option.

>**注意**：有关--shared选项以及--dissociate选项的信息，请参阅注释。

**--dissociate**

>Borrow the objects from reference repositories specified with the --reference options only to reduce network transfer, and stop borrowing from them after a clone is made by making necessary local copies of borrowed objects. This option can also be used when cloning locally from a repository that already borrows objects from another repository—the new repository will borrow objects from the same repository, and this option can be used to stop the borrowing.

>从使用--reference选项指定的参考存储库中借用对象仅是为了减少网络传输，并在复制后通过制作借用对象的必要本地副本来停止从对象借用。 从已经从另一个存储库借用对象的存储库进行本地克隆时，也可以使用此选项-新存储库将从同一个存储库借用对象，并且该选项可用于停止借用。



**--quiet, -q**

>Operate quietly. Progress is not reported to the standard error stream.

>安静地操作。 进展不会报告给标准错误流。

**--verbose, -v**

>Run verbosely. Does not affect the reporting of progress status to the standard error stream.

>详细地运行。 不影响向标准错误流报告进度状态。

**--progress**

>Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

>除非指定了-q，否则默认情况下，将状态错误报告到标准错误流时，将在标准错误流上报告该状态。 即使标准错误流未定向到终端，该标志也会强制显示进度状态。

**--no-checkout, -n**

>No checkout of HEAD is performed after the clone is complete.

>克隆完成后，不执行HEAD检出操作。

**--bare**

>Make a bare Git repository. That is, instead of creating \<directory\> and placing the administrative files in \<directory\>/.git, make the \<directory\> itself the $GIT_DIR. This obviously implies the -n because there is nowhere to check out the working tree. Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are created.

>制作一个裸露的Git存储库。 也就是说，不要创建\<directory\>并将管理文件放置在\<directory\> /.git中，而是将\<directory\>本身设置为$GIT_DIR。 显然，这意味着-n，因为没有地方可以检出工作树。 同样，远程的分支头也直接复制到相应的本地分支头，而无需将其映射到ref/remotes/origin/。 使用此选项时，不会创建远程跟踪分支或相关的配置变量。

**--mirror**

>Set up a mirror of the source repository. This implies --bare. Compared to --bare, --mirror not only maps local branches of the source to local branches of the target, it maps all refs(including remote-tracking branches, notes etc.) and sets up a refspec configuration such that all these refs are overwritten by a git remote update in the target repository.

>设置源存储库的镜像。 这意味着-裸露。 与--bare相比，--mirror不仅将源的本地分支映射到目标的本地分支，还映射所有引用（包括远程跟踪分支，注释等），并设置一个refspec配置，以便所有这些引用 被目标存储库中的git远程更新覆盖。

**--origin \<name\>, -o \<name\>**

Instead of using the remote name origin to keep track of the upstream repository, use \<name\>.

不要使用远程名称来源来跟踪上游存储库，而应使用\<name\>。

**--branch \<name\>, -b \<name\>**

>Instead of pointing the newly created HEAD to the branch pointed to by the cloned repository’s HEAD, point to <name> branch instead. In a non-bare repository, this is the branch that will be checked out.  --branch can also take tags and detaches the HEAD at that commit in the resulting repository.

>不要将新创建的HEAD指向克隆存储库的HEAD所指向的分支，而是指向<name>分支。 在非裸仓库中，这是将被检出的分支。 --branch还可以获取标签并在结果存储库中的提交时分离HEAD。

**--upload-pack \<upload-pack\>, -u \<upload-pack\>**

>When given, and the repository to clone from is accessed via ssh, this specifies a non-default path for the command run on the other end.

>如果指定了要克隆的存储库，则可以通过ssh访问该存储库，这将为另一端运行的命令指定非默认路径。

**--template=\<template_directory\>**

>Specify the directory from which templates will be used; (See the "TEMPLATE DIRECTORY" section of git-init(1).)

>指定将使用模板的目录； （请参见git-init（1）的“模板目录”部分。）

**--config <key>=<value>, -c <key>=<value>**

>Set a configuration variable in the newly-created repository; this takes effect immediately after the repository is initialized, but before the remote history is fetched or any files checked out. The key is in the same format as expected by git-config(1) (e.g., core.eol=true). If multiple values are given for the same key, each value will be written to the config file. This makes it safe, for example, to add additional fetch refspecs to the origin remote.

>在新创建的存储库中设置配置变量； 这将在初始化存储库之后，但在获取远程历史记录或签出任何文件之前立即生效。 密钥的格式与git-config（1）预期的格式相同（例如，core.eol = true）。 如果为同一键指定了多个值，则每个值都将写入配置文件。 例如，这可以安全地将其他提取refspec添加到原始远程服务器。

**--depth <depth>**

>Create a shallow clone with a history truncated to the specified number of commits. Implies --single-branch unless --no-single-branch is given to fetch the histories near the tips of all branches. If you want to clone submodules shallowly, also pass --shallow-submodules.

>创建一个浅表克隆，其历史记录被截断为指定的提交数。 表示--single-branch，除非给出--no-single-branch来获取所有分支的尖端附近的历史记录。 如果要浅层克隆子模块，则还要传递--shallow-submodules。

**--shallow-since=\<date\>**

>Create a shallow clone with a history after the specified time.

>在指定的时间之后，创建具有历史记录的浅表克隆。

**--shallow-exclude=\<revision\>**

>Create a shallow clone with a history, excluding commits reachable from a specified remote branch or tag. This option can be specified multiple times.

创建具有历史记录的浅表克隆，不包括可从指定的远程分支或标记到达的提交。 可以多次指定此选项。

**--[no-]single-branch**

>Clone only the history leading to the tip of a single branch, either specified by the --branch option or the primary branch remote’s HEAD points at. Further fetches into the resulting repository will only update the remote-tracking branch for the branch this option was used for the initial cloning. If the HEAD at the remote did not point at any branch when --single-branch clone was made, no remote-tracking branch is created.

>仅克隆通向单个分支顶端的历史记录，该历史记录由--branch选项指定，或者由主分支远程的HEAD指向。 进一步提取到结果存储库中只会将该选项用于初始克隆的分支的远程跟踪分支更新。 如果在进行--single-branch克隆时，远程的HEAD没有指向任何分支，则不会创建远程跟踪分支。

**--no-tags**

>Don’t clone any tags, and set remote.\<remote\>.tagOpt=--no-tags in the config, ensuring that future git pull and git fetch operations won’t follow any tags. Subsequent explicit tag fetches will still work, (see git-fetch(1)).

>不要克隆任何标签，并设置remote。\<remote\> .tagOpt =-配置中没有标签，以确保将来的git pull和git fetch操作不会跟随任何标签。 随后的显式标签获取仍将起作用（请参见git-fetch（1））。

>Can be used in conjunction with --single-branch to clone and maintain a branch with no references other than a single cloned branch. This is useful e.g. to maintain minimal clones of the default branch of some repository for search indexing.

>可以与--single-branch一起使用，以克隆和维护除单个克隆分支外没有其他引用的分支。 这很有用，例如 维护某些存储库的默认分支的最小克隆以进行搜索索引。

**--recurse-submodules[=<pathspec]**

>After the clone is created, initialize and clone submodules within based on the provided pathspec. If no pathspec is provided, all submodules are initialized and cloned. This option can be given multiple times for pathspecs consisting of multiple entries. The resulting clone has submodule.active set to the provided pathspec, or "." (meaning all submodules) if no pathspec is provided.

>创建克隆后，根据提供的pathspec初始化并克隆其中的子模块。 如果未提供pathspec，则将初始化并克隆所有子模块。 对于由多个条目组成的路径规范，可以多次赋予此选项。 所得的克隆将submodule.active设置为提供的pathspec或“。”。 （表示所有子模块）（如果未提供pathspec）。


>Submodules are initialized and cloned using their default settings. This is equivalent to running git submodule update --init --recursive \<pathspec\> immediately after the clone is finished. This option is ignored if the cloned repository does not have a worktree/checkout (i.e. if any of --no-checkout/-n, --bare, or --mirror is given)

>子模块使用其默认设置进行初始化和克隆。 这等效于克隆完成后立即运行git子模块更新--init --recursive \<pathspec\>。 如果克隆的存储库没有工作树/签出（即如果给出了--no-checkout / -n，-bare或--mirror中的任何一个），则忽略此选项

**--[no-]shallow-submodules**

>All submodules which are cloned will be shallow with a depth of 1.

>克隆的所有子模块将变浅，深度为1。
**--separate-git-dir=\<git dir\>**

>Instead of placing the cloned repository where it is supposed to be, place the cloned repository at the specified directory, then make a filesystem-agnostic Git symbolic link to there. The result is Git repository can be separated from working tree.

>与其将克隆的存储库放置在指定的目录中，还不如将克隆的存储库放置在指定的目录中，然后在此处建立与文件系统无关的Git符号链接。 结果是可以将Git存储库与工作树分离。

**-j \<n\>, --jobs \<n\>**

>The number of submodules fetched at the same time. Defaults to the submodule.fetchJobs option.

>同时获取的子模块数。 默认为submodule.fetchJobs选项。

**\<repository\>**

>The (possibly remote) repository to clone from. See the GIT URLS section below for more information on specifying repositories.

>要克隆的（可能是远程的）存储库。 有关指定存储库的更多信息，请参见下面的GIT URLS部分。

**\<directory\>**

>The name of a new directory to clone into. The "humanish" part of the source repository is used if no directory is explicitly given (repo for /path/to/repo.git and foo for host.xz:foo/.git).

>要克隆到的新目录的名称。 如果未明确指定目录，则使用源存储库的“人性化”部分（对于/path/to/repo.git，为repo；对于host.xz：foo / .git，为foo）。

>Cloning into an existing directory is only allowed if the directory is empty.

>仅当目录为空时才允许克隆到现有目录。

## GIT URLS
In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

通常，URL包含有关传输协议，远程服务器的地址以及存储库路径的信息。 根据传输协议，某些信息可能不存在。

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching, but this is inefficient and deprecated; do not use it).

Git支持ssh，git，http和https协议（此外，可以使用ftp和ftps进行获取，但这效率低下且不建议使用；请勿使用它）。

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

本机传输（即git：// URL）不进行身份验证，在不安全的网络上应谨慎使用。

The following syntaxes may be used with them:

以下语法可以与它们一起使用：

- ssh://[user@]host.xz[:port]/path/to/repo.git/
- git://host.xz[:port]/path/to/repo.git/
- http[s]://host.xz[:port]/path/to/repo.git/
- ftp[s]://host.xz[:port]/path/to/repo.git/
  > An alternative scp-like syntax may also be used with the ssh protocol:

  > ssh协议也可以使用类似scp的语法：
- [user@]host.xz:path/to/repo.git/
  >This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path foo:bar could be specified as an absolute path or ./foo:bar to avoid being misinterpreted as an ssh url.

  >只有在第一个冒号之前没有斜杠时才能识别他的语法。 这有助于区分包含冒号的本地路径。 例如，可以将本地路径foo：bar指定为绝对路径，或者将./foo:bar指定为避免被误解为ssh url。

The ssh and git protocols additionally support ~username expansion:

ssh和git协议还支持〜username扩展：

- ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/
- git://host.xz[:port]/~[user]/path/to/repo.git/
- [user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

对于本地存储库（Git本身也支持），可以使用以下语法：

- /path/to/repo.git/
- file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except the former implies --local option.
这两种语法几乎是等效的，除了前者暗含--local选项。

When Git doesn’t know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one exists. To explicitly request a remote helper, the following syntax may be used:

当Git不知道如何处理某种传输协议时，它会尝试使用remote- <transport>远程帮助程序（如果存在）。 要显式请求远程帮助程序，请使用以下语法可能用过了：

-  \<transport\>::\<address\>

>where \<address\> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being invoked. See gitremote-helpers(1) for details.

>其中，\<address\>可以是路径，服务器和路径，也可以是被调用的特定远程帮助程序识别的类似于URL的任意字符串。 有关详细信息，请参见gitremote-helpers（1）。

If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

如果存在大量类似名称的远程存储库，并且您要为它们使用不同的格式（这样，您使用的URL将被重写为有效的URL），则可以创建表单的配置部分：

                   [url "<actual url base>"]
                           insteadOf = <other url base>

       For example, with this:

                   [url "git://git.host.xz/"]
                           insteadOf = host.xz:/path/to/
                           insteadOf = work:

       a URL like "work:repo.git" or like "host.xz:/path/to/repo.git" will be rewritten in any context that takes a URL to be "git://git.host.xz/repo.git".

       If you want to rewrite URLs for push only, you can create a configuration section of the form:

                   [url "<actual url base>"]
                           pushInsteadOf = <other url base>

       For example, with this:

                   [url "ssh://example.org/"]
                           pushInsteadOf = git://example.org/

       a URL like "git://example.org/path/to/repo.git" will be rewritten to "ssh://example.org/path/to/repo.git" for pushes, but pulls will still use the original URL.

## EXAMPLES  范例
       ·   Clone from upstream:

               $ git clone git://git.kernel.org/pub/scm/.../linux.git my-linux
               $ cd my-linux
               $ make

       ·   Make a local clone that borrows from the current directory, without checking things out:

               $ git clone -l -s -n . ../copy
               $ cd ../copy
               $ git show-branch

       ·   Clone from upstream while borrowing from an existing local directory:

               $ git clone --reference /git/linux.git \
                       git://git.kernel.org/pub/scm/.../linux.git \
                       my-linux
               $ cd my-linux

       ·   Create a bare repository to publish your changes to the public:

               $ git clone --bare -l /home/proj/.git /pub/scm/proj.git

