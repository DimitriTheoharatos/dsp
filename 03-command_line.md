# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

> > pwd : show current working directory path.   
> > mkdir <directory_name> : create a directory.   
> > rm -rf <directory_name> : deleting a directory.   
> > touch <filename> : creating a file using `touch` command.    
> > rm <filename> : deleting a file.    
> > cp <old_filename> <new_filename> : renaming a file.    
> > ls -a: listing hidden files.    
> > cp </path/to/file> <path/to/new/diretory> : copying a file from one directory to another.    
> > cat <filename> : output content of file to command line console.    
> > mv <filename> </path/to/new/location> : move a file.    

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

> > `ls` : Shows the content in the current directory.  
> > `ls -a` : Shows the content in the current directory and the hidden files.   
> > `ls -l` : Shows file size, date modified, user information, and read/write file type in a tabular format.  
> > `ls -lh` : Same as above, but gives file size in a more digestible format.   
> > `ls -lah` : Same as above but includes the hidden file information.   
> > `ls -t` : Sorts by time modified first before lexicographical ordering.  
> > `ls -Glp` : Highlights the folder a different color, and adds a forward slash to directories.   

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > `ls -S` : Sort files by size.  
> > `ls -m` : Stream output format, list files across the page, separated by commas.   
> > `ls -r` : Displays files in reverse order.   
> > `ls -W` : Displays whiteouts when scanning directories.   
> > `ls -R`: Recursively list subdirectories encountered.   

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > Xargs basically reads data from standard input and executes the command supplied one or more times based on the input.  Blanks and spaces are treated as delimiters and blank lines are ignored. If you wanted to find files that contain specific text, you can do the following:  
> > `find -name "*.txt" | xargs grep "abc"`    
> > This will find all text files in the current directory and subdirectories that contain the text 'abc' in it. 

 

