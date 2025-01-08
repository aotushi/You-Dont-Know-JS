# You Don't Know JS Yet: Get Started - 2nd Edition
# Chapter 3: Digging to the Roots of JS

If you've read Chapters 1 and 2, and taken the time to digest and percolate, you're hopefully starting to *get* JS a little more. If you skipped/skimmed them (especially Chapter 2), I recommend going back to spend some more time with that material.
如果你已经读完了章节1和章节2,并且花时间消化和过滤, 那幺你希望你开始更多地了解一下 JS.如果你跳过/略过他们(特别是章节2), 我推荐你回去花时间了解细节.

In Chapter 2, we surveyed syntax, patterns, and behaviors at a high level. In this chapter, our attention shifts to some of the lower-level root characteristics of JS that underpin virtually every line of code we write.
在章节2中, 我们高标准的调查了语法,范式和行为.在本章节中,我们的注意力转移到更低尺度的JS的根角色上, 其实际上支撑我们写的每行代码.

Be aware: this chapter digs much deeper than you're likely used to thinking about a programming language. My goal is to help you appreciate the core of how JS works, what makes it tick. This chapter should begin to answer some of the "Why?" questions that may be cropping up as you explore JS. However, this material is still not an exhaustive exposition of the language; that's what the rest of the book series is for! Our goal here is still just to *get started*, and become more comfortable with, the *feel* of JS, how it ebbs and flows.
请注意：本章的深入探讨可能比您习惯的编程语言要深入得多。我的目标是帮助你觉察JS工作的核心, 是什么让他运转起来的.本章节应该开始回答一些当你探索JS时候涌现的'为什么'的问题. 然而, 这份材料仍然不是对这种语言的详尽阐述; 那是这本书接下来的系列.我们的目标仍然只是 *开始*，并更加适应 JS 的 *感觉* ，以及它是如何起伏的。

Don't run so quickly through this material that you get lost in the weeds. As I've said a dozen times already, **take your time**. Even still, you'll probably finish this chapter with remaining questions. That's OK, because there's a whole book series ahead of you to keep exploring!
不要快速浏览这份资料,否则你迷失. 正如我已经说过十几次的，**慢慢来**。即便如此，您仍可能会带着剩余的问题结束本章。没关系，因为有一整本书系列等着你继续探索！

## Iteration迭代

Since programs are essentially built to process data (and make decisions on that data), the patterns used to step through the data have a big impact on the program's readability.
由于程序本质上是为处理数据（并根据该数据做出决策）而构建的，因此用于逐步遍历数据的模式对程序的可读性有很大影响。

The iterator pattern has been around for decades, and suggests a "standardized" approach to consuming data from a source one *chunk* at a time. The idea is that it's more common and helpful to iterate the data source—to progressively handle the collection of data by processing the first part, then the next, and so on, rather than handling the entire set all at once.
迭代器模式已经存在了几十年, 且提议为每次从源*块*消费数据的"标准"方法. 其思想是, 迭代数据源更普遍更有帮助-通过处理第一部分,然后下一个部分,以此类推, 而不是一次处理整个数据的逐步处理数据集合的方式.


Imagine a data structure that represents a relational database `SELECT` query, which typically organizes the results as rows. If this query had only one or a couple of rows, you could handle the entire result set at once, and assign each row to a local variable, and perform whatever operations on that data that were appropriate.
想象表示关系型数据库`SELECT`查询的数据解构, 通常将结果组织为行. 如果查询结果只有一行或几行, 你能一次性处理整个结果集合, 声明每行为一个本地变量, 在数据上执行任何适当的操作.

But if the query has 100 or 1,000 (or more!) rows, you'll need iterative processing to deal with this data (typically, a loop).
但是如果查询100或1000(甚至更多)行,你将需要迭代处理来进行数据处理(特别是循环).

