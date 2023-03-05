---
{"dg-publish":true,"permalink":"/500-catalog-of-notes/513-web-dev/c/c-language/"}
---

- # Program Structure
	- Hello World in C
	```
	#include <stdio.h>
	
	int main() {
		/* my first program in C */
		printf("Hello, World! \n");
	
		return 0;
		}
	```
	Let us take a look at the various parts of the above program −
	
	-   The first line of the program _#include <stdio.h>_ is a preprocessor command, which tells a C compiler to include stdio.h file before going to actual compilation.
	    
	-   The next line _int main()_ is the main function where the program execution begins.
		- #### Freestanding environment
			- may not provide an operating system and is typically used in embedded programming
		- Effective C assumes a hosted environment
	    
	-   The next line /*...*/ will be ignored by the compiler and it has been put to add additional comments in the program. So such lines are called comments in the program.
	    
	-   The next line _printf(...)_ is another function available in C which causes the message "Hello, World!" to be displayed on the screen.
	    
	-   The next line **return 0;** terminates the main() function and returns the value 0.
	## Compile and Execute C Program
	
	Let us see how to save the source code in a file, and how to compile and run it. Following are the simple steps −
	
	-   Open a text editor and add the above-mentioned code.
	    
	-   Save the file as _hello.c_
	    
	-   Open a command prompt and go to the directory where you have saved the file.
	    
	-   Type _gcc hello.c_ and press enter to compile your code.
	    
	-   If there are no errors in your code, the command prompt will take you to the next line and would generate _a.out_ executable file.
	    
	-   Now, type _a.out_ to execute your program.
	    
	-   You will see the output _"Hello World"_ printed on the screen.
```
	$ gcc hello.c
	$ ./a.out
	Hello, World!
```
# Basic Syntax
## Tokens in C

A C program consists of various tokens and a token is either a keyword, an identifier, a constant, a string literal, or a symbol. For example, the following C statement consists of five tokens −
```
printf("Hello, World! \n")
Individual tokens:
printf
(
	"Hello, World! \n"
)
;
```
## Identifiers

A C identifier is a name used to identify a variable, function, or any other user-defined item. An identifier starts with a letter A to Z, a to z, or an underscore '_' followed by zero or more letters, underscores, and digits (0 to 9).

C does not allow punctuation characters such as @, $, and % within identifiers. C is a **case-sensitive** programming language. Thus, _Manpower_ and _manpower_ are two different identifiers in C. Here are some examples of acceptable identifiers −

mohd       zara    abc   move_name  a_123
myname50   _temp   j     a23b9      retVal

## Keywords you can't use - djasfjkl

# Data Types
- Data types in c refer to an extensive system used for declaring variables or functions of different types. The type of a variable determines how much space it occupies in storage and how the bit pattern stored is interpreted.
	- ### 1. **Basic Types**
		- They are arithmetic types and are further classified into: (a) integer types and (b) floating-point types.
	- ### 2. Enumerated types
		- They are again arithmetic types and they are used to define variables that can only assign certain discrete integer values throughout the program.
	- ### 3. The type void
		- Type specifier void indicates no value is available
	- ### 4. Derived Types
		- They include (a) Pointer types, (b) Array types, (c) Structure types, (d) Union types and (e) Function types.
## Integer Types

| -- Type --     | -- Storage Size --                | -- Value Range --                                    |
| -------------- | --------------------------------- | ---------------------------------------------------- |
| char           | 1 byte                            | -128 to 127 or 0 to 255                              |
| unsigned char  | 1 byte                            | 0 to 255                                             |
| int            | 2 or 4 bytes                      | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647 |
| unsigned int   | 2 or 4 bytes                      | 0 to 65,535 or 0 to 4,294,967,295                    |
| short          | 2 bytes                           | -32,768 to 32,767                                    |
| unsigned short | 2 bytes                           | 0 to 65,535                                          |
| long           | 8 bytes or (4bytes for 32 bit OS) | -9223372036854775808 to 9223372036854775807          |
| unsigned long  | 8 bytes                           | 0 to 18446744073709551615                                         |

- ## sizeof operator
	- To get the exact size of a type or a variable on a particular platform, you can use the **sizeof** operator. The expressions _sizeof(type)_ yields the storage size of the object or type in bytes. Given below is an example to get the size of various type on a machine using different constant defined in limits.h header file 
	- example of sizeof:
