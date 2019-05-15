# Const

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

## const expression:
const expression: A constant expression is an expression whose value cannot change and that can be evaluated at compile time. A literal is a constant expression. A const object that is initialized from a constant expression is also a constant expression.  

Constexpr variable
* compiler will verify that a variable is a constant expression.
* literal type: arithmetic, reference, and pointer types are literal types. 

const int max_files = 20; // max_files is a constant expression.  
const int limit = max_files + 1; // limit is a constant expression. 
int staff_size = 27; // staff_size is not a constant expression. 
const int sz = get_size(); // sz is not a constant expression. 
Although staff_size is initialized from a literal, it is not a constant expression because it is a plain int, not a const int. On the other hand, even though sz is a const, the value of its initializer is not known until run time. Hence, sz is not a constant expression.