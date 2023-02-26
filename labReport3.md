# Lab Report 3: Researching Commands
The focus of this lab report will be the `find` command in bash.
The `find` command in Bash is used to search for files and directories in a directory hierarchy based on various criteria such as name, size, type, modification time, etc.

Let's go over sopme interesting command-line options:

## 1) find -name
### a) Finding all .txt files
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

### b) Finding files starting with a specific keyword
Now let's say that we are interested in finding a very specific file name/s, let's say all the files starting with the word "Bahamas". We can also use find -name to find all the files that start with that word!

```
[cs15lwi23adg@ieng6-201]:written_2:535$ find -name "Bahamas-*"
./travel_guides/berlitz2/Bahamas-History.txt
./travel_guides/berlitz2/Bahamas-Intro.txt
./travel_guides/berlitz2/Bahamas-WhatToDo.txt
./travel_guides/berlitz2/Bahamas-WhereToGo.txt
```

The command searches through the current directory and all its subdirectories and returns the paths to all the files that start with "Bahamas". Isn't that neat?

## 2) find -type
### a) Finding all directories
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

### b) Finding all regular files
Here's an example of using find -type to find all the regular files within the written_2 directory:
```
[cs15lwi23adg@ieng6-201]:written_2:539$ find -type f
./non-fiction/OUP/Abernathy/ch1.txt 
./non-fiction/OUP/Abernathy/ch14.txt
./non-fiction/OUP/Abernathy/ch15.txt
./non-fiction/OUP/Abernathy/ch2.txt 
./non-fiction/OUP/Abernathy/ch3.txt 
./non-fiction/OUP/Abernathy/ch6.txt 
./non-fiction/OUP/Abernathy/ch7.txt 
./non-fiction/OUP/Abernathy/ch8.txt 
./non-fiction/OUP/Abernathy/ch9.txt 
./non-fiction/OUP/Berk/CH4.txt      
./non-fiction/OUP/Berk/ch1.txt      
./non-fiction/OUP/Berk/ch2.txt      
./non-fiction/OUP/Berk/ch7.txt 
...etc...
```
This command will search for all regular files (excluding directories and special files) in the current directory and its subdirectories.

## 3) find -mtime
### a) Finding files that were modified less/more than x days ago
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

### b) Finding files that were accesed less/more than x days ago

Here's an example of using find -atime to search for files that were accessed less than one day ago:

```
[cs15lwi23adg@ieng6-201]:written_2:553$ find -atime -1
.
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
...etc...
```
In this particular instance, the command searches for all files and directories that were accessed within the last 1 day in the current directory and its subdirectories.

## 4) find -exec
### a) Find all text files and remove them
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

