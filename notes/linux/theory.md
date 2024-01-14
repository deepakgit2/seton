### History of Linux
- **Birth of C and Unix** Unix was developed by Dennis Ritchie and Ken Thompson at Bell Laboratories of AT&T (American Telephone & Telegraph) in 1969. Dennis Ritchie also has also created the C programming language, which became the primary language for UNIX development.
- AT&T licensed UNIX to various organizations and academic institutions, allowing them to use and modify the system for their own purposes. Lots of developers and scientist colaborated in Unix. Since At&T was founded Unix they started commercial sell of Unix. But it didn't went well because it was the efforts of other developers and scinetist who contribubuted to growth of Unix but they were not getting any benifit.
-  However, in the late 1970s and early 1980s, The University of California, Berkeley developed their own version of UNIX, known as the Berkeley Software Distribution (BSD). BSD included significant enhancements and modifications to the original UNIX code. Berkeley distributed BSD UNIX under a permissive license, which allowed others to use, modify, and redistribute the code freely. This led to the development of numerous open-source UNIX-like operating systems based on BSD, such as FreeBSD, OpenBSD, and NetBSD.
- After that story chnaged, Instead of buying Unix from AT&T. Companies started developing their own Unix: IBM(AIX), Solaries(Sun OS), HP(HP-UX)
- Since there were many version of unix available it was becoming problematic because each version was different from other. So Richard Stallman comes up with GNU project (recusive acronym for GNU's Not UNIX). GNU is a free and open-source operating system developed by the Free Software Foundation (FSF). The project's goal of creating a Unix-like operating system that adheres to the principles of free software. Here "Free" refers to freedom, rather than cost. 
- Although the GNU project developed various components of the operating system, including a compiler (GCC), a text editor (Emacs), and numerous utilities, it lacked a kernel. To complete the operating system, a kernel was needed, and that's where the Linux kernel came into play.
- GNU is an important project in the history of open-source software and has greatly contributed to the development and promotion of free software principles and practices. The GNU General Public License (GPL), developed by the FSF, is one of the most widely used free software licenses, ensuring that software licensed under it remains free and open source.
- Around the same time, in 1991, Linus Torvalds, a Finnish computer science student, developed an open-source kernel known as Linux. Linus released the Linux kernel under the GNU General Public License (GPL), which aligns with the principles of the GNU project. The Linux kernel quickly gained attention and support from developers worldwide.
- Recognizing that the Linux kernel would be an ideal complement to the GNU system, the GNU project and Linux began collaborating. The GNU system, with its userland tools and utilities, combined with the Linux kernel, created a complete, functional operating system. This combination became known as "GNU/Linux" or simply "Linux."
-  The vast majority of Linux-based operating systems are derived from GNU/Linux e.g Ubuntu, Fedora, Debian, and CentOS are all Linux distributions that fall under the category of GNU/Linux operating systems. They are derived from the combination of the Linux kernel and the GNU userland tools, along with additional software packages and applications.

### Linux File System
-  In Linux and other Unix-like operating systems, there is a concept is often referred to as the "Everything is a file" principle. It means that various aspects of the system, such as devices, processes, network sockets, and hardware components, are represented and accessed through the file system interface. Even folders are files
- Every directory/file in the Linux filesystem is nested under the root / directory
- Special Characters
    - The dot (.) , dot-dot (..) , forward slash (/), and tilde (~), all have special functionality in the Linux filesystem
    - The dot (.) represents the current directory in the filesystem.
    - The dot-dot (..) represents one level above the current directory.
    - The forward slash (/) represents the "root" of the filesystem.
    - The tilde (~) represents the home directory of the currently logged in user.
- Special dir/files
    - `/dev/null`  It is often referred to as the "null device" or "bit bucket". It is a special file that discards any data written to it. It's commonly used to redirect output for programs or commands when you don't need or want to see the output.
    - `~/.bash_history` stroes bash command histroy which can be shown using `history` command. By default it stores 1000 recent commands but can be changed using "HISTSIZE" variable

### Users, Groups and Permission
- Users
    - In linux, we can have mulitple accounts 
- Groups
    - A group is a collection of user accounts that can be used to assign permissions and access rights to files, directories, and other system resources
    - Each user in Linux belongs to at least one group, known as their primary group. Additionally, users can be members of multiple secondary groups. The primary group is specified when a user account is created, and by default, it shares the same name as the username.
    - Groups are identified by a numeric group ID (GID) and optionally a group name.
    - To manage groups in Linux typically involves commands like `groupadd` to create a new group, `groupmod` to modify an existing group, `groupdel` to delete a group, and `usermod` to add or remove users from a group.
- File/Dir Permission
    - Each file or folder contains the permission which can be seen using `ls -l` cmd and output looks like following 
        ```
        -rw-r--r--  1 john  developers  1024 Jun 1 10:30 file.txt
        drwxr-xr-x  2 jane  users       4096 May 5 16:45 directory
        lrwxrwxrwx  1 mary  users          6 Jun 2 09:15 link -> file.txt
        ```
    - Permission: the first column consists of ten characters. Each character represents a specific permission or attribute. which can be divided into 4 parts `d` `rwx` `r-x` `r-x`
        1. File Types
            - **d**: directory, **-**: normal file, **c**: binary special file, **c**: character special file
        2. User Permission: always in a sequene rwx
            - **r**: read, **w**: write, **x**: executable, **-**: not allowed
        3. Group Permission: 
            - **r**: read, **w**: write, **x**: executable, **-**: not allowed
        4. Other's Permission: always in a sequene rwx
            - **r**: read, **w**: write, **x**: executable, **-**: not allowed
    - Number of Links: The second column represents the number of hard links to the file or directory.
    - Owner: The third column displays the owner of the file or directory.
    - Group: The fourth column shows the group associated with the file or directory.
    - File Size: The fifth column specifies the size of the file in bytes.
    - Modification Date and Time: The sixth column displays the date and time when the file or directory was last modified.

File/Directory Name: The last column represents the name of the file or directory.


#### File/string Manupulations
- `head`
    - `head <file>` show first 10 lines by default we can pass -n 5 to change it
- `uniq`
    - `echo 1\n2\n2\n3 | uniq` show only uinque lines
- `tail`
    - `tail <file>` show last 10 lines by default we can pass -n 5 to change it
- `wc` word count
    - `wc <file>` It returns the no of line, words and character in a files




### Acronym
- BSD: Berkeley Software Distribution
- FSF: Free Software Foundation
- GNU: GNU's Not UNIX
- GPL: General Public License
- LINUX: Linux Is Not UNIX [Lovable Intellect Not Using XP]
- RHEL: Red Hat Enterprise Linux
- UNIX: UNiplexed Information Computing System (also referred to as UNICS)

### Acronym [cmd]
- bash: Bourne Again SHell
- chmod: Change Mode
- grep: Global Regular Expression Print
- pwd: Print Working Directory
- nohup: no hang up
- sed: stream editor
- su: Switch User or Substitute User 
- sudo: Super User Do
- ssh: Secure Shell
- tar: tape archive
