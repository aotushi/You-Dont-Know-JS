# You Don't Know JS Yet: Get Started - 2nd Edition
# Chapter 2: Surveying JS
# Chapter 2: 总览JS

学习JS的最好方式就是开始写JS.

为了做到这一点,你需要知道这门语言如何工作,且知道我们应该将注意力集中到哪.即使你之前用其它语言编程,花点时间熟悉JS,确保每个章节都练习.

这一章不是JS语言语法的全面引用,也不打算做全面的"JS介绍"的入门书.

相反,我们仅仅了解一些这门语言的主要领域主题.我们的目标是对这门语言有一个更好的*感知*,所以我们可以提前写程序. 在您阅读本书的其余部分和本系列的其余部分时，我们将依次更详细地回顾其中的许多主题。

请不要把这一章节当作一个快速入门. 其内容较多,慢慢来.

| TIP: |
| :--- |
|我建议你预留足够的额外时间来阅读这一章。阅读每一部分，思考和探索主题一段时间。浏览现有的JS程序，并将其中的内容与本文提供的代码和解释（以及观点！）进行比较。在对JS的本质有了坚实的基础后，您将从本书和系列的其余部分中获得更多。|

## 每个文件都是一个程序

你用的绝大多数网站(网页应用)是由很多不同的JS文件(通常使用 .js 扩展)构成. 人们很容易把整个东西（应用程序）看作一个程序。但是JS有不同的看法。

在JS中, 每个独立的文件都是JS的独立程序.

这很重要的原因主要是关于错误处理. 因为JS把文件视作程序, 一个文件可能失败(在解析/编译或执行阶段)不一定会阻止后续文件的处理.明显看来, 如果你的应用依赖5个.js文件,且其中一个失败了, 应用整体可能只有部分执行,最乐观的情况下.确保每个文件工作正常是非常重要的,并且在任何可能的范围内，尽可能优雅地处理其他文件中的故障。

将独立的.js文件当作独立的JS程序可能会让你很惊讶. 从你使用应用的角度来说,它的确像一个大一点的程序. 那是因为应用的执行允许这些独立的*程序*合并和作为单独一个程序运行.

| NOTE: |
| :--- |
| 很多项目使用构建处理工具来,最终将项目各独立文件合并和一个文件,交付给web页面.当发生这种情况时, JS将这个单独的组合文件视为整个程序。|

多个单独的.js文件作为一个独立程序运行的唯一方式是通过'global scope'共享它们的状态(和访问它们公共的功能). 它们在全局作用域空间中混杂在一起,所以在运行时,它们作为整体运行.

从ES6以来,除了典型的独立JS程序格式,JS也支持模块格式. 模块也是基于文件的.如果一个文件通过模块加载机制进行加载,例如一个`import`语句或`<script type=module>`标签, 那它的代码会被当作独立模块对待.

尽管您通常不会将模块（状态和公开的方法来操作该状态的方法的集合）视为一个独立的进程, JS事实上仍然独立对待每个模块. 和'global scope'如何允许独立文件在运行时混入在一起一样, 引入另一个模块到另一个,也运行在它们之间运行时的互操作.

无论文件(独立的还是模块的)使用哪种代码组织模式(和加载机制), 你应该依旧认为每个文件作为它自己的(迷你)程序,可能之后和其它(迷你)程序合作来执行你整体应用的功能.

## Values(值)

程序中最基础的信息单元就是'值'. 值是数据.值是程序中维持状态的方式. 值在JS中有两种形式: 原始值(primitive)和对象(object)

值使用字面量(literals)嵌入到程序中:

```js
greeting("My name is Kyle.");
```

在此程序中,值`"My name is Kyle"`是原始字符串字面量(primitive string literal); 字符串(string)是有序的字符(characters)集合,通常用作标识单词或句子.

我用双引号`"`字符来分割(包围,分离,定义)字符串值.但是我也能使用单引号`'`. 引号的选择完全取决于风格. 重要的是,为了代码的可读性和可维护性,在程序中选择其中一种并一直使用它.

另一种分割(delimit)字符串字面量的方式是使用反引号`` ` ``字符. 然而,这种选择不仅仅是风格上的,还有行为上的不同. 考虑如下内容:


```js
console.log("My name is ${ firstName }.");
// My name is ${ firstName }.

console.log('My name is ${ firstName }.');
// My name is ${ firstName }.

console.log(`My name is ${ firstName }.`);
// My name is Kyle.
```

假设此程序已经定义一个`firstName`变量,其值为`"Kyle"`, 这`` ` ``- 分割字符串然后解析变量表达式(指的是`${...}`)为当前的值. 这被称作**插值(interpolation)**

反引号`` ` ``分割字符串可以在没有包含插值表达式的情况下使用,但是这破坏替代字符串字面量语法的目的:

```js
console.log(
    `Am I confusing you by omitting interpolation?`
);
// Am I confusing you by omitting interpolation?
```

对字符串使用`"`或`'`(再次强调,选择一种并坚持下去)更好的方式是,*除非你需要*插值; 只给哪些将会包含插值表达式的字符串保留`` ` ``.

除了字符串外, JS程序经常包含其它原始字面量(primitive literal values),例如布尔和数值:

```js
while (false) {
    console.log(3.141592);
}
```

`while`代表一个循环类型, *当(white)*它的条件是true的时候的重复操作的一种方式.

在这个例子中,循环将永远不会运行(也不会打印任何东西),因为我们使用`false`布尔值作为循环条件. `true`将会生成一个循环并且一直执行, 所以要注意.

数值`3.141592`,就像你了解的一样,是数学上圆周率前六位的近似值. 相比较程序中嵌入这样的值,你通常使用预定义的`Math.PI`来标识这个值.对数字的另一种变化是 bigint（大整数）原始类型，它用于存储任意大的数字。

数值(Numbers)是在程序中计算步骤最长使用的,例如循环迭代(loop iterations), 获取数字位置的信息(比如,数组索引).我们简单介绍以下数组/对象.例如,如果有一个数组称作`names`,我们可以在它第二个位置获取到元素,例如:

```js
console.log(`My name is ${ names[1] }.`);
// My name is Kyle.
```

我们使用`1`标识第二个位置的元素,而不是`2`,因为像大多数编程语言,JS数组索引是基于0的(`0`是第一个位置).

除了字符串strings, 数值numbers,和布尔值booleans, 在JS程序中另两个原始值是`null`和`undefined`. 然而在这两者之间有不同(一些历史和现在的原因),大大多数情况下这俩值都是标识值的*空*(或缺少).

很多开发者更愿意以这种方式一致地对待它们,也就是说,假设这个俩值是不可区分的.如果小心的话,这通常是可能的. 然而,最安全最好的使用方式是,只用`undefined`作为单个空值,即使`null`看起来更有吸引力,因为它的写起来更短.

