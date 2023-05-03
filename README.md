Download Link: https://assignmentchef.com/product/solved-cs2211a-lab-no-6-introduction-to-c
<br>
The objective of this lab is:

o to practice the <em>xxgdb</em> debugging tool o to practice the use of loop statements, as well as calling some C standard functions

If you would like to leave, and at least 30 minutes have passed, raise your hand and wait for the TA.

Show the TA what you did. If, and only if, you did a reasonable effort during the lab, he/she will give you the lab mark.

<strong>==================================================================================== </strong>

<h1>Debugging C Programs</h1>

When you develop a C program, you need to compile it and make it syntax error-free before you can run it.  After doing so, you may get an unexpected output. You may also find that your program occasionally crashes. This is what we call runtime errors. Such errors are not always easy to locate. The process of identifying the runtime errors in your code and fixing them is called debugging your program.

<ul>

 <li>The first step in debugging your program is to attempt to reproduce the problem, .i.e., identifying the set of inputs that lead to the problem.</li>

 <li>After the bug is reproduced, the input of the program may need to be simplified to make it easier to debug. Such simplification can be made manually, using a divide-and-conquer approach, where you will try to remove some parts of original test case and check if the problem still exists.</li>

 <li>After the test case is sufficiently simplified, you can carefully examine program states (values of variables and the order of execution) and track down the origin of the problem(s).</li>

</ul>

The simplest way to do so is to insert some printf statements here and there. This is sometimes called <em>printf</em> debugging. While it is simple to do, it becomes a boring and confusing process when you have a complex bug.  Alternatively, there are software tools that allow you to inspect what the program is doing at a certain point <strong><em>during execution</em></strong>. These programs include, <em>gdb</em>, <em>dbx</em>, <em>xxgdb</em>. Errors like <em>segmentation faults</em> may be easier to find with the help of such tools.

<em>gdb</em> and <em>dbx</em> debuggers allow you to see what is going on <em>inside</em> another program while it executes — or what another program was doing at the moment it crashed.

They can do four main things (plus other things in support of these) in order to help you catch bugs in the act:

<ul>

 <li><strong><em>Start</em></strong> your program.</li>

 <li><strong><em>Stop</em></strong> your program on specified conditions.</li>

 <li><strong><em>Examine</em></strong> what has happened, when your program has stopped.</li>

 <li><strong><em>Change</em></strong> things in your program, so you can experiment the effects of one bug and go on to learn about another.</li>

</ul>

<em>xxgdb</em> is a source code debugging system. It is a graphical user interface to the <em>gdb</em> debugger under the X Window System. It provides visual feedback and mouse input for the user to control program execution through breakpoints, to <strong><em>examine</em></strong> and <strong><em>traverse</em></strong> the function call stack, to <strong><em>display</em></strong> values of variables as well as data structures, and to <strong><em>browse</em></strong> source files as well as functions.




To use such<em> debuggers,</em> the program must be compiled using the -g compiler flag set. For example, the command:   gcc -g -o prog prog.c

compiles the file prog.c. The -g flag causes the compiler to <em>insert</em> <em>information</em> into the executable file (named prog) that <em>gdb</em> and <em>xxgdb</em> require in order to work.



















To invoke <em>xxgdb</em> in the background, execute xxgdb&amp; in the command prompt which will open the following screen:










The main <em>xxgdb</em> window can be thought of as three subdivided windows:

<ul>

 <li>The first part is called the <em>source window</em> because the source file is displayed in this part.</li>

 <li>The second part is called the <em>command window</em> where essentially all the <em>xxgdb</em> commands are present. To invoke any of them, simply click on the appropriate button.</li>

 <li>The third part is the <em>dialog window</em> which provides a typing interface to the <em>xxgdb</em>.</li>

</ul>




<strong>It             is             worth    mentioning         that        once       you         click       on           a              button  in            the command            window,               the         equivalent          <em>gdb</em>         command            is             generated           and executed              in            the         dialog    window.               </strong>




To load a file to the debugger, click the <em>file</em> command button in the <em>Command Window</em> and select the <em>executable</em> file prog. The source code of prog.c appears on the window. You can also invoke <em>xxgdb</em> followed by the name of the executable file as an argument to the command.




To know how to use the various <em>xxgdb</em> commands, key in <em>help &lt;command name&gt;.</em> For example, if you key in help run in the <em>Dialog Window</em>, you will get the description of the <em>run</em> command.

<h1>Practicing <em>xxgdb</em></h1>

To learn how to debug a C program, let us create the following C program that calculates and prints the factorial of a number. This C program contains some errors for our debugging purpose.




#include &lt;stdio.h&gt;




int main()

{

int i, num, j;




printf (“Enter the number: “);  scanf (“%d”, &amp;num );




for (i=1; i&lt;num; i++)

j=j*i;




printf(“The factorial of %d is %d
”,num,j);




return 0;

}




Below is what you will get if you attempt to execute this program:




$ ./a.out

Enter the number: 3

The factorial of 3 is -8392248




In order to debug this program, you should complete the following steps:

