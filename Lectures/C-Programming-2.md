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

## Introduction (or dereference) Operator: *

\* on Rside - read the contents of the variable to get an address

## Compare indirection operator and address operator

### address operator (&): 

- get the address of this box

### indirection operator (*)

- follow the arrow to the next box and get its contents

## Introduction: indirection operator Lside

- 