```js
while (value != undefined) {
    console.log("Still got something!");
}
```

最后一个需要主要的原始值是symbol, 它是一个特殊用途的值,它的行为就像一个隐藏的不可猜测的值.Symbols几乎完全用作对象上的特殊键:

```js
hitchhikersGuide[ Symbol("meaning of life") ];
// 42
```

在典型的JS程序中,你不会经常遇到symbols的直接使用.它们绝大多数用在低代码(low-level code)中例如库和框架中.

### Arrays And Objects(数组和对象)

除了原始值primitives之外, 在JS中其它值类型是一个对象值.

像之前提到的, 数组是一个特殊类型的对象,其由有序的数字索引的数据列表组成:

```js
var names = [ "Frank", "Kyle", "Peter", "Susan" ];

names.length;
// 4

names[0];
// Frank

names[1];
// Kyle
```

JS数组可包含任意值类型,原始值或对象(包含其它数组). 正如我们将在第三章末尾看到的，即使函数也是可以保存在数组或对象中的值。

| NOTE: |
| :--- |
| 函数,例如数组,是对象的一种特殊类型(又名,子类型). 稍后我们将更详细的介绍函数.|

对象是更普遍的: 无需,不同值的键集合. 换句话说,你通过一个字符串位置名称(又名, '键(key)'或属性(property))访问元素,而不是通过它数字位置(类似数组). 例如:

```js
var me = {
    first: "Kyle",
    last: "Simpson",
    age: 39,
    specialties: [ "JS", "Table Tennis" ]
};

console.log(`My name is ${ me.first }.`);
```

`me`表示一个对象,`first`表示在对象(值集合)中位置信息的名字. 在一个对象中另一个访问信息的语法选项,是通过他自己的属性/键(property/key)来使用中括号, 例如`me["first"]`.

### Value Type Determination值类型检测

为了分辨值, `typeof`操作符告诉你值的内建类型,如果是原始值primitive, 否则是`"object"`:

```js
typeof 42;                  // "number"
typeof "abc";               // "string"
typeof true;                // "boolean"
typeof undefined;           // "undefined"
typeof null;                // "object" -- oops, bug!
typeof { "a": 1 };          // "object"
typeof [1,2,3];             // "object"
typeof function hello(){};  // "function"
```

| WARNING: |
| :--- |
| `typeof null`不幸地返回`"object"`而不是期待的`"null"`. 同样的, `typeof`为函数返回特定的`"function"`,但为数组不会返回期待中的`"array"`.|

转换一种值类型为另一种,例如从字符串到数值,在JS中指的是强制类型转换"coercion". 我们将在之后的章节更详细的介绍它.

原始值和对象值当分配或传递时,行为不同.我们将在附录A中介绍细节, "值于引用(Values vs References)".

## Declaring and Using Variables声明和使用变量

明确说明上一节中可能不明显的事情: 在JS程序中, 值可以作为字面量(如前面许多示例所示)出现, 或者它们可以保存在变量中; 可以把变量看作值的容器.

变量(Variables)必须声明(创建)才可以使用.有很多不同的语法形式来声明变量(又名, 标识符'identifiers'), 每个形式具有不同的隐含行为.

例如, 考虑以下`var`语句:

```js
var myName = "Kyle";
var age;
```

`var`关键字声明一个变量用来在程序中使用,可选的对值进行初始赋值.

另一种相似关键是`let`:

```js
let myName = "Kyle";
let age;
```

`let`关键字对`var`关键字有些不同,最明显的是`let`允许对变量的访问比`var`更优先. 这被称作`block scope(块作用域)`,与常规作用域(regular)和函数作用域(function scoping)相对.

思考以下:

```js
var adult = true;

if (adult) {
    var myName = "Kyle";
    let age = 39;
    console.log("Shhh, this is a secret!");
}

console.log(myName);
// Kyle

console.log(age);
// Error!
```

The attempt to access `age` outside of the `if` statement results in an error, because `age` was block-scoped to the `if`, whereas `myName` was not.
在`if`语句外尝试获取`age`导致一个错误,因为`age`是在`if`的块作用域(block-scope)中,而`myName`则不是.

Block-scoping is very useful for limiting how widespread variable declarations are in our programs, which helps prevent accidental overlap of their names.
块作用域是对限制程序中变量声明的应用范围很有用,这有助于防止变量名称的重叠.

But `var` is still useful in that it communicates "this variable will be seen by a wider scope (of the whole function)". Both declaration forms can be appropriate in any given part of a program, depending on the circumstances.
但是`var`仍然很有用,因为它传达了"这个变量将被更广泛的范围(整个函数)看到".根据情况，这两种声明形式都可以适用于进程的任何给定部分。
| NOTE: |
| :--- |
| It's very common to suggest that `var` should be avoided in favor of `let` (or `const`!), generally because of perceived confusion over how the scoping behavior of `var` has worked since the beginning of JS. I believe this to be overly restrictive advice and ultimately unhelpful. It's assuming you are unable to learn and use a feature properly in combination with other features. I believe you *can* and *should* learn any features available, and use them where appropriate! 
通常建议避免使用`var`,而支持使用`let`(或`const`),通常因为从JS开始以来,人们对`var`作用域如何工作是感到困惑的.我认为这是严格的建议且最终没啥帮助.它假设你无法正确的将某项功能与其它功能结合使用. 我相信*能*且*应该*学习任何可用的特性,并在合适地方使用它们.
|

A third declaration form is `const`. It's like `let` but has an additional limitation that it must be given a value at the moment it's declared, and cannot be re-assigned a different value later.
第3种声明形式是`const`. 它像`let`但是有一个额外的限制,在声明时必须给一个初始值,而且之后不能重复声明.

Consider:

```js
const myBirthday = true;
let age = 39;

if (myBirthday) {
    age = age + 1;    // OK!
    myBirthday = false;  // Error!
}
```

The `myBirthday` constant is not allowed to be re-assigned.
`myBirthday`常量不允许被重复声明.

`const` declared variables are not "unchangeable", they just cannot be re-assigned. It's ill-advised to use `const` with object values, because those values can still be changed even though the variable can't be re-assigned. This leads to potential confusion down the line, so I think it's wise to avoid situations like:
`const`声明变量是不是不能"改变"的,它们不能被重新赋值(re-assigned). 为对象值使用`const`是不明智的,因为即使变量不能被重新赋值,这些对象值仍然可以被改变.这导致下面的混淆,所以我认为避免像下面这种情况是明智的:

```js
const actors = [
    "Morgan Freeman", "Jennifer Aniston"
];

actors[2] = "Tom Cruise";   // OK :(
actors = [];                // Error!
```

