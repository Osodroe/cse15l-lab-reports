# Week 7 – Vim

## Part 1: 

For this part, we are going to demonstrate how fast vim can be used to change a file. <br>
Specifically, we are going to show you how to change the name of the start parameter of getFiles, and all of its uses, to instead be called base in our DocSearchServer.java file. 

![Vim Example](/cse15l-lab-reports/labs/images/lab-5/VimExample.png)

It's easy to replace all the start in getFiles by typing: \<shift\>;10,30s/start/base \<enter\>
This gets you this: 

![Vim Result](/cse15l-lab-reports/labs/images/lab-5/VimResult.png)

Then, all you need to do is save and quit with the command \<shift\>;wq \<enter\>
In the end, you should have this before quitting:

![Vim Save](/cse15l-lab-reports/labs/images/lab-5/VimSave.png)

So, with \<shift\>;10,30s/start/base \<enter\> \<shift\>;wq \<enter\>, a 23 key press series of commands, you can edit, save, and quit the file with the correct changes made. 

## Part 2: 

This is all about figuring out, is it faster to edit local and run remote or should you edit on the remote as well.

Well, after editing, copying the file over to the remote, and running test.sh, I was able to finish in around 1 minute and 4 seconds.

After logging into the remote, finding my file, editing with vim, saving, and running test.sh, I was able to finish in 42 seconds. 

If I had to run the file remotely, then I would most likely edit remotely, especially on a device that may require me to enter a password to log in or copy a file over everytime. It is show to be much faster, and just using vim more often will allow me to get more used to the control and thus be faster.

I think it really comes down to the local device I am working on. For example, do I have to type in a password to get to the remote? Can the local device run bash? Do I have to write from scratch or am I editing an already made file? All of these have a huge affect on my choice. If it's faster to just edit locally and send over then I will work with what I'm more familiar with. If I'm not limited by my local deivce, then I can probably do all the work locally and just send the final work to the remote. And since I'm not experiened with vim, taking on a whole file from scratch may be too much and it would be much easier to just do what I can locally.