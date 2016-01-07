# Backmasking
AD325 - Assignment 1 - Backmasking
Assignment: Backmasking

Back

Objectives

Gain familiarity with implementing stacks.
Gain familiarity with raising exceptions.
The goal of this assignment is to ease back into programming by implementing the stack abstract data type using two different data structures.

Overview

Backmasking is the technique of recording an audio track backward. Its use was popularized by the Beatles and used rather extensively at that period; other artists using backmasking include Jimi Hendrix and Ozzie Ozbourne. We will use a stack to reverse a digitized sound file.

Most of the work for this application has been completed already. Here is the starting point code:

ReverseDat.java
NumberStack.java
LinkedStackNode.java
Your task is to implement NumberStack. It is a simple ADT, a stack that holds double values:

public interface NumberStack {

   public void push(double number);

   public double pop();

   public double peek();

   public boolean isEmpty();

   public String toString();

}

Notice there are no comments in this source code file.

Here are quick recaps of the methods of this interface:

The push and pop methods should be pretty obvious. They are mutators, changing the state of the stack.
The push method adds the parameter value to the top of the stack.
The pop method removes the top element of the stack, returning that value.
The pop method throws IllegalStateException is the stack is empty.
The peek method is an accessor, returning the top value in the stack, without changing the state of the stack. The peek method throws IllegalStateException is the stack is empty.
The isEmpty method is another simple accessor. This should be pretty obvious as well.
The toString method violates the abstraction of a stack. It's an accessor that creates a String representation of the all of the values within the stack.
The values are separated by spaces within brackets. The top of the stack is to the left; the bottom, to the right.
For example: [0.5 1.0 1.5]
An empty stack is represented by empty brackets: []
Implementing the toString method is optional. In fact, it can be completely ignored when implementing the interface. However, it can be very helpful in debugging your code.
Use String concatenation to create string representations of the double values in the stack.
The correct implementation must avoid OBOE. Use the "fencepost" algorithm.
For this assignment, you will create two implementations of NumberStack:

ArrayStack, which uses an array as the underlying data structure, and
LinkedStack, which uses a linked list as the underlying data structure. Use LinkedStackNode when implementing the underlying linked list.
These classes are used on lines 21 and 23 of ReverseDat.java.

Minus Version

These are the tasks for the minus version:

Create ArrayStack.java which will implement NumberStack using an array as the underlying data structure.
The implementation will need fields for the array of doubles and an int counter which indicates how full the array is.
The initial size of the array is 10 elements.
When the array is full, the next call to push will create a new array which is twice as big as the current array.
Use java.util.Arrays.copyOf to create and populate the new array. This is the only time your code should use any resources from java.util.
Create LinkedStack.java which will implement NumberStack using a linked list as the underlying data structure. This should use LinkedStackNode internally.
Omit the implementation of toString from both ArrayStack and LinkedStack.
Include JavaDoc comments in both ArrayStack and LinkedStack. Remember to include a comment for the class, as well as for each of the four (five) methods.
Download and reverse the following sound files. These are all short clips (sound bites) from movies.
movie1.wav
movie2.wav
movie3.wav
Use sox (SOund eXchange) to create .dat files from these sounds files. See Background Information for more details.
Create an ASCII text file, readme.txt, which answers the following questions:
How did you test your implementations of NumberStack?
Use sox and ReverseDat to reverse the three sound clips, movie1, movie2, and movie3.
Transcribe the sound clip, movie1.
Transcribe the sound clip, movie2.
Transcribe the sound clip, movie3.
What did you enjoy the most about this assignment?
What was the most challenging aspect of this assignment for you?
Check Version

For the check version, complete all of the tasks for the minus version, with these additions:

Update the implementation of ArrayStack and LinkedStack to include toString.
Additionally, answer the following questions in readme.txt:
Given that the initial size of the underlying array in ArrayStack is 10 elements, how many time would the array need to grow to accommodate a .dat file with one million lines? one billion? one trillion? Explain your answer.
Generally, all the methods of an interface must be overridden in a class that implements that interface. Explain why the toString method could be completely ignored in the minus version implementations of NumberStack.
Assume that you also implement the NumberQueue ADT. Can you implement this ADT using both the partially-filled array and linked list data structures? Give pseudo-code for the implementation of the four core methods. Omit toString.
Make sure you update the answer to question 1 to include toString in your report about testing.
Plus Version

For the plus version, complete all of the tasks for the check version, with these additions:

Additionally answer the following questions in readme.txt:
How could the NumberQueue ADT change the implementation of ReverseDat?
Compare your implementations of NumberStack and NumberQueue in regard to efficiency? Which are more effecient? Which are less? Explain your answer.
How would you redesign this homework assignment, if you had the chance?
Submission

Submit the following files:

ArrayStack.java
LinkedStack.java
readme.txt
Background Information

In this assignment, you will work with backmasking of short audio clips. To manipulate the sound clips, they will be converted to DAT (digital audio tape) format. DAT is a textual format, which simplifies the manipulation.

DAT Format

DAT format was developed by Sony for a recording format that they developed in the 80s. As the name implies, the data is stored in digital format, rather than analog.

A monaural sound track is represented as a single sound wave, a continuous differentiable function in time. Analog-to-digital conversion (ADC) is the process of taking that continuous input, recording values at discrete intervals of time (the sampling rate), and representing those values as digital levels of displacement from zero.



Here are some examples of data taken from a DAT file: Here is the beginning of the file:

; Sample Rate 44100
; Channels 1
               0                0 
   2.2675737e-05                0 
   4.5351474e-05                0 
   6.8027211e-05                0 
   9.0702948e-05                0 
   0.00011337868                0 
   0.00013605442                0 
And here is some data from later in the same file:

      0.59077098     0.0010375977 
      0.59079365     0.0024108887 
      0.59081633     0.0026855469 
        0.590839   -9.1552734e-05 
      0.59086168    -0.0025634766 
      0.59088435    -0.0038452148 
      0.59090703    -0.0037536621 
The file starts out with some header information, indicated by an initial semicolon. The sampling rate of 44.1 kHz is the typical sampling rate for CDs, since it will capture the top end of human hearing, 22.05 kHz. This recording contains a single audio channel, that is, it's monaural.

Following the header lines comes the data. Each data entry is composed of two numbers: a time offset and a "displacement" value.

To create a DAT version of a sound clip, you can use sox (SOund eXchange) or some equivalent utility. Download version 14.4.1 of sox:

sox-14.4.1a-win32.exe (for Windows)
sox-14.4.1-macosx.zip (for OS-X)
Go to http://sourceforge.net/projects/sox/ to access other versions and formats of this utility. However, the current version, 14.4.2, displayed a problem with the conversion back into the wav format. This is why we're using version 14.4.1 for this assignment.

The sox utility is a command-line application with a number of options and capabilities. We will use only the simplest ones to change format. The command is as follows, where the formats are indicated by the file extension.

sox current-format desired-format

Let's change bot.wav into DAT format.

In Windows, you can use:

sox bot.wav bot.dat

In Unix-like systems, such as OS-X, you can use:

./sox bot.wav bot.dat

This assumes that the sox executable file and bot.wav are in the current working directory.
