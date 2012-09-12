##Lab Worksheet \#1
#####Resident TA: Jon Gluck
***

###What is this?
One set of correct answers to the questions on Lab Worksheet #1.

###Question 1

a)
	
	if(a)
		printf("some output\n");
	
value that would make the printf print: 1

value that would make the printf not print: 0

b) 

	if(!a)
		printf("some output\n");
		
value that would make the printf print: 0

value that would make the printf not print: 1

c)

	if(a||!b)
		printf("some output\n");
		
value that would make the printf print:  a = 1, b = 0

value that would make the printf not print: a = 0, b = 1

d)

	if((a<b)!=(a==b)) 
		printf("some output\n");
		
value that would make the printf print:  a = 1, b = 1

value that would make the printf not print: a = 2, b = 1

e)

	if(a+b)
		printf("some output\n");
		
value that would make the printf print:  a = -1, b = 40

value that would make the printf not print: a = 0, b = 0

###Question 2 

Consider each of the following while loop outlines, where stmts1 and stmts2 represent arbitrary statements (we don’t know what they are), and a and b are declared of type int, and done is an int variable with value 0.

Determine the following:

a. Which loops will quit before the next iteration if a becomes equal to b in stmts1?

	1,2,3,4

b. Which ones will quit before the next iteration if a becomes equal to b in stmts2?

	4

c. Which ones will execute stmts2 before quitting if a becomes equal to b in stmts1?

	1,3,4
	
	
###Question 3

The correct output for this is:

	2 1
	enter fn: 2 3 4 5
	leave fn: 6 7 12 14
	6 1
	enter fn: 6 7 4 14
	leave fn: 6 7 12 23
	6 1