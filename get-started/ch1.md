# 你不知道的 JS: 入门 - 第 2 版

# 第一章: 什么*是*JavaScript?

你不知道的 JS. 我也不完全了解. 我们中没有人完全理解它. 但是我们可以开始更好的了解 JS.

在你不知道的 JS(YDKJSY)系列的第一本书的第一章中,我们将花些时间来构建基础并继续前进.我们需要从掌握很多重要背景管理细节开始,澄清关于关于这门语言是什么(和不是什么)的一些神话和误解.

这是对 JS 的身份和组织维护过程的宝贵洞见.所有的 JavaScript 开发者应该理解它.如果你想开始了解 JS,这就是如何*开始*旅程的第一步.

## 关于此书

我要强调的是旅程这个词因为*了解 JS*不是终点, 它是一个方向. 无论你在在这门语言上花费了多少时间, 你将总是能找到其它东西来学习和更好地理解. 所以不要把看这本书当做为了快速成就而匆匆完成的事情. 相反,耐心和坚持是你迈出最开始几步时最好的.

在背景章节以后,书籍剩余部分将会为你提供高标准的地图,当通过'你不知道的 JS'深入研究和学习 JS 时候你会发现什么.

尤其是第 4 章确定围绕 JS 语言组织的 3 大支柱: 作用域/闭包,原型/对象,和类型/强制转换. JS 是一门广泛和复杂的语言,拥有很多特性和功能.但是所有的 JS 都是建立在这 3 个基础支柱上的.

记住即使这本书被命名为'入门',它也不是准备作为初学者/入门的书.这本书的主要任务是做好准备来深入学习剩余系列的 JS; 它假设你已经熟悉 JS 至少几个月,在继续'你不知道的 JS'之前. 所以为了好好利用*入门*章节,确保你花足够多时间写 JS 代码来来构建经验.

即使之前您已经写了很多 JS,这本书不应该被略读或跳过; 花时间充分掌握这里的知识. **好的开始总是依赖于坚实的第一步**

## 关于那个名字是怎么回事?

JavaScript 这个名字可能是最被误解的编程语言名称.

这门语言和 Java 有关吗? 它只是 Java 的脚本形式吗?它是只用来写脚本和并非真正的编程语言吗?

事实是, JavaScript 这个名字是市场恶作剧的人为结果. 当 Brendan Eich 第一次构想出这门语言时, 他给它起了个 Mocha 的代号. 在 Netscape 内部, LiveScript 的品牌已经使. 但是当公开命名语言时, 'JavaScript'赢得了投票.

Why?因为这门语言本来被设计来吸引大多数 Java 程序员观众,并且因为'script'这个单词在那个时间是受欢迎的用来指向轻量级程序. 这些轻量级'scripts'将会是第一批插入被称为新事物的 web 上的东西.

换句话说,JavaScript 是种营销策略,旨在将这门语言定位为当时写更重更知名的 Java 的合适的替代品. 由于这个关系,它可以和容易的被称为'WebJava'.

在 JavaScript 的代码和 Java 代码之间有一些表面的相似. 这个相似性并非特别来自共享开发,而是来自两种语言,针对开发人员,他们假定语法期望来自 C(在某种程度上,C++).

举个例子, 我们用`{`开始代码块,`}`来结束代码块,就像 C/C++和 Java. 我们也用`;`来强调一个语句的结束;

在某种程度上,法规关系比语法更深.甲骨文(通过 Sun),依然掌控和运营 Java 的公司, 也掌控'JavaScript'这个名字的的商标.这个商标机会从未被执行过,而且很可能在这点上不可能执行.(?)

由于这些原因,一些人建议我们用 JS 代替 JavaScript. 这是一个非常通用的简写,如果不是一个正式语言品牌自身的良好候选者.实际上,书籍几乎只使用 JS 来代指这门语言.

进一步将语言和 Oracle 拥有的商标区分开发, TC39 指定并由 ECMA 标准机构正式确定的语言的正式名称是 **ECMAScript**。事实上,自从 2016 年开始,这个正式的语言名称也以修订年为后缀;在撰写本文时,是 ECMAScript2019,或者缩写为 ES2019.

换句话说,运行在你浏览器或 Node.js 中的 JavaScript/JS,是 ES2019 标准的一个实现.

| 笔记:                                                                                                                    |
| :----------------------------------------------------------------------------------------------------------------------- |
| 不要用例如'JS6'或'ES8'的术语代指这门语言. 已有部分人这样做了,这些称呼只会导致长期的困惑. 'ES20XX'或仅'JS'是你应该坚持的. |

