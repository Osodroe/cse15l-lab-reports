# Week 1 – Remote Access and the Filesystem

## Step 1: Visual Studio Code

[Visual Studio](https://code.visualstudio.com/)

For this course, we were expected to visual studio code. So, if it is not already downloaded onto your device, you must do so now. Provided is the link to their website, from there you can download the program. Continue to step 2 once you see something like this:

![Visual studio startup page](/cse15l-lab-reports/labs/images/VSExample.png)

## Step 2: Remotely Connecting

Now it's time to actually log into your remote account. To log in, you have to use `ssh (account name)@ieng6.ucsd.edu` command. You will then be prompted to enter a password, which you should have set up prior to this lab. Continue to step 3 once you see something like this:

![Logged In Succefully](/cse15l-lab-reports/labs/images/LoggedInExample.png)

## Step 3: Run Some Commands

Running some commands is important for understanding what is available to you in your remote workplace, the commands available, and to just generally undderstand how to interact with a computer in this new way. Feel free to `sd`, `sd ~`, and `cat /home/linux/ieng6/cs15lfa22/public/hello.txt` are all good commands to run, but they are by far not the only ones. Down below is an image of an example of some commands, but feel free to move on to step 4 as soon as you feel you have practiced enough.

![Command Examples](/cse15l-lab-reports/labs/images/CommandExample.png)

## Step 4: Moving Files over SSH with scp

```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
Now it's time for some of the most useful reasons to use this kind of remote connection, being able to transfer files remotely between your device and another. Above is a simple java program, feel free to copy it into and save this as a `WhereAmI.java`. Then you just need to find the file in your directory and compile and run the file with the `javac WhereAmI.java` and `java WhereAmI.java` commands which will run the now compiled program. This is assuming you have Java installed on your computer, if not you can downloud it now or later. Then type `scp WhereAmI.java (account name)@ieng6.ucsd.edu:~/` and enter your password. The file should now be in your remote device where you can compile and run it with no issue, and you should see something like this: 

![File Transfer Example](/cse15l-lab-reports/labs/images/FileTransferExample.png)

## Step 5: SSH Keys

After all this logging in and logging out, it's time to set up a key so that you'll never have to type in a password again! Immediately logging in and file transfer makes everything a lot faster if you have to be jumping between local and remote devices. To make the key, you have to use the `ssh-keygen` command on your local device. You will be prompted to enter a file and passcode, pressing enter without entering anything will set them to their defaults which is prefered in this case. You should see something like this:

![Making a Key](/cse15l-lab-reports/labs/images/KeyRandomArt.png)

Next, you have to make the directory for the key to be stored on your remote device. Simply log in, use the command `mkdir .ssh` to create the directory, and log back out. Now, we just have to copy over the key from directory given provided to use during the generation of the key and save it into the directory you just created with a command that looks like `scp /Users/user/.ssh/id_rsa.pub (account name)@ieng6.ucsd.edu:~/.ssh/authorized_keys`. Now you should be able to log in without being prompted for a password, and should be able to move on to step 6 and see something similar to this in your prompt: 

![Transfering My Key](/cse15l-lab-reports/labs/images/KeyTransferExample.png)

## step 6: Optimizing Remote Running

Now we can log in easily and quickly, it's time to make other parts of this process faster. For example, if you include `"(commands)"` on the same line as you log in, those commands will be run as well. So, we can quickly take local edits to a file, like `WhereAmI.java`, and quickly copy over the edits in one line. For example, I edited my `WhereAmI.java` to also output some related text. Now, I'm going to quickly transfer and run the new `WhereAmI.java` in my remote device with one command. 

![Transfering My Key](/cse15l-lab-reports/labs/images/OneLineExample.png)

With that, we should have a basic idea on how to interact with a remote computer! Good luck with the next labs!