The best semantic use of a `const` is when you have a simple primitive value that you want to give a useful name to, such as using `myBirthday` instead of `true`. This makes programs easier to read.
`const`的最好语义使用方式是当你有一个原始值,你想给一个有用的名字,例如`myBirthday`而不是`true`. 这让程序更容易读.

| TIP: |
| :--- |
| If you stick to using `const` only with primitive values, you avoid any confusion of re-assignment (not allowed) vs. mutation (allowed)! That's the safest and best way to use `const`. 
如果你对原始值坚持使用`const`,你会避免任何重复赋值(不允许)和突变(允许)的混淆. 这是最安全和最好的使用`const`的方式.
|

Besides `var` / `let` / `const`, there are other syntactic forms that declare identifiers (variables) in various scopes. For example:
除了`var` / `let` / `const`外, 还有其它语法形式可以在各种作用域内声明标识符(变量). 例如:

```js
function hello(myName) {
    console.log(`Hello, ${ myName }.`);
}

hello("Kyle");
// Hello, Kyle.
```

The identifier `hello` is created in the outer scope, and it's also automatically associated so that it references the function. But the named parameter `myName` is created only inside the function, and thus is only accessible inside that function's scope. `hello` and `myName` generally behave as `var`-declared.
标识符`hello`在外部作用域中创建, 它自动关联,以便它引用函数.但是命名参数`myName`只在函数内部创建, 所以只能在函数的作用域内部访问. `hello`和`myName`通常表现为`var`声明.

Another syntax that declares a variable is a `catch` clause:
另一个声明变量的语法是`catch`语句.

```js
try {
    someError();
}
catch (err) {
    console.log(err);
}
```

The `err` is a block-scoped variable that exists only inside the `catch` clause, as if it had been declared with `let`.

`err`是一个块作用域变量,且只存在于`catch`句子内部,就像是它用`let`声明一样.
## Functions

The word "function" has a variety of meanings in programming. For example, in the world of Functional Programming, "function" has a precise mathematical definition and implies a strict set of rules to abide by.
`function`这个单词在编程中具有非常广泛的含义.例如,在函数式编程的世界中,'function'有一个精确的数学定义并要遵守一套严格的规则.

In JS, we should consider "function" to take the broader meaning of another related term: "procedure." A procedure is a collection of statements that can be invoked one or more times, may be provided some inputs, and may give back one or more outputs.
在JS中,我们可以考虑'function'具有另一个相关术语'procedure'的更宽泛的含义. 一个程序(procedure)是语句的集合,且能被调用1到多次,可能会提供一些输入,可能返回一些输出

From the early days of JS, function definition looked like:
从JS早期开始,函数定义是这样的:

```js
function awesomeFunction(coolThings) {
    // ..
    return amazingStuff;
}
```

This is called a function declaration because it appears as a statement by itself, not as an expression in another statement. The association between the identifier `awesomeFunction` and the function value happens during the compile phase of the code, before that code is executed.
这杯称作函数声明,因为它本身显示为一个语句,而不是另一个语句的表达式.标识符`awesomeFUnction`和函数值在代码执行前的编译阶段相关联.

In contrast to a function declaration statement, a function expression can be defined and assigned like this:
与函数声明语句相反,函数表达式能像下面这样定义和赋值:

```js
// let awesomeFunction = ..
// const awesomeFunction = ..
var awesomeFunction = function(coolThings) {
    // ..
    return amazingStuff;
};
```

This function is an expression that is assigned to the variable `awesomeFunction`. Different from the function declaration form, a function expression is not associated with its identifier until that statement during runtime.
上面这个函数是一个表达式且赋值给变量`awesomeFunction`. 和函数声明形式不同,函数表达式直到运行时才与其标识符关联.

It's extremely important to note that in JS, functions are values that can be assigned (as shown in this snippet) and passed around. In fact, JS functions are a special type of the object value type. Not all languages treat functions as values, but it's essential for a language to support the functional programming pattern, as JS does.
在JS中需要记住这非常重要的一点,函数是值且能被赋值(就像在上面代码片段中那样)和传递. 事实上,JS函数是对象类型中一种特殊类型. 不是所有的语言把函数当作值,但是对一门语言来说,支持函数编程范式很重要,就像JS做的那样.

JS functions can receive parameter input:
JS函数可以接收参数:

```js
function greeting(myName) {
    console.log(`Hello, ${ myName }!`);
}

greeting("Kyle");   // Hello, Kyle!
```

In this snippet, `myName` is called a parameter, which acts as a local variable inside the function. Functions can be defined to receive any number of parameters, from none upward, as you see fit. Each parameter is assigned the argument value that you pass in that position (`"Kyle"`, here) of the call.
在这段代码中, `myName`被称作参数,其行为像是函数内的局部变量.  函数可以被定义接收任意数量的参数(形参),从0到多个,直到你认为适合.每个形参会被赋值为调用时候相同位置(这里是`"Kyle"`)你传递的实参值(argument value).

Functions also can return values using the `return` keyword:
使用`return`关键字返回函数值:

```js
function greeting(myName) {
    return `Hello, ${ myName }!`;
}

var msg = greeting("Kyle");

console.log(msg);   // Hello, Kyle!
```

You can only `return` a single value, but if you have more values to return, you can wrap them up into a single object/array.
你只能`return`单个值,如果你有多个值需要返回,你可以把它们包装成一个对象/数组.

Since functions are values, they can be assigned as properties on objects:
因为函数是值,它们能当作对象的属性(object properties)被赋值.

```js
var whatToSay = {
    greeting() {
        console.log("Hello!");
    },
    question() {
        console.log("What's your name?");
    },
    answer() {
        console.log("My name is Kyle.");
    }
};

whatToSay.greeting();
// Hello!
```

In this snippet, references to three functions (`greeting()`, `question()`, and `answer()`) are included in the object held by `whatToSay`. Each function can be called by accessing the property to retrieve the function reference value. Compare this straightforward style of defining functions on an object to the more sophisticated `class` syntax discussed later in this chapter.
这上面的代码块中, 对3个函数(`greeting()`, `question()`, and `answer()`)的引用包含在`whatToSay`持有的对象中.每个函数可以通过访问属性来检索函数引用值来调用.在之后的章节中,将会比较对象上定义函数的简单风格和更复杂的`class`语法.

There are many varied forms that `function`s take in JS. We dig into these variations in Appendix A, "So Many Function Forms."
JS中有很多不同形式的函数.我们将在附录A中深入这些变化, "So Many Function Forms".
## Comparisons 比较

Making decisions in programs requires comparing values to determine their identity and relationship to each other. JS has several mechanisms to enable value comparison, so let's take a closer look at them.
在程序中做出需要比较值来决定它们相等或其它关系的决策. JS有多个机制实现值比较,所以我们仔细看看.

