
# References and borrowing

*``Note: The opposite of referencing by using & is dereferencing, which is accomplished with the dereference operator, *.``*

&var creates reference that points to memory location of *var* on heap

*``but the value pointed to by the reference is not dropped when s (reference variable) stops being used because s doesn’t have ownership. ``*

*``Just as variables are immutable by default, so are references. We’re not allowed to modify something we have a reference to.``*

*``Mutable references have one big restriction: if you have a mutable reference to a value, you can have no other references to that value.``*

*``We also cannot have a mutable reference while we have an immutable one to the same value.``*

It would be terrible if someone changes value that is considered immutable by some other "user" (immutable reference variable). Of course, if immutable users are out of scope () then it is possible to make mutable refernece.

     |
     |
     |    
     V
 - **The ability of the compiler to tell that a reference is no longer being used at a point before the end of the scope is called Non-Lexical Lifetimes (NLL for short)**

*``In Rust, by contrast, the compiler guarantees that references will never be dangling references: if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.``*

This means that as long as reference variable is in scope, referenced value must be present and cannot be dropped

 - **At any given time, you can have either one mutable reference or any number of immutable references.**

*``Tuple structs are useful when you want to give the whole tuple a name and make the tuple a different type from other tuples, and when naming each field as in a regular struct would be verbose or redundant.``*

Struct tuple has keeps all functionalities as tuple, like destructuring or indexed-accessing. Only difference ist that type must be explicit.

*``The &self is actually short for self: &Self``*

This implies that borrowing happens here. Methods can take ownership of self, borrow self immutably as we’ve done here, or borrow self mutably, just as they can any other parameter.
