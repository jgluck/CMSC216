##Notes for Class Sept26
#####Resident TA: Jon Gluck
***

###Debugging C: gdb and why its your friend

The purpose of today's lab is to show you gdb (a fantastic debugger for C) and get you acquainted with some of its features.

###What is a Debugger?

Debuggers are basically programs you can run that latch into your currently running program. You can set breakpoints (pauses in code execution) and step through the instructions step by step, checking values along the way. Extremely useful for finding out where things went wrong.

####That sounds great! Gimme! (How to use gdb)

In order to hook gdb into your program you're going to need to add yet another compilation flag to gcc. This flag is:

	-g

This flag basically allows gdb to get a hold of line numbers and variable names that might otherwise not be included in the executable to save space. 

Now that you've successfully compiled your program with hooks for gdb you just need to run it in gdb. This can be done two ways. Lets say I have an executable I've compiled with this command:

	gcc -g -o awesome.exe supercool.c
	
I have two choices in how to run this with gdb. The first option is from the command line. 

	gdb awesome.exe
	
The other option is from within gdb, in which case you would just need to run:

	gdb
	(gdb) file awesome.exe


#### Running your executable

Now that gdb has our executable we can tell it to run using the command:

	r
	
This will tell gdb to run until it hits a breakpoint (or crashes, or returns successfully.) 

####Exiting gdb

If you are done with gdb and you want out, simply type:

	quit
	
or

	q
	
####Useful commands

Now you're inside of gdb, what do you want to do? Well you can print the segment code where gdb is currently looking by typing:

	list
	
or
	
	l
	
This should cause gdb to output something a bit like:

	(gdb) l
	4	
	5	extern int a;
	6	static int b= 1;
	7	
	8	int main() {
	9	    printf("%d %d\n", a, b);
	10	    fn();
	11	    printf("%d %d\n", a, b);
	12	    fn();
	13	    printf("%d %d\n", a, b);
	
Now you seem to be having an error in fn() so you can set a breakpoint (pause in execution) on line 9 by typing:

	break 9
	
or

	b 9
	
Now when you run the program with "r" its execution should halt at line 9. You can step through the program using either the "Step" command or the "Next" command.

	step
	s

or 

	next
	n

The big difference between these two is that step will step into function calls whereas next will step over them.

If you grow tired of stepping through the function you can cause it to coninue its execution normally by typing

	cont

or

	c

####Advanced breakpoint commands

So we've already talked about breakpoints and how useful they are but there is so much more.

We've gone over how to set breakpoints, but maybe we want a breakpoint that only exists until you hit it once. This can be accomplished with the

	tbreak
	
command. What if you get tired of a breakpoint? Well you can delete it with 

	delete
	d
	
If you have set so many breakpoints that you've lost track of them you can always get all of their info with

	info breakpoints
	i b

Sometimes we just don't care about setting a breakpoint at a line. Maybe we want to set a breakpoint on if a variable gets modified. We can do this with the watch command.

	watch <var>
	w <var>
	
####Data examination!!

So you've set a breakpoint the line before a colossal error, you know that if you type "n" your program will execute the bad code and crash, what do you do? Well one thing you can do is try to figure out a bit about the current program state. You can print the value of any known variable (in your current scope) by typing 

	print <var>
	p <var>
	
Lets say you want to know the value of a variable every time execution is stopped (perhaps a counter or an iterator.) You can accomplish this with

	display <var>
	d <var>
	
you can remove a display with the undisplay command. You can list the values of all current local variables with 

	info locals
	i locals
	
Lets say you want to see where you are in the execution stack (which function you're in and who called it.) Well this can be done with the command:

	where
	
you can navigate this stack using 

	up
	down
	
to allow you to view variables in the scope of the other functions.

######GDB EMACS

There is a fancy gdb Emacs mode. I am not entirely familiar with it but we can try and figure it out. It is activated from within Emacs by typing

	M-x "gdb" <enter>
	
You will have to enter the name of the program you want to debug. Then you can work with gdb just the same as from the command line, with a few extra graphical features.
	
	