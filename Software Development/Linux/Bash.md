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