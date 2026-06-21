List the files and directories in a directory.  
```shell
ls [path]
```
Options:  
- `-l`: Show files in long listing format with details.
	- Permissions.
	- Owner.
	- Size.
	- Modified time.
- `-a`: Show all files, including hidden files whose name start with `.`.
- `-d`: Show the **directory itself** instead of listing its contents.

E.g.  
```shell
ls -l file.txt
```
Output:  
```
-rw-r--r--  1 user  staff  1234 May 27 19:30 file.txt
```
Meaning:  
```
-rw-r--r--   file type + permissions
1            number of hard links
user         owner
staff        group
1234         file size in bytes
May 27 19:30 last modified time
file.txt     file/directory name
```

The first character shows **file type**:  
- `d`: Directory.
- `l`: Symbolic link.
- `-`: Regular file.

The next nine characters shows **permissions**:  
```
rw- r-- r--
│   │   │
│   │   others' permissions
│   group's permissions
owner's permissions
```
- `r`: Read.
- `w`: Write.
- `x`: Execute file/enter directory.
- `-`: Permission not granted.

`ls` uses colors to visually distinguish file types and permissions. The exact colors depend on your shell. Common colors include:  
- White: Regular file.
- Green: Executable file.
- Blue: Directory.