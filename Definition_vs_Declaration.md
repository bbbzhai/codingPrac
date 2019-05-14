Difference between definition and declaration in C++/C
* A variable declaration: specifies the type and name of a variable. It makes a name known to the program. A file that wants to use a name defined elsewhere includes a declaration for that name.

* A definition: creates the associated entity. (Gives it a memory location)

## A variable definition is a declaration. 
*except* some situations where it only declare the variable:

The reason that one want to declare but not define a variable sometimes is that if one want to use a variable in more than one file (multiple files), then we must define that variable in **one-and only one-** file! Other files that use that variable must declare- **but not** *define* that variable

