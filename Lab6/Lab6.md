# EE160 Lab 6: If Statements and Separate Compilation 

(Repo of lab notes: <https://github.com/duck8880/EE160>)

(Lab assignment: <http://www-ee.eng.hawaii.edu/~tep/EE160/Labs/Lab6/lab6.html>)

  ​

## Notes

- Make sure your programs compile and eliminate all the warnings.. 

  Example:  

  ```c
  #include <stdio.h>
  float avg(int a, int b, int c);
  int main(){
      int a, b, c;
      float d;
      
      printf("Enter a b c: ");
      scanf("%d %d %d", &a, &b, &c);
      d = avg(a, b, c);  
      printf("Average: %f\n", %d);
  }
  float avg(int a, int b, int c){
      float d;
      d = (a + b + c) / 3;
      return d;
  }
  ```

- Use conditional compilation to debug
  
   ```c
   #define DEBUG
   ...
   int main(){
   #ifdef DEBUG
       printf("debug: %d\n", value);
   #endif
   }
   ```

- Separate compilation for multiple source files

   **func.c**: (function definitions)

   ```c
   int func1(int arg1, int arg2){
       ...
   }
   float func2(int arg1, int arg2){
       ...
   }
   ```

   **func.h**: (prototypes of the functions defined in **func.c**)

   ```c
   int func1(int arg1, int arg2);
   float func2(int arg1, int arg2);
   ```

   **driver.c**: (include the **func.h** and make function calls)

   ```c
   #include "func.h"
   int main(){
       int arg1, arg2, ret1;
       float arg3, arg3, ret2;
       ...
       ret1 = func1(arg1, arg2);
       ret2 = func2(arg3, arg4);
       ...
   }
   ```

   To compile: (write only the .c files in the command line)

   ```bash
   cc driver.c func.c
   ```

- **Write your algorithms as comments in your .c files.**

- Check your grades:

   `mygrades ee160s2`

- If you want to review the topics covered by the lecture so far, see the [summary](http://www-ee.eng.hawaii.edu/cgi-local/mklec.cgi?18+3+EE160/S18). 

  Ask me if you have any question about the midterm.

- Useful VI commands to copy, cut paste, etc.

    `v`: enter visual mode;    `h`, `j`, `k`, `l`: move cursor  
    `0`: to the beginning of a line;    `$`: to the end of a line  
    `c`: cut;    `y`: copy;    `p`: paste;    `cc` or `dd`: cut the current line;    `yy`: copy the current line  
    `u`: undo;    `Ctrl`+`r`: redo

  ​

## Programs

- Create a new directory called **Lab6** in your **EE160/Labs** directory. Work in this directory.

- (3 Points). Do **problem 4** in [section 2.9](http://www-ee.eng.hawaii.edu/~tep/EE160/Book/chap2/section2.1.9.html) of the text.   

  Write a program **numbers.c** that reads a set of integers until a zero is entered. Excluding zero, the program should print a **count** of and a **sum** of:

  1. positive numbers (e.g. 15, 2)
  2. negative numbers (e.g. -3, -8)
  3. even numbers (e.g. 2, -8)
  4. odd numbers (e.g. 15, -3)
  5. positive even numbers (e.g. 2)
  6. negative odd numbers (e.g. -3)
  7. all numbers

  Hint :

  - Implement this program incrementally; i.e. first build the loop and test for only one set of conditions (e.g. even and odd). Get that program to work, and then add features to it a little at a time, testing as you go along.
  - Use #ifdef DEBUG conditional compilation around your debug statements to turn on and off debugging. **Turn debugging off when you turn in your program.**

  Example input and output with debug information:

  ```bash
  15
  debug:15 is positive(count = 1, total = 15)
  debug:15 is odd(count = 1, total = 15)
  debug:Total(count = 1, total = 15)
  2
  debug:2 is positive(count = 2, total = 17)
  debug:2 is even(count = 1, total = 2)
  debug:2 is positive and even(count = 1, total = 2)
  debug:Total(count = 2, total = 17)
  -3
  debug:-3 is negative(count = 1, total = -3)
  debug:-3 is odd(count = 2, total = 12)
  debug:-3 is negative and odd(count = 1, total = -3)
  debug:Total(count = 3, total = 14)
  -8
  debug:-8 is negative(count = 2, total = -11)
  debug:-8 is even(count = 2, total = -6)
  debug:Total(count = 4, total = 6)
  0
  There were 2 positive numbers totaling 17
  There were 2 negative numbers totaling -11
  There were 2 even numbers totaling -6
  There were 2 odd numbers totaling 12
  There were 1 positive even numbers totaling 2
  There were 1 negative odd numbers totaling -3
  There were 4 total numbers totaling 6
  ```

- (2 Points). This is a variation of **problem 4** in [section 3.9](http://www-ee.eng.hawaii.edu/~tep/EE160/Book/chap3/section2.1.9.html) of the text. We will do this problem in two parts:

  1. In **maxmin.c**, write a function `float max(float n1, float n2);` that returns the greater of `n1` and `n2`. Write a function `float min(float n1, float n2);` that returns the lesser of `n1` and `n2`.  
  In **maxmin.h**, write the prototypes for these functions (and don't forget to include this header where needed). 

  2. In **driver1.c**, write a test driver, main() to test functions **max** and **min**. The driver should allow the user to test these functions by entering **one pair of float values** and verify the functions return the correct values each time. Use **EOF**(end-of-file) to end the test input.  

  Compile this program with the command:

  ```bash
  cc driver1.c maxmin.c
  ```

  Example input and output:
  ```bash
  Enter 2 numbers n1 n2: 10 20
  Max: 20.000000, Min: 10.000000
  Enter 2 numbers n1 n2: 30 40
  Max: 40.000000, Min: 30.000000
  Enter 2 numbers n1 n2:[Ctrl-D]
  ```

- (3 Points). Use the same **maxmin.c** file from above for this program. Write a new driver **main()** in the file **driver2.c** which reads numbers one at a time, and keeps track of the biggest and smallest number seen so far. Use your functions **max()** and **min()** to do the comparisons. Finally print the maximum and minimum of the bunch of numbers. Use **0** to end the test input.

  Example input and output with debug information:

  ```bash
  Enter numbers n:
  23.5
  debug: Max: 23.50, Min: 23.50
  16.1
  debug: Max: 23.50, Min: 16.10
  -35.2
  debug: Max: 23.50, Min: -35.20
  90
  debug: Max: 90.00, Min: -35.20
  -13.1
  debug: Max: 90.00, Min: -35.20
  0
  The maximum is 90.00 and minimum is -35.20

  ```

  Use **debug statements** (with conditional compilation) to show that the maximum and minimum are being updated correctly with each input number. **Turn debugging off when you turn in your program.**

  You can compile this program with the command:

  ```
  cc driver2.c maxmin.c
  ```

- (2 Points). Do **problem 18** in [section 3.9](http://www-ee.eng.hawaii.edu/~tep/EE160/Book/chap3/section2.1.9.html) of the text.  

  Write a function, `float pos_power(float base, int exponent);` which returns the value of base raised to a positive exponent. **If the exponent is negative, the function should return 0**. Put your function **pos_power()** in the file **exponent.c** and the prototype in the file **exponent.h**.

  Print debug information to show the argument passed into the function **pos_power()**:

  ```c
  printf("debug:Enter pos_power: base = %f exponent= %d\n", base, exponent);
  ```

  Also print the result (return value) of the function:

  ```c
  printf("debug:Exit pos_power: result = %f\n", value);
  ```


  **Turn debugging off when you hand in your programs.**

  Write a driver, **main()** in file **driver3.c**, to allow you to test the function.

  Compile this program with the command:

  ```bash
  cc driver3.c exponent.c
  ```

  Example input and output with debug information:

  ```bash
  Enter base and exponent:2 3
  debug:Enter pos_power: base = 2.000000 exponent = 3
  debug:Exit pos_power: result = 8.000000
  The power is: 8.000000  
  ```
  ```bash
  Enter base and exponent:1.5 2
  debug:Enter pos_power: base = 1.500000 exponent = 2
  debug:Exit pos_power: result = 2.250000
  The power is: 2.250000
  ```
  ```bash
  Enter base and exponent:2 0
  debug:Enter pos_power: base = 2.000000 exponent = 0
  debug:Exit pos_power: result = 1.000000
  The power is: 1.000000
  ```
  ```bash
  Enter base and exponent:2 -1
  debug:Enter pos_power: base = 2.000000 exponent = -1
  debug:Exit pos_power: result = 0.000000
  The power is: 0.000000
  ```
  ​




## Turn in

- Use the "**grade**" command to turn in **six source files** (**numbers.c, maxmin.c, exponent.c, driver1.c, driver2.c, and driver3.c**) and the **two header files** (**maxmin.h and exponent.h**), and verify.

  `grade -lab6s2,ee160  *.c *.h `  
  ` grade -lab6s2,ee160`  


  



## Tutorial offering from the CoE

<http://web.eng.hawaii.edu/Tutor/intro.html>

## Unix/Linux Command Cheat Sheet

<https://files.fosswire.com/2007/08/fwunixref.pdf>
