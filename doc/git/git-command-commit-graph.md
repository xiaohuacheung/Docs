 # commit-graph 
GIT-COMMIT-GRAPH(1)                                                                               Git Manual                                                                              GIT-COMMIT-GRAPH(1)

NAME
       git-commit-graph - Write and verify Git commit graph files

SYNOPSIS
       git commit-graph read [--object-dir <dir>]
       git commit-graph write <options> [--object-dir <dir>]

DESCRIPTION
       Manage the serialized commit graph file.

OPTIONS
       --object-dir
           Use given directory for the location of packfiles and commit graph file. This parameter exists to specify the location of an alternate that only has the objects directory, not a full .git
           directory. The commit graph file is expected to be at <dir>/info/commit-graph and the packfiles are expected to be in <dir>/pack.

COMMANDS
       write
           Write a commit graph file based on the commits found in packfiles.

           With the --stdin-packs option, generate the new commit graph by walking objects only in the specified pack-indexes. (Cannot be combined with --stdin-commits.)

           With the --stdin-commits option, generate the new commit graph by walking commits starting at the commits specified in stdin as a list of OIDs in hex, one OID per line. (Cannot be combined with
           --stdin-packs.)

           With the --append option, include all commits that are present in the existing commit-graph file.

       read
           Read a graph file given by the commit-graph file and output basic details about the graph file. Used for debugging purposes.

EXAMPLES
       ·   Write a commit graph file for the packed commits in your local .git folder.

               $ git commit-graph write

       ·   Write a graph file, extending the current graph file using commits

       ·   in <pack-index>.

               $ echo <pack-index> | git commit-graph write --stdin-packs

       ·   Write a graph file containing all reachable commits.

               $ git show-ref -s | git commit-graph write --stdin-commits

       ·   Write a graph file containing all commits in the current

       ·   commit-graph file along with those reachable from HEAD.

               $ git rev-parse HEAD | git commit-graph write --stdin-commits --append

       ·   Read basic information from the commit-graph file.

               $ git commit-graph read

GIT
       Part of the git(1) suite

Git 2.18.2                                                                                        01/03/2020                                                                              GIT-COMMIT-GRAPH(1)
