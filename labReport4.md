# Lab Report 4: CSE Labs "Done Quick" Challenge
* In this lab report we will be going over the lab task for Week 7.

## Steps 1-3 : These steps are skipped because they are meant to help with the setup for the challenge.
## Step 4: Log into ieng6
Keys pressed: `<up><enter>`\
The ssh command was 1 up in the search history, so I used up arrow to access it. 

![image](https://user-images.githubusercontent.com/122497486/224593657-db99fc91-afa2-476e-ba0e-b823a41f0538.png)

## Step 5: Clone your fork of the repository from your Github account
Keys pressed: `<typed git clone><^C><right-click>`\
Typed `git clone`, copied the link to the repository using `<^C>` and pasted the link using `<right click>`.

![image](https://user-images.githubusercontent.com/122497486/224593894-df7edaa4-f007-4203-84de-ae6166190ea8.png)

## Step 6: Run the tests, demonstrating that they fail
Keys pressed: `<typed cd l><Tab><Enter><^C><right-click><enter><^C><right-click><enter>`\
Typed `cd l` and autocompleted using `<Tab>` which completes to cd lab7.\
Copied javac command using `<^C>` and pasted onto terminal using `<right-click>`\
Finally, copied java command using `<^C>` and pasted onto terminal using `<right-click>`

![image](https://user-images.githubusercontent.com/122497486/224594253-a48a92dc-e0a1-495b-9b1a-9be1617cd6da.png)

There's some bugs in the code! How do we fix it?

## Step 7: Edit the code file to fix the failing test
It looks like the bug is caused by a small typo in line 43 of ListExamples.java. Let's look at it...

![image](https://user-images.githubusercontent.com/122497486/224595493-56a79402-66e1-4711-8b9f-c1c9532d6240.png)

Keys pressed: `<typed sed -i '43 s/1/2/1' L><Tab><typed .java><enter>`
Typed the sed command and autocompleted from just L to ListExamples using `<Tab>` and completed the rest typing.
The overall effect of the sed command is to find the first occurrence of the character "1" on line 43 of the file "ListExamples.java" and replace it with the character "2", and save the changes back to the file.

![image](https://user-images.githubusercontent.com/122497486/224594358-aa697a1a-1123-4e55-8928-97a251d7600b.png)

If we were to look at the file after the sed command has run, it would look like this:

![image](https://user-images.githubusercontent.com/122497486/224595321-aec5519f-5bfe-436d-b63f-ab682661f380.png)

## Step 8: Run the tests, demonstrating that they now succeed
Keys pressed: `<up><up><up><up><enter>`, `<up><up><up><up><enter>`\
The javac command was 4 up in the search history, so I used the up arrow 4 times to access it. After that, the java command was 4 up in the history, so I accessed it and ran it in the same fashion.

![image](https://user-images.githubusercontent.com/122497486/224594627-c1344c75-89e5-4d95-b3a4-96baab18ab52.png)

## Step 9 : Commit and push the resulting change to your Github account
Keys pressed: `<typed git add ListExamples.java><enter><typed git commit -m "C"><enter><typed git push><enter>`
Typed `git add` command to add ListExamples.java to the list of files to commit. Then, typed `git commit` command to commit changes. Finally, pushed changes using `git push`.

![image](https://user-images.githubusercontent.com/122497486/224595809-48a36e18-4221-475e-91b5-d4089b09c647.png)
