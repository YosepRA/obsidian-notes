
*Tuesday, September 10, 2024 - 16:53*

Status:

Tags: [[software engineering]] [[javascript]]

---

Before I start, I would like to say that I'm new to writing technical topics, such as compilers which I want to talk about today. It is going to feel like I don't know what I'm rambling about below, but this note, like many other notes, is written so that I can explain what I read in my studies in my own language. 

What I'm saying is don't take the writing below seriously, and please take it as an attempt for someone who has never written technical docs or even form proper sentences when he tries to explain a certain technical concept. Thank you!

---

When I think about compilers, I'm thinking about a process where a code that is written in a language which human can understand are transformed into yet another form of language that can be understood by machine. In my current level, I have not the sophistication to truly appreciate what compilers do to my code thus far. However, the curiosity remains. And the desire to dive deep continues to rage within me. So this marks one of my first steps to seriously face software engineering.

I'm reading Volume 2: *Scope & Closure* from *You Don't Know JS* book series by Kyle Simpson. It is a book about JavaScript, like *all* about JavaScript, both the good and "bad" parts. Or to be more precise, the casual and hardcore part. The former is the one that is makes you good enough to do your job, while the latter is the part you take if you want to seriously learn about the language. And the topic of today, my first peek on JavaScript compilers in an action as mundane as variable declaration.

For the purpose of this note, let's take a code snippet such as below as a reference:

```js
var a = 2;

console.log(a);
```

When I think about variable declaration, I used to think that somehow, someway, the machine would find the value of `a` from the memory, it will see whether such variable exist or not. If it does, assign the `2` value to it. Otherwise, it will create a new identifier `a`, then does the same to assign `2` to it. That's it.

Today, I was introduced by how JavaScript compiler does its works. Mr. Simpson uses an engaging example of a conversation between three friends, Engine, Compiler, and Scope. Engine is the one who does the execution of the code from start to finish. Compiler is the one responsible to parse and code generation. And Scope is the one who maintains a look-up list of all declared variables, and uphold the regulation as to how the code could access these variables.

Please do note that my knowledge of compilers is still shallow. However for context, I would like to explain a bit about it here. When faced with your code, compiler takes 3 steps to turn your code into a list of instruction which machine could understand. They are:

1. Tokenizing/Lexing
   Turn your code into a series of tokens such as "var, a, =, 2". I assume these pieces of "alphabets" are just lying there for the next part to use.
2. Parsing
   Using an array of tokens, compiler forms an *abstract syntax tree* (AST). Based on the simple list of tokens above, compiler determines a `VariableDeclaration` as the parent node, which has children of `Identifier` with a value of `a`, `AssignmentExpression` with a child of `NumericLiteral` with a value of `2`.
3. Code generation
   According to the tree structure as a result of parsing, compiler continues with generating machine codes ready to be executed.

Now, lets go back to the conversation between Engine, Compiler, and Scope when they see a variable declaration such as example above.

C: (It's time to compile yet another code. Hmm, I see that it's a variable declaration with an identifier of `a`. Let's ask my buddy Scope  if he has it.) "Yo, S! I have another variable declaration coming up. Do you have an identifier named `a` in your list?"
S: "Wait up, C. (…) No, I don't have one."
C: "I see. Could you make one and let its value empty for now? I'll let our buddy Engine know to assign it with value `2` later."
S: "I got you."
E: (Ah, Compiler has finished its job. Let's see what we have here. Hmm, a variable declaration of identifier `a` with value `2`. Let's ask Scope if he has `a` in his list.) "Ay, S! That Compiler sent me an instruction to assign a variable. Do you happen to have `a` in your list?"
S: "Oh yeah, bud, I have it ready. Here you go. You can use it anytime."
E: "Thanks, pal." (Now, let's assign this `2` value into `a` and return it to Scope so that the other part of the code can access it.)
E: "Hey, Scope. I have assigned `a` to value `2`. You better remember it because I may need it later."
S: "I got you, man. Unlike you who forgot what you watch on TV last night, I can always remember what is in my list."
E: "Oh, quiet you. Alright, I will come back later."
S: "Yeah, sure bud."

Haha, Mr. Simpson doesn't actually illustrate it this way, but I like to imagine this to happen. One key note to pay attention to is that the identifier `a` has actually existed before the Engine runs the code, even though the value is empty at first. The actual variable assignment is run by Engine with the instruction written by Compiler. And the result of this assignment is stored in Scope who holds and regulate this list of variables for different part of the code to use.

That's pretty much it for the high-level understanding, or to be more precise, my simplistic attempt to understand what I've been reading today. There may be a miss here and there, but I will continue on learning. Actually, I wanted to talk a bit more about how the Engine asks the Scope about a value lookup. But honestly, I have run out of juice to write anything more technical today, haha. So, please spare me today.

Hopefully, I was able to illustrate my point about variable declaration compilation in JavaScript today. Thank you for reading.

---
## References

[[You Don't Know JS - Kyle Simpson]]