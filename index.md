# How to log into a course-specific account on `ieng6`.

## Step 1: Installing VSCode.

In order to download VSCode, you're gonna want to visit the following website <https://code.visualstudio.com/> and follow the instructions for your specific OS.

Once you've installed VSCode on your PC and opened the application, you should see a window that looks something like this:

![image](https://user-images.githubusercontent.com/122497486/212068353-9fad66e5-70cd-4eb7-a07b-47c7faab8f31.png)

Now that you've succesfully installed VSCode onto your computer, we can now use the built-in terminal to remotely connect to your account.

## Step 2: Remotely Connecting.

If you are using a Windows computer, first you need to install [git](https://gitforwindows.org/) for Windows.

After you've installed git with all the default settings, we are now ready to use `git bash` in VSCode to remotely connect to a server.

#### Using `git bash` on Windows in VSCode:

1. Open a new VSCode window and open a terminal using the `Terminal` -> `New Terminal` menu option.

![image](https://user-images.githubusercontent.com/122497486/212080071-b04d6522-637d-4f29-a453-a68a2d0cefbc.png)


2. Once the new terminal pops up, enter the following command with the `xxx` replaced by the letters in your course-specific account:\
`$ ssh cs15lwi23xxx@ieng6.ucsd.edu`

3. Because it's your first time connecting to this server, you will get a message prompting you to enter yes/no. Go ahead and type `yes` and press enter.

4. Enter your password and after that you should receive a message that looks like this:

```
Last login: Tue Dec 14 10:48:47 2021 from 43.sub-174-195-143.myvzw.com
Hello cs15lwi23xxx, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   05:20:01   3  0.02,  0.12,  0.12
ieng6-202   05:20:01   1  0.01,  0.07,  0.07
ieng6-203   05:20:01   1  0.06,  0.13,  0.11

 
Thu Jan 12, 2023  5:22am - Prepping cs15lwi23
```

You are now succesfully connected to a computer other than your own through a server! Let's see what types of commands we can run...

## Step 3: Trying Some Commands.

Some useful commands you might want to try include:
* `cat <path1> <path2>`
* `ls <path>`
* `pwd`
* `cd <path>`

Let's see what happens when we try using the `ls` command inside the cs15lwi23 directory:

![image](https://user-images.githubusercontent.com/122497486/212083338-2c5fd4b8-5a82-485d-a462-b959a0580189.png)

Look, now a list of all your other classmates' accounts appeared! 

What do you think will hapeen if we try to access the directory to another person's account?

![image](https://user-images.githubusercontent.com/122497486/212084402-f4a98657-5c47-4b80-b968-cd745740eccc.png)

Have fun experimenting with different commands! 

Once you are ready to exit the remote server, run the `exit` command or use `Ctrl-D` to log out.