The iterator pattern defines a data structure called an "iterator" that has a reference to an underlying data source (like the query result rows), which exposes a method like `next()`. Calling `next()` returns the next piece of data (i.e., a "record" or "row" from a database query).
迭代器模式定义称作'迭代器'的数据结构,其对底层数据源(例如查询结构行)有一个引用,暴露一个像`next()`的方法. 调用`next()`返回数据的下一段(例如, 来自数据库查询的'record'或'row').

You don't always know how many pieces of data that you will need to iterate through, so the pattern typically indicates completion by some special value or exception once you iterate through the entire set and *go past the end*.
你并不总是知道你需要迭代多少块数据,所以一旦你迭代完整个集合并且*走过终点*的话,迭代器模式通常使用特殊的值或例外值来特别表示完成.

The importance of the iterator pattern is in adhering to a *standard* way of processing data iteratively, which creates cleaner and easier to understand code, as opposed to having every data structure/source define its own custom way of handling its data.
迭代器模式的重要之处是遵从了迭代处理数据的*标准*方式,其创建了理解代码的简单和简介,与每个数据结构/数据源定义它自定义处理数据的方式相反.

After many years of various JS community efforts around mutually agreed-upon iteration techniques, ES6 standardized a specific protocol for the iterator pattern directly in the language. The protocol defines a `next()` method whose return is an object called an *iterator result*; the object has `value` and `done` properties, where `done` is a boolean that is `false` until the iteration over the underlying data source is complete.
经过多年不同的JS社区围绕勾心斗角的迭代技术的努力, ES6直接在语言中为迭代器模式标准化了一个特定的协议. 协议定义了一个`next()`方法,其返回其是一个称作*迭代结果*的对象; 这个对象具有`value`和`done`属性, `done`是一个布尔值,在底层数据源迭代完成之前, 它是'false'.

### Consuming Iterators

With the ES6 iteration protocol in place, it's workable to consume a data source one value at a time, checking after each `next()` call for `done` to be `true` to stop the iteration. But this approach is rather manual, so ES6 also included several mechanisms (syntax and APIs) for standardized consumption of these iterators.
使用ES6迭代器协议, 就可以一次使用数据源的一个值, 每次`next()`调用之后,`done`如果为`true`就停止迭代. 但是这个方案是更手动的, 所以ES6也包含了几种机制(语法和APIs)来标准化迭代器的使用.

One such mechanism is the `for..of` loop:
一个类似的机制是`for...of`循环:

```js
// given an iterator of some data source:
var it = /* .. */;

// loop over its results one at a time
for (let val of it) {
    console.log(`Iterator value: ${ val }`);
}
// Iterator value: ..
// Iterator value: ..
// ..
```

| NOTE: |
| :--- |
| We'll omit the manual loop equivalent here, but it's definitely less readable than the `for..of` loop! 
我们在这里忽略等效的manual loop等效项, 但它肯定比`for...of`缺少可读性.

Another mechanism that's often used for consuming iterators is the `...` operator. This operator actually has two symmetrical forms: *spread* and *rest* (or *gather*, as I prefer). The *spread* form is an iterator-consumer.
另一个经常用来消费迭代器的机制是`...`操作符. 这个操作符实际上有两个对称的形式: *spread扩展*和*剩余rest*(或是*收集gather*, 我更喜欢这个). *扩展*形式是迭代器消费者(iterator-consumer).

To *spread* an iterator, you have to have *something* to spread it into. There are two possibilities in JS: an array or an argument list for a function call.
要*扩展*一个迭代器, 你必须有*东西*才能扩展它. 在JS中有两个可能: 数组或函数调用的参数列表.

An array spread:
数组扩展:

```js
// spread an iterator into an array,
// with each iterated value occupying
// an array element position.
var vals = [ ...it ];
```

A function call spread:

```js
// spread an iterator into a function,
// call with each iterated value
// occupying an argument position.
doSomethingUseful( ...it );
```