无论是你称呼它为 JavaScript, JS, ECMAScript, 或 ES2019, 它绝对不是一 Java 语言的翻版.

> "Java 对于 JavaScript 就像 ham(火腿)对于 hamster(仓鼠)." --Jeremy Keith, 2009

## 语言规范 Language Specification

我提到的 TC39, 管理 JS 的技术指导委员会. 它们的首要任务是管理语言的官方规范.它们按时开会来为已经同意的更改进行投票, 它们将提交到 ECMA, 这个标准组织.

JS 的语法和行为在 ES 规范中定义.

ES2019 碰巧是第 10 个主要编号规范/修正自从 1995 年 JS 发布以来, 所以由 ECMA 托管的规范的官方 URL 中, 你将会找到'10.0'.

https://www.ecma-international.org/ecma-262/10.0/

TC39 委员会由 50 到大概 100 个来自广泛网络投资公司的人组成, 例如浏览器厂商(Mozilla,Google, Apple)和设备厂商(三星等). 委员会所有成员是志愿者, 尽管它们中的很多人是这些公司的员工,因此可能会因为在委员会职责而获得补偿.

TC39 会议通常是每隔一个月,通常为期大约三天,来回顾自上月来成员完成的工作,讨论问题,且对提案投票. 会议地点在愿意组织的会员间轮换.

所有的 TC39 提案都经过一个 5 个阶段的流程,因为我们是程序员,它是以 0 为基准,从阶段 0 到阶段 4.你可以在这里阅读更多的阶段过程: http://tc39.es/process-document/

阶段 0 大致意味着,TC39 的某人认为这是一个有价值的想法并且计划支持和实施它. 这意味着非 TC39 成员通过非正式手段例如社交媒体或发布的博客'提出'的想法实际上是'前阶段 0'. 你必须得到一个 TC39 成员来支持提案,为这个提案正式被定义为'阶段 0'.

一旦一个提案到达'阶段 4'状态, 它是合格的可被包含在下一年度的语言修订中.一项提案到发挥作用通过这几个阶段可能从几个月到几年.

所有的提案开放管理,在 TC39 的 github 仓库: https://github.com/tc39/proposals

任何人,无论在 TC39 还是不在,都被欢迎参与正在解决的提案的公共讨论和进程.然而,只有 TC39 成员能参加会议和在提案和变更上投票.所以在影响力上,一个 TC39 成员的声音在 JS 将走向哪里有很重的影响力.

和一些既定和让人沮丧的长存神话不同,世界上不存在多个版本的 JavaScript.仅仅有**一个 JavaScript**, TC39 和 ECMA 制定的官方标准.

早在 2000 年初,当微软维护一个分支并反向工程(且不完全兼容)称为'JScript'的 JS 的版本, 有合理的多个版本的 JS.但是这些日子已经远去.今天做出如此关于 JS 的声明是过时和不准确的.

所有的主流浏览器和设备制造商承诺让他们的 JS 应用遵循当前核心规范.当然,在引擎不同时期实现功能.与 SpiderMonkey 引擎(Mozilla 的引擎)相比,永远不会出现这种情况, v8 引擎(Chrome 的 JS 引擎)实现指定的特效的不同或不兼容

这意味着你可以学习**一种 JS**,并在任意地方依赖相同的 JS.

### 关于 JS 的网页规范的所有事情

虽然运行 JS 的环境在不断扩展(从浏览器,到服务器(Node.js),到机器人,到灯泡,到...),管理 JS 的环境是 web.换句话说,如何在 web 浏览器中实现 JS 是唯一重要的事情.

从绝大部分来说,在规范中定义的 JS 和运行在基于浏览器 JS 引擎中的 JS 是一样的.但是有些差异必须考虑到.

有时 JS 规范将强加一些新的或改进的行为,可是并不精确匹配在它基于浏览器 JS 引擎中的工作方式.这种不匹配是历史性的: JS 引擎有 20 多年观察行为,围绕功能的一些细节,这些细节已经被网络内容所依赖.正因为如此,有时 JS 引擎将拒绝遵照规范指示变化因为规范变化将破坏网页内容.

在这些案例中, TC39 经常出尔反尔和轻易选择使规范遵循网页的实际情况.举个例子, TC39 计划为数组添加一个`contains()`方法,但是发现这个名字和在一些网站上让在使用的旧 JS 框架相冲突,所以它们更改这个名字为不冲突的`includes()`. 同样的情况发生在一个被称为'smooshgate'的喜剧/悲剧 JS*社区危机*上, 计划`flatten()`方法最终被命名为`flat()`.

但是偶然情况下, TC39 也将决定规范在一些点上的坚持即使基于浏览器的 JS 引擎将不太符合.

