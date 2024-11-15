### Scripting

#### Question

On ServerB, write a script "/yes-no.sh" that does the following:
a. If the argument is 'yes', the script should run the command echo “that's nice”.
b. If the argument is 'no', the script should run the command echo "I am sorry to hear that".
c. If the argument is anything else, the script should run the command echo "unknown argument provided".


<details> <summary>Solution</summary>

1. To open the file “/yes-no.sh” for editing using the vim editor, run:

vim /yes-no.sh

2. Add the following lines:
```
    #!/bin/bash
    # check that an argument was provided or exit
    if [ -z $1 ]
    then
    echo you have to provide an argument
    exit 2
    fi
     
    # rewrite all in lowercase
    TEXT=$(echo $1 | tr [:upper:] [:lower:])
     
    # evaluate arguments
    case $TEXT in
    yes)
    echo that\'s nice
    ;;
    no)
    echo i\'m sorry to hear that
    ;;
    *)
    echo unknown argument provided
    esac
```

3. To change the permissions of the file "yes-no.sh" to make it executable by all users (a = all, +x = add execute permission), run:
chmod a+x /yes-no.sh

This command allows the script to be run as an executable program.

4. To execute the script “/yes-no.sh” using the sh shell, run:
```bash
# sh /yes-no.sh 
```
</details>