---
{"dg-publish":true,"permalink":"/200-books/206-effective-c/chapter-2-objects-functions-and-types/"}
---

- An object is storage that can represent values
- Variables have a declared type that tells you the kind of object its value represents
	- Example: object with type int contains an integer
- Functions are not objects, but they do have types
	- Function is characterized by both its return type as well as the number and types of its parameters
- C Lang also has pointers, which are addresses - a location in memory where an object or function is stored.
	- A pointer type drived from a function or object is called the referenced type. 
- ## Declaring Variables
```#include <stdio.h>

void swap(int, int); // defined in listing 2-2

int main(void) {
  int = 21;
  int b = 17;

  swap(a, b);
  print("main: a = %d, b = %d\n", a, b);
  return 0;
}

```

- This is known as a compound statement
	- We define two variables a and b within the function
	- We declare the variables having the type int and init them to 21 and 17 respectively
	- Main function calls the swap function to try and swap th e values of the two integers
- ### Swapping Values (1st attempt)
	- Objects have storage durations that determine its lifetime, or the time an object exists, has storage, has a constant address, and retains its last stored value
	- The earlier function has automatic storage duration, telling tus they exist until execution leaves the block in which they're defined 
```
void swap(int a, int b) {
  int t = a;
  a = b;
  b = t;
  print("swap: a = %d, b = %d\n", a, b);
}
```

- C distinguishes between parameters, which are objects declared as part of the function decclaration that acquire a value on entry to the function and arguments which are comma-separated expressions uou iclude in the functino call expression
- Compile above for:
```
% ./a.out
swap: a = 17, b = 21
main: a = 21, b = 17
```
- C is a call-by-value language which meaens that when you provide an argument inside a function, that argument value is copied into distinct value for use within that function.

#### Swapping Values (second attempt)
- TO repair the bug we can use pointers to rewrite the swap function. Use indirection ( * ) operator to declare pointers and dereference them
```
void swap(int)
```

### Scope 
- Objects functions, macros, and other C lang indentifiers have scope that delimits the contiguous region where they can be accessed 
- Four types of scope:
	- file
	- block
	- function prototype
	- function
- Determined by where it is declared
	- File scope: Outside any block or parameter list
	- Block Scope: Inside any block or parameter list
	- Function prototype scope: Declaration appers within the list of aparameter declarations in a function prototype
	- Function Scope: Area between the opening of a function definitive and its closing
	- labesl are identifiers followed by a colon and identify a statement in a function tow hich control may be transferred
- Scopes can be nested with inner and outers scopes
	- See listing 2-5 scope

### Storage Duration
- Objects have a storage duation that determines their lifetime - four storage durations are available:
	- automatic
	- static: Objects declared in file scope, lifetime is the entire execution of the program and stored value is initilzed prior to program startupcountcpc
	- thread - concurrent programming
	- allocated - discussed in chapter 6

#### Alignment
- requirements that place restrictions on the addrewsses at which objects of that type may be allocated. 
- Represents the number of bytes between successive addresses at which teh given object can be allocated. 
- Could be a performance penaltiy for multibyte accesses on non-word boundaries
	- Word - natural, fixed-sized unit of adata handled gby the instrution set or the hardware of the processor
- Some platforms cannot access unaligned memory
- Compiler typically chooses suitable alignments for various types in C
	- Rare occasions: align data on the boundaries of the memory cache lines that must start power-of-two address boundaries or to meet other system-specific requirements
- Example for specifying alignments:
```
struct S {
	int i; double d; char c;
}

int main(void) {
	unsigned char bad_buff[sizeof(struct S)];
	_Alignas(struct S) unsigned char good_buff[sizeof(struct S)];
struct S *bad_s_ptr = (struct S *)bad_buff; //wrong pointer alignment
struct S *good_s_ptr = (struct S *)good_buff; // correc t pointer alignment
}
```

#### Object Types
- #### Boolean Types
	- When declared _ Bool can only store values 0 and 1. 
	- Was introduced in C99
	- Declared with underscore which means its reserved
	- true = 1
	- false = 0
```
#include <stdbool.h>
_Bool flag1 = 0;
bool flag2 = false;
```

#### Character Types
- 3 types 
	- char - represents character data in C; must be able to represent minimum set of characters required in teh execution environment
	- signed char 
	- unsigned char
	- Inappropriate for integer data
		- signed char works for small integer values
		- unsigned char represents small unsigned values

#### Numerical Types
- Can be used to represent integers, enumerators, and floating point values 