### Equal...ish

The most common comparison in JS programs asks the question, "Is this X value *the same as* that Y value?" What exactly does "the same as" really mean to JS, though?
在JS程序中最常见的比较问题是, 这个X值是否与Y值*相同*?但是对于JS来说, *相同*究竟意味着什么?

For ergonomic and historical reasons, the meaning is more complicated than the obvious *exact identity* sort of matching. Sometimes an equality comparison intends *exact* matching, but other times the desired comparison is a bit broader, allowing *closely similar* or *interchangeable* matching. In other words, we must be aware of the nuanced differences between an **equality** comparison and an **equivalence** comparison.
因为工程和历史原因,相同的含义比*完全相同*类型的匹配更复杂.有时相等比较(equality comparison)旨在*完全*匹配,但有时候所需的比较更宽泛一些,允许*接近相同(closely similar)* 或 *可互换*匹配.换句话说,我们必须一世到在**equality相等**比较和**equivalence全等(等价)**比较的微妙区别.

If you've spent any time working with and reading about JS, you've certainly seen the so-called "triple-equals" `===` operator, also described as the "strict equality" operator. That seems rather straightforward, right? Surely, "strict" means strict, as in narrow and *exact*.
如果你花过时间研究和阅读JS,你肯定直到称作'triple-equals(全等)'`===`操作符,也被描述做"严格相等"操作符. 它看起来并不直接明了,是吧.确定的是,`strict(严格)意味着strict(严格),

Not *exact*ly.

Yes, most values participating in an `===` equality comparison will fit with that *exact same* intuition. Consider some examples:
是的，参与 '===' 相等比较的大多数值都符合那个*完全相同*的直觉。请看一些例子：

```js
3 === 3.0;              // true
"yes" === "yes";        // true
null === null;          // true
false === false;        // true

42 === "42";            // false
"hello" === "Hello";    // false
true === 1;             // false
0 === null;             // false
"" === null;            // false
null === undefined;     // false
```

| NOTE: |
| :--- |
| Another way `===`'s equality comparison is often described is, "checking both the value and the type". In several of the examples we've looked at so far, like `42 === "42"`, the *type* of both values (number, string, etc.) does seem to be the distinguishing factor. There's more to it than that, though. **All** value comparisons in JS consider the type of the values being compared, not *just* the `===` operator. Specifically, `===` disallows any sort of type conversion (aka, "coercion") in its comparison, where other JS comparisons *do* allow coercion. 
另一种常用描述‘ === ’相等性比较的方法是同时检查值和类型。在最近几个我们查看过的例子中, 像`42===42`,两个值(数值,字符串等)的类型似乎是区别因素.尽管有比这更多的因素. 在JS中**所有**值比较都会在比较时考虑被比较值的类型, 不仅仅是`===`操作符. 特别是, `===`在比较中不允许任何形式的类型转换(别名,'coercion'强制), 然而其它JS比较**是**允许强制类型转换.|

But the `===` operator does have some nuance to it, a fact many JS developers gloss over, to their detriment. The `===` operator is designed to *lie* in two cases of special values: `NaN` and `-0`. Consider:
但是`===`操作符确实有一些细微差异,这是许多JS开发人员掩盖的事实, 会对它们不利. `===`操作符在两种特殊情况下被设计为*不准确*: ``NaN`和`-0`. 请考虑:

```js
NaN === NaN;            // false
0 === -0;               // true
```

In the case of `NaN`, the `===` operator *lies* and says that an occurrence of `NaN` is not equal to another `NaN`. In the case of `-0` (yes, this is a real, distinct value you can use intentionally in your programs!), the `===` operator *lies* and says it's equal to the regular `0` value.
在`NaN`的情况下, `===`操作符*撒谎(不准确)*表示一个 `NaN` 实例与另一个 `NaN` 不相等。在`-0`的情况下(是的, 这确实是一个真实的、独特的值，您可以在程序中有意使用！), `===`操作符*不准确*表示它等于普通的`0`值.

Since the *lying* about such comparisons can be bothersome, it's best to avoid using `===` for them. For `NaN` comparisons, use the `Number.isNaN(..)` utility, which does not *lie*. For `-0` comparison, use the `Object.is(..)` utility, which also does not *lie*. `Object.is(..)` can also be used for non-*lying* `NaN` checks, if you prefer. Humorously, you could think of `Object.is(..)` as the "quadruple-equals" `====`, the really-really-strict comparison!
由于此类比较不准确会很困扰,最好避免对`NaN`和`-0`使用`===`. 对`NaN`比较, 使用`Number.isNaN(..)`工具,这个不会不准确. 对`-0`比较, 使用`Object.is(..)`工具. `Object.is(..)`也可以用来做准确(non-lying)`NaN`检查, 如果你更愿意的话. 有趣的是,你可以认为`Object.is(..)`是4倍(quadruple-equals)`====`, 真-真-严格比较.(really-really-strict-comparison).

There are deeper historical and technical reasons for these *lies*, but that doesn't change the fact that `===` is not actually *strictly exactly equal* comparison, in the *strictest* sense.
对这些*不准确*是有更深的历史和技术原因, 但是不会改变`===`是不是真正的*严格准确相等*比较, 在*最严格(strictest)*意义上.

The story gets even more complicated when we consider comparisons of object values (non-primitives). Consider:
当我们考虑对象值比较,事情会更加复杂. 请考虑:

```js
[ 1, 2, 3 ] === [ 1, 2, 3 ];    // false
{ a: 42 } === { a: 42 }         // false
(x => x * 2) === (x => x * 2)   // false
```

What's going on here?
在这里发生了什么呢?

It may seem reasonable to assume that an equality check considers the *nature* or *contents* of the value; after all, `42 === 42` considers the actual `42` value and compares it. But when it comes to objects, a content-aware comparison is generally referred to as "structural equality."
相等检查(equality check)考虑值的*特性*和*内容*的假设看起来是合理的; 比较, `42 === 42`会考虑实际`42`的值并比较. 但是当涉及到对象时, 内容敏感的比较通常被称为"结构相等".

JS does not define `===` as *structural equality* for object values. Instead, `===` uses *identity equality* for object values.
JS没有定义`===`为对象值的*结构相等*. 相反,`===`对对象值使用*完全相等(identity equality)*.

