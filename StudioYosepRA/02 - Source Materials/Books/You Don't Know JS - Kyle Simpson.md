
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


