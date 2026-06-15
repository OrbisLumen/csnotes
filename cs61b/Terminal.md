# Terminal 
## Common command
- `cd`: change your working directory
    ```bash
    cd hw
    ```
    This command will change your directory to hw.
---
- `pwd`: present working directory
    ```bash
    pwd
    ```

---
- `.`: means your current directory
    ```bash
    cd .
    ```
---
- `..`: means one parent directory above your current directory
    ```bash
    cd ..
    ```
---
- `ls`: list files/folders in directory
    ```bash
    ls
    ```
    This command will list all the files and folders in your current directory.
    ```bash
    ls -l
    ```
    This command will list all the files and folders in your current directory with timestamps and file permissions. This can help you double-check if your file updated correctly or change the read-write-execute permissions for your files.
---
- `mkdir`: make a directory
    ```bash
    mkdir dirname
    ```
    This command will make a directory within the current directory called dirname.
---
- `rm`: remove a file
    ```bash
    rm file1
    ```
    This command will remove file1 from the current directory. It will not work if file1 does not exist.
    ```bash
    rm -r dir1
    ```
    This command will remove a whole directory dir1.
---
- `cp`: copy a file
    ```bash
    cp lab1/original lab2/duplicate
    ```
    This command will copy the original file in the lab1 directory and create a duplicate copy in the lab2 directory.
---
- `mv`: move or rename a file
    ```bash
    mv lab1/original lab2/original
    ```
    This command moves original from lab1 to lab2.
    ```bash
    mv lab1/original lab1/newname
    ```
    This command renames the file from original to newname.
---
## Common press
- `tab`: autocomplete 
- `up`: find instruction used recently
