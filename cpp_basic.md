# cpp basic
<!-- TOC depthFrom:1 depthTo:2 withLinks:1 updateOnSave:1 orderedList:0 -->

- [C++ Basic](#cpp-basic)
	- [1.0 Definition and Declaration](#def_decl)
	- [1.1 Reference and Pointer](#11-overview)
		- [1.1.1 Reference](#reference)
		- [1.1.2 Pointer](#Pointer)
	- [1.2 Const Keyword](#const)
		- [1.2.1 const pointer](#constPointer)
		- [1.2.2 const expression](#constExpr)
	- [1.3 Typedef](#typedef)

<!-- /TOC -->

## Definition & Declaration
* A variable declaration: specifies the type and name of a variable. It makes a name known to the program. A file that wants to use a name defined elsewhere includes a declaration for that name.

* A definition: creates the associated entity. (Gives it a memory location)

**A variable definition is a declaration.** 
*except* some situations where it only declare the variable:

The reason that one want to declare but not define a variable sometimes is that if one want to use a variable in more than one file (multiple files), then we must define that variable in **one-and only one-** file! Other files that use that variable must declare- **but not** *define* that variable.

(Momory Tip: declare is like talking out loud, you can always declare something, but one can only be define once)

1. extern keyword
extern int i; // declares but does not define i.  
int j;        // declares and defines j.  
extern int i = 5; // definition.  
// note: it is a error to provide an initilizer on an *extern* inside a function. 

// extern int i; tells the compiler that an object of type int calls x existes somewhere (declaration), but it is not the compiler's job to know where it exists, it just needs to know the type and name so it knows how to use it. ONce all of the source files have been compiled, the linker will resolve all of the references of i to the one definition that it finds in one of the compiled source files. 
[stackoverflow](https://stackoverflow.com/questions/10422034/when-to-use-extern-in-c)

2. function without definition
int f(int); // declares, but doesn't define f;

There are other situations, but extern keyword is the most important one.


The reason for this distinction is you can't put the same variable in two different memory location (otherwise they are two different object)


## reference and pointer

### lvalue reference (or simply reference)

int ival = 1024;
int &refVal = ival; // refVal is another name for ival
int &refVal2; //error: a reference must be **initialized**!

"Ordinarily, when we initialize a variable, the value of the initializer is copied into the object we are creating. When we define a reference, instead of copying the initializer’s value, we bind the reference to its initializer. Once initialized, a reference remains bound to its initial object. There is no way to rebind a reference to refer to a different object. Because there is no way to rebind a reference, references must be initialized."

* A reference is not an object. Instead, a reference is just another name for an already existing object

* A reference must reference to an **OBJECT**(lvalue), can't reference to temporaty value (rvalue). 
	* (Confused about one point: const reference can be initialized with literal, but non-const reference cannot) 
	* This is actually an exception. const-reference can be initialize from any expression taht can be converted to the type of the reference. 
	* If we want to use non-const, must use rvalue reference
	* Text book explanation: In this case, ri is bound to a temporary object. A temporary object is an unnamed object created by the compiler when it needs a place to store a result from evaluating an expression. C++ programmers often use the word temporary as an abbreviation for temporary object. Now consider what could happen if this initialization were allowed but ri was not const. If ri weren’t const, we could assign to ri. Doing so would change the object to which ri is bound. That object is a temporary, not dval. The programmer who made ri refer to dval would probably expect that assigning to ri would change dval. After all, why assign to ri unless the intent is to change the object to which ri is bound? Because binding a reference to a temporary is almost surely not what the programmer intended, the language makes it illegal.
	* 其实还算ok make sense


* I think of reference as a special case of pointer. I guess in implementation, the reference "stores" the address of that variable, but to use it, you don't need to dereference. Sort of "convenient". 

* one ugly looking definition: \*&r = p; // r is a reference to the pointer p

[A good place to look at](https://www.ntu.edu.sg/home/ehchua/programming/cpp/cp4_PointerReference.html)


### pointer

* nullptr  //null pointer literal. 
* advice: initialize all pointers. 


Will write more about lvalue and rvalue later.



## Const Keyword

example: 
int i = 43;
const int ci = i; 
int j = ci; 

Although ci is a const int, the value in ci is an int. The constness of ci matters only for operations that might change ci. When we copy ci to initialize j, we don’t care that ci is a const. Copying an object doesn’t change that object. Once the copy is made, the new object has no further access to the original object.


reference to const must also be a const reference: 
i.e: 
const int ci = 2015;
const int &r1 = ci;
r1 = 42    // error, r1 is a reference to const. 
int &r2 = ci;   // error: non const reference to a const object. 


* Because we can't change the value of a const object after we create it, it must be **initialized**

* A reference must reference to an **OBJECT**(lvalue), can't reference to temporaty value (rvalue). 
	* (Confused about one point: const reference can be initialized with literal, but non-const reference cannot) 
	* This is actually an exception. const-reference can be initialize from any expression taht can be converted to the type of the reference. 
	* If we want to use non-const, must use rvalue reference
	* Text book explanation: In this case, ri is bound to a temporary object. A temporary object is an unnamed object created by the compiler when it needs a place to store a result from evaluating an expression. C++ programmers often use the word temporary as an abbreviation for temporary object. Now consider what could happen if this initialization were allowed but ri was not const. If ri weren’t const, we could assign to ri. Doing so would change the object to which ri is bound. That object is a temporary, not dval. The programmer who made ri refer to dval would probably expect that assigning to ri would change dval. After all, why assign to ri unless the intent is to change the object to which ri is bound? Because binding a reference to a temporary is almost surely not what the programmer intended, the language makes it illegal.
	* 其实还算ok make sense，这就是为什么在function parameter里是const reference的话可以pass temporary variable

### const pointer and pointer to const
* pointer to const: 
const int a = 10; 
const int* ptr = &a;
\*ptr = 5; // wrong! 
ptr++; //right

* const pointer:
int a = 10;
int \*const ptr = \&a;  
\*ptr = 5; // right
ptr++;    // wrong

* 具体看const的位置在哪！

### const expression:
const expression: A constant expression is an expression whose value cannot change and that can be evaluated at compile time. A literal is a constant expression. A const object that is initialized from a constant expression is also a constant expression.  

Constexpr variable
* compiler will verify that a variable is a constant expression.
* literal type: arithmetic, reference, and pointer types are literal types. 

const int max_files = 20; // max_files is a constant expression.  
const int limit = max_files + 1; // limit is a constant expression. 
int staff_size = 27; // staff_size is not a constant expression. 
const int sz = get_size(); // sz is not a constant expression. 
Although staff_size is initialized from a literal, it is not a constant expression because it is a plain int, not a const int. On the other hand, even though sz is a const, the value of its initializer is not known until run time. Hence, sz is not a constant expression.




const int \*p = nullptr; // p is a pointer to a const int. 
constexpr int \*q = nullptr; // q is a const pointer to int. 
Despite appearances, the types of p and q are quite different; p is a pointer to const, whereas q is a constant pointer. The difference is a consequence of the fact that constexpr imposes a top-level const





## Type def

typedef double wages;  // wages is a synonym for double. 
typedef unsigned long ulong; 

C++11:
using SI = Sales_item; 