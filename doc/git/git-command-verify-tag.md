 # verify-tag 
GIT-VERIFY-TAG(1)                                                                                 Git Manual                                                                                GIT-VERIFY-TAG(1)

NAME
       git-verify-tag - Check the GPG signature of tags

SYNOPSIS
       git verify-tag [--format=<format>] <tag>...

DESCRIPTION
       Validates the gpg signature created by git tag.

OPTIONS
       --raw
           Print the raw gpg status output to standard error instead of the normal human-readable output.

       -v, --verbose
           Print the contents of the tag object before validating it.

       <tag>...
           SHA-1 identifiers of Git tag objects.

GIT
       Part of the git(1) suite

Git 2.18.2                                                                                        01/03/2020                                                                                GIT-VERIFY-TAG(1)
