# Anisa-LPIC-1-Jan-2023-Fridays-HW4

# MohammadALi Heidari-LPIC1-Fridays-HW4
## Task 1: Report of the following command:

 - **Command:** `dd if=/dev/sda of=/dev/sdb status=progress`

- **Outcome:** 
![outcome](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Task1")

## Task 2: Number and address of a file's hard links and soft links

First to list all of the hard links of a file we need its inode number. We can get that by `ls -li` command. Then we use `find` command with `-inum- option to list all files with same inode number which are hard links.
 - **Final command:** `find -inum INODE_NUMBER`

- **Outcom:**
![outcome](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Task2-1")

Now to find all of the soft links of a file we can use `find -type l` command that will show symbolic links for the address we give it `/` because we want it to search through all the system then we use `-ls` option too because it will show more details which contain the name of the original file and then redirect the errors to `/dev/null`. Now it will show us all the soft links that we can see on the system. All we need to do is to pipe the outcome to `grep` command and filter out our wanted links by the original file's name.

- **Final Command:** `find / -type l -ls 2> /dev/null | grep \bFILE_NAME\b`

- **Outcome:** 
![outcome](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Task2-2")

## Task 3: Hard links for directories yes or no? How and Why?

You can create a soft link to a directory but when you try to create a hard link to a directory, you’ll see an error like this: 

`ln: newdir/test_dir: hard link not allowed for directory` 

It’s because using hard links for directory may break the filesystem. Theoretically, you can create hard link to directories using -d or -F option. But most Linux distributions won’t allow that even if you are root user.

Now When does the link count of a directory change?
The link count of a directory increases whenever a sub-directory is created. The default link count of any directory is 2. The extra count is because for every directory created, a link gets created in the parent directory to point to this new directory.
