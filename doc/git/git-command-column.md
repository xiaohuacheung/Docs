 # column 
GIT-COLUMN(1)                                                                                     Git Manual                                                                                    GIT-COLUMN(1)

NAME
       git-column - Display data in columns

SYNOPSIS
       git column [--command=<name>] [--[raw-]mode=<mode>] [--width=<width>]
                    [--indent=<string>] [--nl=<string>] [--padding=<n>]

DESCRIPTION
       This command formats its input into multiple columns.

OPTIONS
       --command=<name>
           Look up layout mode using configuration variable column.<name> and column.ui.

       --mode=<mode>
           Specify layout mode. See configuration variable column.ui for option syntax.

       --raw-mode=<n>
           Same as --mode but take mode encoded as a number. This is mainly used by other commands that have already parsed layout mode.

       --width=<width>
           Specify the terminal width. By default git column will detect the terminal width, or fall back to 80 if it is unable to do so.

       --indent=<string>
           String to be printed at the beginning of each line.

       --nl=<N>
           String to be printed at the end of each line, including newline character.

       --padding=<N>
           The number of spaces between columns. One space by default.

GIT
       Part of the git(1) suite

Git 2.18.2                                                                                        01/03/2020                                                                                    GIT-COLUMN(1)
