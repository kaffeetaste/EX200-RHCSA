### Locate and copy

#### Question 10

Locate and copy all files larger than 3MB within the "/etc" directory on ServerA to a new directory "/find/3mfiles".


<details><summary>Solution</summary>


1. Create the target directory:
```
$ sudo mkdir -p /find/3mfiles
```

2. Locate files in the "/etc" directory that exceed 3 megabytes in size and copy them to the "/find/3mfiles/" directory with the following command:
```
$ sudo find /etc -size +3M -exec cp {} /find/3mfiles/ \;
```

The -size +3M option finds files larger than 3 megabytes.
The -exec option executes the cp command for each found file.

Note: To prevent accidental overwrites, consider using the -i option with cp:
```
$ sudo find /etc -size +3M -exec cp -i {} /find/3mfiles/ \;
```
This will prompt for confirmation before overwriting existing files.


Alternative method using rsync:
```
$ sudo rsync -av --min-size=3M /etc/ /find/3mfiles/
```
The rsync command offers additional features like incremental backups and synchronization.


3. Verify the copied files:
```
$ ls -lh /find/3mfiles
```

Explanation:

    mkdir -p: Creates the target directory and any necessary parent directories.
    find: Locates files matching the specified criteria.
    cp: Copies files to the target directory.
    rsync: Provides a more robust file transfer and synchronization mechanism.
    ls -lh: Lists files in human-readable format with file sizes.

    </details>