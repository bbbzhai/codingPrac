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