#### Integer Types
- Signed integer types: represent negative numbers, positive numbers, and zero
- Include unsigned char, unsigned short int, unsigned int, unsigned long int, and unsigned long long int
- Unsigned int can only represent positive numbers and zero
- Types are ordered by width
- Wider types are at least as loarge as narrower types 
- Actual size is specified in the <limits.h> header file
- Natural size suggested by the architecture of the execution environment 16 bits wide on a 16 bit architecture, 32 bits on 32...
- Can specify actual width integers by using tuype definitions <stdint.h> <inttypes.h> headers like uint32_t 
- uintmax_t intmax_t

#### enum types
- allows you to define a type that assignes names (enumerators) to integer values in cases with an enumerable set of constant values
- Examples:
```
enum day { sun, mon, tue, wed, thu, fri, sat }
enum cardinal_points { north = 0, east = 90, south = 80, west = 270 }
enum months { jan =1, feb, mar, apr, may, june, july ... }
```
- If you don't specify a value, starts at 0 and increments by 1

#### Floating-Point Types
- 3 types supported in C
	- Float
	- Double
	- Long Double

#### Void Types
- strange
- Cannot hold value, can use to indeicate that a funciton doesn't return a value
- Derived type void*

#### Function Types
- Derived types
- Function declarator - specifies the name of the function and the return type
```
int f(void);
int *fip();
void g(int i, int j);
void h(int, int)
```
- 1st: decalre function f with no parameters that returns an int
- Declare function fip with no specified parameters returns a point to an int
- Declare two functions, g and h, each returning void and taking two parameters of type int
- function prototype: function type with a parameter type list
- function definitions are used in compliers when they verify that the correct number and type of parameters used in the function definition and any calls in the function
- Function definition:
```
int max(int a, int b)
{ return a > b ? a : b; }
```
- function says; return type is int; function declarator is max(int a, int b) funciton body is end
	- says if a is greater than b return a, otherwise return b

#### Derived Types
- Types that are constructed form other types

#### Pointer Types
- derived form the function or object type taht it points to called referenced type. 
- Proivides a refrernece to an entity of the referenced type
```
int  *ip;
char *cp;
void *vp;
```
- declare pointer to int, char and void
- Result of th operator has tyhe type pointer to int
```
int i = 17;
int *ip = &i;
```

```
ip = &*ip;
```
- Unary operator converst a pointer to a type into a value of that type 
- denotes inderection and operates only on pointers

#### Arrays
- Contiguously allocated sequence of ebjects that all have the same element type
- Characterized by their element types and the number of elements in the array
- example:
```
int ia[11];
float *afp[17];
```
How to assign values to the elements of an array:
```
char str[11];
for (unsigned int i = 0; i < 10; ++i) {
  str[i] = 'o' + i;
}
str[10] = '\o';
```
- First line - declares an array of char with a bound of 11
	- allocates sufficient storage to create a string w/ 10 characters plus a null character
- `for` loop iterates 10 times with the values of i ranging from 0 to 9
- Each iteration assings the result of the expression '0' + i to str[i]
- Following end of loop, th enull character is copied to the final elmement of array str[10]
	- In the expression ` = 'o' + i;` str is automatically converted to a pointer to the first member of the array and i has an unsigned integer type
- If the operand of the unary & operator is the result of a [] operator, the result is as if the & operator were removed and the [] operator were thcanged to a + operator 
	- for example, &str[10] is same as str + 10
- You can also declare multidimensional arrays:
```
void func(int arr[5]);
int main(void) {
  unsigned int i = 0;
  unsigned int j = 0;
  int arr[3][5];
  func(arr[i]);
  int x = arr[i][j];
  return 0;
}
```
- When expression arr[i]  occurs:
	- 1. arr is converted to a pointer in the initial array of five elements of type `int` starting at arr[i]
	- 2. `i` is scaled to the type of arr by multiplying i by the size of one array of five int objects
	- 3. The results from steps 1 and 2 are added
	- 4. Indirection si applied to the result to prduce an array of five elements of type int
- When used in expression arr[i][j] at 2, that array is converted to a pointer to the first element of type `int` so arr[i][j] produces an object of type int

#### Structures 
- A structure types contains sequentially allocated member objects
	- each has its own name and have a distinct type

```
struct sigrecord {
  int signum;
  char signame[20];
  char sigdesc[100];
} sigline, *sigline_p;
```
- 3 member objects
	- `signum` object of type int, signame is an array of type char consisting of 20 elements, and sigdesc is an array of type char consisting of 100 elements 
	- Useful for delaring collections of related objects and may be used to represent things such as a date, customer, or personnel record
	- Especially useful for grouping objects that are frequently uspassed together as arguments to a function so you don't need to repeatedly pass individual objects separately