解决方案? 附录 B, "为 web 浏览器新增的 ECMAScript 特性". [^specapb]]JS 规范包括这个附录到细节 详细说明官方 JS 规范和网页上真实 JS 间的任何已知不匹配. 换句话说, 这些是只被允许在 web JS 上的例外; 其它 JS 环境必须遵循规范的确切意义.

B.1 和 B.2 章节涵盖 web JS 包括的 JS(语法和 APIS)的*额外内容*, 又因为历史原因, 但是 TC39 不打算在核心 JS 中声明. 包括`0`前缀的 8 进制文本,全局`escape()`/`unescape()`工具, 字符串"helpers"例如`anchor()`和`blink()`, 和正则`compile()`方法.

B.3 章节包括一些冲突,其代码可能运行在 web 和非 webJS 引擎之间,但是其行为*可能*明显不同, 导致不同的输出. 大多数列举的更改都涉及在严格模式下运行时被标为早期的错误的情况.

附录 B*gotchas*不经常遇到,但为了未来安全起见,避免使用这些结构仍然是一个好主意.

### 不是所有的(WEB)JS...

这个代码是 JS 程序吗?

```js
alert("Hello, JS!");
```

取决于你如何看待这件事情. `alert()`函数在这里展示是不包含在 JS 规范中的,但是它在所有 web JS 环境中都有.至此,你将在附录 B 中不会找到它,所以发生了什么?

不同的 JS 环境(例如浏览器 JS 引擎,Node.js, 等等)添加 APIs 到你 JS 程序的全局作用域提供给你环境规范的兼容性,例如在用户浏览器中有能力弹出 alert-style 盒子.

事实上, 一系列看起来像 JS 的 APIs, 例如`fetch()`,`getCurrentLocation()`,和`getUserMedia()`,是看起来像 JS 的所有 web APIs. 在 Node.js 中,我们能从不同的内建模块,例如`fs.write()`是访问数百个 APIs 方法.

另一个常见的案例是`console.log()`(和所有其它的`console.*`方法). 这些方法在 JS 中并没有被明确声明,但是由于它们的全局功能被相当多的 JS 环境所定义,根据大致商定的共识.

所以`alert()`和`console.log()`不是被 JS 定义的.但是它们*看起来*像 JS. 它们是函数和对象方法并且它们遵循 JS 语法规则. 它们背后的行为被运行 JS 引擎的环境约束,但是在表面上它们必须明确遵循 JS 以能够在 JS 环境中使用.

大多数人抱怨的跨浏览器差异都与“JS 太不一致了！”有关，但实际上这些差异是由于这些环境行为的工作方式不同，而不是 JS 本身工作方式不同。

所以一个`alert()`调用是 JS,但是`alert()`自身实际上仅是一个客户,不是官方 JS 规范的一部分.

### 它并不总是 JS

在你的浏览器开发者工具(或 Node)使用 console/REPL(读取-评估-打印-循环)第一眼感觉像非常直接的 JS 环境.但是,实际上,它不是.

开发者工具是...提供给开发者的工具.它们首要的目的是让开发者的生涯更简单.它们优先考虑 DX(开发者经验).

顺便一提,这个便利是一件不错的事情.我高兴开发者工具让开发者生涯更轻松! 我高兴我们拥有漂亮 UX 体验,例如变量/属性的自动完成等. 我只是指出一点我们不能也不应该期望工具*总是*严格遵循 JS 程序被处理的方式, 因为这不是哪些工具的目的.

因为这种工具在浏览器到浏览器上行为的变化,并且因为它们的变化(有时而不是经常),我不准备'硬编码'任何规范细节到这篇文章, 所以确保了这本书文字不会迅速过期.

但是我只是暗示一些在不同 JS 控制环境中不同的点上真实的怪异案例, 以增强我的观点,当使用它们时不要假设原生 JS 行为:

-   '在控制台顶级'顶级作用域中,一个`var`或`function`声明是否实际创建一个真实的全局变量(和镜像`window`属性,反之亦然)

-   在顶级作用域中,多个`let`和`const`声明将会发生什么.

-   Whether `"use strict";` on one line-entry (pressing `<enter>` after) enables strict mode for the rest of that console session, the way it would on the first line of a .js file, as well as whether you can use `"use strict";` beyond the "first line" and still get strict mode turned on for that session.

-   非严格模式下`this`默认绑定如何用于函数调用, 并且是否'全局对象'用来包含预期的全局变量.

-   提升(见第二本书籍, 作用域&闭包)如何用于跨越多个行入口.

-   ...若干其它部分

