
*Thursday, June 27, 2024 - 08:44*

Tags: [[software engineering]] [[javascript]]

---

#### Vol. 2 - Scope and Closure

**p1**
"It may be self-evident, or it may be surprising, depending on your level of interaction with various languages, but despite the fact that JavaScript falls under the general category of “dynamic” or “interpreted” languages, it is in fact a compiled language."


**p2**
Simple and dumb steps of *code compilation:*
1. Tokenizing
   Turning the code text into a series of tokens. Say `var a = 2;` is tokenized into "var, a, =, 2".
2. Parsing
   Based on the stream of tokens, turn it into a tree of nested elements. From the example above, it could go with something like "It's a `VariableDeclaration` with a child named `Identifier` with a value of `a`, one other child named `AssignmentExpression` which has a child of itself named `Numericliteral` with a value of `2`."
3. Code generation
   From the tree structure above, generate machine code.
   
Again, I know no shit about code compilation. The definition above shouldn't be taken seriously, and take it from a view of an amateur. (That's why I'm studying it, duh)


**p3**
"For one thing, JavaScript engines don’t get the luxury (like other language compilers) of having plenty of time to optimize, because JavaScript compilation doesn’t happen in a build step ahead of time, as with other languages."

JavaScript is a compiled language (sort of). But the compilation is unlike a more traditional language where their compilation happens on build time. JavaScript is compiled on *runtime.*


**p7**
"You might be tempted to conceptualize the function declaration function foo(a) {… as a normal variable declaration and assignment \[…] However, the subtle but important difference is that Compiler handles both the declaration and the value definition during code-generation \[…]"

So, is this how 'hoisting' happen? That is the value of a function is seemingly already declared even before the function declaration hasn't appeared before the expression which invoked the function.

Therefore, even if we put function declaration at the bottom of the script, the code above it can still use it. Because the function identifier and definition assignments happen on Compiler layer, rather than the usual Compiler-identifier and Engine-definition.


**p10**
Why does it matter to differentiate between LHS or RHS? Because these two lookups behaves differently when the variable hasn't been declared.

Consider the following:
```js
function foo(a) {
	console.log(a + b)
}

/* Variable 'b' is declared beforehand. Compiler has asked Scope to create one on compile time. Even if it's empty, it's there in the Scope for whoever needs it. */
var b; 

/* On the other hand, if variable 'b' is never declared. Then, Compiler would never asked Scope to create an empty 'b' container beforehand. Leading to whatever part of the code that asked for 'b' to the Scope to not be able to find anything at all. Thus, results in 'ReferenceError' */
// var b;

foo(2);
```

Remember that variable identifier is declared by Compiler when the variable isn't found in the Scope. Compiler will then ask Scope to create identifier `b`, albeit with an empty value. And then generate a code for Engine to assign it with a proper value according to the script. As for the example above, the value is `undefined.`

On the contrary with RHS look-ups, if variable `b` is not found in all Scopes, as in the Compiler never see any resemblance of variable declaration for identifier `b`, then it will throw a `ReferenceError: b is not defined` error.

To conclude, if LHS look-up couldn't find a certain variable, it will ask Scope to create one on compile time. On the other hand, if RHS look-up couldn't find a certain variable in the Scope, it will throw a `ReferenceError`.

Now, let's switch the case for a bit to differentiate between variable declaration by Compiler, and variable assignment by Engine.
```js
function foo(a) {
	console.log(a + b);
}

foo(2); // NaN.

var b = 2;

foo(2); // 4.
```

I find this case very intriguing. As someone who has always been simply thinking of program execution from top to bottom, with the addition of knowledge of JavaScript Compiler creating an empty variable container on compile time, it makes me wonder about the case as written above.

Previously, I would think of the first `foo(2)` to throw a `ReferenceError`. Because at that point, `var b = 2` hasn't appeared yet for the first `foo(2)` execution context.

However, knowing about Compiler and its creating an empty variable container before execution, I wonder if the actual value would be `undefined` instead of simply "variable doesn't exist." I had a hypothesis that if it's truly `undefined`, then the result should be `NaN`. Otherwise, it would throw a `ReferenceError`. Lo and behold, the result is `NaN`. My hypothesis is proven to be correct.

At the time of executing the first `foo(2)`, Scope only know the value of `b` to be `undefined`. However, after the Engine arrives at line `var b = 2`, and it executes the second `foo(2)`, Scope now knows the value of `b` to be `2`. Scope returns `2` to Engine, and Engine gives it to `foo` function, which resulted in `4`.


**p11**
"`ReferenceError` is scope resolution-failure related, whereas `TypeError` implies that scope resolution was successful, but that there was an illegal/impossible action attempted against the result."

`ReferenceError` is because you can't find the value you're looking for in the scope. While `TypeError` is you using the successful result from scope to do something inappropriate. Weird. Yeah, you.