# Work with Bash

Work with Bash in Linux environment

## Bash commands

### A. Work with file

1. Find all files with specific extension:
```
$(find ./ -name "$fileExt")

```
It can go with `wc` to count all lines of all files with specific extension likes this:
```
$(find ./ -name "$fileExt") | xargs wc -l

```

2. Combine/Redirect output from two commands or more:

```
$(command1 ; command2) | cat
```
Example:
```
(cat fileA.txt; cat fileB.txt) | cat
```

3. Save output to a variable:

```
myVar=$(mycommand)
```
Example:
```
myVar=$(cat myfile.txt)
```
Then you can access it:
```
echo $myVar
```

For reading content and save ouput to a variable we can simple do this:

```
myVar=$(<./myFile)
```

4. Concat variable and string:

We can use template string like this:

```
"${protocol}google.com"
```

## Shell scripts

### A. Something basic

1. Passing parameters to your bash script:
```
./myScript.sh myParameter1 myParameter2
```
When we want to use ```myParameter1``` or ```myParameter2```, simple we use ```$1``` or ```$2``` 

Example we have `myScript.sh` file
```
#!/bin/bash

echo "My first parameter: $1"
# it should print myParameter1

echo "My second parameter: $2"
# it should print myParameter2

```

2. Loop by line or space in a text file:

```
values=$(<./textFile)
# note: $values does not have double quote here
for i in $values; do
  echo "$i"
done
```


### B. Something magic when work with bash

1. Run parallel command using jobs

Example we have `myFile`:
```
line1
line2
line3
```
We can run parallel command using `&`.

File `myParallelScript.sh`:

```
#!/bin/bash

# Read line by line from `myFile`
myVar=$(<./myFile)

for i in $value; do
  command $i &
  # the & will make unique process for each our command
done
wait
echo "Done"
```

Especially we use `wait` here to wait for all jobs done before print "Done"

And we can excute commands after `myParallelScript.sh` done using `&&`, like this:
```
./myParallelScript.sh && ./myAnotherScript.sh
```