开发者控制台不应该伪装成 JS 编译器,该编译器处理你输入的代码和 JS 引擎处理 a.js 文件完全相同. 它视图让你轻松快速输入若干行代码并迅速看到结果. 这些是完全不同的使用案例,因此,希望一个工具来公平处理两方面是不合理的.

不要信任你在开发者工具中看到的行为代表精确的 JS 语义.为此,请阅读规范,相反,将控制台视为 JS 友好的环境. 这本身就很有用.

## 多张面孔

在程序语言上下文中的术语'paradigm(范式)'代表广泛(几乎是全部)思维方式和构建代码的方法.在一个范式内,有无数的风格和形式的变化来区分程序,包括无数不同库和框架,它们在任何给定的代码上都留下了独特的印记.

但是无论一个程序的独特风格可能是什么,围绕范式的大局划分几乎总是在任何程序的第一眼就非常明显. (???)

典型的范式类别代码包括程序化,面向对象(OO/类),和函数化(FP):

-   过程式风格通过自上而下的线性进程组织代码,通过预先确定的一组操作,通常收集在被称为过程的相关单元中.

-   OO 风格通过收集逻辑和数据到称为类的单元中来组织代码

-   FP 风格组织代码到函数中(和过程对反的纯计算),并且这些函数改编为值.

范式没有正确和错误之分.它们是组织和塑造程序员如何解决问题和方案,如何构造和维护代码的方向.

一些语言着重倾向一种范式-C 是过程化的,Java/C++几乎全是面向类的,Haskell 是完全的 FP.

但是很多语言也支持来自,甚至混合和匹配不同范式的代码风格.所以称作'多范式'的语言提供基本的扩展性.在一些例子中,一个单独的程序甚至能用两个或多个并排在一起的范式表达式.

JavaScript 是最直接的多范式语言.你可以写过程化(procedural),面向类(class-oriented),或函数程序(FP)风格的代码,你能在逐行做出这些决定,而不是被迫做出全有或全屋的选择.

## 向后和向前

引导 JavaScript 的一个最基础的原则是保留向后兼容. 很多人对这个术语的含义感到困惑,并且也经常将其与一个相关但是不同的术语混淆: _向前兼容_.

让我们澄清事实.

向后兼容意味着过去的东西被作为合法 JS 被接受,未来语言的任何更改都不会导致该代码成为无效 JS.在 1995 年写的代码-无论多么原始或有限,今天应该仍然有效.就像 TC39 成员经常宣称的那样,"我们不会破坏网页!"

这个想法是 JS 开发者可以带着自信写代码,他们的代码不会因为发布的浏览器更新而不可预测停止工作.这使得为程序选择 JS 在未来几年是更安全和明智的投资

这个'保证'不是一件小事情.维持向后兼容,跨越了这门语言几乎 25 年的历史,带来了巨大的负担和一系列独特的挑战. 你很难找到很多其它案例, 在计算这种向后兼容的承诺时.

坚持这个方案的花费不应该被轻易推卸(dismiss). 它必然创建一个高标准来为包含更改或扩展这门语言;任何决定(错误和所有的)都会永久有效.一旦这种情况出现在 JS 中,它不能被移出因为它可能破坏程序,即使我们真想真想移除它.

对这个规则来说有一些小例外. JS 曾有一些向后不兼容变化,但是 TC39 在这样做时非常小心.他们研究 web 上的代码(通过浏览器数据收集)来评估这种故障的影响,并且浏览器厂商最终决定并投票他们是否愿意为一个小规模的故障而承担用户的压力,相比之下修复或改进语言的某些方面为更多的网站(和用户)的受益.

这种类型的变化不多,并且几乎总是在很多网站中不太可能被观察到的稀少案例用法.

将_向后兼容_与它对应物_向前兼容_比较.向前兼容意味着语言包含一个新增,在程序中不会导致故障即使运行在比较旧的JS引擎中. **JS不是向前兼容的**,尽管很多人希望如此,甚至错误的相信它就是的神话.

与之相比,HTML和CSS是向前兼容但不是向后兼容.如果你挖掘在1995年写的一些HTML和CSS,它可能有可能在今天不起作用(或者一样工作). 但是,如果你在浏览器中使用2010到2019年的新特性,这个页面不会'故障'--这些未识别的CSS/HTML将会略过,而剩下的CSS/HTML将被相应处理.

在程序语言设计中包含向前兼容看起来让人满意,但是这样做通常不实用. 标签(HTML)和样式(CSS)本质上是声明式的,所以它很容易'跳过'无法识别的声明,对其它已识别的声明影响最小.

