# The evil Programming Language Specification

Version 0.2. Includes the basic language but not the standard libraries.

## Background

evil is a minimalistic, but vaguly useful programming language with a simple programming model and trivial syntax.

The language was invented while I was a graduate student at the University of Colorado, probably sometime in the year 1999. I cannot, in all fairness, take complete blame...err..credit for evil. Considerable support was provided by the other members of the "gang of four": Glenn Blauvelt, Dave Mankin, and Eric Scharf. I am particularly indebted to Dave Mankin for producing the wonderful logo for the language, which so inspired me throughout those final few semesters as a graduate student. Finally, I must thank Juanita's Mexican Restuarnt for the Margaritas which had a major part in the invention of this programming language.

This is the second major revision of the language. The first version used the non-alphanumeric characters as language primitives. This, the second revision, uses lowercase characters as the basic evil language while uppercase letters are reserved for the standard library.

While evil is in some ways similar to the language Brainf*ck and its isomorph Ook, these languages had no part in its invention, as I had not heard of either when I came up with the idea. I tip my hat to the inventors of these and similar languages. While I may not have stood on their shoulders, I am comforted in knowing that I follow in the footsteps of such giants.

Note that the name "evil" in all lowercase is the proper name for the basic language without the standard library. When combined with the standard library the proper name is "Evil" starting with an uppercase letter. Alterative library sets should start with an uppercase letter that identifies the library include "evil" after that. For example, the standard windowing library version of evil is named "Wevil" while the special database library version is called "Devil".

## The Virtual Machine Model

The virtual machine includes three pools of memory, a single register, and a few hidden state variables that indicate special processing modes. Each memory cell can, in this version, hold a single byte of memory. Sometimes this byte will be interpreted as an unsigned integer, and sometimes as a character value (assumes the 8 bit Unicode encoding system).

The first pool of memory is the source code. This is typically loaded from a file at runtime, but might in some cases be stored in some other fashion. (For example, in ROM for embedded applications). This piece of memory can be any size and can vary in size during the execution of the program (how this can happen is described later). There is always a current position pointer that keeps track of the position in this pool.

The second pool of memory is the wheel. This is a circular queue of bytes/characters. At program initialization it contains a single cell whose value is zero, and program commands can add and subtract track of the position of the wheel. Since the wheel is circular, this pointer wraps around as necessary.

The third pool is the pental. This is simliar to the wheel, but has a fixed size of five memory cells. Like the wheel there is a current position pointer that wraps as necessary. At program start all five elements of the pental contain a zero value.

Finally there is a single register. At program startup this register contains a zero value.

To aid in the writing of complex programs there is a command in evil that swaps the roles of the source code and wheel pools. While this can be used to write self-modifying code, it is more commonly used to step outside the normal flow-of-control commands, which can be rather restrictive.

The evil system runs by examining the current cell in the source code (viewed as a character) executing that code if it is valid, ignoring it if it is not valid, then incrementing the source pointer. When the source pool pointer is past the end of the source code, the program ends.

## evil Command Reference

In these command definitions, 'A' refers to the register. 'P' refers to the current pental cell. 'W' refers to the current wheel cell. 'S' refers to the current source code cell. Pp, Wp, and Sp refer to the current pental, wheel, and source pointers respectively.

Command|Description
-------|-----------
a|    A=A+1
b|    Scans backward to the first valid marker character. Sets Sp to the position of that marker character.
c|    Insert a new wheel cell. Move the current cell to just after the new cell. Change Wp to point to the new cell.
d|    Delete the cell pointed to by Wp from the wheel.
e|    A=weave(A). The weave function is described below.
f|    Scans forward to the first valid marker character. Sets sp to the position of that marker character.
g|    A = P
h|    Pp=Pp+1
i|    Wp=Wp+1
j|    This is the alternate mark character, used as a target by b and f instructions when the mark state is "alternate".
k|    P = A
l|    temp=A; A=W; W=temp; (Swap A and W)
m|    This is the standard mark character, used as a target by b and f instructions when teh mark state is "standard".
n|    Pp=Pp-1
o|    Wp=Wp-1
p|    A = W
q|    Swap the wheel and source data structures including the Wp and Sp values.
r|    Read a character from standard input and put it into A (A = read(stdin)).
s|    Skip next character if A is zero (IF A==0 THEN Sp=Sp+1).
t|    Skip next character if A is not zero (IF A!=0 THEN Sp=Sp+1).
u|    A=A-1
v|    temp=A; A=P; P=temp; (Swap A and P)
w|    Write the current value of A (as a character) to standard out. (write((char)A)).
x|    Swap the mark state. If it is "standard" make it "alternate", if it is "alternate" make it "standard".
y|    W=A
z|    A=0

The weave operation is critically important to reducing the amount of code necessary to construct constant values (This is the biggest drawback of languages like Brainf*ck and Ook). The weave operation shifts the bits around in the following pattern (bit zero is the least significant bit, bit 7 the most significant).

```Text
Bit 0 is moved to bit 2
Bit 1 is moved to bit 0
Bit 2 is moved to bit 4
Bit 3 is moved to bit 1
Bit 4 is moved to bit 6
Bit 5 is moved to bit 3
Bit 6 is moved to bit 7
Bit 7 is moved to bit 5
```

So, for example, the code fragment zaee which puts the value weave(weave(1))=64 into A. Note that applying weave eight times in a row (eeeeeeee) leaves A unchanged.

## Some sample code fragments

The program raw reads in a single character from standard input, increments that character to the next character, and writes it to standard output.

The fragment **cygmtfulalbmpd** will add the values in A and P (the current pental value) and put the result in A (in other words A=A+P). The code cleans up after itself so there are no side effects at all. By changing a single command this can be turned into A=A-P: **cygmtfululbmpd**. Note that you can dress up these sequences by adding spaces and punctuation: **cygm t-ful alb mpd**. This makes them seem almost like they should make sense.
