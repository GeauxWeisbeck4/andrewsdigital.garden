---
{"dg-publish":true,"permalink":"/200-books/206-effective-c/effective-c/"}
---

[/toc/]
1. ((Chapter 1 - Getting Started With C))
2. [[200 Books/206 Effective C/Chapter 2 - Objects Functions and Types\|Chapter 2 - Objects Functions and Types]]
3. 


## Chapter 1: Getting Started with C
- ## The void type
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

