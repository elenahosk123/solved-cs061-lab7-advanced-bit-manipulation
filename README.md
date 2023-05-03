Download Link: https://assignmentchef.com/product/solved-cs061-lab7-advanced-bit-manipulation
<br>
The purpose of this lab is to give you some experience in doing some advanced bit manipulation techniques, making use of both left- and right-shifting.

<ul>

 <li><strong>Our Objectives for This Week </strong></li>

</ul>

<ol>

 <li>Exercises 01 – Review &amp; extend assignment 4</li>

 <li>Exercise 02 – Counting bits</li>

 <li>Exercise 03 – Right Shift<strong>        </strong></li>

</ol>

<strong>REMEMBER:   ALL your programs must now be written as subroutines!! </strong>

Call your subroutines with the JSRR instruction <em>(</em>​ <em>it works with subroutines located anywhere in memory) </em>

And remember to include all four steps of subroutine construction, being <em>especially</em>​    ​ careful <u>to back​       </u> <u>up &amp; restore R7</u> <u>​ </u><em>(</em>​ <em>or your program won’t work and you won’t be able to figure out why!) </em>

<h1>Exercise 01</h1>

Hey, remember that Programming Assignment (assn 4) you are working on? Sweet, huh? Let’s reverse it:

<strong>Specs: </strong>

<ol>

 <li>The main code block (which is basically a test harness) should just invoke subroutine 1, and then subroutine 2, using the register value created by sub 1 to set up input for sub 2.</li>

 <li>Subroutine 1: This subroutine will just take a hard-coded (.FILL) value, and load it into a register of your choice.</li>

 <li>(In the test harness) add 1 to the number and invoke subroutine 2:</li>

 <li>Subroutine 2: Using your chosen output register from sub 1 as an input register for sub 2, print the new value out to the console as a decimal number <em>(</em>​ <em>e. the inverse of Programming Assignment 04)</em>​.</li>

</ol>

Work out the algorithm for yourself by studying the algorithm we give you for assn 4, and then working “backwards” from that.

ALWAYS, ALWAYS, WRITE OUT YOUR ALGORITHM – express it in bullet points, in pseudo-code, in C++, however you like – but DO IT!

<ol start="5">

 <li>Just for fun, try entering the number #32767 into this program; what do you get?</li>

</ol>

<h1>Exercise 02</h1>

Write a subroutine that counts the number of binary 1’s in the value stored in a given register <em>(</em>​ <em>this is part of a technique known as a “parity check” – go look it up!) </em>

<strong>Specs: </strong>

<ol>

 <li>The main code block (test harness) should ask the user to input a single character at the keyboard.</li>

 <li>The input should be “passed” as a parameter to the subroutine (i.e. the input character is copied to a register that is available to the subroutine).</li>

 <li>The subroutine should “return” the number of binary 1’s in the input character in another register (i.e. it counts the number of 1’s in the original character, and stores that value in a “return” register).</li>

 <li>The main code block should then print the result in a reasonably intelligent format: Example: The ASCII code for a semi-colon (‘;’) is x3B == b0000 0000 0011 1011 which contains five binary 1’s, so your program will output:</li>

</ol>

The number of 1’s in ‘;’ is: 5

Hint: We will test this exercise only with asciii characters – i.e. the maximum possible number of 1’s will be 8, i.e. your output will always be a single digit numeric character.

<h1>Exercise 03</h1>

<em> </em>​<strong><em>You have to read &amp; understand this exercise, but you don’t need to code it – you just need to show your TA the algorithm you would use</em></strong>​<em> (use the outline below)</em>​<strong><em>. </em></strong>

Ok, here we go. Are you feeling advanced? You ​<em>look </em>​advanced. You’re awesome! You can totally do this! Ready? Ok!

Build a subroutine that takes, as a parameter, the value of a register and ​<strong>right-shifts</strong>​ it by one bit, losing the trailing bit, and filling in the empty leading bit with 0:

<strong>Example: </strong>

(R1) ← xABCD     ; (b1010 1011 1100 1101)

[call the right-shift subroutine]

[now (R1) == x55E6 == b​<strong>0</strong>​101 0101 1110 0110]

Note how we shifted-in a 0 when we did the right-shift, and “lost” the 1 in the lsb?

This is called a <u>​<em>logical</em></u><u>​</u><em> right shift</em>​; there are two other variations, the arithmetic right-shift (which maintains the sign bit rather than always shifting-in a 0 to the msb); and a right-rotate, which shifts in to the msb the bit shifted out of the lsb. For the moment, we will just deal with the logical right-shift.

<strong>Discussion: </strong>

Alright, let’s think about this thing. When we ​<strong>left-shift</strong>​, we are doubling the number (aka: multiplying it by two – aka: adding it to itself – aka: ADD R1, R1, R1), right? So if left-shift is multiplication, then what might ​<strong>right-shift</strong>​ be?

Yep, you guessed it: Division. If you left-shift the number 2, you get 4. If you right-shift 4, you go back to having 2. So, division. Right. Got it.

“How in blazes are we suppose to right shift?!” the TA said rhetorically.

[Whacky Student]: If left-shifting is ADDing a number to itself, then right-shift must be subtracting it from itself, right?

[TA]: *blank stare*

[Less Whacky Student]: *whispers* “Dude, that would make it zero.”

[Whacky Student]: *facepalm*

Well, sadly, there is no super-simple way to perform a binary right-shift. Still, it’s not insanely difficult. Let’s think about it:

<ul>

 <li>Left-shifting is short and sweet: add the number to itself.</li>

 <li>Right-shifting is not quite as simple. There is no way to directly do it.</li>

 <li>Hmm… how else can we mess around with the bits? We can shove them left and shift-in a 0 every time to the lsb (that’s a logical left-shift)… but what if instead we ​<strong>rotated</strong>​ the bits (i.e. take the msb being shifted out, and shift it in as the new lsb)?<strong>      </strong></li>

</ul>

<strong>Hmmm: </strong>

<ul>

 <li>Given the 4-bit (unsigned) number xC == b1100 == #12 (UNsigned magnitude)</li>

 <li>[Rotate left, noting that msb is 1, which gets rotated in to the lsb]</li>

 <li>Now we have b1001 == #9</li>

 <li>[Rotate left, noting that msb is 1, which gets rotated in to the lsb]</li>

 <li>Now we have b0011 == #3</li>

 <li>[Rotate left, noting that msb is 0, which gets rotated in to the lsb]</li>

 <li>Now we have b0110 == #6 – note that msb is now 0</li>

</ul>

Ok, this is boring. Let’s stop.

Hey wait! Oh my gosh!

We have 12/2 == 6 now! How’d that happen?!?

[This is where you, the Less Whacky Student, fill in the blanks &#x263a;]

<em>Note: This only works for </em>​<strong><em>unsigned </em></strong>​<em>representation. How could it be made to work for two’s complement representation? </em>