<ol>

 <li>Compile your C program with -g This allows the compiler to collect the debugging information.</li>

</ol>

$ gcc -g factorial.c

Note: The above command creates an a.out file which will be used during the debugging process, as shown below.

<ol start="2">

 <li>Launch the C debugger (<em>xxgdb</em>) as shown below.</li>

</ol>

$ xxgdb a.out &amp;

<ol start="3">

 <li>Place break points in the C program where you suspect errors. While executing the program, the debugger will stop at the break points, and give you the prompt to debug.</li>

</ol>

So before starting up the program, let us place a break point in our program by clicking on the <em>main</em> function and then clicking on the <em>break</em> button. You can also set break points in your program by clicking at the beginning of a line you wish to break at and then clicking on the <em>break</em> button.

You can show the current break points by clicking on <em>show brkpts</em> button. Let us put another breakpoint <em>at</em> j=j*i; line.

<ol start="4">

 <li>Run the program by clicking on the <em>run</em> button, or type <em>run</em> in the dialog window. You can also give the command line arguments to the program via <em>run args</em>. <em>B: the example program we used here does not require any command line arguments.</em></li>

</ol>

Once you have executed the C program, it will execute until the first break point, and then give you the prompt for debugging. You can use various <em>xxgdb</em> commands to debug the C program.

For the time being, as we are at the beginning of the program, we will proceed to the second break point by clicking on the <em>cont</em> button. Yes, it is the <em>cont</em> button not the <em>run</em> button, as <em>run</em> will restart the program from the beginning.  To enter the value to the scanf statement, you have to click on the dialog window and then enter the data.

<ol start="5">

 <li>Print the values of various variables that you want checked by highlighting the variable and then clicking on the <em>print</em> button, or just executing <em>print &lt;variable_name&gt;</em> in the dialog window, or simply <em>p &lt;variable_name&gt;</em>. In our case, print the values of i, j, and num.</li>

</ol>

As you see, in the program, we have not initialized the variable j. So, it gets a garbage value resulting in a big number as the factorial value.

Fix this issue by initializing variable j with 1, compile the C program and execute it again.

<ol start="6">

 <li>Keep looping in this cycle until having a program which is free from any semantic errors. This will eventually produce a program that gives the correct answer every time.</li>

</ol>

In our example, even after performing the fix above, there seems to be some problems in the program, as it still gives a wrong factorial value. So, you need to recompile it again with –g, run <em>xxgdb</em> again, put suitable <em>breakpoins</em> here and there, and start running the program again.

When you stop at a break point, you may choose to do one of the following actions to resume execution:

<ul>

 <li>Click on the<em> cont</em> button: debugger will continue executing until the next break point.</li>

 <li>Click on the<em> next</em> button: debugger will execute the next line as single instruction.</li>

 <li>Click on the<em> step</em> button: same as <em>next</em>, but does not treats a function as a single instruction, instead goes into the function and executes it line by line.</li>

</ul>

By <em>continuing</em> or <em>stepping through</em>, you would have found that the issue in the program is because we have not used the &lt;= in the for loop condition checking. So changing &lt; to &lt;= will solve the issue.

<strong>During  this        lab          you         should  get          familiar                with       <em>xxgdb</em>     so            that        you         can <em>fluently</em> use         it             from      now        on           whenever            developing          any         C              program              in the         future.                  </strong>

Below, you will find a summary of all <em>xxgdb</em> commands and a brief description for each one of them.

<h1>Command buttons</h1>

<strong><em>Execution Commands </em></strong>

<table width="673">

 <tbody>

  <tr>

   <td width="108"><strong>Run</strong></td>

   <td width="565">Begin program execution.</td>

  </tr>

  <tr>

   <td width="108"><strong>Cont</strong></td>

   <td width="565">Continue execution from where it stopped.</td>

  </tr>

  <tr>

   <td width="108"><strong>Next</strong></td>

   <td width="565">Execute one source line, without stepping into any function call.</td>

  </tr>

  <tr>

   <td width="108"><strong>Step</strong></td>

   <td width="565">Execute one source line, stepping into a function if the source line contains a function call.</td>

  </tr>

  <tr>

   <td width="108"><strong>Finish</strong></td>

   <td width="565">Continue execution until the selected procedure returns; the current procedure is used if none is selected.</td>

  </tr>

 </tbody>

</table>

<strong><em>Breakpoint Commands </em></strong>

<table width="723">

 <tbody>

  <tr>

   <td width="108"><strong>Break</strong></td>

   <td width="615">Stop program execution at the line or in the function selected. To set a breakpoint in the program, place the caret at the start of the source line or on the function name and click the <em>break</em> button</td>

  </tr>

  <tr>

   <td width="108"><strong>Tbreak</strong></td>

   <td width="615">Set a breakpoint enabled only for one stop. This is the same as the <em>break</em> button except the breakpoint is automatically disabled the first time it is hit.</td>

  </tr>

  <tr>

   <td width="108"><strong>Delete</strong></td>

   <td width="615">Remove the breakpoint on the source line selected or the breakpoint number selected.</td>

  </tr>

  <tr>

   <td width="108"><strong>Show brkpts</strong></td>

   <td width="615">Show the current breakpoints (both active and inactive).</td>

  </tr>

 </tbody>

