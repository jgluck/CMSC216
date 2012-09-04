##Notes for Class Sept4
#####Resident TA: Jon Gluck
***


###What is the purpose of this class?

1) Get closer to what's really going on with the machine. 

2) Get comfortable with UNIX

###Our Environment


We're going to be programming in C, which is one heck of a language. Many people say C is basically high level machine code.

We're going to be using the UNIX operating system. Some modern systems you might know use UNIX:
	* Mac OS X
	* Ubuntu (Linux in General)
	* iOS

This class is going to use the EMACS editor. I'm a fan of Vim, the other big editor, so bear with me as I try to help you. 

###Connecting to the cluster


Although you have to option work on your own machines, we're going to be using the Linux grace cluster this semester. There are several ways to connect to this cluster from your laptops. More detail may be found at [THIS](http://www.cs.umd.edu/~nelson/classes/utilities/BasicUnix.html) link.

####Linux or OS X

Connecting from either of these operating systems is relatively easy as you already have SSH (Secure SHell) installed. Open your favorite terminal app. (In OS X this may be found at /Applications/Utilities/Terminal.app, you can search for it in spotlight).

When the terminal comes up you should see a prompt that looks something like:

	MyUserName@MyAwesomeComputer: 
	
to connect to the grace cluster you should type
	
	ssh myCSUserName@Linux.grace.umd.edu
	
and hit enter. You should be prompted for your password, which you should type and hit enter. No characters will show up, this is a security feature. If you think you mistyped something, just hold down backspace for a few seconds and try again.

If you see something that looks like this:

	grace#:~:
	
then you're good.

####Windows

Connecting from Windows is a little more complicated, but is made easy by a program called PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html). There are plenty of good tutorials online for how to connect using PuTTY, [here's one](http://kb.mediatemple.net/questions/1595/Using+SSH+in+PuTTY+%28Windows%29#gs). When you first open putty you'll see a box labeled 

	HostName (or IP address)
	
Fill that box with:

	MyCSUserName@linux.grace.umd.edu
	
and hit Open. This should prompt you for your password. If you see something that looks like this:

	grace#:~:
	
then you're good.

***

###Setting up our Environment

Because this class uses a few special tools that aren't set by default, we need to run a quick setup script that changes a few options for us. You can run this script by entering:

	/afs/glue/class/fall2012/cmsc/216/0101/public/bin/setup_216
	
into the prompt and hitting enter. (This should be done on a Grace machine). If no complaints come back then you should be good. You should only run this script once, it is designed to not work a second time. (If something goes wrong just tell me and I'll try to help).

####What did this do?

This script did three things, and we can quickly check to see if they worked.

1) It added a line to our $PATH variable. This allows your terminal (shell) 
to access additional programs. Your $PATH variable is a list of places to look for programs. We can check to see if this step worked by typing.
	
	source ~/.path
	rehash
	which submit
	
We should see:
	
	/afs/glue/class/fall2012/cmsc/216/0101/public/bin/submit
	
and not:

	/usr/local/scripts/submit
	
2) It created two symbolic links _(Think of these as shortcuts)_. One to the course public space, and one to your individual extra work space. This is important because the space credited to your account is very limited, and files you put in these folders do not count towards that limit. we can check to see if this worked by typing:

	cd ~/216/
	pwd

pwd stands for _Print Working Directory_. This should print out something like:

	/afs/glue/class/fall2012/cmsc/216/0101/MyCSName
	
This is the folder to which the symlink _(shortcut)_ we put in your home directory points. Its really important to try and keep your work for this class in that directory so you don't run up to your disk limit.

3) It switches the version of Java used by your environment. This is important for the handin scripts you'll be using. To test this type:

	source ~/.cshrc.mine
	rehash
	which java
	
this should print:

	/afs/glue.umd.ed/software/java/current/sys/bin/java

***
	
###UNIX... 

Explaining all of UNIX to in such a short time would be impossible (partially because I don't know all of UNIX). Here are some helpful programs and concepts though!

####What are these folders ~/ , /usr/local, etc?

The file system in UNIX is structured in a hierarchical tree. That is, the root folder:

	 /

is the very highest folder in this tree. The root folder contains folders such as:

	/bin /dev /mnt /home
	
which in turn have folders inside of them. when you type something like:

	/afs/glue/class/fall2012
	
you're specifying the location of the files you care about in that tree. Sometimes you'll see a tilde in these paths. For instance:

	~/

tilde is just shorthand for your home directory. for instance if you type

	echo ~
	
it will tell you what it stands for.

	~/
	
is equivalent to

	/homes/MyCSName
	
Other interesting directory aliases are **./** and **../**. **./** refers to the current directory, and **../** refers to its parent directory. These paths are relative. Assume you are in the following directory:

	/home/sam  <----- your current location
	
the following is a valid reference to a directory

	../../home/./.././home/sam/./../sam
	
and, in fact, it points to the same directory you were already in. See if you can parse the relative path.

####Auto Complete and Command History

Arguably the most useful shortcuts you can learn are auto completion (sometimes called tab completion) and command history. They remove a lot of repetition, so make sure you use them!

#####Auto Complete

when typing a command you can double tap the tab key. This will prompt your shell to suggest possible endings for what you wanted to type. For instance if I wanted to cd to:

	/home/MyCSName
	
I could type:
	
	/hom

and then double-strike tab. This autocompletes to:

	/home/
	
If I were to double-strike tab again, it would provide me with a list of all of /home/'s chid directories. 

#####Command History
If you ever want to re-run a command, instead of retyping it, you can just hit the up arrow key to scroll back through your previous commands. This is a huge time saver, especially when you make typos.


####Some useful commands

+	**ls**  _Lists the contents of the current directory. Super useful._
+	**ls -l** _Most programs in UNIX have command line flags like the -l here. This will display the permissions on the files, as well as other helpful data_
+	**cd \<target dir\>**_Change dictory. Your second most used command, lets you switch between dirctories_
+	**pwd** _Print Working Dictory. Outputs the name of your current directory_
+	**mv \<source\> \<destination\>**	_Allows you to move files and folders from \<source\> to \<destination\>_
+	**cp \<source\> \<destination\>** _Allows you to copy files from \<source\> to \<destination\>_
+   **rm \<target\>** _Removes target file_
+	**mkdir \<dir name\>** _Creates a directory with name \<dir name\>_
+   **rmdir \<dir name\>** _Removes an empty directory with name \<dir name\>_
+	**logout** _Seems self explanatory ;)_
+	**man \<command\>**	_Very important command that lets you look up the instructions for other commands. Most useful. There may be multiple man pages for a given command (the same name for different commands.) There are [helpful guides](http://www.cs.bgu.ac.il/~arik/usail/concepts/basic-unix-know/man-pages.html) on using man_



