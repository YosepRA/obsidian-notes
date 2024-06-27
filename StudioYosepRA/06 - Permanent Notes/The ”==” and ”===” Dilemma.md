
*Thursday, June 27, 2024 - 09:45*

Status:

Tags: [[software engineering]] [[javascript]]

---

```js
const a = '42';
const b = 42;

a == b; // true
a === b; // false
```

JavaScript is an the programming language of the web. At the moment, there is no other alternative that can take JavaScript from its throne, mainly because it has become so huge that the alternatives are simply not worth the time and effort to learn. 

However, it is also a well-known fact that JavaScript has its *peculiarities.* I'm not saying that other programming languages don't have their own weird quirks, but there are some in JavaScript that I could never understand why it was invented.

I'm reading *You Don't Know JS* by Kyle Simpson. I want to dive deep into JavaScript to thoroughly understand all about it. I'm still on book 1 *Up & Going* which serves as an introduction of the whole book series. Book 1 introduces many essential building blocks in JavaScript and a few peculiar quirks that the language has. One of them is *implicit type coercion.*

Type coercion is a feature of JavaScript that converts one value type to another. There are two ways it can happen, explicit and implicit. Explicit coercion can be done by *intentionally* converting one value type to another, such as using the native type objects `String` and `Number`. On the other hand, implicit coercion happens when the JavaScript runtime itself that is doing the type coercion.

Such is the case from the code block at the top of this post. We have two variables, one is holding the value of string 42, while the other number 42. Using the loose equal operator (`==`), the comparison results in `true`. While on the other hand, when using the strict equal operator `(===)`, the comparison results in `false`.

This happens because loose equal operator implicitly coerce the type of its operand. In this case, string 42 is converted into number 42. Then the final comparison results in `42 == 42`, which results in `true`. While on the other hand, strict equal operator doesn't coerce its type, therefore comparing the presented values as is, resulting in `false`.

Implicit type coercion has always been a bug in my mind. I'm rather averse of using it because it adds an unnecessary layer of complexity that can be solved using a simpler approach of strict equality. Perhaps I don't understand enough about its peculiarity that it's rather a guesswork for me had I use it in my code, resulting in myself expecting the unexpected in my code had I use implicit coercion. And this is why I read *You Don't Know JS* for exactly this reason, which is to understand more about implicit coercion, and perhaps many other quirks that I couldn't recall.

However, from what I already know about its behavior, I conclude that even if I know the nitty gritty of implicit coercion, I don't think I would use it in my code. Why? Because, again, it introduces an unnecessary layer of complexity and guesswork to the software.

If one truly understands how implicit coercion works, then he must have had a clear expectation of what kind of data the program is going to have, will he not? Say I expect a number from user's form:

```js
function processForm() {
	const age = form.values.age; // e.g. '30'

	if (age == 30) {
		console.log('Wow, you are indeed 30 years old.');
	} else {
		console.log('I guess, you are not 30 years old.');
	}
}
```

Forms in the web always results in string. Even if you expect data that is clearly a number, such as age, it will always turn out to be a string when we read it. Therefore, it is necessary to convert these values into number, especially if you are going to use it for numerical operations later on.

Using loose equality in the case above may have work, and it does make the code readable. But once again, only if you understand how implicit coercion works. If you don't understand how it works, then again, everything becomes guesswork. You will only notice the bug when you are trying to use the string value for numerical operations.

Now, compare the `processForm` with the one below:

```js
function processForm() {
	const age = parseInt(form.values.age, 10); // '30' converted to 30.

	if (age === 30) {
		console.log('Wow, you are indeed 30 years old.');
	} else {
		console.log('I guess, you are not 30 years old.');
	}
}
```

I've only added an explicit coercion from string to number using the `parseInt` function. Then on the `if` block, the comparison is using string equal operator. At this point, just from reading the code, it becomes obvious what kind of data that is entering the comparison block. It is clear that variable `age` is holding a number version of the user's age input. This way, I don't have to think anymore about coercion and whatnot, because I know what kind of data I'm expecting, and how I'm about to use said data in my algorithm. There is no guesswork, just straightforwardness of the code. And I argue, that even if I add a layer of type coercion using `parseInt`, this code is more readable than the one that uses loose equality.

I'm not against using JavaScript's peculiarities into strength in your code. However, it is clear to me that having an implicit coercion in your code adds an unnecessary layer of guesswork in your code. I favor for a code that is both readable and straightforward, meaning there is little to no guesswork and falsehood. If the app needs a number, then give it a number. Turn the possibly incompatible value type into the one that the app actually needs. Especially if you know from the case above that form values are often a string by default. If one of your form field is a number, and you are expecting it to be a number, then turn it into a number before going any further, for goodness' sake. 🤣

Once again, this post is perhaps the result of my insufficient knowledge of implicit coercion that I can't imagine a practical cases for it to not only useful, but also pleasing to use. And again, this is why I'm reading *You Don't Know JS* for this exact reason. Will my view of implicit coercion (and many other JavaScript peculiarities) be changed at the end of it? We will see.

---
## References

[[You Don't Know JS - Kyle Simpson]]