### b) Copy files that match a given search criteria to another directory
Here is an example of using the find -exec command to do just that:
```                                                             
[cs15lwi23adg@ieng6-201]:skill-demo1-data:562$ find written_2/ -type f -name "*.txt" -exec cp {} destination/ \;
[cs15lwi23adg@ieng6-201]:skill-demo1-data:563$ ls
destination  written_2
[cs15lwi23adg@ieng6-201]:skill-demo1-data:564$ cd destination/
[cs15lwi23adg@ieng6-201]:destination:565$ ls
Algarve-History.txt      Berlin-WhatToDo.txt          Costa-WhereToGo.txt       HistoryEgypt.txt         IntroHongKong.txt       Portugal-WhatToDo.txt     WhatToMadeira.txt        ch14.txt
Algarve-Intro.txt        Berlin-WhereToGo.txt         CostaBlanca-History.txt   HistoryFWI.txt           IntroIbiza.txt          Portugal-WhereToGo.txt    WhatToMalaysia.txt       ch15.txt
Algarve-WhatToDo.txt     Bermuda-WhatToDo.txt         CostaBlanca-WhatToDo.txt  HistoryFrance.txt        IntroIndia.txt          PuertoRico-History.txt    WhatToMallorca.txt       ch2.txt
Algarve-WhereToGo.txt    Bermuda-WhereToGo.txt        Crete-History.txt         HistoryGreek.txt         IntroIsrael.txt         PuertoRico-WhatToDo.txt   WhereToDublin.txt        ch3.txt
Amsterdam-History.txt    Bermuda-history.txt          Crete-WhatToDo.txt        HistoryHawaii.txt        IntroIstanbul.txt       PuertoRico-WhereToGo.txt  WhereToEdinburgh.txt     ch4.txt
Amsterdam-Intro.txt      Boston-WhereToGo.txt         Crete-WhereToGo.txt       HistoryHongKong.txt      IntroItaly.txt          Vallarta-History.txt      WhereToEgypt.txt         ch5.txt
Amsterdam-WhatToDo.txt   Budapest-History.txt         CstaBlanca-WhereToGo.txt  HistoryIbiza.txt         IntroJamaica.txt        Vallarta-WhatToDo.txt     WhereToFWI.txt           ch6.txt
Amsterdam-WhereToGo.txt  Budapest-WhatToDo.txt        Cuba-History.txt          HistoryIndia.txt         IntroJapan.txt          Vallarta-WhereToGo.txt    WhereToFrance.txt        ch7.txt
Athens-History.txt       Budapest-WhereoGo.txt        Cuba-WhatToDo.txt         HistoryIsrael.txt        IntroJerusalem.txt      WhatToDublin.txt          WhereToGreek.txt         ch8.txt
Athens-Intro.txt         CH4.txt                      Cuba-WhereToGo.txt        HistoryIstanbul.txt      IntroLakeDistrict.txt   WhatToEdinburgh.txt       WhereToHawaii.txt        ch9.txt
Athens-WhatToDo.txt      California-History.txt       HandRHawaii.txt           HistoryItaly.txt         IntroLasVegas.txt       WhatToEgypt.txt           WhereToHongKong.txt      chA.txt
Athens-WhereToGo.txt     California-WhatToDo.txt      HandRHongKong.txt         HistoryJamaica.txt       IntroLosAngeles.txt     WhatToFWI.txt             WhereToIbiza.txt         chB.txt
Bahamas-History.txt      California-WhereToGo.txt     HandRIbiza.txt            HistoryJapan.txt         IntroMadeira.txt        WhatToFrance.txt          WhereToIndia.txt         chC.txt
Bahamas-Intro.txt        Canada-History.txt           HandRIsrael.txt           HistoryJerusalem.txt     IntroMadrid.txt         WhatToGreek.txt           WhereToIsrael.txt        chL.txt
Bahamas-WhatToDo.txt     Canada-WhereToGo.txt         HandRIstanbul.txt         HistoryLakeDistrict.txt  IntroMalaysia.txt       WhatToHawaii.txt          WhereToIstanbul.txt      chM.txt
Bahamas-WhereToGo.txt    CanaryIslands-History.txt    HandRJamaica.txt          HistoryLasVegas.txt      IntroMallorca.txt       WhatToHongKong.txt        WhereToItaly.txt         chN.txt
Bali-History.txt         CanaryIslands-WhatToDo.txt   HandRJerusalem.txt        HistoryMadeira.txt       JungleMalaysia.txt      WhatToIbiza.txt           WhereToJapan.txt         chO.txt
Bali-WhatToDo.txt        CanaryIslands-WhereToGo.txt  HandRLakeDistrict.txt     HistoryMadrid.txt        Nepal-History.txt       WhatToIndia.txt           WhereToJerusalem.txt     chP.txt
Bali-WhereToGo.txt       Cancun-History.txt           HandRLasVegas.txt         HistoryMalaysia.txt      Nepal-WhatToDo.txt      WhatToIsrael.txt          WhereToLakeDistrict.txt  chQ.txt
Barcelona-History.txt    Cancun-WhatToDo.txt          HandRLisbon.txt           HistoryMallorca.txt      Nepal-WhereToGo.txt     WhatToIstanbul.txt        WhereToLosAngeles.txt    chR.txt
Barcelona-WhatToDo.txt   Cancun-WhereToGo.txt         HandRLosAngeles.txt       IntroDublin.txt          NewOrleans-History.txt  WhatToItaly.txt           WhereToMadeira.txt       chV.txt
Barcelona-WhereToGo.txt  China-History.txt            HandRMadeira.txt          IntroEdinburgh.txt       Paris-WhatToDo.txt      WhatToJamaica.txt         WhereToMadrid.txt        chW.txt
Beijing-History.txt      China-WhatToDo.txt           HandRMadrid.txt           IntroEgypt.txt           Paris-WhereToGo.txt     WhatToJapan.txt           WhereToMalaysia.txt      chY.txt
Beijing-WhatToDo.txt     China-WhereToGo.txt          HandRMallorca.txt         IntroFWI.txt             Poland-History.txt      WhatToLakeDistrict.txt    WhereToMallorca.txt      chZ.txt
Beijing-WhereToGo.txt    Costa-History.txt            HistoryDublin.txt         IntroFrance.txt          Poland-WhatToDo.txt     WhatToLasVegas.txt        ch1.txt
Berlin-History.txt       Costa-WhatToDo.txt           HistoryEdinburgh.txt      IntroGreek.txt           Portugal-History.txt    WhatToLosAngeles.txt      ch10.txt
[cs15lwi23adg@ieng6-201]:destination:566$
```
Let's go over what's happening here: 
1) `find written_2` specifies the directory where the search will begin.
2) `type f` specifies that only regular files should be searched for.
3) `name "*.txt"` specifies that only files with a .txt extension should be searched for.
4) `exec cp {} destination/ \;` executes the cp command on each file that matches the search criteria. The {} is a placeholder for the filename, and the \; specifies the end of the command.

In summary, this command searches for all regular files with a .txt extension in the source directory (written_2) and its subdirectories, and copies them to the destination directory.