In both cases, the iterator-spread form of `...` follows the iterator-consumption protocol (the same as the `for..of` loop) to retrieve all available values from an iterator and place (aka, spread) them into the receiving context (array, argument list).
在两个案例中, 迭代器-扩展形式`...`遵循迭代器-消费(iterator-consumption)协议(和`for...of`循环相同)来从一个迭代器中检索所有可用值并且安置(又名,扩展)他们到接收的上下文中(数组, 参数列表).

### Iterables迭代对象

The iterator-consumption protocol is technically defined for consuming *iterables*; an iterable is a value that can be iterated over.
迭代器-消费协议为消费*迭代对象(iterables)*定义的; 一个迭代对象是可以迭代的值.

The protocol automatically creates an iterator instance from an iterable, and consumes *just that iterator instance* to its completion. This means a single iterable could be consumed more than once; each time, a new iterator instance would be created and used.
迭代器-消费协议从一个迭代对象中自动创建了一个迭代器示例, 消费*迭代器实例*直到完成. 这意味着一个单独的迭代对象可以被消费多次; 每一次, 一个新的迭代器实例将会被创建并使用.

So where do we find iterables?
所以我们从哪里找到迭代对象?

ES6 defined the basic data structure/collection types in JS as iterables. This includes strings, arrays, maps, sets, and others.
ES6在JS中定义基本的数据结构/集合类型作为迭代对象. 这包括字符串, 数组, 映射, 集合和其它.

Consider:

```js
// an array is an iterable
var arr = [ 10, 20, 30 ];

for (let val of arr) {
    console.log(`Array value: ${ val }`);
}
// Array value: 10
// Array value: 20
// Array value: 30
```

Since arrays are iterables, we can shallow-copy an array using iterator consumption via the `...` spread operator:
既然数组是迭代对象, 我们可以通过`...`扩展运算符使用迭代器消费来浅拷贝数组:

```js
var arrCopy = [ ...arr ];
```

We can also iterate the characters in a string one at a time:

我们也可以在字符串中一次性迭代字符: 
```js
var greeting = "Hello world!";
var chars = [ ...greeting ];

chars;
// [ "H", "e", "l", "l", "o", " ",
//   "w", "o", "r", "l", "d", "!" ]
```

A `Map` data structure uses objects as keys, associating a value (of any type) with that object. Maps have a different default iteration than seen here, in that the iteration is not just over the map's values but instead its *entries*. An *entry* is a tuple (2-element array) including both a key and a value.
`Map`数据结构使用对象作为keys,将值与该对象关联. Maps的默认迭代与此处不同, 迭代的不仅仅是map的值,而是其'entries'. 一个*entry*是一个元组(2元数组),包含键和值.

Consider:

```js
// given two DOM elements, `btn1` and `btn2`

var buttonNames = new Map();
buttonNames.set(btn1,"Button 1");
buttonNames.set(btn2,"Button 2");

for (let [btn,btnName] of buttonNames) {
    btn.addEventListener("click",function onClick(){
        console.log(`Clicked ${ btnName }`);
    });
}
```

In the `for..of` loop over the default map iteration, we use the `[btn,btnName]` syntax (called "array destructuring") to break down each consumed tuple into the respective key/value pairs (`btn1` / `"Button 1"` and `btn2` / `"Button 2"`).
`for...of`循环了默认map的迭代, 我们用`[btn, btnName]`语法(称作"数组解构")来分解每个消费的元素为各自的key/value对(`btn1` / `"Button 1"` and `btn2` / `"Button 2"`).

Each of the built-in iterables in JS expose a default iteration, one which likely matches your intuition. But you can also choose a more specific iteration if necessary. For example, if we want to consume only the values of the above `buttonNames` map, we can call `values()` to get a values-only iterator:
在JS中每个内建的迭代对象暴露了一个默认的迭代, 一个可能契合你意图的东西.但如果需要的话你可以选择一个更具体的迭代.例如, 如果我们想只消费上面`buttonNames`映射的值的话, 我们可以调用`values
()`来获取只有值的迭代器.

```js
for (let btnName of buttonNames.values()) {
    console.log(btnName);
}
// Button 1
// Button 2
```

