Download Link: https://assignmentchef.com/product/solved-cop3502-assignment-5-sneakyrooks
<br>
This is a wrap-up assignment designed to reinforce the kinds of algorithmic and clever thinking we’ve been building up together over the course of the semester. In particular, this will serve as an additional exercise in coming up with efficient solutions to problems, since your solution for this assignment needs to have a worst-case runtime that does not exceed O(<em>m</em> + <em>n</em>) (linear runtime). The assignment also involves a direct application of the base conversion material we covered recently (albeit with a minor twist).

You might find this problem a bit tricky at first. It’s important to struggle with it. Don’t be discouraged if you don’t solve it right away. Maybe walk away, take a break, and come back to it later (perhaps even the following day). You might be amazed by what your brain can do if you let it work on a problem in the background and/or if you come back to a problem well-rested, with a fresh perspective.

Please feel free to seek out help in office hours if you’re lost, and remember that it’s okay to have conceptual discussions with other students about this problem, as long as you’re not sharing code (or pseudocode, which is practically the same thing). Just keep in mind that you’ll benefit more from this problem if you struggle with it a bit before discussing it with anyone else.

<strong>Deliverables</strong>

SneakyRooks.c

<strong><em>Note!</em></strong> The capitalization and spelling of your filename matter!

<strong><em>Note!</em></strong> Code must be tested on Eustis, but submitted via Webcourses.

<h1>1. Problem Statement</h1>

You will be given a list of coordinate strings for rooks on an arbitrarily large square chess board, and you need to determine whether any of the rooks can attack one another in the given configuration.

In the game of chess, rooks can move any number of spaces horizontally or vertically (up, down, left, or right). For example, the rook on the following board (denoted with a letter ‘R’) can move to any position marked with an asterisk (‘*’), and no other positions:

<strong><em>Figure 1:</em></strong><em> The rook at position d3 can move to any square marked with an asterisk.</em>

Thus, on the following board, none of the rooks (denoted with the letter ‘R’) can attack one another:

<strong><em>Figure 2:</em></strong><em> A 4×4 board in which none of the rooks can attack one another.</em>

In contrast, on the following board, the rooks at <em>c6</em> and <em>h6</em> can attack one another:

<strong><em>Figure 3:</em></strong><em> An 8×8 board in which two of the rooks can attack one another.</em>

<h1>2. Chess Board Coordinates</h1>

<strong>2.1.     Coordinate System</strong>

One standard notation for the location of a chess piece on an 8×8 board is to give its column, followed by its row, as a single string with no spaces. In this coordinate system, columns are labeled <em>a</em> through <em>h</em> (from left to right), and rows to be numbered 1 through 8 (from bottom to top).

So, for example, the board in Figure 2 (above, on pg. 2) has rooks at positions <em>a3</em>, <em>b1</em>, <em>c4</em>, and <em>d2</em>.

Because you’re going to be dealing with much larger chess boards in this program, you’ll need some sort of notation that allows you to deal with boards that have more than the 26 columns we can denote with the letters <em>a</em> through <em>z</em>. Here’s how that will work:

Columns will be labeled <em>a</em> through<em> z</em> (from left to right). After column <em>z</em>, the next 26 columns will be labeled <em>aa </em>through <em>az</em>. After column <em>az</em>, the next 26 columns will be labeled <em>ba</em> through <em>bz</em>, and so on. After column <em>zz</em>, the next 26 columns will be labeled <em>aaa</em> through <em>aaz</em>.

Essentially, the columns are given in a base 26 numbering scheme, where digits 1 through 26 are represented using <em>a</em> through <em>z</em>. However, this counting system is a bit jacked up since there’s no character to represent the value zero. (That’s part of the fun.)

All the letters in these strings will be lowercase, and all the strings are guaranteed to be valid representations of board positions. They will not contain spaces or any other unexpected characters.

<em>For example:</em>

<ol>

 <li>In the coordinate string <em>a1</em>, the <em>a</em> tells us the piece is in the first column (from the left), and the 1 tells us the piece is in the first row (from the bottom).</li>

 <li>Similarly, the string <em>z32</em> denotes a piece in the 26<sup>th</sup> column (from the left) and 32<sup>nd</sup> row (from the bottom).</li>

 <li>The string <em>aa19</em> represents a piece in the 27<sup>th</sup> column (from the left) and 19<sup>th</sup> row (from the bottom).</li>

 <li>The string <em>fancy58339</em> would represent a piece in the 2,768,999<sup>th</sup> column (from the left) and the 58,339<sup>th</sup> row (from the bottom).</li>

</ol>

Converting these strings to their corresponding numeric coordinates is one of a few key algorithmic / mathemagical challenges you face in this assignment. You will have to write a function that does that for you.

