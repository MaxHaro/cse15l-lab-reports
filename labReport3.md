# Lab Report 3: Researching Commands
The focus of this lab report will be the `find` command in bash.
The `find` command in Bash is used to search for files and directories in a directory hierarchy based on various criteria such as name, size, type, modification time, etc.

Let's go over sopme interesting command-line options:

## 1) find -name
Here's an example of using find -name to find all the files that end with .txt in the written_2 directory:

```
[cs15lwi23adg@ieng6-202]:written_2:351$ find -name "*.txt"
./non-fiction/OUP/Abernathy/ch1.txt
./non-fiction/OUP/Abernathy/ch14.txt
./non-fiction/OUP/Abernathy/ch15.txt
./non-fiction/OUP/Abernathy/ch2.txt
./non-fiction/OUP/Abernathy/ch3.txt
./non-fiction/OUP/Abernathy/ch6.txt
./non-fiction/OUP/Abernathy/ch7.txt
./non-fiction/OUP/Abernathy/ch8.txt
./non-fiction/OUP/Abernathy/ch9.txt
...etc...
```

The command searches through the current directory and all its subdirectories and returns the paths to all the files that end in `.txt`.
If we wanted to search in a specific directory, you can add the path to that directory. 
For example, find /path/to/directory -name ".txt" will search for .txt files only in the /path/to/directory directory and its subdirectories.

## 2) find -type
Here's an example of using find -type to find all the directories within the written_2 directory:

```
[cs15lwi23adg@ieng6-202]:written_2:357$ find -type d
.
./non-fiction
./non-fiction/OUP
./non-fiction/OUP/Abernathy
./non-fiction/OUP/Berk
./non-fiction/OUP/Castro
./non-fiction/OUP/Fletcher
./non-fiction/OUP/Kauffman
./non-fiction/OUP/Rybczynski
./travel_guides
./travel_guides/berlitz1
./travel_guides/berlitz2
```

In this case, the command searches for directories within the current directory. 
This is useful when you want to know how many subdirectories live in a single directory.

## 3) find -mtime
Here's an example of using find -mtime to search for files that were modified more than one day ago:

```
[cs15lwi23adg@ieng6-202]:written_2:358$ find -mtime +1
./non-fiction
./non-fiction/OUP
./non-fiction/OUP/Abernathy
./non-fiction/OUP/Abernathy/ch1.txt
./non-fiction/OUP/Abernathy/ch14.txt
./non-fiction/OUP/Abernathy/ch15.txt
./non-fiction/OUP/Abernathy/ch2.txt
./non-fiction/OUP/Abernathy/ch3.txt
./non-fiction/OUP/Abernathy/ch6.txt
./non-fiction/OUP/Abernathy/ch7.txt
./non-fiction/OUP/Abernathy/ch8.txt
./non-fiction/OUP/Abernathy/ch9.txt
./non-fiction/OUP/Berk
./non-fiction/OUP/Berk/CH4.txt
./non-fiction/OUP/Berk/ch1.txt
./non-fiction/OUP/Berk/ch2.txt
./non-fiction/OUP/Berk/ch7.txt
...etc...
```

In this case, the command searches for all the files and directories that were modified more than 1 day ago (hence the +1 as an argument).
Likewise, if we wanted to find the files that were modified less than 3 days ago we'd use the command find -mtime -2.

## 4) find -exec
Here we can see an example of using find -exec to find all text files and remove them from the current directory and its subdirectories:

```
[cs15lwi23adg@ieng6-202]:written_2:361$ find -name "*.txt" -exec rm {} \;
[cs15lwi23adg@ieng6-202]:written_2:362$ find -name "*.txt"
[cs15lwi23adg@ieng6-202]:written_2:363$ 
```
The find command searches for all files in the current directory and its subdirectories that have names ending in .txt. The -name option is used to specify the pattern to match.     
The -exec option is used to execute a command on each file found. In this case, the command is rm, which stands for "remove". 
The {} placeholder represents the name of the file found by find.     
The \; sequence indicates the end of the command to execute for each file.  
So, when the find command finds a file whose name matches the pattern *.txt, it will execute the rm command on that file, effectively deleting it.
