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

