 # unpack-file 
GIT-UNPACK-FILE(1)                                                                                Git Manual                                                                               GIT-UNPACK-FILE(1)

NAME
       git-unpack-file - Creates a temporary file with a blob's contents

SYNOPSIS
       git unpack-file <blob>

DESCRIPTION
       Creates a file holding the contents of the blob specified by sha1. It returns the name of the temporary file in the following format: .merge_file_XXXXX

OPTIONS
       <blob>
           Must be a blob id

GIT
       Part of the git(1) suite

Git 2.18.2                                                                                        01/03/2020                                                                               GIT-UNPACK-FILE(1)
