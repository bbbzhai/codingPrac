# Difference between definition and declaration in C++/C
* A variable declaration: specifies the type and name of a variable. It makes a name known to the program. A file that wants to use a name defined elsewhere includes a declaration for that name.

* A definition: creates the associated entity. (Gives it a memory location)

### A variable definition is a declaration. 
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
