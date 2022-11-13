## Memory

1 bit has 2 states: 0, 1

Memory: organized into a fixed unit of 8 bits - 1 bytes
  - Most significant bit - MSB
  - Least significant bit - LSB

Memory is a single, large array of bytes, where <span style = "color:blue">each byte has a unique</span> <span style = "color:red">address (byte addressable memory)</span>

Each byte in memory can be individually accessed and operated on given its unique address.

## Address and Pointers

A pointer is a variable whose contents (or value) can be properly used as an address
  - value: a valid address allocated to the process by the operating system
  - values can be changed

## Variables in Memory: Size and Address

The number of contiguous bytes a variable uses is based on the type of the variable
  - char - 1 byte
  - short int - 2 bytes
  - int - 4 bytes

Variable names map to a starting address in memory

## sizeof(): Variable Size Operator

sizeof() operator returns a value of type size_t, i.e. the # of bytes used to store a variable or variable type

size_t type may vary by system but is always unsigned

valid: size_t size = sizeof(variable_type)
preferred: size_t size = sizeof(variable_name)
  - argument: often an expression
  - eg: size = sizeof(int * 10);

## Memory Addresses & Memory Content

Variable name in a C statement

### Lvalue
on left side of the = sign
- address where it is stored in memory - a constant
- address assigned to a variable cannot be changed at runtime

### Rvalue
on the right side of an = sign
- contents or value stored in the variable 
- requires a memory read to obtain
- ![LRvalue](/images/C2-0.png)

Example 1
- ![LRvalue1](/images/C2-1.png)
- x is on left side of the = assignment operator: using x's Lvalue
- y is on right side of the assignment operator: using y's Rvalue
- x = y: read memory at y (Rvalue), write it to memory at x's address (Lvalue)

## Introduction: Address Operator: &

produces the address of where an identifier is in memory
- identifier must have a Lvalue; e.g.: cannot not be &12
- get an address for use on the Rside
  - &variable
  - function_name: equivalent &functtion_name; not function()
  - array_name: equivalent - &array_name;

printf(): to display an address/pointer (in hex) is "%p"

Introduction: Pointer variables

Pointer: the Rside of contains a memory address
- content: an unsigned memory address
- need specify the type of variable to which the pointer points

```c
int *p = &i; // * is part of the definition

// same as below

int *p;
p = &i;
```

- Pointer variables all use the ***same amount of memory*** no matter what they point at

### Introduction: indirection (or dereference) Operator: *

```c
z = *x
```
\* on Rside
 - read the contents of the variable to get an address
 - read and return the contents at that address
 - two reads of memory on the Rside

```c
*z = x
```
\* on Lside
 - read the contents of the variable to get an address
 - write the evaluation of the Rside expression to that address 
 - 1 read and 1 write on the Lside

## The NULL Constant and Pointers

- NULL is a constant that evaluates to zero (0)
- assign NULL to a pointer vairable - the pointer does not point at anything, and it is called a "NULL pointer"
- memory location 0 is not a valid memory address in any C program
deferencing(*) NULL at runtime will cause a program fault (segmentation fault)
- e.g. 
![NULL pointer](/images/C2-2.png)

## Aliasing

Variables are aliases of each other when they all reference the same memory
- e.g. create an alias by copying one pointer to another pointer
- side effect: changing one variable's value changes others' too

## Arrays

- allocates (count * sizeof(type)) bytes of contiguous memory
- array names are constants (cannot appear on the Lside by itself)
- e.g. 
![array](/images/C2-3.png)

### Array Initialization

- type name[countt] = {val0, val1,..., valN};
  - {} (optional) initialization list can only be used at time of definition
  - an array name isjust the address of the first element in a block of contiguous memory

```c
// determining element count for a compiler calculated array
#include <stddef.h>
  int block[] = {2, 3, 5, 6, 11, 13};    // automatic: compiler calculates array size

int cnt = (int)(sizeof(block) / sizeof(block[0])); 	// in this case cnt = 6
   
for (int indx = 0; indx < cnt; indx++)
	block[indx] = 0;
```

### Pointer and Arrays 

```c
int buf[] = {2,3,5,6,11};
```

- buf and &buf[0] on the Rside are equivalent

### Pointer Arithmetic In Use - C's Performance Focus

- C performance focus does not oerform any array "bounds checking"
- OS only "faults" for an incorrect access to memory (read-only or not assigned to your process)
- lack of bound checking is a common source of errors and bugs and is a common criticism of C

## C Strings

Strings in c are not objects
  - no embedded information about them, you just have a name and a memory location
  - cannot use + or += to concatenate strings
  - terminated by a sentinel terminal character '\0'

### String initialization

- when you combine the automatic length definition for arrays with double quote(") initialization
  - compiler addes the null terminator '\0' for you

```c
char a[4] = {'c', 'a', 't', '\0'}; 
char b[] = "cat"; // compiler calculates size, adds '\0'
char c[] = {'c', 'a', 't', '\0', 'a', 'b'}; // array size 6, string length 3
char empty[] = ""; // empty, contains '\0', string length 0
```

equivalent 4-character arrays
- these are all strings as they include a null('\0') terminator

```c
char a[4] = {'c', 'a', 't', '\0'};
char b[4] = {'c', 'a', 't', 0};
char c[4] = {'c', 'a', 't'}; // missing initial value defaults to 0
char d[4] = {99, 97, 116, 0}; // 99 = 'c', 97 = 'a', 116 = 't'
char e[4] = "cat";
char f[4] = "cat\0"; // literal has 5 chars; array f string length is 3
```

## Different ways to pass parameters
