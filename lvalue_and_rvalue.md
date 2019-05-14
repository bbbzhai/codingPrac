#lvalue (reference) and rvalue (reference)

##lvalue reference (or simply reference)

int ival = 1024;
int &refVal = ival; // refVal is another name for ival
int &refVal2; //error: a reference must be **initialized**!

"Ordinarily, when we initialize a variable, the value of the initializer is copied into the object we are creating. When we define a reference, instead of copying the initializer’s value, we bind the reference to its initializer. Once initialized, a reference remains bound to its initial object. There is no way to rebind a reference to refer to a different object. Because there is no way to rebind a reference, references must be initialized."

* A reference is not an object. Instead, a reference is just another name for an already existing object

* A reference must reference to an **OBJECT**(lvalue), can't reference to temporaty value (rvalue) 

* I think of reference as a special case of pointer. I guess in implementation, the reference "stores" the address of that variable, but to use it, you don't need to dereference. Sort of "convenient". 

* one ugly looking definition: \*&r = p; // r is a reference to the pointer p

[A good place to look at](https://www.ntu.edu.sg/home/ehchua/programming/cpp/cp4_PointerReference.html)


## pointer

* nullptr  //null pointer literal. 
* advice: initialize all pointers. 


Will write more about lvalue and rvalue later.