</table>

<strong><em>Stack Commands </em></strong>

<table width="340">

 <tbody>

  <tr>

   <td width="108"><strong>Stack</strong></td>

   <td width="232">Show a stack trace of the functions called.</td>

  </tr>

  <tr>

   <td width="108"><strong>Up</strong></td>

   <td width="232">Move up one level on the call stack.</td>

  </tr>

  <tr>

   <td width="108"><strong>Down</strong></td>

   <td width="232">Move down one level on the call stack.</td>

  </tr>

 </tbody>

</table>




<strong><em>Data Display Commands </em></strong>

<table width="723">

 <tbody>

  <tr>

   <td width="108"><strong>Print</strong></td>

   <td width="615">Print the value of a selected expression.</td>

  </tr>

  <tr>

   <td width="108"><strong>Print *</strong></td>

   <td width="615">Print the value of the object the selected expression is pointing to.</td>

  </tr>

  <tr>

   <td width="108"><strong>Display</strong></td>

   <td width="615">Display the value of a selected expression in the display window, updating its value every time the execution stops.</td>

  </tr>

  <tr>

   <td width="108"><strong>Undisplay</strong></td>

   <td width="615">Stop displaying the value of the selected expression in the display window. If the selected expression is a constant, it refers to the display number associated with an expression in the display window.</td>

  </tr>

  <tr>

   <td width="108"><strong>Args</strong></td>

   <td width="615">Print the arguments of the selected frame.</td>

  </tr>

  <tr>

   <td width="108"><strong>Show display</strong></td>

   <td width="615">Show the names of currently displayed expressions</td>

  </tr>

  <tr>

   <td width="108"><strong>Locals</strong></td>

   <td width="615">Print the local variables of the selected frame.</td>

  </tr>

  <tr>

   <td width="108"><strong>Stack</strong></td>

   <td width="615">Print a backtrace of the entire stack.</td>

  </tr>

 </tbody>

</table>

<strong><em>Miscellaneous Commands </em></strong>

<table width="723">

 <tbody>

  <tr>

   <td width="108"><strong>Search</strong></td>

   <td width="615">Pop up a search panel which allows both forward (&gt;&gt;) and reverse (&lt;&lt;) searches of text strings in the source file. Hitting carriage return after entering the search string will begin a forward search and pop down the search panel.</td>

  </tr>

  <tr>

   <td width="108"><strong>File</strong></td>

   <td width="615">Pop up a directory browser that allows the user to move up and down in the directory tree, to select a text file to be displayed, to select an executable file to debug, or to select a core file to debug. Directory entries are marked with a trailing slash (‘/’) and executables with a trailing asterisk (‘*’). Filenames beginning with a dot (‘.’) or ending with a tilde (‘~’) are not listed in the menu.</td>

  </tr>

  <tr>

   <td width="108"><strong>Yes</strong></td>

   <td width="615">Send ‘y’ (yes) to <em>gdb</em> (to be used when <em>gdb</em> requires a yes/no response).</td>

  </tr>

  <tr>

   <td width="108"><strong>No</strong></td>

   <td width="615">Send ‘n’ (no) to <em>gdb</em> (to be used when <em>gdb</em> requires a yes/no response).</td>

  </tr>

  <tr>

   <td width="108"><strong>Quit</strong></td>

   <td width="615">Exit <em>xxgdb</em>.</td>

  </tr>

 </tbody>

</table>




<h1>Practicing loops and calling some standard functions</h1>

<ol>

 <li>There are 9,870 people in a town whose population increases by 10 percent each year. Write a loop that displays the annual population and determines how many years it will take for the population to surpass 30,000. Your program should accept the current number of people as an input.</li>

 <li>The following program uses the sqrt function from the math library; hence, h must be included at the beginning of the program (Read man 3 sqrt). To compile such program, you have to inform the compiler to use the math library during the linking step. To do so, you should use “<strong>gcc prog.c –lm</strong>” Unfortunately, there are some errors in this code. Type the program, compile it, fix its errors, and run it correctly.</li>

</ol>

#include &lt;stdio.h&gt;

#include &lt;math.h&gt;




int main()

{   int i;

printf(“Number t Square Root

”);




for (i=0, i&lt;=30, ++i);

printf(“%d tt %d 
”,i, sqrt(1.0 * i));




return 0;

}

<ol start="3">

 <li>Write a program to read a positive integer value, and compute the following sequence:        If the number is even, halve it;</li>

</ol>

    if it is odd, multiply by 3 and add 1.

<strong><u>Repeat</u></strong> this process until the value becomes 1. Print out each intermediate value. Finally print out how many of these operations you have performed. If the input value is less than 1, print an error message and perform an exit(EXIT_FAILURE); Note that, the function exit() is defined in stdlib.h. Hence, stdlib.h must be included at the beginning of the program.