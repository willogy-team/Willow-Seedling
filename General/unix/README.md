
# Linux Introduction
Introductory Linux for Beginners

| **Author(s)** | Vi Pham |
| :------------ | :-------------------------------------------------------------------------------------------- |
| **Reviewer(s)** | Quang Tran |
| **Start Date** | Nov 23rd, 2020 |
| **Topic(s)** | General Techniques, OS |
| **Status**       | **In Progress** |

## Index
- [Introduction](#introduction)
- [References](#references)


## Introduction
### What is Linux?
> UNIX is an operating system which is a stable, multi-user, multi-tasking system for servers, desktops and laptops.
> It has a GUI but require that, is not covered by a graphical program or no windows interface available.  

>The most popular varieties of UNIX: Sun Solaris, GNU/Linux, and MacOS X.
>We concern with GNU/Linux (simply Linux)

Three parts of UNIX OS:

| Part           | Meaning | Role|
| ------------- | ------------- |------------- |
| The kernel | The hub of the OS | Allocate time, memory to programs.<br/> Handle the filestore communications.<br/>Response to system call. |
| The shell  | A command line interpreter (CLI) | Interpret the commands the user types in<br/>and arrange for them to be carried out|
| The programs | A collection of instuctions| Can be executed by a computer to perform a specific task |

Files and Processes:
- File: a collection of data.
- Process: an executing program identified by a unique PID.

The Directory Structure:
- All the files are grouped together
- A hierarchical structure like tree, with the top is root (slash /)


## Directory:

| Command | Meaning | Using | Note |
| ------------- | ------------- |------------- |------------- |
| ls \<directory> | List file in a directory | ls | Default: the current directory |
| ls -a | List all files and directories | ls -a | Even hidden files |
| mkdir \<namedir> | Make a directory | mkdir mydir ||
| cd \<new_dir> | Change the current working directory to new directory | cd sub_dir ||
| .| The currend working directory |||
|..|The parent directory |||
|~|The home directory|||
|pwd| Display the path ofthe current directory|||

## Manage files:
| Command / Symbol         | Meaning                                                       | Using                               | Note                                                                                    |
|--------------------------------|---------------------------------------------------------------|-------------------------------------|-----------------------------------------------------------------------------------------|
| touch file             | Create a file                                                 | touch myfile                        |                                                                                         |
| echo \<test>              | Create a text                                                 | echo ‘this is my test’              |                                                                                         |
| cp \<file1> \<file2>       | Copy file1 which name is file2                                | cp myfile newfile                   |                                                                                         |
| mv \<file1> \<file2>       | Move (or rename) file1 to file2                               | mv myfile newfile                   | Rename if same directory                                                                |
| rm \<file>                | Remove a file                                                 | rm myfile                           |                                                                                         |
| rmdir \<directory>        | Remove a directory                                            | rm mydirectory                      |                                                                                         |
| cat \<file>               | Display the contents of a file on the screen                  | cat myfile.txt                      | The file is longer than the size of the window, so it scrolls past making it unreadable |
| less \<file>              | Display the contents of file onto the screen a page at a time | less myfile.txt                     | Scrollable, type [q] to quit                                                            |  
| head -[\<lines>] \<file>   | Display the first few lines of a file                         | head myfile.txt head  -5 myfile.txt | Default lines=10                                                                        |
| tail -[\<lines>] \<file>   | Display the last few lines of a file                          | tail myfile.txt tail -5 myfile.txt  | Default lines=10                                                                        |
| grep \<keyword> \<file>    | File search a file for keywords                               | grep monday myfile.txt              |                                                                                         |
| wc [-c] [-w] [-l] \<file> | Count number of lines/words/characters in file                | wc myfile.txt wc -c myfile.txt      | default: all -c: characters -w: words -l: lines                                         |

## Redirect the input/output:
| Command / Symbol              | Meaning                                                                      | Using                                                                                        | Note                                              |   
|-------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------------|
| cat                           | Write the contents of a file to the screen without specifying a file to read | Type a few words on the keyboard and press the [Return] key. Press [Ctrl+D] to end the input |                                                   |
| sort                          | Alphabetically or numerically sort a list                                    |                                                                                              | without specifying a file to sort as using of cat |
| <                             | Redirect standard input to a file                                            | command < file                                                                               |                                                   |  
| >                             | Redirect standard output from a file                                         | command > file                                                                               | write over the content of the file                |  
| >>                            | Append standard output to a file                                             | command >> file                                                                              | write at the end of the content of the file       |  
| pipe                          | Pipe the output of command1 to the input of command2                         | command1 pipe command2                                                                       | \| is a pipe                                      |   
| cat \<file1> \<file2> > \<file0> | Concatenate file1 and file2 to file0                                         |                                                                                              |                                                   |   
| who                           | List users currently logged in                                               |                                                                                              |                                                   |                                        

## Special character to help us managing files:
| Command / Symbol  | Meaning                                                 | Examples                    | Note    |   
|-------------------|---------------------------------------------------------|-----------------------------|---------|
| *                 | Wildcard, match against none or more character(s)       |                             |         |   
| abc*              | All files in the current directory starting with abc... | **abc**ss,**abc**t,**abc**d,**abc**         |         |   
| *abc              | All files in the current directory ending with ...abc   | sff**abc**,f**abc**,**abc**             |         |   
| ~                 | Willcard, match exactly one character                   | ~ouse: **h**ouse, **m**ouse, ~~grouse~~ |         |   
| man <command>     | Read the online manual page for a command               |                             |         |   
| help <command>    | Short description of the use of the command             |                             | using   |   
| whatis <command>  | Brief description of a command                          |                             | meaning |   
| apropos <keyword> | Match commands with keyword in their man pages          |                             |         |   

## Security system and permissions, process:
| Command / Symbol           	| Meaning                                   	| Examples                                                                                                                                                                               	| Note                                                                                                                                       	|   	
|----------------------------	|-------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|--------------------------------------------------------------------------------------------------------------------------------------------	|
| ls -l                      	| List access rights for all files          	| #                                                                                                                                                                                      	| d: directory<br/>r: read permission<br/>w: write permission<br/>x: execution permission<br/>-: no permission                                               	|   	
| chmod [\<options>] \<file> 	| File change access rights for named file  	| chmod go-rwx mylist<br/>to remove,read ,write and execute permissions on the file biglist for the group and others<br/><br/>chmod a+rw mylist<br/>to read and write permissions on the file biglist to all 	| u: user<br/>g: group<br/>o: other<br/>a: all<br/>r: read<br/>w: write (and delete)<br/>x: execute (and access directory)<br/>+: add permission<br/>-: take away permission 	|   	
| ps                         	| See information about your processes      	|   PID TTY          TIME CMD 10544 pts/0    00:00:00 bash 11426 pts/0    00:00:00 ps                                                                                                    	|                                                                                                                                            	|   	
| bg                         	| Show background the suspended job         	|                                                                                                                                                                                        	|                                                                                                                                            	|   	
| jobs                       	| List current jobs                         	|                                                                                                                                                                                        	|                                                                                                                                            	|   	
| fg %jobnumber              	| Restart(foreground) a suspended progress  	| fg %1                                                                                                                                                                                  	|                                                                                                                                            	|   	
| [Ctrl+C]                   	| Kill the job running in the foreground    	|                                                                                                                                                                                        	|                                                                                                                                            	|   	
| [Ctrl+Z]                   	| Suspend the job running in the foreground 	|                                                                                                                                                                                        	|                                                                                                                                            	|   	
| kill %jobnumber            	| Kill job number                           	| kill %2                                                                                                                                                                                	|                                                                                                                                            	|   	
| kill processnumber         	| Kill process number                       	| kill 26152                                                                                                                                                                             	| PID                                                                                                                                        	|   	

## Other commands:
| Command / Symbol     	| Meaning                                                         	| Examples                                        	| Note 	|
|----------------------	|-----------------------------------------------------------------	|-------------------------------------------------	|------	|
| df                   	| Space left on the system                                        	|                                                 	|      	|
| du                   	| Kilobytes used by a directory                                   	|                                                 	|      	|
| gzip \<file>          	| Compress a file                                                 	| gzip science.txt -> zipped file: science.txt.gz 	|      	|
| gunzip \<file>        	| To expand the file                                              	| gunzip science.txt.gz                           	|      	|
| zcat \<file>          	| Read zipped file without needing to uncompress them first       	| zcat science.txt.gz                             	|      	|
| file \<directory>     	| Classifies the file according to its type                       	|                                                 	|      	|
| diff \<file1> \<file2> 	| Compares the contents of two files and displays the differences 	|                                                 	|      	|
| history              	| Keeps an ordered list of all the commands                       	|                                                 	|      	|

## The download, installation and compilation process of a programme in Linux:

> Steps needed to install the software:
>- Locate and download the source code (which is usually compressed)
>- Unpack the source code
>- Compile the code (the most difficult)
>- Install the resulting executable
>- Set paths to the installation directory

> The wy to compile a package:
>- **cd** to the directory containing the package's source code
>- Type **./configure** to configure the package for your system
>- Type **make** to compile the package
>- Optionally, type **make check** to run any self-tests that come with the package
>- Type **make install** to install the programs and any data files and documentation
>- Optionally, type **\`** make clean to remove the program binaries and object files from the source code directory

> Example:
>- Download source code: A piece of free software that converts between different units of measurements.<br/>First create a download directory:<br/> **% mkdir download** <br/> [Download the software here](http://www.ee.surrey.ac.uk/Teaching/Unix/units-1.74.tar.gz) and save it to your new download directory.
>- Extract source code:<br/>Go into your download directory and list the contents:<br/>**% cd download**<br/>**% ls -l**<br/>First unzip the file using the gunzip command. This will create a .tar file.<br/>**% gunzip units-1.74.tar.gz** <br/>Then extract the contents of the tar file. <br/>**% tar -xvf units-1.74.tar**<br/>Again, list the contents of the download directory, then go to the units-1.74 sub-directory.<br/>**% cd units-1.74**
>- Configure and create the Makefile:<br/>The units package uses the GNU configure system to compile the source code. We will need to specify the installation directory, since the default will be the main system area which you will not have write permissions for. We need to create an install directory in your home directory.<br/>**% mkdir ~/units174**<br/>Then run the configure utility setting the installation path to this.<br/>**% ./configure --prefix=$HOME/units174**
>- Build the package: <br/> Now you can go ahead and build the package by running the make command.  <br/>**% make**<br/>After a minute or two (depending on the speed of the computer), the executables will be created. You can check to see everything compiled successfully by typing<br/>**% make check**<br/>If everything is okay, you can now install the package.<br/>**% make install**<br/>This will install the files into the **~/units174** directory you created earlier.
>- Run the software:<br/> You are now ready to run the software (assuming everything worked).  <br/>**% cd ~/units174**<br/>If you list the contents of the units directory, you will see a number of subdirectories (bin,info,man,share)<br/>To run the program, change to the **bin** directory and type<br/>**% ./units** <br/> As an example, convert 6 feet to meters.<br/>**You have: 6 feet**<br/>**You want: metres**<br/>**\* 1.8288**<br/>If you get the answer 1.8288, congratulations, it worked.<br/>To view what units it can convert between, view the data file in the share directory (the list is quite comprehensive).<br/>To read the full documentation, change into the info directory and type <br/>**% info --file=units.info**


## UNIX Variables

>Standard UNIX variables are split into two categories:
>- ENVIRONMENT variables: have a farther reaching significance, and those set at login are valid for the duration of the session
>- shell variables: apply only to the current instance of the shell and are used to set short-term working conditions

Some ENVIRONMENT variables:
|Variable|Meaning|
|-|-|
|USER|your login name|
|HOME|the path name of your home directory|
|HOST|the name of the computer you are using|
|ARCH|the architecture of the computer's processor|
|DISPLAY|the name of the computer screen to display X windows|
|PRINTER|the default printer to send print jobs|
|PATH|the directories the shell should search to find a command|
|OSTYPE|the value of this is the current operating system you are using|

Some shell variables:
|Variable|Meaning|
|-|-|
|cwd|your current working directory|
|home|the path name of your home directory|
|path|the directories the shell should search to find a command|
|prompt|the text string used to prompt for interactive commands shell your login shell|

## References
[1] [UNIX Tutorial for Beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/)<br/>
[2] [Erle Robotics Unix Introduction Gitbook](https://erlerobotics.gitbooks.io/erle-robotics-unix-introduction-gitbook-free/content/index.html)
