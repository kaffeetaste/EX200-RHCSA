### Find task

#### Question
On ServerB, find the regular files owned by the user root in the “/usr/bin” and copy the files into the “/find/rootfiles/” directory.

<details><summary>Solution</summary>

1. To create a new directory named “rootfiles” inside the “/find” directory, run:
```
# mkdir -p /find/rootfiles
```
The "-p" option makes sure that any parent directories that don't already exist are also created.


2. To search for all the files in the “/usr/bin” directory that are owned by the root user and copy them to the “/find/rootfiles” directory, run:
```
# find /usr/bin/ -type f -user root -exec cp {} /find/rootfiles/ \;
```

Here is what each part of the command does:

    find /usr/bin/:   
    starts the search in the /usr/bin directory

    -type f:   
    specifies that only regular files should be searched

    -user root:   
    filters the results to only include files owned by the root user

    -exec cp {} /find/rootfiles/ \;:   
    executes the cp command to copy each file found to the /find/rootfiles directory. 
    The curly braces {} are replaced with the name of each file found by the find command. The backslash before the semicolon 
    is used to escape the semicolon, which is required to terminate the -exec command.

3. To list the contents of the directory "/find/rootfiles/" in a long format, run:
```
# ls -l /find/rootfiles/ 
```
</details>