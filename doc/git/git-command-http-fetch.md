 # http-fetch 
GIT-HTTP-FETCH(1)                                                                                 Git Manual                                                                                GIT-HTTP-FETCH(1)

NAME
       git-http-fetch - Download from a remote Git repository via HTTP

SYNOPSIS
       git http-fetch [-c] [-t] [-a] [-d] [-v] [-w filename] [--recover] [--stdin] <commit> <url>

DESCRIPTION
       Downloads a remote Git repository via HTTP.

       This command always gets all objects. Historically, there were three options -a, -c and -t for choosing which objects to download. They are now silently ignored.

OPTIONS
       commit-id
           Either the hash or the filename under [URL]/refs/ to pull.

       -a, -c, -t
           These options are ignored for historical reasons.

       -v
           Report what is downloaded.

       -w <filename>
           Writes the commit-id into the filename under $GIT_DIR/refs/<filename> on the local end after the transfer is complete.

       --stdin
           Instead of a commit id on the command line (which is not expected in this case), git http-fetch expects lines on stdin in the format

               <commit-id>['\t'<filename-as-in--w>]

       --recover
           Verify that everything reachable from target is fetched. Used after an earlier fetch is interrupted.

GIT
       Part of the git(1) suite

Git 2.18.2                                                                                        01/03/2020                                                                                GIT-HTTP-FETCH(1)
