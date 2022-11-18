#### 命名

- 私有属性、变量、方法以下划线\_开头

```
let _privateMethod={}
```

- 枚举变量 使用 Pascal 命名法。 枚举的属性， 使用全部字母大写，单词间下划线分隔的命名方式。

```
let TargetState = {
    READING: 1,
    READED: 2,
    APPLIED: 3,
    READY: 4
};
```

- boolean 类型的变量使用 is 或 has 开头

```
let isReady = false;
let hasMoreCommands = false;
```

- 声明提升
  var 声明会被提升至该作用域的顶部，但它们赋值不会提升。let 和 const 被赋予了一种称为「暂时性死区（Temporal Dead Zones, TDZ）」的概念。这对于了解为什么 typeof 不再安全相当重要。
  匿名函数表达式的变量名会被提升，但函数内容并不会。

```function example() {
  console.log(anonymous); // => undefined

  anonymous(); // => TypeError anonymous is not a function

  var anonymous = function() {
    console.log('anonymous function expression');
  };
}
```

#### 函数设计

函数设计基本原则：低耦合，高内聚。（假如一个程序有 50 个函数；一旦你修改其中一个函数，其他 49 个函数都需要做修改，这就是高耦合的后果。）

- 函数的长度，[建议] 一个函数的长度控制在 50 行以内。 将过多的逻辑单元混在一个大函数中，易导致难以维护。一个清晰易懂的函数应该完成单一的逻辑单元。复杂的操作应进一步抽取，通过函数的调用来体现流程。 特定算法等不可分割的逻辑允许例外。
- 参数设计
  [建议] 一个函数的参数控制在 6 个以内。
  解释：除去不定长参数以外，函数具备不同逻辑意义的参数建议控制在 6 个以内，过多参数会导致维护难度增大。某些情况下，如使用 AMD Loader 的 require 加载多个模块时，其 callback 可能会存在较多参数，因此对函数参数的个数不做强制限制。
  [建议] 通过 options 参数传递非数据输入型参数。解释：有些函数的参数并不是作为算法的输入，而是对算法的某些分支条件判断之用，此类参数建议通过一个 options 参数传递。

这种模式有几个显著的优势：

- boolean 型的配置项具备名称，从调用的代码上更易理解其表达的逻辑意义。
- 当配置项有增长时，无需无休止地增加参数个数，不会出现 removeElement(element, true, false, false, 3) 这样难以理解的调用代码。
- 当部分配置参数可选时，多个参数的形式非常难处理重载逻辑，而使用一个 options 对象只需判断属性是否存在，实现得以简化。
- 当你必须使用函数表达式（或传递一个匿名函数）时，使用箭头函数符号。因为箭头函数创造了新的一个 this 执行环境，通常情况下都能满足你的需求，而且这样的写法更为简洁。（ 参考 Arrow functions - JavaScript | MDN ）
- 如果你有一个相当复杂的函数，你或许可以把逻辑部分转移到一个函数声明上。

```
// Not recommended
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});
// Recommended
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;//如果一个函数适合用一行写出并且只有一个参数，那就把花括号、圆括号和 return 都省略掉。如果不是，那就不要省略。
});
```

- 块内函数必须用局部变量声明

```
// Not recommended
 var call = function(name) {
     if (name == "hotel") {
         function foo() {
             console.log("hotel foo");
         }
     }

     foo && foo();
 }

// Recommended
 var call = function(name) {
     var foo;

     if (name == "hotel") {
         foo = function() {
             console.log("hotel foo");
         }
     }

     foo && foo();
 }
```
