##Questions
#####Resident TA: Jon Gluck
***

###What is this page?

I want a place to try and share the questions I've received from you guys and my _attempted_ answers.

***

####Quiz Sept 12

#####Question:
	
	How do you copy all c files present in the directory to your home directory
	
#####Answer:

As to the UNIX command that copies all c files present in the directory to your home directory, 

you know that you want: "cp", but how do you copy multiple files at once? In your terminal the "*" character is also known as the "wildcard."

Lets say you are in some directory (it doesn't really matter which.)

if you were to type:

	cp * ~/.

that would copy ALL files from wherever you currently are into your home directory. This is because * is in the source argument and all file names match the wild card.

What you can do is add to the wild card and it will only work on files that match, such as:

	cp c*t.txt ~/.

This would copy files like:

	cot.txt
	cat.txt
	cant.txt
	cmylongfilenamethatbeginswithcandendswitht.txt

to your home directory. Because c files all end with ".c" you should be able to figure out how to use this wildcard to copy all ".c" files to your home dir. 


#####Question:

	What are flags and how do they relate to gcc?
	
#####Answer:

The word _flag_ is really just another word for _option_. When we call commands at the command line we can use these _flags_ or _options_. For instance in the case of "_ls_":

	ls -l
	
uses the "_-l_" flag which tells the program to list additional information about the contents of the directory.

gcc is a very complex program and as such has hundreds of possible flags. One common flag is "_-o_"

	gcc -o myAwesomeProgramName myPrettyGoodCode.c

 which allows you to define the name of the output executable (your compiled program). If this flag isn't set, the compiled executable will simply be called "a.out". If you want to read more about gcc's flags you can find a [list of all of them](http://tigcc.ticalc.org/doc/comopts.html) online.
 
#####Question:

	How do you run shell commands from inside of Emacs
	
#####Answer

If you remember the notation for Emacs commands M- is the meta key (escape) and C- (is control). In order to run shell commands from inside of Emacs the key stroke is:

	M-! <Command>

#####Question

What does it mean to dereference a pointer?

#####Answer

Ok so we know that a pointer is a variable that holds a memory location for a given type. These look a bit like the following:

	int*
	char*
	void*

lets say we have an actual int (not a pointer) called 'a'

	int a = 37;


We also have an int* (a pointer to an int) called 'myPointer'

	int* myPointer;

we can set myPointer to point at our int 'a'.

	myPointer = &a;

Just for the sake of argument we're going to claim that 'a' was located at memory address 0x083. Which is now also myPointer's value. Dereferencing a pointer means reaching through the pointer to the data stored at the memory location. This looks like the following.

	*myPointer

The following print statements and their outputs should give you some information.


	Code: 
		printf("MyPointer: %p Address of a: %p\n", myPointer, &a);  

		printf("MyPointer dereferenced: %d value of a: %d\n", *myPointer, a);

	Output:
		MyPointer: 0x083 Address of a: 0x083
		MyPointer dereferenced: 37 value of a: 37

Hope that Helps!


