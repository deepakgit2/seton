## Commands
- [`cat`](#cat) [`cd`](#cd) [`chgrp`](#chgrp) [`chmod`](#chmod) [`chown`](#chown) [`cp`](#cp)
- [`find`](#find)
- [`grep`](#grep) [`group`](#group)
- [`history`](#history)
- [`ls`](#ls)
- [`mkdir`](#mkdir) [`mv`](#mv)
- [`pwd`](#pwd)
- [`rm`](#rm) [`rmdir`](#rmdir)
- [`sed`](#sed) [`sort`](#sort)
- [`tar`](#tar)
- [`users`](#users)

## cat
- `cat` it use to display the file content and concatenate multiple files into one
    - `cat file.txt` show the content of file.txt
    - `cat file1.txt file2.txt` concatenate the content of file1 and file2 with '\n' and display them
    - `cat > newfile.txt` it prompts a user input. we can type text and the Ctrl+D then all the typed content will save into newfile.txt
    - `cat -n file.txt` add line numbers to all lines
    - `cat -b file.txt` add line numbers to non blank lines
    - `cat -s file.txt` squeeze multiple blank lines into one
## cd
- `cd` use to change the current working dir
    - `cd` change dir to the home dir of user [by default]
    - `cd ~` similar to above
    - `cd <path>` chnage to given path
## chgrp
- `chgrp` change the group ownership of files and directories
    - `chgrp developers file.txt`: Changes the group ownership of "file.txt" to the group "developers"
    - `chgrp -R users <directory>`: Recursively changes the group ownership to "users" for all files and directories within "directory".
## chmod
- `chmod` It is used to change the permissions of files and directories. `chmod [ugo][+-=][rwx] <file>`
    - `chmod u+wx file.txt` adds read, write permission for the user (owner) of the file "file.txt"
    - `chmod g-x file.txt` remove execute permission for the group of the file "file.txt"
    - `chmod o=rw file.txt` sets read and write permissions for the others on "file.txt", removing any other prev permissions
    - `chmod ug+rw  file.txt` file.txt: adds read, write permissions for theuser and group on "file.txt"
    - `chmod u+w, o-x  file.txt` adds write for user and remove execute permissions for other on "file.txt"
    - `chmod -R u+w, o-x  <folder>` adds write for user and remove execute permissions for other recursively in folder
    - Using Numeric Values:
        - numerical values for all permission r=4, w=2, & x=1. We can generate all possible permission using these number by adding e.g rwx = 7 (4+2+1), rx=5, rw=6, etc. We can only one number can represent any permission
        - `chmod 640 script.sh`: Gives the owner read and write permissions (6), read permissions for the group (4), and no permissions for others (0)
## chown
- `chown` change the owner and group ownership of files and directories
    - `chown john file.txt` : Changes the owner of "file.txt" to the user "john"
    - `chown :users file.txt`: Changes the group ownership of "file.txt" to the group "users" while leaving the owner unchanged
    - `chown john:users file.txt`: Changes both the owner to "john" and the group ownership to "users" for "file.txt"
    - `chown -R john:users directory`: Recursively changes the owner to "john" and the group ownership to "users" for all files and directories within "directory"
## cp
- `cp` use to copy file and folder [by default over write if already exists]
    - `cp <src_file> <dst_file>` src file will be copied to dst file. If dst filename is different the it will renamed also
    - `cp <src_file> <dst_folder>` src file will be copied into the dst folder. We can pass multple files also
    - `cp *.py <dst_folder>` It will copy all .py files from src to dst
    - `cp -r <src_folder> <dst_folder>` to copy a whole folder (including hidden files) we have to paas -r [--recursive] flag. **If dst_folder not exists, it will be created [At first level not nestedly] and all the content of src_folder will be copied into dst_folder and if If dst_folder exists then src_folder will be copied into the dst_folder
    - `cp -i <src> <dst>` enters interactive mode and ask before over writing files
    - `cp -n <src> <dst>` does not over write
    - `cp -v <src> <dst>` verbose; prints informative messages
    - `cp -u <src> <dst>` update the dst file only if src file is different from dst file
## find
- `find` to search for files and directories in a directory hierarchy based on various criteria. It allows you to locate files based on their names, types, sizes, timestamps, permissions, and other attributes
    - `find <dir> -name "*.txt"` Finds all files ending with ".txt" in the dir directory and its subdirectories.
    - `find <dir> -type d` returns all folders in the dir. more types f: regular files, d: directories, l: symbolic links, and more
    - `find <dir> -mtime -7` Finds files modified within the last 7 days in the dir
    - `find <dir> -perm /u+w` Finds files in the directory that are writable by the owner
    - `find <dir> -perm 644` Finds files with permission 644 in the directory.
    - `find / -size +100M` Finds files larger than 100 megabytes in the whole system [-size n[ckMG]]
    - `find /home -name "*.txt" -exec rm {} +` Deletes all files ending with ".txt" in the /home directory and its subdirectories. {} placeholder represents the file name, and + indicates that the command should be run with multiple files at once
## grep
- `grep` command is use to search for a perticular string/pattern in a file
    - `grep pattern <file>` returns all the lines that matches pattern
    - `grep pattern <file1> <file2>` returns all the lines that matches pattern in both files
    - `grep -i pattern <file>` returns all the lines that matches pattern but for case insensitive also
    - `grep -n pattern <file>` returns all the lines that matches pattern along with line number
    - `grep -v pattern <file>` returns all the lines that not matches pattern
    - `grep -c pattern <file>` returns all the number of lines that matches pattern
    - `grep -o pattern <file>` show only mathces not the whole line
    - `grep -r pattern <dir>` recursively search for all files
    - `<any command> | grep pattern` grep can also be used for output of any command even grep cmd also 
## group
- `group` Following are few commands to manage groups in linux
    - `groupadd` creates a new group 
        - `groupadd developers` creates a group named "developers" 
    - `groupmod` modify an existing group 
        - `groupmod -n newname oldname` renames an existing group from "oldname" to "newname"
    - `groupdel` delete a group
        - `groupdel developers` delete a group named "developers"
    - `groupmems` manage group members
        - `groupmems -g developers -a john` adds the user "john" to the group "developers"
        - `groupmems -g developers -d john` removes the user "john" from the group "developers"
    - `newgrp` change the current group to another group
        - `newgrp developers` switches the current group to "developers" (if the user is a member of that group)
    - `getent group developers` displays detailed information about the "developers" group    
## history
- `history` show recent used command
    - `history` display the list of previously executed commands default 1000 and can be change using HISTSIZE env var
    - `history -c`  clears the history file and removes all previously executed commands from the current session
    - `!!` repeat 
    - `!42` Enter the command number preceded by an exclamation mark (!)
    - Note:
        - It's important to note that the command history is specific to each terminal session and is not shared among different terminal windows or different users

## mkdir
- `mkdir` Create the DIRECTORY(ies), if they do not already exist
    - `mkdir <folder1> <folder2>` It will create two directories
    - `mkdir -p /folder1/folder2/folder3` By default it does not create nested folder. We can pass -p [--parent] flat to do same.
## rm
- `rm` Remove the Files and Directories
    - `rm <file1> <file2>` Remove files
    - `rm -r <folder>` remove directories and their contents recursively, we have to pass -r [--recursive] flag
    - `rm -f [--force]` forcely remove
    - `rm -i` prompts before every removal
    - `rm -v` verbose
## rmdir
- `rmdir` Remove the DIRECTORY(ies), if they are empty
    - `rmdir <folder1> <folder1>` Remove both folders if empty
    - `rmdir -p ./folder1/folder2` Remove folder2 and its parent folder1 also
## sed
- `sed` is a powerful text processing tool which can be used for replacing, adding, deleting the text using regex
    - `echo "Hello, world world!" | sed 's/world/John/'` it substitute (s) first occurance with new string
    - `echo "Hello, world world!" | sed 's/world/John/g'` it substitute (s) all occurance (global g) with new string
    - `echo "Line 1\nLine 3" | sed '2i\Line 2'` insert (i) text before a specified line number or pattern
    - `echo "Line 1\nLine 3" | sed '2a\Line 2'` append (a) text after a specified line number or pattern
    - `echo -e "Line 1\nLine 2\nLine 3" | sed '/Line 2/d'` deletes (d) lines that match a specified pattern
    - `sed -r 's/([0-9]+)th/\1th/g' file.txt` Enables the use of extended regular expressions
    - `sed -e 's/foo/bar/g; s/baz/qux/g' input.txt` Allows specifying multiple sed commands or scripts separated by semicolons. Each command is applied sequentially to the input text [--expression]
## sort
- `sort` command is use to sort the content of a file
    - `sort` takes userinput and sort them when we press Ctrl+D
    - `sort <file>` sort in alphabetical order
    - `sort <file1> <file2>` sort both files content in alphabetical order
    - `sort -r <file>` sort in reverse order
    - `sort -f <file>` case insensitive sorting
    - `sort -n <file>` sort as per numerical order
    - `<any command> | sort` sort can also be used for output of any command  
## tar
- `tar` It is used to manipulate and create tar archives, commonly referred to as tarballs
    - `tar -cvf archive.tar <file1> <file2>` creates new archive [-c: compress, -v: verbose, -f tarfile name]
    - `tar -cvf archive.tar <folder1> <folder2>` it accepts the multiple folders also
    - `tar -xvf archive.tar` extract files from archive [-x: extract]
    - `tar -rvf archive.tar file2.txt` appends files to an existing archive
    - `tar -uvf archive.tar file3.txt` Updates an archive by adding newer files
    - `tar -czvf archive.tar.gz <file1> <file2>` creates new compressed archive
    - Points:
        - tar is primarily used for bundling files and directories together, and it does not perform compression by default. It is often combined with compression tools like gzip or bzip2 e.g (tar.gz or tar.bz2)
## ls
- `ls` list information about and files and directories
    - `ls` list all contents in current dir
    - `ls <path>` list all contents for given path
    - `ls -a [--all]` do not ignore entries starting with . (hidden files)
    - `ls -l` list all contents alongs with its owner setting, permissions & time stamp (long format)
    - `ls -R [--recursive]` list all contents in sub folders recursively
    - `ls -h [--human-readable]` with -l or -s, print sizes like 1K 10M 2G etc
    - `ls -S [--sort]` Sort by file size in descending order
    - `ls *.py` We can use regex also [TODO]
## mv
- `mv` Similar to cut & paste [by default over write if already exists].
    - `mv <src_file> <dst_file>` src file will be moved to dst file. If dst filename is different the it will renamed also
    - `mv <src_file> <dst_folder>` src file will be moved into the dst folder. We can pass multple files also.
    - `mv *.py <dst_folder>` It will move all .py files from src to dst
    - `mv <src_folder> <dst_folder>` to move folder (including hidden files). **If dst_folder not exists, it will be created [At first level not nestedly] and all the content of src_folder will be moved into dst_folder and if If dst_folder exists then src_folder will be moved into the dst_folder**
    - `mv -i <src> <dst>` enters interactive mode and ask before over writing files
    - `mv -v <src> <dst>` verbose; prints informative messages
    - `mv -u <src> <dst>` update the dst file only if src file is different from dst file
## pwd
- `pwd` prints the current directory
## users
- `users` following are few commands to manage users in linux
    - `useradd` create a new user account.
        - `useradd john` creates a user account with the username "john"
    - `userdel` to delete a user account
        - `userdel john`  deletes the user account for "john"
    - `usermod` is used to modify user account properties. 
        - `usermod -l newname oldname` changes the username from "oldname" to "newname"
        - `usermod -d /new/home/dir john` changes the home directory of the user john
    - `passwd` change a user's password
        - `passwd` change the password for the current user
        - `passwd john` change the password for the user "john"
    - `id` displays information about deea user, including user and group IDs
        - `id` displays the current user information
        - `id john` displays the information for user "john"
    - `su` allows you to switch to another user account
        - `su` switches to root user
        - `su john` switches to the user account "john"
    - `finger` displays user information, including login, name, and other details.
        - `finger` shows information about the current user
        - `finger john` shows information about the user "john"
    - `w` shows a list of logged-in users, including their activity and terminal information.
    - `whoami` returns the username of the current use
    