```
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <float.h>

int main(int argc, char** argv) {

    printf("CHAR_BIT    :   %d\n", CHAR_BIT);
    printf("CHAR_MAX    :   %d\n", CHAR_MAX);
    printf("CHAR_MIN    :   %d\n", CHAR_MIN);
    printf("INT_MAX     :   %d\n", INT_MAX);
    printf("INT_MIN     :   %d\n", INT_MIN);
    printf("LONG_MAX    :   %ld\n", (long) LONG_MAX);
    printf("LONG_MIN    :   %ld\n", (long) LONG_MIN);
    printf("SCHAR_MAX   :   %d\n", SCHAR_MAX);
    printf("SCHAR_MIN   :   %d\n", SCHAR_MIN);
    printf("SHRT_MAX    :   %d\n", SHRT_MAX);
    printf("SHRT_MIN    :   %d\n", SHRT_MIN);
    printf("UCHAR_MAX   :   %d\n", UCHAR_MAX);
    printf("UINT_MAX    :   %u\n", (unsigned int) UINT_MAX);
    printf("ULONG_MAX   :   %lu\n", (unsigned long) ULONG_MAX);
    printf("USHRT_MAX   :   %d\n", (unsigned short) USHRT_MAX);

    return 0;
}
```
- compiles to this on linux:
```
CHAR_BIT    :   8
CHAR_MAX    :   127
CHAR_MIN    :   -128
INT_MAX     :   2147483647
INT_MIN     :   -2147483648
LONG_MAX    :   9223372036854775807
LONG_MIN    :   -9223372036854775808
SCHAR_MAX   :   127
SCHAR_MIN   :   -128
SHRT_MAX    :   32767
SHRT_MIN    :   -32768
UCHAR_MAX   :   255
UINT_MAX    :   4294967295
ULONG_MAX   :   18446744073709551615
USHRT_MAX   :   65535
```

## Floating-Point Types

| -- Type --  | -- Storage Size -- | -- Value Range --      | -- Precision --   |
| ----------- | ------------------ | ---------------------- | ----------------- |
| float       | 4 byte             | 1.2E-38 to 3.4E+38     | 6 decimal places  |
| double      | 8 byte             | 2.3E-308 to 1.7E+308   | 15 decimal places |
| long double | 10 byte            | 3.4E-4932 to 1.1E+4932 | 19 decimal places                  |

- The header file float.h defines macros that allow you to use these values and other details about the binary representation of real numbers in your programs. The following example prints the storage space taken by a float type and its range values −
```
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <float.h>

int main(int argc, char** argv) {

    printf("Storage size for float : %d \n", sizeof(float));
    printf("FLT_MAX     :   %g\n", (float) FLT_MAX);
    printf("FLT_MIN     :   %g\n", (float) FLT_MIN);
    printf("-FLT_MAX    :   %g\n", (float) -FLT_MAX);
    printf("-FLT_MIN    :   %g\n", (float) -FLT_MIN);
    printf("DBL_MAX     :   %g\n", (double) DBL_MAX);
    printf("DBL_MIN     :   %g\n", (double) DBL_MIN);
    printf("-DBL_MAX     :  %g\n", (double) -DBL_MAX);
    printf("Precision value: %d\n", FLT_DIG );

    return 0;
}
```
- Compiled to linux
```
Storage size for float : 4 
FLT_MAX      :   3.40282e+38
FLT_MIN      :   1.17549e-38
-FLT_MAX     :   -3.40282e+38
-FLT_MIN     :   -1.17549e-38
DBL_MAX      :   1.79769e+308
DBL_MIN      :   2.22507e-308
-DBL_MAX     :  -1.79769e+308
Precision value: 6
```
## The void type
- #### 1. Function returns as void
	- There are various functions in C which do not return any value or you can say they return void. A function with no return value has the return type as void. For example, **void exit (int status);**
- #### 2. Function arguments as void
	- There are various functions in C which do not accept any parameter. A function with no parameter can accept a void. For example, **int rand(void);**
- #### 3. Pointers to avoid
	- A pointer of type void * represents the address of an object, but not its type. For example, a memory allocation function **void *malloc( size_t size );** returns a pointer to void which can be casted to any data type

## Portability issues
- #### Implementation-defined behavior 
	- Program behavior that's not specified by the C standard and that may offer different results among implementations but has consistent documented behavior within an implementation
- #### Unspecified behavior 
	- Program behavior for which the standard provides two or more options and imposes no requirements
- #### Undefined behavior
	- Behavior that isn't defined by the C Standard or less cirucularly. "Behavior upon use of a nonportable or erroneous program construct of erroneous data"
	- Undefined in the standard are as follows:
		- When a "shall" or "shall not" requirement is violated and the requirement appears outside a constraint
		- When behavior is explicityly specified by the words "undefined behavior"
		- By the omission of any explicit definition of behavior
	- We have explicit and implicit undefined behavior - none of the three are differentin emphasis
	- Behaviors are classified as undefined by the C standards comittee to do the following:
		- Give the implementer license not to catch program errors that are difficult to catch
		- Avoid defining obscure corner cases that owuld favor one of the implementations strategy over another
		- Identify areas of possible conforming language extension in which the implementer may augment the language by providing a definition of the officially undefined 
	- Compilers (implementations) have the latitude to do the following:
		- Ignore undefined behavior completely, giving unpredictable results
		- Behave in a documented manner characterstic of the enironment (with or without a diagnostic)
		- Terminate a transaltion or execution
	- 
- Locale-specific behavior
- Common extensions

