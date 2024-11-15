### Bash script with args

#### Question 12

On ServerA, create a Bash script named /script.sh that outputs the second argument followed by the first argument when executed with two arguments
(e.g., "test2 test1" for ./script.sh test1 test2).


<details><summary>Solution</summary>

1. Create the following script "/script.sh":

    #!/bin/bash 
    if [ $# -eq 2 ]; 
      then  echo "$2 $1"
    else  
      echo "Usage: $0 argument1 argument2"  
      exit 1
    fi

2. Make the script executable by running:
```
$ sudo chmod +x /script.sh
```

3. Verify by running:
```
$ ./script.sh test1 test2
```

This will output "test2 test1" in the terminal.


Explanation:  

    ```
    if [ $# -eq 2 ]
    ```

    This line checks if the script received exactly two arguments using the $# special variable that holds the number of arguments passed.

    ```
    echo "$2 $1"
    ```
    If two arguments are provided, this line prints the second argument followed by a space and then the first argument.

    ```
    else
    ```
    If not exactly two arguments are provided, the script displays a usage message and exits with an error code (1).
    $0: This refers to the script's filename itself.


   This script handles errors by informing the user about the expected number of arguments.

</details>