Or if we want the index *and* value in an array iteration, we can make an entries iterator with the `entries()` method:
或者如果我们想要索引*和*值在一个数组的迭代中, 我们可以用`entries()`方法来生成一个entries迭代器.

```js
var arr = [ 10, 20, 30 ];

for (let [idx,val] of arr.entries()) {
    console.log(`[${ idx }]: ${ val }`);
}
// [0]: 10
// [1]: 20
// [2]: 30
```

For the most part, all built-in iterables in JS have three iterator forms available: keys-only (`keys()`), values-only (`values()`), and entries (`entries()`).
最重要的是, 在JS中所有内建的迭代对象具有3个可用的迭代形式: keys-only(`keys()`), values-only(`values()`), 和entries(`entries()`).

Beyond just using built-in iterables, you can also ensure your own data structures adhere to the iteration protocol; doing so means you opt into the ability to consume your data with `for..of` loops and the `...` operator. "Standardizing" on this protocol means code that is overall more readily recognizable and readable.
除了使用内建的迭代对象外, 你也能确保你自己的数据解构遵循迭代器协议; 这么做意味着你选择使用`for...of`循环和`...`操作符消费你数据的能力. '协议上的标准化(Standardizing)'意味着代码整体上更容易识别和可读.

| NOTE: |
| :--- |
| You may have noticed a nuanced shift that occurred in this discussion. We started by talking about consuming **iterators**, but then switched to talking about iterating over **iterables**. The iteration-consumption protocol expects an *iterable*, but the reason we can provide a direct *iterator* is that an iterator is just an iterable of itself! When creating an iterator instance from an existing iterator, the iterator itself is returned. 
你可能注意到了在讨论中的细微变化. 我们从讨论消费**迭代器**开始, 但是之后跳到了讨论迭代**迭代对象**. 迭代-消费协议期待一个*迭代对象*, 但是我们可以提供一个直接*迭代器*的原因是一个迭代器就是迭代对象自身! 当现有的迭代器上创建迭代器实例时, 返回的迭代器本身.
|

## Closure闭包

Perhaps without realizing it, almost every JS developer has made use of closure. In fact, closure is one of the most pervasive programming functionalities across a majority of languages. It might even be as important to understand as variables or loops; that's how fundamental it is.
可能不相信, 几乎每个JS开发人员都使用过闭包. 事实上, 闭包是大多数语言中最普遍的编程功能之一.它甚至可能和理解边喝或循环一样重要; 它是非常基础的的.

Yet it feels kind of hidden, almost magical. And it's often talked about in either very abstract or very informal terms, which does little to help us nail down exactly what it is.
感觉闭包有点隐蔽,近乎魔术. 在抽象或正式的术语中它经常被谈论, 其帮助我们明确它具体是什么有那么点帮助.

We need to be able to recognize where closure is used in programs, as the presence or lack of closure is sometimes the cause of bugs (or even the cause of performance issues).
我们需要有能力认识到在程序中闭包在什么地方使用, 闭包的出现或缺少有时是bugs的起因(或者说, 性能问题的原因).

So let's define closure in a pragmatic and concrete way:
所以我们以务实和精确的方式来定义闭包:

> Closure is when a function remembers and continues to access variables from outside its scope, even when the function is executed in a different scope.
闭包是当一个函数记住并能持续访问其外部作用域的变量, 即使该函数在不同的作用域下执行完.

We see two definitional characteristics here. First, closure is part of the nature of a function. Objects don't get closures, functions do. Second, to observe a closure, you must execute a function in a different scope than where that function was originally defined.

Consider:

```js
function greeting(msg) {
    return function who(name) {
        console.log(`${ msg }, ${ name }!`);
    };
}

var hello = greeting("Hello");
var howdy = greeting("Howdy");

hello("Kyle");
// Hello, Kyle!

hello("Sarah");
// Hello, Sarah!

howdy("Grant");
// Howdy, Grant!
```

