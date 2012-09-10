##Notes for Class Sept10
#####Resident TA: Jon Gluck
***

###Getting Comfortable in Our Environment

The purpose of today's lab is to show you how to get a graphical environment, as well as to show you a few basic emacs tricks.

###X-forwarding and you

Terminals are great but sometimes its helpful to use a graphical environment. For instance it is nice to be able to interact with programs using the mouse. Linux uses a graphical environment known simply as _X11_. Being able to access X11 remotely will be a huge help over the course of this semester. Most programmers find it more pleasant to work outside of the terminal.


Luckily for us it is relatively easy to send this graphical information through our SSH connection. 

####X-forwarding on Linux

If you are running a distribution of Linux X-forwarding is trivial. Remember how you SSH'd into the grace cluster last week?

	ssh myCSUserName@Linux.grace.umd.edu
	
Good. Well now you're going to add a few more options to that command. Try the following:

	ssh -X -C myCSUserName@Linux.grace.umd.edu
	
The _-X_ option is what sets up X-forwarding. _-C_ requests that all data be compressed. This is an optional flag which you can remove if things act odd, but it should speed up your connection.

You can verify that this worked by running:

	Firefox
	
If (after a few seconds) Firefox pops up, you're good.

####X-forwarding on OSX

If you're on a mac, X-forwarding is also pretty easy. There is just one additional step. Before you run the following line in your favorite terminal:

	ssh -X -C myCSUserName@Linux.grace.umd.edu
	
You will need to run a program called X11. You can find this by using spotlight or by navigating to _Applications>Utilities>X11.app_. Once this is open, you should just run:

	ssh -Y -C myCSUserName@Linux.grace.umd.edu
	
In your favorite terminal. (Basically this prepares OSX to receive X11 windows). Note that we changed -X to -Y. Don't ask me why, -Y just seems to work better on macs. They should be functionally identical. 

####X-forwarding on Windows

This is where things get tricky. Both OSX and Linux have built in X-servers. Windows does not. However, there is a free X-server for Windows. It is called xming and it is absolutely worth getting. You can download it [here](http://sourceforge.net/projects/xming/files/Xming/).

Unfortunately, you'll need to do a little more set up than the mac or Linux folks. You should only need to do this once though! After installing xming, you should run it by opening it from the Start menu. 

Now open up PuTTY and load your saved preferences. In the left pane of PuTTY you should see a whole bunch of preferences, underneath connection click the + next to ssh and then click on X11. That is connection>ssh>X11. 

You should check the box next to _"Enable X11 forwarding"_. In the X display location box you should enter:

	localhost:0
	
Now save your settings again.

From here on out, in order to SSH you should open xming and PuTTY before connecting. You can also try typing:

	Firefox
	
to see if things worked.

####Tricky bits

You can now run more than one program at once through SSH. (If those programs are graphical.) Try typing:

	Firefox

You'll notice that, even though Firefox has finished launching, you can no longer do anything in your terminal. This is because Firefox's process has grabbed the terminal's **STDIN** (what you type into the terminal) and **STDOUT** (what the terminal displays). You can avoid by adding an "&" to the end of any command. This makes the program run in the background. For instance:

	 Firefox &
	 
Try that, you should notice that you can now also launch:

	emacs &
	
and anything else you want without gunking up the terminal.

####If you REALLY don't want to use X-forwarding

That's alright, there is a non-graphical version of most of the programs you will use this semester. Most importantly EMACS can be run without graphics by typing:

	emacs -nw
	
***

###Emacs

Oh boy. Okay, so there is something of a conflict between programmers who use VI, and programmers who use Emacs. Think of it as sort of a college team rivalry. You can read a bit more about this [here](http://en.wikipedia.org/wiki/Editor_war). I use VI; however, I'm going to be endeavoring to teach you all Emacs so bear with me.

####Opening a file in Emacs

You can run emacs simply by typing:

	emacs &

however, most of the time you have a file in mind that you want to edit. The file doesn't even need to exist yet. You can do this by typing:

	emacs <Filename> &
	
####Saving and Quitting

The next most important things are how to save and how to quit. If you want to save in Emacs you can type:

	<ctrl> X <ctrl> S

In Emacs commands are invoked by holding down the control key. In the above command, and in all other cases, you should hold down control for the entire duration of the command. If you want to quit Emacs you can type:

	<ctrl> X <ctrl> C
	
and the editor should exit.

####Example: Hello World in Emacs

We're going to run through programming a simple HelloWorld.C program in Emacs and compiling it. Begin by opening helloWorld.c in emacs.

	emacs helloWorld.c &
	
Now paste the following code into emacs:

	/* Hello World program */

	#include<stdio.h>
	
	main()
	{
		int x = "apple";
    	printf("Hello World");
		printf("Goodnight Moon")

	}
	
	
Save the file by typing:

	<ctrl> X <ctrl> S
	
Now hit the escape key and then X. This will put you in execute mode. While in execute mode type:

	compile
	
and hit enter. You should see emacs suggest "make -k" as a compilation command. Instead you should erase that and type:

	gcc helloWorld.c
	
OH NO! There were errors in the file. Luckily for us we were using emacs. If you click on any of the errors in the bottom frame emacs will move your cursor to the syntax error. This can be very helpful in large files. Fix these errors and then try compiling again. 


 

####Helpful Links

You can also find these Emacs cheat sheets on the class's [Reources Page](http://www.cs.umd.edu/class/fall2012/cmsc216/resources.shtml) but [Here](http://www.rgrjr.com/emacs/emacs_cheat.html) is one and [Here](https://ccrma.stanford.edu/guides/package/emacs/emacs.html) is another. 
	

***

###A few more UNIX concepts

I know you are all in love with UNIX by now.

####TARBALLS

 Files that end in .tgz are known as "tarballs". They are just compressed files, a lot like .zip or .rar files. You can create a tarball by putting all the files you want compressed in a directory and running:

	tar -pczf <name_of_your_archive.tar.gz> </path/to/directory>

You can unzip these by running:
	
	tar -xvf <myTarfile>.tgz
	
####Wildcards "*"

We went over the cp and mv command the other day. These commands take file names as arguments; however, what if we wanted to specify a few files to mv, or maybe just mv all the files? This can be accomplished with the wildcard _"*"_.

If you type the following:

	cp * ~/.
	
it will copy all the files in your current directory into your home directory. That is because the wildcard matches ALL file names. What if we only wanted to copy file names that begin with "myF"? We can do this too:

	cp myF* <destination>
	
This will copy all files that begin with "myF" to the destination you specified. This is particularly useful and might show up on a future quiz. 

**WARNING** - Be careful when using this with mv and rm. It can cause changes that are hard, or impossible, to correct.

