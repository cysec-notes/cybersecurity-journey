# Module 2: Tools of the Trade: Linux and SQL
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
   

## Next Steps
Continue Course 1 Module 2