<strong>2.2.      Coordinate Struct (SneakyRooks.h)</strong>

To store rook coordinates, you must use the struct definition we have specified in SneakyRooks.h without any modifications. You must #include that header file from SneakyRooks.c like so:

#include “SneakyRooks.h”

The struct you will use to hold rook coordinates is defined in SneakyRooks.h as follows:

<strong>    typedef struct</strong> Coordinate     { <strong>       int</strong> col;  // The column where this rook is located (1 through board width).        <strong>int</strong> row;  // The row where this rook is located (1 through board height).     } Coordinate;

<h1>3. Runtime Requirements</h1>

In order to pass all test cases, the worst-case runtime of your solution cannot exceed O(<em>m</em> + <em>n</em>), where <em>m</em> is both the length and width of the square chess board, and <em>n</em> is the number of coordinate strings to be processed. This figure assumes that the length of each coordinate string is bounded by some constant, which means you needn’t account for that length in your runtime analysis, provided that each string is processed or examined only some small, constant number of times (e.g., once or twice).

Equivalently, you may conceive of all the string lengths as being less than or equal to <em>k</em>, in which case the worst-case runtime that your solution cannot exceed would be expressed as O(<em>m</em> + <em>nk</em>).

<strong><em>Note!</em></strong> O(<em>m</em> + <em>n</em>) is just another way of writing O(<sub>MAX</sub>{<em>m</em>, <em>n</em>}), meaning that your runtime can be linear with respect to <em>m</em> or <em>n</em> – whichever one happens to be the dominant term for any individual test case.

<h1>4. Function Requirements</h1>

In the source file you submit, SneakyRooks.c, you must implement the following functions. You may implement any auxiliary functions you need to make these work, as well. Please be sure the spelling, capitalization, and return types of your functions match these prototypes exactly.

<strong>Note:</strong> Your source file for this assignment <strong><u>must not</u></strong> contain a main() function.

int allTheRooksAreSafe(char **rookStrings, int numRooks, int boardSize);

<strong>Description:</strong> Given an array of strings, each of which represents the location of a rook on a boardSize × boardSize chess board, return 1 if none of the rooks can attack one another. Otherwise, return 0. You must do this in O(numRooks + boardSize) time.

<strong>Parameter Restrictions:</strong> boardSize will be a positive integer describing both the length and width of the square board. (So, if boardSize = 8, then we have an 8 × 8 board.) rookStrings will be a non-NULL (but possibly empty) array of strings, and any strings within that array will be unique (there will be no repeats), and all of those strings will follow the format described above for valid coordinates on a boardSize × boardSize board. numRooks will be a nonnegative integer indicating the number of strings in the rookStrings array.

<strong>Output:</strong> This function should <strong><u>not</u></strong> print anything to the screen.

<strong>Runtime Requirement:</strong> The runtime for this function must be no worse than

O(numRooks + boardSize). For details, see Section 3, “Runtime Requirements” (above).

<strong>Returns:</strong> 1 if all the rooks are safe. Otherwise, return 0.

void parseCoordinateString(char *rookString, Coordinate *rookCoordinate);

<strong>Description:</strong> Parse through rookString to determine the numeric row and column where the given rook resides on the chess board, and populate rookCoordinate with that information. You may assume that rookString is non-NULL, and that it contains a valid coordinate string using the format described above in Section 2.1, “Coordinate System.” You may assume that rookCoordinate is non-NULL and is a pointer to an existing Coordinate struct.

<strong>Returns:</strong> Nothing. This is a void function.

double difficultyRating(void);

<strong>Returns:</strong> A double indicating how difficult you found this assignment on a scale of 1.0 (ridiculously easy) through 5.0 (insanely difficult).

double hoursSpent(void);

<strong>Returns:</strong> An estimate (greater than zero) of the number of hours you spent on this assignment.

<h1>5. Special Requirement: Memory Leaks and Valgrind</h1>

Part of the credit for this assignment may be awarded based on your ability to implement the program without any memory leaks. To test for memory leaks, you can use a program called valgrind, which is installed on Eustis.

To run your program through valgrind at the command line, compile your code with the -g flag, and then run valgrind, like so:

gcc SneakyRooks.c testcase01.c -g valgrind –leak-check=yes ./a.out

For help deciphering the output of valgrind, see: <a href="http://valgrind.org/docs/manual/quick-start.html">http://valgrind.org/docs/manual/quick-start.html</a>

In the output of valgrind, the magic phrase you’re looking for to indicate that you have no memory leaks is:

All heap blocks were freed – no leaks are possible

<h1>6. Test Cases and the test-all.sh Script</h1>

We’ve included a few test cases with this assignment to show some ways in which we might test your code and to shed light on the expected functionality of your code. We’ve also included a script, testall.sh, that will compile and run all test cases for you.

<table width="477">

 <tbody>

  <tr>

   <td width="29">The</td>

   <td width="88">test-all.sh</td>

   <td width="360"> script is the safest, most sure-fire way to test your code.</td>

  </tr>

 </tbody>

</table>

You can run the script on Eustis by placing it in a directory with SneakyRooks.c, SneakyRooks.h, the sample_output directory, and all the test case files, and typing:

bash test-all.sh

Please note that we have only included a very small number of test cases this time around because we want to encourage you to create your own test cases and to think about how to test your code thoroughly. In creating your own test cases, you should always ask yourself, “How could these functions be called in ways that don’t violate the function descriptions, but which haven’t already been covered in the test cases included with the assignment?”

<em>The fun continues on the following page!</em>




<h1>Compilation and Testing (Linux/Mac Command Line)</h1>

To compile multiple source files (.c files) at the command line:

gcc SneakyRooks.c testcase01.c

By default, this will produce an executable file called a.out, which you can run by typing:

./a.out

If you want to name the executable file something else, use:

gcc SneakyRooks.c testcase01.c -o SneakyRooks.exe

…and then run the program using:

./SneakyRooks.exe

Running the program could potentially dump a lot of output to the screen. If you want to redirect your output to a text file in Linux, it’s easy. Just run the program using the following command, which will create a file called whatever.txt that contains the output from your program:

./SneakyRooks.exe &gt; whatever.txt

Linux has a helpful command called diff for comparing the contents of two files, which is really helpful here since we’ve provided several sample output files. You can see whether your output matches ours exactly by typing, e.g.:

diff whatever.txt sample_output/output01.txt

If the contents of whatever.txt and output01.txt are exactly the same, diff won’t have any output:

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="e39086828d9099a3869690978a90">[email protected]</a>:~$ diff whatever.txt sample_output/output01.txt <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="e09385818e939aa0859593948993">[email protected]</a>:~$ _

If the files differ, it will spit out some information about the lines that aren’t the same. For example:

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="ed9e888c839e97ad88989e99849e">[email protected]</a>:~$ diff whatever.txt sample_output/output01.txt

1c1

&lt; fail whale &#x1f641;

—

&gt; Hooray!

<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="522137333c212812372721263b21">[email protected]</a>:~$ _

<h1>Style Restrictions (<em>Super Important!</em>)</h1>

Please conform as closely as possible to the style I use while coding in class. To encourage everyone to develop a commitment to writing consistent and readable code, the following restrictions will be strictly enforced:

 Any time you open a curly brace, that curly brace should start on a new line.

 Any time you open a new code block, indent all the code within that code block one level deeper than you were already indenting.

 Be consistent with the amount of indentation you’re using, and be consistent in using either spaces or tabs for indentation throughout your source file. If you’re using spaces for indentation, please use at least two spaces for each new level of indentation, because trying to read code that uses just a single space for each level of indentation is downright painful.

 Please avoid block-style comments: /*<em> comment </em>*/

 Instead, please use inline-style comments: //<em> comment</em>

 Always include a space after the “//” in your comments: “// <em>comment</em>” instead of “//<em>comment</em>”

 The header comments introducing your source file should always be placed above your #include statements.

 Comments longer than three words should always be placed <em><u>above</u></em> the lines of code to which they refer. Furthermore, such comments should be indented to properly align with the code to which they refer. For example, if line 16 of your code is indented with two tabs, and line 15 contains a comment referring to line 16, then line 15 should also be intended with two tabs.

 Any libraries you <em>#include</em> should be listed <em>after</em> the header comment at the top of your file that includes your name, course number, semester, NID, and so on.

 Please do not write excessively long lines of code. Lines must be no longer than 100 characters wide.

 Avoid excessive consecutive blank lines. In general, you should never have more than one or two consecutive blank lines.

 When defining a function that doesn’t take any arguments, always put <em>void</em> in its parentheses. For example, define a function using <em>int do_something(void)</em> instead of <em>int do_something()</em>.

 Please leave a space on both sides of any binary operators you use in your code (i.e., operators that take two operands). For example, use <em>(a + b) – c</em> instead of <em>(a+b)-c</em>.

 When defining or calling a function, do not leave a space before its opening parenthesis. For example: use <em>int main(void)</em> instead of <em>int main (void)</em>. Similarly, use <em>printf(“…”)</em> instead of <em>printf (“…”)</em>.

 Do leave a space before the opening parenthesis in an <em>if</em> statement or a loop. For example, use use <em>for (i = 0; i &lt; n; i++)</em> instead of <em>for(i = 0; i &lt; n; i++)</em>, and use <em>if (condition)</em> instead of <em>if(condition)</em> or <em>if( condition )</em>.

 Use meaningful variable names.