First, the `greeting(..)` outer function is executed, creating an instance of the inner function `who(..)`; that function closes over the variable `msg`, which is the parameter from the outer scope of `greeting(..)`. When that inner function is returned, its reference is assigned to the `hello` variable in the outer scope. Then we call `greeting(..)` a second time, creating a new inner function instance, with a new closure over a new `msg`, and return that reference to be assigned to `howdy`.

When the `greeting(..)` function finishes running, normally we would expect all of its variables to be garbage collected (removed from memory). We'd expect each `msg` to go away, but they don't. The reason is closure. Since the inner function instances are still alive (assigned to `hello` and `howdy`, respectively), their closures are still preserving the `msg` variables.

These closures are not a snapshot of the `msg` variable's value; they are a direct link and preservation of the variable itself. That means closure can actually observe (or make!) updates to these variables over time.

```js
function counter(step = 1) {
    var count = 0;
    return function increaseCount(){
        count = count + step;
        return count;
    };
}

var incBy1 = counter(1);
var incBy3 = counter(3);

incBy1();       // 1
incBy1();       // 2

incBy3();       // 3
incBy3();       // 6
incBy3();       // 9
```

Each instance of the inner `increaseCount()` function is closed over both the `count` and `step` variables from its outer `counter(..)` function's scope. `step` remains the same over time, but `count` is updated on each invocation of that inner function. Since closure is over the variables and not just snapshots of the values, these updates are preserved.

Closure is most common when working with asynchronous code, such as with callbacks. Consider:

```js
function getSomeData(url) {
    ajax(url,function onResponse(resp){
        console.log(
            `Response (from ${ url }): ${ resp }`
        );
    });
}

getSomeData("https://some.url/wherever");
// Response (from https://some.url/wherever): ...
```

The inner function `onResponse(..)` is closed over `url`, and thus preserves and remembers it until the Ajax call returns and executes `onResponse(..)`. Even though `getSomeData(..)` finishes right away, the `url` parameter variable is kept alive in the closure for as long as needed.

It's not necessary that the outer scope be a function—it usually is, but not always—just that there be at least one variable in an outer scope accessed from an inner function:

```js
for (let [idx,btn] of buttons.entries()) {
    btn.addEventListener("click",function onClick(){
       console.log(`Clicked on button (${ idx })!`);
    });
}
```

Because this loop is using `let` declarations, each iteration gets new block-scoped (aka, local) `idx` and `btn` variables;  the loop also creates a new inner `onClick(..)` function each time. That inner function closes over `idx`, preserving it for as long as the click handler is set on the `btn`. So when each button is clicked, its handler can print its associated index value, because the handler remembers its respective `idx` variable.

Remember: this closure is not over the value (like `1` or `3`), but over the variable `idx` itself.

Closure is one of the most prevalent and important programming patterns in any language. But that's especially true of JS; it's hard to imagine doing anything useful without leveraging closure in one way or another.

If you're still feeling unclear or shaky about closure, the majority of Book 2, *Scope & Closures* is focused on the topic.

## `this` Keyword

One of JS's most powerful mechanisms is also one of its most misunderstood: the `this` keyword. One common misconception is that a function's `this` refers to the function itself. Because of how `this` works in other languages, another misconception is that `this` points the instance that a method belongs to. Both are incorrect.

As discussed previously, when a function is defined, it is *attached* to its enclosing scope via closure. Scope is the set of rules that controls how references to variables are resolved.

But functions also have another characteristic besides their scope that influences what they can access. This characteristic is best described as an *execution context*, and it's exposed to the function via its `this` keyword.

Scope is static and contains a fixed set of variables available at the moment and location you define a function, but a function's execution *context* is dynamic, entirely dependent on **how it is called** (regardless of where it is defined or even called from).

`this` is not a fixed characteristic of a function based on the function's definition, but rather a dynamic characteristic that's determined each time the function is called.

One way to think about the *execution context* is that it's a tangible object whose properties are made available to a function while it executes. Compare that to scope, which can also be thought of as an *object*; except, the *scope object* is hidden inside the JS engine, it's always the same for that function, and its *properties* take the form of identifier variables available inside the function.

