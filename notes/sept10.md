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

You'll notice that, even though Firefox has finished launching, you can no longer do anything in your terminal. This is because Firefox's process has grabbed the terminal's **STDIN** (what you type into the terminal) and **STDOUT** (what the terminal displays). You can avoid by adding an "&" to the end of any command. For instance:

	 Firefox &
	 
Try that, you should notice that you can now also launch:

	emacs &
	
and anything else you want without gunking up the terminal.


	


