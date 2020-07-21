# Typical Linux commands for finding, listing, and checking memory usage of files

## Find files and directories with find command
```bash
find [where to start searching from] [expression determines what to find] [-options] [what to find]
```
* [expression determines what to find] can be file, folder, name, creation day, modification day owner or permissions.

For example, to find xyz.ER from current directory or its subdirectories, one could run 
```bash
find . -name xyz.ER
```
* . = current directory
* -name = find names (directories or files)
* xyz.ER = file we are searching

If one wants to find all text files in subdirectory 'annotations' of the current directory, one could write
```bash
find ./annotations -name *.txt
```

Empty files in annotations directory can be found with command
```bash
find ./annotations -empty
```

Find all python files from current directory and its subdirectories by user tijarvin
```bash
find -user tijarvin -name "*.py"
```

Find all files modified in the last 24 hours

```bash
find -mtime -1
```
* -mtime = Search by modification date
* -1 = Changed 1 day or less ago (+1 = 1 day or more ago)

Exec command can be used with find to execude commands on found files. 
```bash
find ./annotations -name *.txt -exec rm -i {} \;
```
* rm = remove file
* -i = Interactive delete, user confirms every delete with Y/y
* {} = pass every found file as an argument to exec command rm
* \ = Escape next character, which ends exec command instead of being part of it
* ; = End exec command

And if you want to find texts with certain patterns from all text files, you can use for example
```bash
find ./ -type f -name "*.txt" -exec grep 'chr1' {} \;
```
* ./ = current directory and its subdirectories
* -type f = Search only files
* grep 'chr1' = find and print lines that contain 'chr1' in found files

Most examples are from website https://www.geeksforgeeks.org/find-command-in-linux-with-examples/


## List files and directories with ls command

If you want to list all files and directories in current directory, write
```bash
ls
```

You can specify listing with commands
* ```ls -F``` = Add character / to the end of each listed directory
* ```ls -a`` = List also hidden files starting with '.'
* ```ls -ltr``` = List by modification date (r = List in reverse order)
* ```ls -lS``` = List sorted by size
* ```ls -F -a -ltr``` = Add / to the end of each listed directory, also list hidden files, reverse order by modification date
* ```ls --help``` = More listing options

If you want to list files in current directory one file below another with long listing information
```bash
ls -l
```

In the result there could be for example
```bash
drwxrws---  2 mkankain sg_mustjoki    8192 Mar  4 22:39 annovar_all
drwxrws---  2 mkankain sg_mustjoki   28672 Mar 29 13:33 annovar_org
```

* First column (drwxrws---) is file type and permissions. For example in drwxrws--- first letter d indicates directory.
- would be a file, s would be socket file and l would be a link. First 3 letters after d are user (your) permissions,
next three are group (sg_mustjoki) permissions, last 3 are global (all cluster users) permissions. r = read, w = write,
x/s = execute, - = No permissions.
* Next column (2) is number of links for that file or directory.
* Third column (mkankain) is the owner of that file or directory
* Fourth column (sg_mustjoki) is the group
* Fifth column (8192) is the size. With ```ls -lh``` size would be in human readable form, 8.0K
* Next columns specify last modification date of that file or directory
* Last column (annovar_all) is the name of that file

## Check disk space with
```bash
df
```

Again, options can be added
* -a = Display all file system disk space usage
* -h = disk space in human readable form (GB)
* -kh / --block-size=1K -h = Display memory in 1024-byte blocks
* -mh = Memory in Mega bytes, human readable form
* /path/to/example_directory = Memory usage in example_directory
* --help = All available options


## Check memory usage of files, directories and subdirectories with
```bash
du
```
Again, options can be added
* -sh = Summary of total disk usage of an directory
* -a = Display all file system disk space usage
* -h = disk space in human readable form (GB)
* -k / --block-size=1K = Display memory in 1024-byte blocks
* -mh = Memory in Mega bytes
* -c = Print total disk usage on the last line
* --exclue="*.txt" = Exclude all text files
* /path/to/example_directory = Memory usage in example_directory
* --help = All available options

## Print only output lines containing certain patterns with
```bash
grep
```
You can pipe commands to grep if you want to pick only certain lines from output. If you want to list for example all files and directories you have permission to read, you can write
```bash
ls -l | grep '^.r'
```
* | = Give output as an argument to next command
* ^ = In the beginning of line
* . = Any character (We don't care if it's - (file), d (directory) or l (link)
* r = character r (permission to read)

Or if you want all edited in May
```bash
ls -l | grep '\sMay\s'
```
* \s = space

grep can be used with any output.
