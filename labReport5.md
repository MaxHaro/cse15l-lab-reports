# Lab Report 5: CSE Labs "Done *VERY* Quick"
One of my favorite parts about CSE 15L was the lab from Week 7, where we did a competititon to see who could run a series of tasks the fastest. This lab report revisits the concept from that lab and we attempt to make the FASTEST run yet.

## The Challenge Tasks
1. *Setup - Delete any existing forks of the repository you have on your account*
2. *Setup - Fork the repository*
3. *Setup - The real deal Start the timer!*
4. Log into ieng6
5. Clone your fork of the repository from your Github account
6. Run the tests, demonstrating that they fail
7. Edit the code file to fix the failing test
8. Run the tests, demonstrating that they now succeed
9. Commit and push the resulting change to your Github account

Now, the point of the competition was to see who could perform this series of tasks the fastest WITHOUT using a bash script, but today, we are trying to do the *fastest* bash script to complete these tasks, which should be far quicker than our human attempts.

## The Script
Originally, this is what my script looked like:

```
//BEFORE//
//INSIDE fix.sh//
ssh cs15lwi23adg@ieng6.ucsd.edu
git clone git@github.com:MaxHaro/lab7.git
cd lab7
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
sed -i '43 s/1/2/1' ListExamples.java
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
git add ListExamples.java
git commit -m “C”
git push
```

It's pretty much a line-by-line instruction list for the computer to do for me. In fact, these are the same commands I gave the machine when I first did the lab in class.\
So it should be simple and straight-forward, right? Well I was not getting the correct behavior that I was hoping for.
Instead, when I would try and run a series of commands on the remote server, only the first command would execute to establish an SSH connection to the remote server, bringing the rest of the script to a halt.

I did some research online and found that in order to execute the rest of the commands on the remote server, I need to pass them to the SSH command using the `-t` option, which allocates a terminal session on the remote server to run the commands.

So with this in mind, I updated the bash script to look like this:

```
//AFTER//
//INSIDE fix.sh//
ssh -t cs15lwi23adg@ieng6.ucsd.edu '
    git clone git@github.com:MaxHaro/lab7.git
    cd lab7
    javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
    java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
    sed -i "43 s/1/2/1" ListExamples.java
    javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
    java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
    git add ListExamples.java
    git commit -m "C"
    git push
'
```

It's basically the same code I had originally in mind but we're passing all the commands inside a single-quoted string to the `ssh` command using the `-t` option. This way, the commands will be executed on the remote server, and the output will be printed to your local terminal.

## The Real Deal

With the bash script ready to go and with all the setup steps complete, the only thing that is left is to test the script.\
Here's how it went:

![image](https://user-images.githubusercontent.com/122497486/224918501-9ee84211-2659-4e02-bf0c-7a1221969b5f.png)

In significantly less time, we were able to complete all the tasks by typing a single line of code into the command-line.

![image](https://user-images.githubusercontent.com/122497486/224919569-7996d2d9-2008-4d87-a33d-1f7a6f234d3d.png)

Here is some confirmation that the file was pushed to GitHub successfully. We did it!

What's interessting about this is that we never see the welcome message that the user normally gets when they establish an SSH connection.\
Another thing that caught my eye was that the SSH connection actually ends the second that the commands are run.\
