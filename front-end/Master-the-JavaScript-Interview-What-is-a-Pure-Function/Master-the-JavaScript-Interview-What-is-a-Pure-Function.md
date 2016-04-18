---
layout:		post
title:		'Master the JavaScript Interview: What is a Pure Function?'
excerpt:	'Pure functions are essential for a variety of purposes, including functional programming, reliable concurrency, and React+Redux apps. But what does "pure function" mean?'
categories:	['JavaScript', 'translation']
tags:		['Functional', 'ProgrammingJavaScript']
---

### Master the JavaScript Interview: What is a Pure Function?

![Image: Pure — carnagenyc (CC-BY-NC 2.0)](./img/1.jpeg)

Pure functions are essential for a variety of purposes, including functional programming, reliable concurrency, and React+Redux apps. But what does "pure function" mean?

We're going to answer this question with a free lesson from "[Learn JavaScript with Eric Elliott](http://ericelliottjs.com/product/lifetime-access-pass/)":

[Video Placeholder](https://player.vimeo.com/video/160326750)

Before we can tackle what a pure function is, it's probably a good idea to take a closer look at functions. There may be a different way to look at them that will make functional programming easier to understand.

#### What is a Function?

A **function** is a process which takes some input, called **arguments**, and produces some output called a **return value**. Functions may serve the following purposes:

- **Mapping:** Produce some output based on given inputs. A function maps input values to output values.
- **Procedures:** A function may be called to perform a sequence of steps. The sequence is known as a procedure, and programming in this style is known as **procedural programming**.
- **I/O:** Some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network.

#### Mapping
#### 映射

Pure functions are all about mapping. Functions map input arguments to return values, meaning that for each set of inputs, there exists an output. A function will take the inputs and return the corresponding output.

纯函数都是关于映射的。函数映射指的是输入参数会返回新的值，这意味着对于每一组输入的参数，都有对应的输出。一个函数接收输入并返回相应的输出。

`Math.max()` takes numbers as arguments and returns the largest number:

`Math.max()` 函数接收数字作为参数并返回一个最大的数字：

```
Math.max(2, 8, 5); // 8
```

In this example, 2, 8, & 5 are arguments. They're values passed into the function.

在这个例子中，2、8 和 5 都是参数。他们是被传入函数的值。

`Math.max()` is a function that takes any number of arguments and returns the largest argument value. In this case, the largest number we passed in was 8, and that's the number that got returned.

`Math.max()` 函数接收任意数字作为参数并返回一个最大的数字。这个例子中，我们传入的最大数字是 8，也就是函数返回的那个数字。

Functions are really important in computing and math. They help us process data in useful ways. Good programmers give functions descriptive names so that when we see the code, we can see the function names and understand what the function does.

函数在计算和数学中都非常重要。它们以一种更有效的方式来帮助我们来处理数据。优秀的程序员会给函数取一个有意义的名字，这样我们看到函数名的时候就可以知道这个函数的作用是什么了。

Math has functions, too, and they work a lot like functions in JavaScript. You've probably seen functions in algebra. They look something like this:

数学中也有函数，它们的工作原理和 JavaScript 中的函数很像。你可能在代数学中看过函数。他们看起来像下面的例子一样：

f(x) = 2x

Which means that we're declaring a function called f and it takes an argument called x and multiplies x by 2.

这意思是我们声明了一个叫 `f` 的函数同时接收了一个叫 `x` 的参数并且返回的值是 `x` 乘以 2。

To use this function, we simply provide a value for x:

要使用这个函数，我们可以简单的船体一个值给 `x`：

f(2)

In algebra, this means exactly the same thing as writing:

在代数学中，这意味着完全等价于下面写的值：

4

So any place you see f(2) you can substitute 4.

所以你在任何地方看到 `f(2)` 你都可以用 4 来代替。

Now let's convert that function to JavaScript:

现在让我们回到 JavaScript 中的函数：

```
const double = x => x * 2;
```

You can examine the function's output using `console.log()`:

你可以用 `console.log()` 来查看函数的输出：

```
console.log( double(5) ); // 10
```

Remember when I said that in math functions, you could replace `f(2)` with `4`? In this case, the JavaScript engine replaces `double(5)` with the answer, `10`.

记住，当我说数学中的函数时，你可以用 `f(2)` 来代替 4。在这种情况下，JavaScript 引擎会把 `double(5)` 替代成 10。

So, `console.log( double(5) );` is the same as `console.log(10);`

所以，`console.log( double(5) );` 等价于  `console.log(10);`。

This is true because `double()` is a pure function, but if `double()` had side-effects, such as saving the value to disk or logging to the console, you couldn't simply replace `double(5)` with 10 without changing the meaning.

这样是正确的，因为 `double()` 是一个纯函数，但是如果 `double()` 有副作用，比如该函数把值保存到了磁盘或输出到了控制台，你不可以在没有改变含义的情况下简单地把 `double(5)` 替换成 10。

If you want referential transparency, you need to use pure functions.

*如果你想透明地引用，你需要使用纯函数。*

#### Pure Functions
#### 纯函数

A **pure function** is a function which:

**纯函数**的特点：

- Given the same input, will always return the same output.
- Produces no side effects.
- Relies on no external state.

- 对于给定相同的输入，总是返回相同的输出。
- 不会产生副作用。
- 不依赖于外部状态。

I recommend that you favor pure functions. Meaning, if it is practical to implement a program requirement using pure functions, you should use them over other options. Pure functions take some input and return some output based on that input. They are the simplest reusable building blocks of code in a program. Perhaps the most important design principle in computer science is KISS (Keep It Simple, Stupid). I prefer Keep It Stupid Simple. Pure functions are stupid simple in the best possible way.

我推荐你使用纯函数。如果用纯函数实现一个程序的需求是可行的，你应该优先使用它们。纯函数接收参数并返回参数。他们是程序中最简单的可复用代码块。KISS(Keep It Simple, Stupid) 原则可能是计算机科学中最重要的设计原则。纯函数保持简单直白就是最好的方式。

Pure functions have many beneficial properties, and form the foundation of **functional programming**. Pure functions are completely independent of outside state, and as such, they are immune to entire classes of bugs that have to do with shared mutable state. Their independent nature also makes them great candidates for parallel processing across many CPUs, and across entire distributed computing clusters, which makes them essential for many types of scientific and resource-intensive computing tasks.

纯函数有许多有益的特性，并且也是**函数式编程**的基础。纯函数完全不依赖于外部状态，they are immune to entire classes of bugs that have to do with shared mutable state。

Pure functions are also extremely independent — easy to move around, refactor, and reorganize in your code, making your programs more flexible and adaptable to future changes.

纯函数同样是非常独立的，在你的代码中容易对其进行移动、重构和重组，使你的应用程序更灵活的适应未来的变化。

#### The Trouble with Shared State
#### 共享状态的问题

Several years ago I was working on an app that allowed users to search a database for musical artists and load the artist's music playlist into a web player. This was around the time Google Instant landed, which displays instant search results as you type your search query. AJAX-powered autocomplete was suddenly all the rage.

几年前我做过一款应用，该应该用允许用户从歌手的数据中搜索并且把歌手的歌单加载到网页播放器上。也就是大概在 Google Instant （当你键入搜索语句的时候会实时展示搜索的结果）推出的那段时间，基于 Ajax 的自动补齐功能突然间变得非常流行。

The only problem was that users often type faster than an API autocomplete search response can be returned, which caused some strange bugs. It would trigger race conditions, where newer suggestions would be replaced by outdated suggestions.

唯一的问题就是当用户打字的速度快于 API 自动补齐搜索响应的时候，会产生一些奇怪的 Bug。它会触发竞态条件，where newer suggestions would be replaced by outdated suggestions.

Why did that happen? Because each AJAX success handler was given access to directly update the suggestion list that was displayed to users. The slowest AJAX request would always win the user's attention by blindly replacing results, even when those replaced results may have been newer.

为什么会产生这些问题呢？因为每个 Ajax 处理器有权直接更新展示给用户看的建议列表。最慢的 Ajax 请求总是会盲目地替换结果引起用户的注意，即使这些结果是比较新的。

To fix the problem, I created a suggestion manager — a single source of truth to manage the state of the query suggestions. It was aware of a currently pending AJAX request, and when the user typed something new, the pending AJAX request would be canceled before a new request was issued, so only a single response handler at a time would ever be able to trigger a UI state update.

为了修复这个问题，我创建了一个建议管理器（单一可信来源）来管理查询建议的状态。它会注意到当前待定的 Ajax 请求，当用户键入新的语句时，待定的请求会在一个新的请求产生之前被取消掉，所以，在同一时间内只会有一个响应处理器来触发 UI 状态的更新。

Any sort of asynchronous operation or concurrency could cause similar race conditions. Race conditions happen if output is dependent on the sequence of uncontrollable events (such as network, device latency, user input, randomness, etc…). In fact, if you're using shared state and that state is reliant on sequences which vary depending on indeterministic factors, for all intents and purposes, the output is impossible to predict, and that means it's impossible to properly test or fully understand. As Martin Odersky (creator of Scala) puts it:

任何类型的异步或并发操作都会引起类似的竞态条件。如果输出依赖于不可控事件序列（例如网络、设备延迟、用户输入、随机性等等）会导致竞态条件。实际上，如果你正在使用共享状态并且该状态依赖sequences which vary depending on indeterministic factors，从所有的这些来看，输出是无法预测的，也就意味着不可能正确地测试和完全理解。

> non-determinism = parallel processing + mutable state

Program determinism is usually a desirable property in computing. Maybe you think you're OK because JS runs in a single thread, and as such, is immune to parallel processing concerns, but as the AJAX example demonstrates, a single threaded JS engine does not imply that there is no concurrency. On the contrary, there are many sources of concurrency in JavaScript. API I/O, event listeners, web workers, iframes, and timeouts can all introduce indeterminism into your program. Combine that with shared state, and you've got a recipe for bugs.

程序决定论在计算中通常是一个理想的性质。也许你觉得没有问题因为 JS 以单线程的方式运行的，

Pure functions can help you avoid those kinds of bugs.

纯函数可以帮你避免这些问题。

#### Given the Same Input, Always Return the Same Output

With our `double()` function, you can replace the function call with the result, and the program will mean the same thing — `double(5)` will always mean the same thing as `10` in your program, regardless of context, no matter how many times you call it or when.

But you can't say the same thing about all functions. Some functions rely on information other than the arguments you pass in to produce results.

Consider this example:

```
Math.random(); // => 0.4011148700956255
Math.random(); // => 0.8533405303023756
Math.random(); // => 0.3550692005082965
```

Even though we didn't pass any arguments into any of the function calls, they all produced different output, meaning that `Math.random()` is not pure.

`Math.random()` produces a new random number between 0 and 1 every time you run it, so clearly you couldn't just replace it with 0.4011148700956255 without changing the meaning of the program.

That would produce the same result every time. When we ask the computer for a random number, it usually means that we want a different result than we got the last time. What's the point of a pair of dice with the same numbers printed on every side?

Sometimes we have to ask the computer for the current time. We won't go into the details of how the time functions work. For now, just copy this code:

```
const time = () => new Date().toLocaleTimeString();

time(); // => "5:15:45 PM"
```

What would happen if you replaced the `time()` function call with the current time?

It would always say it's the same time: the time that the function call got replaced. In other words, it could only produce the correct output once per day, and only if you ran the program at the exact moment that the function got replaced.

So clearly, `time()` isn't like our `double()` function.

**A function is only pure if, given the same input, it will always produce the same output**. You may remember this rule from algebra class: the same input values will always map to the same output value. However, many input values may map to the same output value. For example, the following function **is pure**:

```
const highpass = (cutoff, value) => value >= cutoff;
```

The same input values will always map to the same output value:

```
highpass(5, 5); // => true
highpass(5, 5); // => true
highpass(5, 5); // => true
```

Many input values may map to the same output value:

```
highpass(5, 123);	// true
highpass(5, 6);		// true
highpass(5, 18);	// true

highpass(5, 1);		// false
highpass(5, 3);		// false
highpass(5, 4);		// false
```

### Pure Functions Produce No Side Effects

A pure function produces no side effects, which means that it can't alter any external state.

### Immutability

JavaScript arguments are passed by reference, which means that if a function were to mutate a property on an object or array parameter, that would mutate state that is accessible outside the function. Pure functions must not mutate external state.

Consider this mutating, **impure** `addToCart()` function:

```
// impure addToCart mutates existing cart
const addToCart = (cart, item, quantity) => {
	cart.items.push({
		item,
		quantity
	});
	return cart;
};


test('addToCart()', assert => {
	const msg = 'addToCart() should add a new item to the cart.';
	const originalCart = {
		items: []
	};
	const cart = addToCart(
		originalCart,
		{
			name: "Digital SLR Camera",
			price: '1495'
		},
		1
	);

	const expected = 1; // num items in cart
	const actual = cart.items.length;

	assert.equal(actual, expected, msg);

	assert.deepEqual(originalCart, cart, 'mutates original cart.');
	assert.end();
});
```

It works by passing in a cart, and item to add to that cart, and an item quantity. The function then returns the same cart, with the item added to it.

The problem with this is that we've just mutated some shared state. Other functions may be relying on that cart object state to be what it was before the function was called, and now that we've mutated that shared state, we have to worry about what impact it will have on the program logic if we change the order in which functions have been called. Refactoring the code could result in bugs popping up, which could screw up orders, and result in unhappy customers.

Now consider this version:

```
// Pure addToCart() returns a new cart
// It does not mutate the original.
const addToCart = (cart, item, quantity) => {
	const newCart = lodash.cloneDeep(cart);

	newCart.items.push({
		item,
		quantity
	});
	return newCart;
};


test('addToCart()', assert => {
	const msg = 'addToCart() should add a new item to the cart.';
	const originalCart = {
		items: []
	};

	// deep-freeze on npm
	// throws an error if original is mutated
	deepFreeze(originalCart);

	const cart = addToCart(
		originalCart,
		{
			name: "Digital SLR Camera",
			price: '1495'
		},
		1
	);


	const expected = 1; // num items in cart
	const actual = cart.items.length;

	assert.equal(actual, expected, msg);

	assert.notDeepEqual(originalCart, cart, 'should not mutate original cart.');
	assert.end();
});
```

In this example, we have an array nested in an object, which is why I reached for a deep clone. This is more complex state than you'll typically be dealing with. For most things, you can break it down into smaller chunks.

For example, Redux lets you compose reducers rather than deal with the entire app state inside each reducer. The result is that you don't have to create a deep clone of the entire app state every time you want to update just a small part of it. Instead, you can use non-destructive array methods, or `Object.assign()` to update a small part of the app state.

Your turn. [Fork this pen](http://codepen.io/ericelliott/pen/MyojLq?editors=0010) and change the impure functions into pure functions. Make the unit tests pass without changing the tests.

[Codepen Placeholder](https://codepen.io/ericelliott/embed/preview/MyojLq)

Did you enjoy the free lesson? Get lots more lessons like this one:

### [Learn JavaScript with Eric Elliott](http://ericelliottjs.com/product/lifetime-access-pass/)

**Eric Elliott** is the author of "Programming JavaScript Applications" (O'Reilly), and "Learn Universal JavaScript App Development with Node & React". He has contributed to software experiences for **Adobe Systems, Zumba Fitness, The Wall Street Journal, ESPN, BBC**, and top recording artists including **Usher, Frank Ocean, Metallica**, and many more.

He spends most of his time in the San Francisco Bay Area with the most beautiful woman in the world.