In JS, all object values are held by reference (see "Values vs References" in Appendix A), are assigned and passed by reference-copy, **and** to our current discussion, are compared by reference (identity) equality. Consider:
在JS中, 所有对象值都是通过引用(见'Values vs References" in Appendix A)来保存, 通过引用拷贝(reference-copy)来赋值和传递, **并且**在我们当前讨论中, 通过引用(身份)相等来进行比较

```js
var x = [ 1, 2, 3 ];

// assignment is by reference-copy, so
// y references the *same* array as x,
// not another copy of it.
var y = x;

y === x;              // true
y === [ 1, 2, 3 ];    // false
x === [ 1, 2, 3 ];    // false
```

In this snippet, `y === x` is true because both variables hold a reference to the same initial array. But the `=== [1,2,3]` comparisons both fail because `y` and `x`, respectively, are being compared to new *different* arrays `[1,2,3]`. The array structure and contents don't matter in this comparison, only the **reference identity**.
在上面的代码片段中, `y===x`结果为true,因为两个变量引用相同的初始数组. 但是`===[1,2,3]`的比较两次都失败,因为`y`和`x`各自比较新*不同*数组`[1,2,3]`. 在比较中,无关数组结构和内容,只有**引用相同(referrence identity)**才有关.

JS does not provide a mechanism for structural equality comparison of object values, only reference identity comparison. To do structural equality comparison, you'll need to implement the checks yourself.
JS对对象值不提供结构相等比较,而只提供引用相等比较. 要实现结构相等比较的话,你需要自己实施检查.

But beware, it's more complicated than you'll assume. For example, how might you determine if two function references are "structurally equivalent"? Even stringifying to compare their source code text wouldn't take into account things like closure. JS doesn't provide structural equality comparison because it's almost intractable to handle all the corner cases!
要小心的是,这比你想得更复杂.例如,你如何确定两个函数引用是"结构等效(structural equality)"? 即使字符串化来比较它们的源代码文本也不会考虑到闭包之类的东西. JS不提供结构等效比较因为处理所有边缘情况是几乎非常难的.

### Coercive Comparisons(强制比较)

Coercion means a value of one type being converted to its respective representation in another type (to whatever extent possible). As we'll discuss in Chapter 4, coercion is a core pillar of the JS language, not some optional feature that can reasonably be avoided.
强制意味着一个类型的值会被转换成另一种类型的相应表示形式(在可能的范围内).我们将在Chapter 4中讨论, 强制转换是JS语言中核心,不是可选的可以合理避免的特性.

But where coercion meets comparison operators (like equality), confusion and frustration unfortunately crop up more often than not.
但是，当强制操作遇到比较操作符（如相等操作符）时，不幸的是，混淆和挫折往往会突然出现。

Few JS features draw more ire in the broader JS community than the `==` operator, generally referred to as the "loose equality" operator. The majority of all writing and public discourse on JS condemns this operator as poorly designed and dangerous/bug-ridden when used in JS programs. Even the creator of the language himself, Brendan Eich, has lamented how it was designed as a big mistake.
在更广泛的 JS 社区中，很少有 JS 功能比 '==' 运算符（通常称为 “松散相等” 运算符）更引起愤怒。大多数关于 JS 的写作和公共讨论都谴责这个运算符在 JS 进程中使用时设计不佳且危险/充满错误。就连该语言的创造者 Brendan Eich 本人也对它的设计是一个大错误感到遗憾。

From what I can tell, most of this frustration comes from a pretty short list of confusing corner cases, but a deeper problem is the extremely widespread misconception that it performs its comparisons without considering the types of its compared values.
我能说的是, 大多数困惑来自比较简短的困惑边缘案例列表,但是更深的问题是非常深非常的误解关于它执行比较时候不会考虑比较值的类型.

The `==` operator performs an equality comparison similarly to how the `===` performs it. In fact, both operators consider the type of the values being compared. And if the comparison is between the same value type, both `==` and `===` **do exactly the same thing, no difference whatsoever.**
`==`操作符执行相等比较类似于`===`操作符的执行相等比较.事实上,两个操作符会考虑比较值的类型.如果比较是在两个相同值类型, `==`和`===`**都会做相同的事,没有任何区别**.

If the value types being compared are different, the `==` differs from `===` in that it allows coercion before the comparison. In other words, they both want to compare values of like types, but `==` allows type conversions *first*, and once the types have been converted to be the same on both sides, then `==` does the same thing as `===`. Instead of "loose equality," the `==` operator should be described as "coercive equality."
如果比较的值类型是不同的,`==`是不同于`===`的,是它在比较之前允许强制类型转换.换句话说,它们都想比较相似类型的值,但是`==`允许类型*首先*转换,一旦类型转换为两边都相同, 届时`==`会做于`===`一样的事情. `==`操作符应该被描述为"强制相等",而非'松散相等'.

Consider:

```js
42 == "42";             // true
1 == true;              // true
```

In both comparisons, the value types are different, so the `==` causes the non-number values (`"42"` and `true`) to be converted to numbers (`42` and `1`, respectively) before the comparisons are made.
两个比较中,值的类型是不同的,所以`==`会在比较发生之前,将非数值的值(`"42"`和`true`)转换为数值(`42`和`1`, 各自)

Just being aware of this nature of `==`—that it prefers primitive numeric comparisons—helps you avoid most of the troublesome corner cases, such as staying away from a gotchas like `"" == 0` or `0 == false`.
要注意到`==`的特性, 它更倾向于原始数值比较-帮助你避免绝大多数的让人困惑的边缘情况,例如,远离像`"" == 0` 或者 `0 == false`之类的陷阱.

You may be thinking, "Oh, well, I will just always avoid any coercive equality comparison (using `===` instead) to avoid those corner cases"! Eh, sorry, that's not quite as likely as you would hope.
你可能会想,"行吧, 我会总是避免强制相等比较(使用`===`代替)来避免这些边缘情况"! 抱歉, 这并不像你希望的那幺可能。

There's a pretty good chance that you'll use relational comparison operators like `<`, `>` (and even `<=` and `>=`).
有相当大的机会你会使用关系运算符, 像`<`, `>`(甚至`<=`, `>=`).

Just like `==`, these operators will perform as if they're "strict" if the types being relationally compared already match, but they'll allow coercion first (generally, to numbers) if the types differ.
就像`==`, 如果要进行关系比较的类型已经相同(match),那么操作符会像严格操作符一样执行,但是如果类型不同,它们将会允许强制类型转换(通常转换成数值).

Consider:

```js
var arr = [ "1", "10", "100", "1000" ];
for (let i = 0; i < arr.length && arr[i] < 500; i++) {
    // will run 3 times
}
```

The `i < arr.length` comparison is "safe" from coercion because `i` and `arr.length` are always numbers. The `arr[i] < 500` invokes coercion, though, because the `arr[i]` values are all strings. Those comparisons thus become `1 < 500`, `10 < 500`, `100 < 500`, and `1000 < 500`. Since that fourth one is false, the loop stops after its third iteration.
这段不翻译了,过于直白.

These relational operators typically use numeric comparisons, except in the case where **both** values being compared are already strings; in this case, they use alphabetical (dictionary-like) comparison of the strings:
关系运算符通常使用数值比较, 除了**双方**比较的值都是字符串; 在这种情况下, 使用字符串alphabetical(类似字典)比较

```js
var x = "10";
var y = "9";

x < y;      // true, watch out!
```

There's no way to get these relational operators to avoid coercion, other than to just never use mismatched types in the comparisons. That's perhaps admirable as a goal, but it's still pretty likely you're going to run into a case where the types *may* differ.
没有方法来避免关系运算符的强制类型转换, 除非在比较时永远不要使用不匹配的类型. 这个目标太大了,但你仍然很可能会遇到类型*可能*不同的情况。

The wiser approach is not to avoid coercive comparisons, but to embrace and learn their ins and outs.
更明智的方法不是避免强制转换,而是拥抱和学习它们的来龙去脉.

Coercive comparisons crop up in other places in JS, such as conditionals (`if`, etc.), which we'll revisit in Appendix A, "Coercive Conditional Comparison."
强制转换也会偶然出现在JS的其它地方,例如条件(`if`,等等),我们可以在附录A "Coercive Conditional"中找到它.

## How We Organize in JS

Two major patterns for organizing code (data and behavior) are used broadly across the JS ecosystem: classes and modules. These patterns are not mutually exclusive; many programs can and do use both. Other programs will stick with just one pattern, or even neither!
两种主要的组织代码的模式(数据和行为)在JS生态中应用广泛: 类和模块. 而且并不互斥; 很多程序能且两个都用. 其它程序则坚持仅有一种模式,甚至都没有.

In some respects, these patterns are very different. But interestingly, in other ways, they're just different sides of the same coin. Being proficient in JS requires understanding both patterns and where they are appropriate (and not!).
在某些方面, 这俩模式是非常不同的.但是有意思的,在另一些方面,它们仅仅是硬币的不同面. 精通JS需要理解两种模式并且理解它们用在哪里合适(不合适).

### Classes

The terms "object-oriented," "class-oriented," and "classes" are all very loaded full of detail and nuance; they're not universal in definition.
"面向对象(object-oriented)", "面向类(class-oriented)"和"类"这些术语,充满了细节和细微差别; 它们在定义上不通用.

We will use a common and somewhat traditional definition here, the one most likely familiar to those with backgrounds in "object-oriented" languages like C++ and Java.
我们在这里将使用常见的和有点传统的定义, 对于那些具有C++和Java等"面向对象"语言背景的人来说, 这个定义很可能很熟悉.

A class in a program is a definition of a "type" of custom data structure that includes both data and behaviors that operate on that data. Classes define how such a data structure works, but classes are not themselves concrete values. To get a concrete value that you can use in the program, a class must be *instantiated* (with the `new` keyword) one or more times.
程序中的类是对包含数据和操作该数据的行为的“自定义数据结构类型”的定义。 类定义了这种数据结构的工作方式，但类本身不是具体的值。 要获得可以在程序中使用的具体值，必须对类进行一次或多次实例化（使用new关键字）。

Consider:

```js
class Page {
    constructor(text) {
        this.text = text;
    }

    print() {
        console.log(this.text);
    }
}

class Notebook {
    constructor() {
        this.pages = [];
    }

    addPage(text) {
        var page = new Page(text);
        this.pages.push(page);
    }

    print() {
        for (let page of this.pages) {
            page.print();
        }
    }
}

var mathNotes = new Notebook();
mathNotes.addPage("Arithmetic: + - * / ...");
mathNotes.addPage("Trigonometry: sin cos tan ...");

mathNotes.print();
// ..
```

In the `Page` class, the data is a string of text stored in a `this.text` member property. The behavior is `print()`, a method that dumps the text to the console.
在`Page`类中, 数据是存储在成员属性`this.text`中的文本字符串, 行为是`print()`, 这是一种将文本输出到控制台的方法。

For the `Notebook` class, the data is an array of `Page` instances. The behavior is `addPage(..)`, a method that instantiates new `Page` pages and adds them to the list, as well as `print()` (which prints out all the pages in the notebook).
`Notebook`类, 数据是`Page`实例的数组.行为是`addPage(...)`, 实例化新的`Page`页面并将它们添加到列表的方法, 和`print()`一样(其打印notebook中的所有pages)

The statement `mathNotes = new Notebook()` creates an instance of the `Notebook` class, and `page = new Page(text)` is where instances of the `Page` class are created.
语句`mathNotes = new Notebook()`创建类`Notebook`的实例, `page = new Page(text)`是`Page`类创建的实例.

Behavior (methods) can only be called on instances (not the classes themselves), such as `mathNotes.addPage(..)` and `page.print()`.
行为(方法)仅能在实例(不是类自身)上调用, 例如`mathNotes.addPage(..)`和`page.print()`.

The `class` mechanism allows packaging data (`text` and `pages`) to be organized together with their behaviors (e.g., `addPage(..)` and `print()`). The same program could have been built without any `class` definitions, but it would likely have been much less organized, harder to read and reason about, and more susceptible to bugs and subpar maintenance.
`class`机制允许将封装的数据(`text`和``pages`)与其行为(例如, `addPage(..)`和`print()`)一起组织起来. 相同的程序可以在没有`class`定义下来构建, 但是这个程序可能组织的更差, 更难阅读和理解,并且更容易出现错误和维护不佳.

#### Class Inheritance类继承

Another aspect inherent to traditional "class-oriented" design, though a bit less commonly used in JS, is "inheritance" (and "polymorphism"). Consider:
传统“面向类”设计的另一个固有方面是“继承”（和“多态”('polymorphism')），尽管在 JavaScript 中使用得相对较少。

```js
class Publication {
    constructor(title,author,pubDate) {
        this.title = title;
        this.author = author;
        this.pubDate = pubDate;
    }

    print() {
        console.log(`
            Title: ${ this.title }
            By: ${ this.author }
            ${ this.pubDate }
        `);
    }
}
```

This `Publication` class defines a set of common behavior that any publication might need.
`Publication`类定义了一系列出版物可能需要的通用行为.

Now let's consider more specific types of publication, like `Book` and `BlogPost`:
现在让我们考虑更详细的出版物类型, 例如`Book`和`BlogPost`:

```js
class Book extends Publication {
    constructor(bookDetails) {
        super(
            bookDetails.title,
            bookDetails.author,
            bookDetails.publishedOn
        );
        this.publisher = bookDetails.publisher;
        this.ISBN = bookDetails.ISBN;
    }

    print() {
        super.print();
        console.log(`
            Publisher: ${ this.publisher }
            ISBN: ${ this.ISBN }
        `);
    }
}

class BlogPost extends Publication {
    constructor(title,author,pubDate,URL) {
        super(title,author,pubDate);
        this.URL = URL;
    }

    print() {
        super.print();
        console.log(this.URL);
    }
}
```

Both `Book` and `BlogPost` use the `extends` clause to *extend* the general definition of `Publication` to include additional behavior. The `super(..)` call in each constructor delegates to the parent `Publication` class's constructor for its initialization work, and then they do more specific things according to their respective publication type (aka, "sub-class" or "child class").
`Book`和`BlogPost`使用`extends`句子来*extend*`Publication`通用的定义,包含额外的行为. 每个构造函数中的 super(..) 调用委托给父类 Publication 的构造函数来执行其初始化工作，然后它们根据各自的出版物类型（也称为“子类”或“子类”）执行更具体的操作。

Now consider using these child classes:

```js
var YDKJS = new Book({
    title: "You Don't Know JS",
    author: "Kyle Simpson",
    publishedOn: "June 2014",
    publisher: "O'Reilly",
    ISBN: "123456-789"
});

YDKJS.print();
// Title: You Don't Know JS
// By: Kyle Simpson
// June 2014
// Publisher: O'Reilly
// ISBN: 123456-789

var forAgainstLet = new BlogPost(
    "For and against let",
    "Kyle Simpson",
    "October 27, 2014",
    "https://davidwalsh.name/for-and-against-let"
);

forAgainstLet.print();
// Title: For and against let
// By: Kyle Simpson
// October 27, 2014
// https://davidwalsh.name/for-and-against-let
```

Notice that both child class instances have a `print()` method, which was an override of the *inherited* `print()` method from the parent `Publication` class. Each of those overridden child class `print()` methods call `super.print()` to invoke the inherited version of the `print()` method.
注意两个子类实例有`print()`方法, 其重写了从父类`Publication`*继承*的`print()`方法. 每个重写的子类`print()`方法调用了`super.print()`来调用继承版本的`print()`方法.

The fact that both the inherited and overridden methods can have the same name and co-exist is called *polymorphism*.
继承(inherited)和重写(overridden)方法能有相同的名称和共存的事实被称为*多态*(polymorphism).

Inheritance is a powerful tool for organizing data/behavior in separate logical units (classes), but allowing the child class to cooperate with the parent by accessing/using its behavior and data.
在分散的逻辑单元(类)中继承是组织数据/行为的有利工具, 但允许子类通过访问/使用父类行为数据来和父类合作.

### Modules模块

The module pattern has essentially the same goal as the class pattern, which is to group data and behavior together into logical units. Also like classes, modules can "include" or "access" the data and behaviors of other modules, for cooperation's sake.
模块模式基本上和类模式有相同的目标, 组织数据和行为为逻辑单元. 也像类一样, 模块,为了合作的目标,可以"包含"或"访问"其它模块的数据和行为.

But modules have some important differences from classes. Most notably, the syntax is entirely different.
但是模块与类有一些重要的不同. 尤其是, 语法完全不同.

#### Classic Modules 类模块

ES6 added a module syntax form to native JS syntax, which we'll look at in a moment. But from the early days of JS, modules was an important and common pattern that was leveraged in countless JS programs, even without a dedicated syntax.
ES6给原生JS语法添加了模块语法形式, 接下来我们将了解一下.但是从早期JS阶段, 模块是重要和通用的模式,在无数JS程序中起到了杠杆作用, 即使没有专用的语法.

The key hallmarks of a *classic module* are an outer function (that runs at least once), which returns an "instance" of the module with one or more functions exposed that can operate on the module instance's internal (hidden) data.
*经典模块* 的关键标志是一个外部函数（至少运行一次），它返回模块的“实例”，其中公开了一个或多个函数，这些函数可以操作模块实例的内部（隐藏）数据。

Because a module of this form is *just a function*, and calling it produces an "instance" of the module, another description for these functions is "module factories".
因为这个形式的模块就是一个函数, 并且调用它回生成模块的一个*实例*, 这些函数的其它描述是"模块工厂module factories".
Consider the classic module form of the earlier `Publication`, `Book`, and `BlogPost` classes:
考虑之前`Publication`, `Book`和`BlogPost`类的经典模块形式:

```js
function Publication(title,author,pubDate) {
    var publicAPI = {
        print() {
            console.log(`
                Title: ${ title }
                By: ${ author }
                ${ pubDate }
            `);
        }
    };

    return publicAPI;
}

function Book(bookDetails) {
    var pub = Publication(
        bookDetails.title,
        bookDetails.author,
        bookDetails.publishedOn
    );

    var publicAPI = {
        print() {
            pub.print();
            console.log(`
                Publisher: ${ bookDetails.publisher }
                ISBN: ${ bookDetails.ISBN }
            `);
        }
    };

    return publicAPI;
}

function BlogPost(title,author,pubDate,URL) {
    var pub = Publication(title,author,pubDate);

    var publicAPI = {
        print() {
            pub.print();
            console.log(URL);
        }
    };

    return publicAPI;
}
```

Comparing these forms to the `class` forms, there are more similarities than differences.
比较这些形式和`类`的形式, 相似多于不同.

The `class` form stores methods and data on an object instance, which must be accessed with the `this.` prefix. With modules, the methods and data are accessed as identifier variables in scope, without any `this.` prefix.
`类`形式是在对象实例上存储了方法和数据, 其访问必须通过`this.`前缀. 模块的话, 方法和数据的方法是通过作用域中的标识符变量(identifier variables),不用任何`this.`前缀.

With `class`, the "API" of an instance is implicit in the class definition—also, all data and methods are public. With the module factory function, you explicitly create and return an object with any publicly exposed methods, and any data or other unreferenced methods remain private inside the factory function.
使用`类`, 实例的"API"是隐含在类定义的, 所有的数据和方法是公共的.使用模块工厂函数, 你显式创建并返回一个对象, 其中包含任何公开暴露的方法,而任何数据或其他未引用的方法都将保持在工厂函数内部私有。

There are other variations to this factory function form that are quite common across JS, even in 2020; you may run across these forms in different JS programs: AMD (Asynchronous Module Definition), UMD (Universal Module Definition), and CommonJS (classic Node.js-style modules). The variations are minor (not quite compatible). However, all of these forms rely on the same basic principles.
工厂函数的其它变种形式,即使在2020年也是非常常见的;你可能在不同的JS程序中执行过这些: AMD(异步模块定义), UMD(统一模块定义), 和CommonJS(经典Node.js-style模块). 变化很小(不太兼容). 然而, 所有的这些形式依赖于相同的基本原则.

Consider also the usage (aka, "instantiation") of these module factory functions:
考虑这些模块工厂函数的用法(别名, '实例')

```js
var YDKJS = Book({
    title: "You Don't Know JS",
    author: "Kyle Simpson",
    publishedOn: "June 2014",
    publisher: "O'Reilly",
    ISBN: "123456-789"
});

YDKJS.print();
// Title: You Don't Know JS
// By: Kyle Simpson
// June 2014
// Publisher: O'Reilly
// ISBN: 123456-789

var forAgainstLet = BlogPost(
    "For and against let",
    "Kyle Simpson",
    "October 27, 2014",
    "https://davidwalsh.name/for-and-against-let"
);

forAgainstLet.print();
// Title: For and against let
// By: Kyle Simpson
// October 27, 2014
// https://davidwalsh.name/for-and-against-let
```

The only observable difference here is the lack of using `new`, calling the module factories as normal functions.
这里唯一观测到的差异是缺少了`new`的使用, 像普通函数一样调用模块函数.

#### ES Modules

ES modules (ESM), introduced to the JS language in ES6, are meant to serve much the same spirit and purpose as the existing *classic modules* just described, especially taking into account important variations and use cases from AMD, UMD, and CommonJS.
ES模块(ESM), 在ES6中被引入到了JS语言, 旨在实现和刚才描述的现有*经典模块*相同的目的，特别是考虑到 AMD、UMD 和 CommonJS 的重要变体和用例。

The implementation approach does, however, differ significantly.
但是实施方法却有很大的不同.

First, there's no wrapping function to *define* a module. The wrapping context is a file. ESMs are always file-based; one file, one module.
首先, *定义*模块不会有包装函数. 包装的上下文是一个文件, ESMs是基于文件的; 一个文件,一个模块.

Second, you don't interact with a module's "API" explicitly, but rather use the `export` keyword to add a variable or method to its public API definition. If something is defined in a module but not `export`ed, then it stays hidden (just as with *classic modules*).
第二, 你不会与模块的'API'显式的交互, 而是用`export`关键字来添加一个变量或方法未公共的API定义. 如果模块中有些定义了却没有`export`ed, 那么它将保持隐藏(就像*经典模块*一样).

Third, and maybe most noticeably different from previously discussed patterns, you don't "instantiate" an ES module, you just `import` it to use its single instance. ESMs are, in effect, "singletons," in that there's only one instance ever created, at first `import` in your program, and all other `import`s just receive a reference to that same single instance. If your module needs to support multiple instantiations, you have to provide a *classic module-style* factory function on your ESM definition for that purpose.
第三, 来自之前讨论过的模式最明显的差异可能是, 你不需要"实例化"一个ES模块, 你仅仅`import`模块来使用这个模块单例. ESMs是,实际上,"单例singletons",  ...., 首先在程序中`import`, 所有其它`import`s仅仅是接收同一个实例的引用. 如果你地模块需要支持多个实例, 你必须在你地ESM定义上, 提供一个`经典模块风格*地工厂函数, 才能实现目的.

In our running example, we do assume multiple-instantiation, so these following snippets will mix both ESM and *classic modules*.
在我们接下来的例子中, 我们假设多个实例,所以接下来的片段将混合ESM和*经典模块*.

Consider the file `publication.js`:

```js
function printDetails(title,author,pubDate) {
    console.log(`
        Title: ${ title }
        By: ${ author }
        ${ pubDate }
    `);
}

export function create(title,author,pubDate) {
    var publicAPI = {
        print() {
            printDetails(title,author,pubDate);
        }
    };

    return publicAPI;
}
```

To import and use this module, from another ES module like `blogpost.js`:
 从其它像`blogpost.js`的ES模块中,导入并使用这个模块: 

```js
import { create as createPub } from "publication.js";

function printDetails(pub,URL) {
    pub.print();
    console.log(URL);
}

export function create(title,author,pubDate,URL) {
    var pub = createPub(title,author,pubDate);

    var publicAPI = {
        print() {
            printDetails(pub,URL);
        }
    };

    return publicAPI;
}
```

And finally, to use this module, we import into another ES module like `main.js`:
最后, 为了用这个模块,我们导入了像`main.js`的ES模块: 

```js
import { create as newBlogPost } from "blogpost.js";

var forAgainstLet = newBlogPost(
    "For and against let",
    "Kyle Simpson",
    "October 27, 2014",
    "https://davidwalsh.name/for-and-against-let"
);

forAgainstLet.print();
// Title: For and against let
// By: Kyle Simpson
// October 27, 2014
// https://davidwalsh.name/for-and-against-let
```

| NOTE: |
| :--- |
| The `as newBlogPost` clause in the `import` statement is optional; if omitted, a top-level function just named `create(..)` would be imported. In this case, I'm renaming it for readability's sake; its more generic factory name of `create(..)` becomes more semantically descriptive of its purpose as `newBlogPost(..)`. |
在`import`句子中的`as newBlogPOst`子句是可选的; 如果忽略, 一个名为`create(..)`的顶级函数将会被导入. 在这个例子中, 为了读取方便的目的,我重命名了它; 

As shown, ES modules can use *classic modules* internally if they need to support multiple-instantiation. Alternatively, we could have exposed a `class` from our module instead of a `create(..)` factory function, with generally the same outcome. However, since you're already using ESM at that point, I'd recommend sticking with *classic modules* instead of `class`.
就像展示的一样, ES模块如果需要支持多个实例的话, 内部能用*经典模块*. 可选的是, 我们可以从模块中暴露一个`类`来代替`create(..)`工厂函数, 结果大致相同. 然而, 既然你已经使用了ESM, 我推荐用`经典模块*代替`类`.

If your module only needs a single instance, you can skip the extra layers of complexity: `export` its public methods directly.
如果你的模块只许看一个单例(single instance), 你可以忽略额外的复杂层: 直接`export`它的公共方法.

## The Rabbit Hole Deepens兔子洞越来越深

As promised at the top of this chapter, we just glanced over a wide surface area of the main parts of the JS language. Your head may still be spinning, but that's entirely natural after such a firehose of information!
在本章上面承诺过的, 我们仅仅是粗略浏览JS语言主要部分的表面. 你的脑袋可能现在还是晕的,但这是在接收了这么多消息后是正常的.

Even with just this "brief" survey of JS, we covered or hinted at a ton of details you should carefully consider and ensure you are comfortable with. I'm serious when I suggest: re-read this chapter, maybe several times.
即便是"简短"了解JS, 我们概述或提示你应该详细了解的很多细节,确保你能适应它. 我很严肃的建议: 反复读这一章, 尽可能地多几次.

In the next chapter, we're going to dig much deeper into some important aspects of how JS works at its core. But before you follow that rabbit hole deeper, make sure you've taken adequate time to fully digest what we've just covered here.
在下一章, 我们将对在JS在核心中如何工作的一些重要方面挖掘的更深. 但是在你进到兔子洞之前, 请确保你已经花了足够的时间来完全消化我们刚刚介绍的内容。