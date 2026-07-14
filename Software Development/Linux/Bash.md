Bash (Bourne Again Shell) is a command-line interpreter for Unix/Linux.

# Variables
Define a variable.  
```bash
name="kettle"
```

Use a variable  
```bash
echo $name
```

Use **quotes** when expanding variables.  
```bash
file="my notes.txt"
cat "$file"
```
Without quotes, Bash may split the value at spaces.

Use `${var}` when the variable name needs to be separated from nearby text.  
```bash
name="txt"
echo "${name}_file"
```

# Bash Script
A **bash script** is a text file containing commands that are executed by Bash.

E.g.
```bash
#!/usr/bin/env bash

echo "Hello"
```

The first line:
```bash
#!/usr/bin/env bash
```
is called the **shebang**.
- `#!` marks the line as the shebang.
- The shebang tells the operating system which interpreter it should use to run this file.
- The shebang only matters when the script is run directly.
## Run
Run by passing the script to Bash.
```shell
bash script.sh
```
The file needs **read** permission.

Run directly.
```shell
./script.sh
```
The file need both **read** and **execute** permission.