```js
function classroom(teacher) {
    return function study() {
        console.log(
            `${ teacher } says to study ${ this.topic }`
        );
    };
}
var assignment = classroom("Kyle");
```

The outer `classroom(..)` function makes no reference to a `this` keyword, so it's just like any other function we've seen so far. But the inner `study()` function does reference `this`, which makes it a `this`-aware function. In other words, it's a function that is dependent on its *execution context*.

| NOTE: |
| :--- |
| `study()` is also closed over the `teacher` variable from its outer scope. |

The inner `study()` function returned by `classroom("Kyle")` is assigned to a variable called `assignment`. So how can `assignment()` (aka `study()`) be called?

```js
assignment();
// Kyle says to study undefined  -- Oops :(
```

In this snippet, we call `assignment()` as a plain, normal function, without providing it any *execution context*.

Since this program is not in strict mode (see Chapter 1, "Strictly Speaking"), context-aware functions that are called **without any context specified** default the context to the global object (`window` in the browser). As there is no global variable named `topic` (and thus no such property on the global object), `this.topic` resolves to `undefined`.

Now consider:

```js
var homework = {
    topic: "JS",
    assignment: assignment
};

homework.assignment();
// Kyle says to study JS
```

A copy of the `assignment` function reference is set as a property on the `homework` object, and then it's called as `homework.assignment()`. That means the `this` for that function call will be the `homework` object. Hence, `this.topic` resolves to `"JS"`.

Lastly:

```js
var otherHomework = {
    topic: "Math"
};

assignment.call(otherHomework);
// Kyle says to study Math
```

A third way to invoke a function is with the `call(..)` method, which takes an object (`otherHomework` here) to use for setting the `this` reference for the function call. The property reference `this.topic` resolves to `"Math"`.

The same context-aware function invoked three different ways, gives different answers each time for what object `this` will reference.

The benefit of `this`-aware functions—and their dynamic context—is the ability to more flexibly re-use a single function with data from different objects. A function that closes over a scope can never reference a different scope or set of variables. But a function that has dynamic `this` context awareness can be quite helpful for certain tasks.

## Prototypes

Where `this` is a characteristic of function execution, a prototype is a characteristic of an object, and specifically resolution of a property access.

Think about a prototype as a linkage between two objects; the linkage is hidden behind the scenes, though there are ways to expose and observe it. This prototype linkage occurs when an object is created; it's linked to another object that already exists.

A series of objects linked together via prototypes is called the "prototype chain."

The purpose of this prototype linkage (i.e., from an object B to another object A) is so that accesses against B for properties/methods that B does not have, are *delegated* to A to handle. Delegation of property/method access allows two (or more!) objects to cooperate with each other to perform a task.

Consider defining an object as a normal literal:

```js
var homework = {
    topic: "JS"
};
```

The `homework` object only has a single property on it: `topic`. However, its default prototype linkage connects to the `Object.prototype` object, which has common built-in methods on it like `toString()` and `valueOf()`, among others.

We can observe this prototype linkage *delegation* from `homework` to `Object.prototype`:

```js
homework.toString();    // [object Object]
```

`homework.toString()` works even though `homework` doesn't have a `toString()` method defined; the delegation invokes `Object.prototype.toString()` instead.

### Object Linkage

To define an object prototype linkage, you can create the object using the `Object.create(..)` utility:

```js
var homework = {
    topic: "JS"
};

var otherHomework = Object.create(homework);

otherHomework.topic;   // "JS"
```

The first argument to `Object.create(..)` specifies an object to link the newly created object to, and then returns the newly created (and linked!) object.

Figure 4 shows how the three objects (`otherHomework`, `homework`, and `Object.prototype`) are linked in a prototype chain:

<figure>
    <img src="images/fig4.png" width="200" alt="Prototype chain with 3 objects" align="center">
    <figcaption><em>Fig. 4: Objects in a prototype chain</em></figcaption>
    <br><br>
