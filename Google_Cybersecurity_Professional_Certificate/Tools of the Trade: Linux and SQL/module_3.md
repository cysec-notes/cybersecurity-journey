# Module 3: Tools of the Trade: Linux and SQL
## Overview
This module introduces Linux commands as entered through the Bash shell. Learners will use Bash to navigate the file system, to manage it, and to authorize and authenticate users. They will also discover how they can independently get the support that they need to use additional Linux commands.

## Learning Objectives
- Navigate the file system using Linux commands via the Bash shell.
- Manage the file system using Linux commands via the Bash shell.
- Describe how Linux handles file permissions.
- Use Linux commands via the Bash shell to authenticate and authorize users.
- Use sudo to provide root user permissions.
- Access resources that provide support on using Linux commands.

## Key Concepts Learned
Bash is the default shell in most Linux distributions.

A command is an instruction telling the computer to do something.

An argument is specific information needed by a command.

One thing that is really important in Linux is that all commands and arguments are case sensitive.

#### Core commands for navigation and reading files
The root directory is the highest-level directory in Linux.
1. **pwd** prints the working directory onto the screen.
2. **ls** displays the names of files and directories in the current working directory.
3. **cd** navigates between directories.
4. **cat** displays the content of a file.
5. **head**, it displays just the beginning of a file, by default ten lines.

#### Manage file content in Bash
1. **grep** command searches a specified file and returns all lines in the file containing a specified string.
    Example: grep OS logsOS.txt. the first argument (OS) is the words inside the second argument which is the text file (logOS.txt)
2. **piping (|)** command sends a standard output of one command as standard input into another command for further processing.
3. **find**, commands which can help you search files and directories for specific information.
   **-name and -iname** - use with the **find** command to find file or directory names that contain a specific string. (-name is case-sensitive, and -iname is not.)
  **-mtime** - to find files or directories last modified within a certain time frame, using **find** commands.
   
#### Create and modify directories and files
1. **mkdir** command creates a new directory.
2. **rmdir** removes or deletes a directory.
3. **touch** command creates a new file,
4. **rm** command removes or deletes a file.
5. **mv** command moves a file or directory to new location, also used to rename files.
6. **cp** copies a file or directory into a new location.
7. **nano** is a command-line file editor that is available by default in many Linux distributions.

 **>** overwrites your existing file, and **>>** adds your content to the end of the existing file instead of overwriting it.

#### File permissions and ownership
**Authorization** is the concept of granting access to specific resources in a system. 

1. **chmod** changes permissions on files and directories.
   example: chmod u+rwx,g+rwx,o+rwx login_sessions.txt. 
Three types of permissions in Linux
1. read
2. write
3. executed

Types of owners
1. user (the owner of the file, but owner can be changed) = u
2. group = g
3. other = o

Options modify the behavior of the command.

**ls -l** displays permissions to files and directories.
**ls -a** displays hidden files.
**ls -la** displays permissions to files and directories, including hidden files.

#### Add and delete users
A root user, or superuser, is a user with elevated privileges to modify the system.
1. **sudo** is a command that temporarily grants elevated permissions to specific users.
2. **useradd** adds a user to the system
 **-g**: Sets the user’s default group, also called their primary group. To use the -g option, the primary group must be specified after -g. For example, entering sudo useradd -g security fgarcia adds fgarcia as a new user and assigns their primary group to be security.
   
**-G**: Adds the user to additional groups, also called supplemental or secondary groups. To use the -G option, the supplemental group must be passed into the command after -G. You can add more than one supplemental group at a time with the -G option. Entering sudo useradd -G finance,admin fgarcia adds fgarcia as a new user and adds them to the existing finance and admin groups.

3. **userdel**. userdel deletes a user from the system.
    userdel -r: delete user and all files in their home directory.
   usermod -L: deactivitang account
4. The **usermod** command modifies existing user accounts.
-d: Changes the user’s home directory.

-l: Changes the user’s login name.

-L: Locks the account so the user can’t log in.

-a: appends the user to an existing group 

5. **chown** commands changes ownership of a file or directory.

#### Man pages
1. **man**. man displays information on other commands and how they work.
2. **whatis** displays a description of a command on a single line.
3. **apropos** searches the manual page descriptions for a specified string.

#### Personal Reflection
In this module, I learn hhow to use linux commands for navigating, viewing contents, change or add permissions and ownership, modify, delete, and helping resources.

## Next Steps
Continue Course 1 Module 2