如果一个编程语言选择性的跳过它不理解的声明(或甚至是表达式)就会出现混乱和不确定性,因为不可能确保程序的后续部分不需要跳过的部分进行处理.

尽管JS不是,也不可能是向前兼容的,但需要充分认识到JS的向后兼容,包含对网页持续的好处和作为结果强加给JS的限制和困难.

### 跳过差距

既然JS不是向前兼容的,它就意味着在你写的合法JS和你网站或应用需要支持的最老的引擎之间总会有间隔. 如果你在2016年的引擎中使用ES2019特征运行程序, 你很有可能看到程序故障和崩溃.

如果这个特征是新语法,程序在编译和执行上会整体失败,通常抛出一个语法错误.如果这个特征是一个API(例如,ES6的`Object.is()`),程序可能运行到某个点随后抛出一个运行时异常,并在遇到未知API引用时停止.

这意味着JS开发者应该总是落后于进步的步伐, 只使用它们需要支持的最老JS引擎环境最后边缘的代码?不行!

但是它的确意味着JS开发者需要特别注意解决这个差距.

对新的且不适配的语法,解决方法是转译. 转译是一个人为和社区发明的术语,用来描述使用工具将程序源代码从一种形式到另一种形式(但是依然作为文本源码).通常,与语法相关向前兼容的问题通过使用转译器(最普遍的是Babel(https://babeljs.io))从新的JS语法版本转换为等效旧的语法来解决.

例如,开发者可能写这样的代码片段:

```js
if (something) {
    let x = 3;
    console.log(x);
} else {
    let x = 4;
    console.log(x);
}
```

这是应用程序的源码树中,这段代码的样子如下:

```js
var x$0, x$1;
if (something) {
    x$0 = 3;
    console.log(x$0);
} else {
    x$1 = 4;
    console.log(x$1);
}
```

最初的片段依赖于`let`来在`if`和`else`句子中创建块作用域的`x`变量,它们不会相互干扰. Babel能生成一个等效的程序(具有最小的重新工作),只是选择用不同的名称命名两个不同的变量,产生相同的非干扰的输出.

| 笔记:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `let`关键字在ES6(2015)中被添加.前面的转译案例只需要在应用程序需要在不支持ES6的JS环境中运行的情况下应用.这里的简单案例仅仅为简单说明.当ES6还是新标准,这种转译的需求是非常盛行的,但是在2020年需要支持非ES6环境是不常见的. 编译使用的'目标'是一个滑动窗口,只有在为某个网站/应用程序决定停止支持某个旧浏览器/引擎时才向上滑动.

你可能好奇:为什么这么麻烦使用工具来将新语法版本转换为旧版本?我们不能仅仅写着两个变量并跳过使用`let`关键字吗?原因是,开发者被强烈推荐使用JS最新版本所以它们代码是干净且能最大效率交流想法

开发者应该聚焦在写干净的新语法形式,让工具考虑生成该代码的向前兼容版本,该版本适合在最旧的支持JS引擎环境中部署和运行.

### 填补差距(Filling the Gaps)

如果向前兼容问题与新语法不相关,而是与只是最近添加的缺失API有关. 最通常的解决方案是为缺失API方法提供定义,它会扮演和老环境中已经原生定义过一样.这种模式被称为polyfill(别名'shim')

考虑这块代码:

```js
// getSomeRecords() returns us a promise for some
// data it will fetch
var pr = getSomeRecords();

// show the UI spinner while we get the data
startSpinner();

pr.then(renderRecords) // render if successful
    .catch(showError) // show an error if not
    .finally(hideSpinner); // always hide the spinner
```

这块代码使用ES2019的特征,promise原型上的`finally()`方法.如果代码在前ES2019环境中使用,`finally()`方法将不会存在,并且将发生一个错误.

在前ES2019环境中`finally()`方法的polyfill可能看起来是这样的:

```js
if (!Promise.prototype.finally) {
    Promise.prototype.finally = function f(fn) {
        return this.then(
            function t(v) {
                return Promise.resolve(fn()).then(function t() {
                    return v;
                });
            },
            function c(e) {
                return Promise.resolve(fn()).then(function t() {
                    throw e;
                });
            }
        );
    };
}
```

| 警告:                                                                                                                                                                                                                                                      |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 这只是“final（..） 的基本（不完全符合规范）polyfill 的简单说明`. 不要在你的代码中使用这个polyfill; 无论在哪里总是使用健壮,正式的polyfill, 就像在ES-Shim中polyfill/shims的集合. |

`if`语句通过阻止polyfill在JS引擎已经定义其方法的环境中执行,来保护polyfill定义.在旧环境中, polyfill已经定义,但在新环境中`if`语句会安静的跳过.

像Babel之类的编译器通常会检测你的代码需要的polyfills并且自动提供给你. 但是偶然情况下你可能需要精确的包含/定义它们, 与我们刚看过的snippet的作用类似.

始终以最合适的特点来编写代码,以有效传达意图和目的.通常来说,这意味着使用最稳定的JS版本. 通过尝试手动适应语法/api差距以避免影响代码的可读性. 这就是工具的目的.

转译器和补丁是两个最有效的技术来解决使用语言的最新稳定特征和旧环境中网站或应用需要依然支持代码之间的代沟.因为JS不会停止发展,代沟也不会消失.两种技术应该作为每个JS项目生产链的标准部分.

## 解析器中是什么?

在JS中编写代码的长期问题是: 它是一个解释节本或者是编译程序?主流的意见看起来JS是一种解释(脚本)语言.但是事实比这个复杂.

For much of the history of programming languages, "interpreted" languages and "scripting" languages have been looked down on as inferior compared to their compiled counterparts. The reasons for this acrimony are numerous, including the perception that there is a lack of performance optimization, as well as dislike of certain language characteristics, such as scripting languages generally using dynamic typing instead of the "more mature" statically typed languages.

Languages regarded as "compiled" usually produce a portable (binary) representation of the program that is distributed for execution later. Since we don't really observe that kind of model with JS (we distribute the source code, not the binary form), many claim that disqualifies JS from the category. In reality, the distribution model for a program's "executable" form has become drastically more varied and also less relevant over the last few decades; to the question at hand, it doesn't really matter so much anymore what form of a program gets passed around.

These misinformed claims and criticisms should be set aside. The real reason it matters to have a clear picture on whether JS is interpreted or compiled relates to the nature of how errors are handled.

Historically, scripted or interpreted languages were executed in generally a top-down and line-by-line fashion; there's typically not an initial pass through the program to process it before execution begins (see Figure 1).

<figure>
    <img src="images/fig1.png" width="650" alt="Interpreting a script to execute it" align="center">
    <figcaption><em>Fig. 1: Interpreted/Scripted Execution</em></figcaption>
    <br><br>
</figure>

In scripted or interpreted languages, an error on line 5 of a program won't be discovered until lines 1 through 4 have already executed. Notably, the error on line 5 might be due to a runtime condition, such as some variable or value having an unsuitable value for an operation, or it may be due to a malformed statement/command on that line. Depending on context, deferring error handling to the line the error occurs on may be a desirable or undesirable effect.

Compare that to languages which do go through a processing step (typically, called parsing) before any execution occurs, as illustrated in Figure 2:

<figure>
    <img src="images/fig2.png" width="650" alt="Parsing, compiling, and executing a program" align="center">
    <figcaption><em>Fig. 2: Parsing + Compilation + Execution</em></figcaption>
    <br><br>
</figure>

In this processing model, an invalid command (such as broken syntax) on line 5 would be caught during the parsing phase, before any execution has begun, and none of the program would run. For catching syntax (or otherwise "static") errors, generally it's preferred to know about them ahead of any doomed partial execution.

So what do "parsed" languages have in common with "compiled" languages? First, all compiled languages are parsed. So a parsed language is quite a ways down the road toward being compiled already. In classic compilation theory, the last remaining step after parsing is code generation: producing an executable form.

Once any source program has been fully parsed, it's very common that its subsequent execution will, in some form or fashion, include a translation from the parsed form of the program—usually called an Abstract Syntax Tree (AST)—to that executable form.

In other words, parsed languages usually also perform code generation before execution, so it's not that much of a stretch to say that, in spirit, they're compiled languages.

JS source code is parsed before it is executed. The specification requires as much, because it calls for "early errors"—statically determined errors in code, such as a duplicate parameter name—to be reported before the code starts executing. Those errors cannot be recognized without the code having been parsed.

So **JS is a parsed language**, but is it _compiled_?

The answer is closer to yes than no. The parsed JS is converted to an optimized (binary) form, and that "code" is subsequently executed (Figure 2); the engine does not commonly switch back into line-by-line execution (like Figure 1) mode after it has finished all the hard work of parsing—most languages/engines wouldn't, because that would be highly inefficient.

To be specific, this "compilation" produces a binary byte code (of sorts), which is then handed to the "JS virtual machine" to execute. Some like to say this VM is "interpreting" the byte code. But then that means Java, and a dozen other JVM-driven languages, for that matter, are interpreted rather than compiled. Of course, that contradicts the typical assertion that Java/etc are compiled languages.

Interestingly, while Java and JavaScript are very different languages, the question of interpreted/compiled is pretty closely related between them!

Another wrinkle is that JS engines can employ multiple passes of JIT (Just-In-Time) processing/optimization on the generated code (post parsing), which again could reasonably be labeled either "compilation" or "interpretation" depending on perspective. It's actually a fantastically complex situation under the hood of a JS engine.

So what do these nitty-gritty details boil down to? Step back and consider the entire flow of a JS source program:

1. After a program leaves a developer's editor, it gets transpiled by Babel, then packed by Webpack (and perhaps half a dozen other build processes), then it gets delivered in that very different form to a JS engine.

2. The JS engine parses the code to an AST.

3. Then the engine converts that AST to a kind-of byte code, a binary intermediate representation (IR), which is then refined/converted even further by the optimizing JIT compiler.

4. Finally, the JS VM executes the program.

To visualize those steps, again:

<figure>
    <img src="images/fig3.png" width="650" alt="Steps of JS compilation and execution" align="center">
    <figcaption><em>Fig. 3: Parsing, Compiling, and Executing JS</em></figcaption>
    <br><br>
</figure>

Is JS handled more like an interpreted, line-by-line script, as in Figure 1, or is it handled more like a compiled language that's processed in one-to-several passes first, before execution (as in Figures 2 and 3)?

I think it's clear that in spirit, if not in practice, **JS is a compiled language**.

And again, the reason that matters is, since JS is compiled, we are informed of static errors (such as malformed syntax) before our code is executed. That is a substantively different interaction model than we get with traditional "scripting" programs, and arguably more helpful!

### Web Assembly (WASM)

One dominating concern that has driven a significant amount of JS's evolution is performance, both how quickly JS can be parsed/compiled and how quickly that compiled code can be executed.

In 2013, engineers from Mozilla Firefox demonstrated a port of the Unreal 3 game engine from C to JS. The ability for this code to run in a browser JS engine at full 60fps performance was predicated on a set of optimizations that the JS engine could perform specifically because the JS version of the Unreal engine's code used a style of code that favored a subset of the JS language, named "ASM.js".

This subset is valid JS written in ways that are somewhat uncommon in normal coding, but which signal certain important typing information to the engine that allow it to make key optimizations. ASM.js was introduced as one way of addressing the pressures on the runtime performance of JS.

But it's important to note that ASM.js was never intended to be code that was authored by developers, but rather a representation of a program having been transpiled from another language (such as C), where these typing "annotations" were inserted automatically by the tooling.

Several years after ASM.js demonstrated the validity of tooling-created versions of programs that can be processed more efficiently by the JS engine, another group of engineers (also, initially, from Mozilla) released Web Assembly (WASM).

WASM is similar to ASM.js in that its original intent was to provide a path for non-JS programs (C, etc.) to be converted to a form that could run in the JS engine. Unlike ASM.js, WASM chose to additionally get around some of the inherent delays in JS parsing/compilation before a program can execute, by representing the program in a form that is entirely unlike JS.

WASM is a representation format more akin to Assembly (hence, its name) that can be processed by a JS engine by skipping the parsing/compilation that the JS engine normally does. The parsing/compilation of a WASM-targeted program happen ahead of time (AOT); what's distributed is a binary-packed program ready for the JS engine to execute with very minimal processing.

An initial motivation for WASM was clearly the potential performance improvements. While that continues to be a focus, WASM is additionally motivated by the desire to bring more parity for non-JS languages to the web platform. For example, if a language like Go supports threaded programming, but JS (the language) does not, WASM offers the potential for such a Go program to be converted to a form the JS engine can understand, without needing a threads feature in the JS language itself.

In other words, WASM relieves the pressure to add features to JS that are mostly/exclusively intended to be used by transpiled programs from other languages. That means JS feature development can be judged (by TC39) without being skewed by interests/demands in other language ecosystems, while still letting those languages have a viable path onto the web.

Another perspective on WASM that's emerging is, interestingly, not even directly related to the web (W). WASM is evolving to become a cross-platform virtual machine (VM) of sorts, where programs can be compiled once and run in a variety of different system environments.

So, WASM isn't only for the web, and WASM also isn't JS. Ironically, even though WASM runs in the JS engine, the JS language is one of the least suitable languages to source WASM programs with, because WASM relies heavily on static typing information. Even TypeScript (TS)—ostensibly, JS + static types—is not quite suitable (as it stands) to transpile to WASM, though language variants like AssemblyScript are attempting to bridge the gap between JS/TS and WASM.

This book isn't about WASM, so I won't spend much more time discussing it, except to make one final point. _Some_ folks have suggested WASM points to a future where JS is excised from, or minimized in, the web. These folks often harbor ill feelings about JS, and want some other language—any other language!—to replace it. Since WASM lets other languages run in the JS engine, on its face this isn't an entirely fanciful fairytale.

But let me just state simply: WASM will not replace JS. WASM significantly augments what the web (including JS) can accomplish. That's a great thing, entirely orthogonal to whether some people will use it as an escape hatch from having to write JS.

## *Strict*ly Speaking

Back in 2009 with the release of ES5, JS added _strict mode_ as an opt-in mechanism for encouraging better JS programs.

The benefits of strict mode far outweigh the costs, but old habits die hard and the inertia of existing (aka "legacy") code bases is really hard to shift. So sadly, more than 10 years later, strict mode's _optionality_ means that it's still not necessarily the default for JS programmers.

Why strict mode? Strict mode shouldn't be thought of as a restriction on what you can't do, but rather as a guide to the best way to do things so that the JS engine has the best chance of optimizing and efficiently running the code. Most JS code is worked on by teams of developers, so the _strict_-ness of strict mode (along with tooling like linters!) often helps collaboration on code by avoiding some of the more problematic mistakes that slip by in non-strict mode.

Most strict mode controls are in the form of _early errors_, meaning errors that aren't strictly syntax errors but are still thrown at compile time (before the code is run). For example, strict mode disallows naming two function parameters the same, and results in an early error. Some other strict mode controls are only observable at runtime, such as how `this` defaults to `undefined` instead of the global object.

Rather than fighting and arguing with strict mode, like a kid who just wants to defy whatever their parents tell them not to do, the best mindset is that strict mode is like a linter reminding you how JS _should_ be written to have the highest quality and best chance at performance. If you find yourself feeling handcuffed, trying to work around strict mode, that should be a blaring red warning flag that you need to back up and rethink the whole approach.

Strict mode is switched on per file with a special pragma (nothing allowed before it except comments/whitespace):

```js
// only whitespace and comments are allowed
// before the use-strict pragma
"use strict";
// the rest of the file runs in strict mode
```

| WARNING:                                                                                                                                                                                                                                                                                             |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Something to be aware of is that even a stray `;` all by itself appearing before the strict mode pragma will render the pragma useless; no errors are thrown because it's valid JS to have a string literal expression in a statement position, but it also will silently _not_ turn on strict mode! |

Strict mode can alternatively be turned on per-function scope, with exactly the same rules about its surroundings:

```js
function someOperations() {
    // whitespace and comments are fine here
    "use strict";

    // all this code will run in strict mode
}
```

Interestingly, if a file has strict mode turned on, the function-level strict mode pragmas are disallowed. So you have to pick one or the other.

The **only** valid reason to use a per-function approach to strict mode is when you are converting an existing non-strict mode program file and need to make the changes little by little over time. Otherwise, it's vastly better to simply turn strict mode on for the entire file/program.

Many have wondered if there would ever be a time when JS made strict mode the default? The answer is, almost certainly not. As we discussed earlier around backwards compatibility, if a JS engine update started assuming code was strict mode even if it's not marked as such, it's possible that this code would break as a result of strict mode's controls.

However, there are a few factors that reduce the future impact of this non-default "obscurity" of strict mode.

For one, virtually all transpiled code ends up in strict mode even if the original source code isn't written as such. Most JS code in production has been transpiled, so that means most JS is already adhering to strict mode. It's possible to undo that assumption, but you really have to go out of your way to do so, so it's highly unlikely.

Moreover, a wide shift is happening toward more/most new JS code being written using the ES6 module format. ES6 modules assume strict mode, so all code in such files is automatically defaulted to strict mode.

Taken together, strict mode is largely the de facto default even though technically it's not actually the default.

## Defined

JS is an implementation of the ECMAScript standard (version ES2019 as of this writing), which is guided by the TC39 committee and hosted by ECMA. It runs in browsers and other JS environments such as Node.js.

JS is a multi-paradigm language, meaning the syntax and capabilities allow a developer to mix and match (and bend and reshape!) concepts from various major paradigms, such as procedural, object-oriented (OO/classes), and functional (FP).

JS is a compiled language, meaning the tools (including the JS engine) process and verify a program (reporting any errors!) before it executes.

With our language now _defined_, let's start getting to know its ins and outs.

[^specapb]: ECMAScript 2019 Language Specification, Appendix B: Additional ECMAScript Features for Web Browsers, https://www.ecma-international.org/ecma-262/10.0/#sec-additional-ecmascript-features-for-web-browsers (latest as of time of this writing in January 2020)

### 注释

[什么是 smooshGate](https://tie.pub/2019/12/dont-break-the-web/)