</figure>

Delegation through the prototype chain only applies for accesses to lookup the value in a property. If you assign to a property of an object, that will apply directly to the object regardless of where that object is prototype linked to.

| TIP: |
| :--- |
| `Object.create(null)` creates an object that is not prototype linked anywhere, so it's purely just a standalone object; in some circumstances, that may be preferable. |

Consider:

```js
homework.topic;
// "JS"

otherHomework.topic;
// "JS"

otherHomework.topic = "Math";
otherHomework.topic;
// "Math"

homework.topic;
// "JS" -- not "Math"
```

The assignment to `topic` creates a property of that name directly on `otherHomework`; there's no effect on the `topic` property on `homework`. The next statement then accesses `otherHomework.topic`, and we see the non-delegated answer from that new property: `"Math"`.

Figure 5 shows the objects/properties after the assignment that creates the `otherHomework.topic` property:

<figure>
    <img src="images/fig5.png" width="200" alt="3 objects linked, with shadowed property" align="center">
    <figcaption><em>Fig. 5: Shadowed property 'topic'</em></figcaption>
    <br><br>
</figure>

The `topic` on `otherHomework` is "shadowing" the property of the same name on the `homework` object in the chain.

| NOTE: |
| :--- |
| Another frankly more convoluted but perhaps still more common way of creating an object with a prototype linkage is using the "prototypal class" pattern, from before `class` (see Chapter 2, "Classes") was added in ES6. We'll cover this topic in more detail in Appendix A, "Prototypal 'Classes'". |

### `this` Revisited

We covered the `this` keyword earlier, but its true importance shines when considering how it powers prototype-delegated function calls. Indeed, one of the main reasons `this` supports dynamic context based on how the function is called is so that method calls on objects which delegate through the prototype chain still maintain the expected `this`.

Consider:

```js
var homework = {
    study() {
        console.log(`Please study ${ this.topic }`);
    }
};

var jsHomework = Object.create(homework);
jsHomework.topic = "JS";
jsHomework.study();
// Please study JS

var mathHomework = Object.create(homework);
mathHomework.topic = "Math";
mathHomework.study();
// Please study Math
```

The two objects `jsHomework` and `mathHomework` each prototype link to the single `homework` object, which has the `study()` function. `jsHomework` and `mathHomework` are each given their own `topic` property (see Figure 6).

<figure>
    <img src="images/fig6.png" width="495" alt="4 objects prototype linked" align="center">
    <figcaption><em>Fig. 6: Two objects linked to a common parent</em></figcaption>
    <br><br>
</figure>

`jsHomework.study()` delegates to `homework.study()`, but its `this` (`this.topic`) for that execution resolves to `jsHomework` because of how the function is called, so `this.topic` is `"JS"`. Similarly for `mathHomework.study()` delegating to `homework.study()` but still resolving `this` to `mathHomework`, and thus `this.topic` as `"Math"`.

The preceding code snippet would be far less useful if `this` was resolved to `homework`. Yet, in many other languages, it would seem `this` would be `homework` because the `study()` method is indeed defined on `homework`.

Unlike many other languages, JS's `this` being dynamic is a critical component of allowing prototype delegation, and indeed `class`, to work as expected!

## Asking "Why?"

The intended take-away from this chapter is that there's a lot more to JS under the hood than is obvious from glancing at the surface.

As you are *getting started* learning and knowing JS more closely, one of the most important skills you can practice and bolster is curiosity, and the art of asking "Why?" when you encounter something in the language.

Even though this chapter has gone quite deep on some of the topics, many details have still been entirely skimmed over. There's much more to learn here, and the path to that starts with you asking the *right* questions of your code. Asking the right questions is a critical skill of becoming a better developer.

In the final chapter of this book, we're going to briefly look at how JS is divided, as covered across the rest of the *You Don't Know JS Yet* book series. Also, don't skip Appendix B of this book, which has some practice code to review some of the main topics covered in this book.
