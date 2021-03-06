# 基础知识

>本节[苹果官方原文](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html)

---
本节目录
 * [常量和变量](#Constants_and_Variables)
 * [注释](#Comments)
 * [分号](#Semicolons)
 * [整型](#Integers)
 * [浮点型数字](#Floating-Point_Numbers)
 * [类型安全和类型推断](#Type_Safety_and_Type_Inference)
 * [数字常量](#Numeric_Literals)
 * [数字类型转换](#Numberic_Type_Conversion)
 * [类型别名](#Type_Aliases)
 * [布尔值](#Booleans)
 * [元组](#Tuples)
 * [可选](#Optionals)
 * [断言](#Assertions)
---

Swift 是一门新的编程语言，用于 iOS 和 OS X 应用程序开发。尽管如此，Swift 中的许多内容与 C 和 Objective-C 相似。

Swift 有自己的一套基础类型，包括整型 `Int`；浮点值 `Double` 和 `Float`；布尔值 `Bool`；文本数据 `String`。Swift 同样提供了来非常重要的[集合类型](Collection_Types.html)：`Array` 和 `Dictionary`。

跟 C 类似，Swift 使用变量 (通过一个标示名称来表示) 来存储和引用值。Swift 同样使用了值不可变的变量，称之为常量，比 C 中的常量还要强大。在编程时，如果用到的值不需要改变，那么使用常量可以让代码更加的安全和整洁。

除了上面这些熟悉的类型，Swift 还引入了一些不存在于 Objective-C 中的高级类型，其中包括元组 (tuples)，通过元组，可以创建和传递一组值。通过元组，还可以从一个函数中返回多个值，就像一个复合值。

Swift 还引入了可选 (optional) 类型，用来处理值的缺失。`可选` 可以理解为 "有一个等于 x 的值"，或者 "值不存在"。`可选` 有点类似在 Objective-C 中使用 `nil` 指针，不过可选值可用于任意类型，不仅仅是类。可选值相比 Objective-C 中的 `nil` 指针来说，更安全，更具表现力，它也是 Swift 中许多强大功能的心脏。

`可选` 实际上是 Swift 类型安全语言的一个实例。使用 Swift 编程，可以帮助你清楚的知道代码中值的类型可以做什么。如果代码中期望传入的是一个 `String`，那么 Swift 的类型安全机制会防止你传入一个错误的 `Int`。这样可以帮助你在开发过程中，尽可能早的捕获并修正错误。

<a name="Constants_and_Variables"></a>
##常量和变量

常量和变量与一个名字关联 (例如 `maximumNumberOfLoginAttempts` 和 `welcomeMessage`)，附带跟上特定类型的一个值 (例如 数字 `10` 或 字符串 `Hello`)。常量的值一旦设定之后就不能再被改变，而变量可以在初始化之后设置不同的值。

###常量和变量的声明

常量和变量在使用之前，必须先声明。声明常量的关键字是 `let`，而变量的关键字是 `var`。下面的示例演示了如何用常量和变量记录用户尝试登录操作的次数：

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

上面的代码可以这样理解：

"声明一个名为 `maximumNumberOfLoginAttempts` 的常量，并给其赋值为 `10`。然后声明一个名为 `currentLoginAttempt` 的变量，并将其初始化为 `0`。"

上面的示例中，允许用户尝试登录最多次数声明为常量，因为这个值永远都不会改变。而当前尝试登录次数被声明为变量，这是因为每次尝试登录失败的话，这个值需要加 1。

可以在一行代码中声明多个常量或变量，只需要用逗号分隔开就行：

```swift
var x = 0.0, y = 0.0, z = 0.0
```

>####注意
>如果在代码中存储的值不会改变，那么总是用 `let` 关键字将其声明为常量。而变量只用于存储的值能够被改变。

###类型标注

在声明常量或变量时，可以提供一个类型标注，这样可以明确指定常量或变量可存储值的类型。类型标注的写法为：在常量或变量名后面写一个冒号，接着跟上一个空格符号，然后把要是用的类型名称写上即可。

下面的示例演示了通过提供一个类型标注，来声明一个名为 `welcomeMessage` 的变量，明确表示这个变量可以存储 `String` 值：

```swift
var welcomeMessage: String
```

声明中的冒号表示 "...类型..." (…of type…)，所以上面的代码可以理解为：
"声明一个名为 `welcomeMessage` 的变量，这个变量的类型是 `String`。"

语句 "类型是 `String`" 表示 "可以存储 `String` 值。"可以把它理解为 可以存储"值的类型"。

`welcomeMessage` 变量现在可以设置为任意的字符串，而不会报错：

```swift
welcomeMessage = "Hello"
```

可以在一行代码中声明多个相同类型的变量，变量之间用逗号隔开，在最后一个变量名之后，跟上冒号和类型标注即可。

```swift
var red, green, blue: Double
```

>####注意
>在实际代码编写中，我们很少需要写出类型标注。如果在声明变量或常量时，就提供了一个初始值，那么 Swift 几乎总是能够推断出常量或变量使用的类型，相关内容在[类型安全和类型推断](#Type_Safety_and_Type_Inference)中有描述。在上面 `welcomeMessage` 示例中，没有提供初始值，所以变量 `welcomeMessage` 的类型通过类型标注指定的，而不是用初始值推断出来的。

###常量和变量的命名

常量和变量的名称几乎可以使用你喜欢的任意字符，包括 Unicode 字符集：

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

常量和变量的名称不能包含数学符号，箭头，私用或无效的 Unicode 编码，以及横线 - 和 方格绘制 (box-drawing) 字符。虽然数字可以包含在名称中，名称但是不能以数字开头。

一旦将常量或变量声明为某个确定的类型，那么就不能用相同的名称对其重新声明，或者修改变量，使其存储另外一种不同的类型。也不可以把常量修改为变量，反过来也不行。

>####注意
>如果需要将常量或变量的名称声明为跟 Swift 预留关键字相同，可以使用反引号 (`) 将关键字包围起来，当做名称使用。不过，我们应该尽量避免将关键字当做常量或变量的名称使用，除非实在是没有别的选择了。

我们可以给已经拥有值的变量赋值另外一个兼容性的值。下面的示例中，`friendlyWelcome` 的值从 `Hello!` 变为 "Bonjour!"：

```swift
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

与变量相反，常量的值一旦赋值之后，就不能再被改变。如果尝试改变常量的值时，会出现编译错误：

```swift
let languageName = "Swift"
languageName = "Swift++"
// 这里会出现编译错误 - languageName 不能改变。
```

###出常量和变量的打印

通过 `println` 方法可以打印出常量或变量的当前值。

```swift
println(friendlyWelcome)
// 打印出 "Bonjour!"
```

`println` 是一个全局方法，用来打印一个值，后面会跟上一个换行符，以做出适当的输出。如果你使用的是 Xcode，`println` 会将结果输出至 Xcode 的 "console" 面板中。(另外一个方法 `print`，输出的结果是一样的，只不过不会在打印出值的尾部追加换行符。)

`println` 方法能打印出传入的任意 `String` 值：

```swift
println("This is a string")
// prints "This is a string"
```

`println` 方法可以打印出更复杂的消息，这跟 Cocoa 中的 NSLog 方法类似。这些消息可以是常量和变量的当前值。

Swift 利用字符插值的方法，在长的字符串中包含常量或变量的名称，来提示 Swift 的编译器用常量或变量的值替换掉名称所占的位置。具体方法是将名称封装在括弧中，然后在做括弧前面添加一个反斜杠，以进行转义。

```swift
println("The current value of friendlyWelcome is \(friendlyWelcome)")
// 打印出 "The current value of friendlyWelcome is Bonjour!"
```

>####注意
>关于字符插值的所有可选内容都在这里[字符插值](strings_and_characters.html#String_Interpolation)描述。

<a name="Comments"></a>
##注释

使用注释可以在代码中包括非执行文本内容，注释起到注意和提醒的作用。当代码被编译时，Swift 编译器会忽略掉注释内容。

Swift 中的注释与 C 中的非常相似。单行注释以两个正斜线 (//) 开始：
```swift
// 这里是注释
```

也可以写多行注释：开头是一个正斜线跟上一个星号 (/\*)，结尾是星号跟上一个正斜线 (*/)：

```swift
/* this is also a comment,
but written over multiple lines */
```

跟 C 中注释不同的地方时，Swift 的多行注释可以嵌套在另外的多行注释中。如下示例的嵌套注释，首先以第一个多行注释块开头，然后在第一个多行注释中开始写第二个多行注释部分，接着是第二个注释块结束，最后才是第一个注释块结束：

```swift
/* 这里是第一个多行注释块的开始
/* 这里是第二个被嵌套的多行注释块 */
这里是第一个多行注释块的结尾 */
```

通过嵌套的多行注释功能可以迅速并简单的注释掉大块代码，即使代码中包含多行注释也行之有效。

<a name="Semicolons"></a>
##分号

与其它大多数编程语言不同的是 Swift 不要求在每个语句后面写分号 (;)，当然，如果你想写，也没问题。不过要想在一行代码中写多个单独的语句，那么必须要加上分号才行：

```swift
let cat = "🐱"; println(cat)
// 打印出 "🐱"

```

<a name="Integers"></a>
##整型

整型就是整个数字中没有小数部分，例如 42 和 -23。整型包括有符号 (正数，0 或负数) 或 无符号 (正数或 0)。

Swift 提供的有符号和无符号整型包括 8，16，32 和 64 位。这些整型遵循类似 C 的命名约定，8 位有符号整型是 `UInt8`，32位的有符号整数是 `Int32`。跟 Swift 中的所有类型一样，这些整型都有相应的冠名了。

###整型范围

通过整型的 `min` 和 `max` 属性可以访问每个整型的最小值和最大值：

```swift
let minValue = UInt8.min  // minValue 等于 0, 类型是 UInt8
let maxValue = UInt8.max  // maxValue 等于 255, 类型是 UInt8
```

上面这些属性的值的类型都是根据整型的位数而定的 (例如 上面示例中的是 `UInt8`)。

###Int

大多数情况下，在代码中，不需要选择特定长度整型。Swift 提供了另外一种整型类型 `Int`，这种类型的长度与当前平台的本地字节码长度相同：

* 在 32位的平台，`Int` 的长度与 `Int32`一样。
* 在 64位的平台，`Int` 的长度与 `Int64`一样。

除非在代码中需要使用特定长度的整型，否则建议总是在代码中使用 `Int` 代表整型。这有利于代码的一致性和互操作性。在 32 位的平台中，`Int` 可以存储值的范围在 `-2,147,483,648` 和 `2,147,483,647` 之间，这对于常用的整数范围够用了。

###UInt

Swift 同样提供了一个无符号整型类型 `UInt`，它的长度与当前平台的本地字节码长度一样：

* 在 32位的平台，`UInt` 的长度与 `Int32`一样。
* 在 64位的平台，`UInt` 的长度与 `Int64`一样。

>####注意
>`UInt` 仅用于当需要与平台字节码长度一样的无符号整型。如果不是这种情况，那么建议使用 `Int`，即使存储的值不是负的。在代码中一致使用 `Int` 整型值有利于代码的互操作性，避免需要将不同的数字类型做转换，以及对整型的推断匹配，相关内容在[类型安全和类型推断](#Type_Safety_and_Type_Inference)中有描述。

<a name="Floating-Point_Numbers"></a>
##浮点型数字

浮点型数字 (floating-point numbers) 是带小数部分的数字，例如 `3.14159`，`0.1`，和 `-273.15`。

浮点型表达的值范围比整型更广，它能存储比整型更大或更小的数字。Swift 提供了两种有符号的浮点型数字类型：

* `Double` 代表 64 位的浮点数。当需要的浮点值必须很大或者要求高精度时，可以使用它。
* `Float` 代表 32 位的浮点数。当浮点值不需要 64 位精度时使用它。

>####注意
>`Double` 的精度至少是 15 位，而 `Float` 的精度是 6 位。具体浮点类型的使用取决于代码的性质和范围。

<a name="Type_Safety_and_Type_Inference"></a>
##类型安全和类型推断

Swift 是一门类型安全的语言。类型安全的语言鼓励你清楚的知道代码中值的类型的相关处理情况。如果代码中期望接收一个 `String`，那么不能传入一个错误的 `Int`。

由于 Swift 是类型安全的，在编译代码时，它会对类型做检查，并标记出任何错误的类型。这有助于在开发过程中尽早的发现和修复相关错误。

类型检查可以帮助我们在使用不同类型值时避免错误发生。当然这不是要求你在声明每一个常量和变量时必须指定相关的类型。如果你没有指定值的类型，Swift 会使用类型推断来计算出一个恰当的类型。当编译代码时，只需要根据提供的值，类型推断就能够使编译器自动推断出某个表达式的类型。

得益于类型推断，Swift 在声明变量或常量时，很少需要指定类型，这有别于其它编程语言，例如 C 和 Objective-C。常量和变量仍然是显示类型，只不过许多类型指定的工作编译器已经帮我们做好了。

当声明一个带有初始值的常量或变量时，类型推断非常有用。此时，一般给常量或变量赋值一个字面值 (literal value)，(常量值是直接出现在源码中的值，例如下面代码中的 `42` 和 `3.14159`)。

示例：如果给一个新的常量赋值一个常量值 `42`，声明过程中没有指明具体的类型，Swift 会推断出你想要的是一个 `Int` 常量，这是因为你用了一个看起来是整型的数字对常量进行赋值。

```swift
let meaningOfLife = 42
// meaningOfLife 将被推断为 `Int`
```

再比如，如在对一个浮点型常量值的初始化中没有指定类型，Swift 会将其推断为你想创建一个 `Double`。

```swift
let pi = 3.14159
// pi 将被推断为 `Double`
```

当对浮点型数字进行推断时，Swift 总是选择 `Double`，而不是 `Float`。

如果在一个表达式中对整型和浮点型的值进行相加操作时，那么最终的结果将被推断为 `Double`：

```swift
let anotherPi = 3 + 0.14159
// anotherPi 同样被推断为 `Double`
```

上面的表达式中，常量值 `3` 并没有明确指定类型，所以结合浮点值，Swift 将结果的类型推断为 `Double`。

<a name="Numeric_Literals"></a>
##数字常量

整型常量可以是：

* 十进制数字，不带前缀
* 二进制数字，以 `0b` 开头
* 八进制数字，以 `0o` 开头
* 十六进制数字，以 `0x` 开头

下面所有的整型常量的值转换为十进制后的值都是 `17`：

```swift
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 在二进制中的表示方法
let octalInteger = 0o21           // 17 在八进制中的表示方法
let hexadecimalInteger = 0x11     // 17 在十六进制中的表示方法
```

浮点型常量可以是十进制 (不带前缀)，或十六进制 (以 `0x` 开头)。这两种进制，在小数点的两端，都必须有数字。它们都可以有一个可选的指数，用一个大写字母或者小写字母表示,十进制浮点数用 `e` 表示，而十六进制浮点数则用 `p` 或 `P` 表示。

对于十进制数跟上一个指数 `exp`，表示基数乘以 10^exp：

* 1.25e2 表示 1.25 × 10^2, or 125.0.
* 1.25e-2 表示 1.25 × 10^-2, or 0.0125.

对于十六进制数跟上一个指数 `exp`，表示基数乘以 2^exp：

* 0xFp2 表示 15 × 2^2, or 60.0.
* 0xFp-2 表示 15 × 2^-2, or 3.75.

下面的这些浮点常量对应的十进制值都是 `12.1875`：

```swift
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

数字常量可以包含额外的格式，让其变得易读。整型和浮点型都可以用 0 补齐，以及下划线来增强其可读性。这两种方式都不会对常量值产生影响：

```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

<a name="Numberic_Type_Conversion"></a>
##数字类型转换

在代码中，使用 `Int` 类型当做声明整型常量和变量的通用类型，即使已经知道不会碰到负数。在代码中涉及到的整型常量和变量，使用默认的类型，可以直接在代码中进行操作，并且会直接匹配整型常量推断出的类型。

其它整型类型仅用于完成特定的任务，例如来自外部源的特定长度数据，或基于性能，内存使用或者其它的必要优化。在这些情况下，使用明确尺寸的类型有助于捕获任何意外的值溢出，以及隐式的记录了正在使用的数据的特性。

###整型转换

整型常量和变量能够存储数字的范围根据不同的类型，有所不同。 一个 `Int8` 常量或变量可以存储的数字范围在 `-128` 到 `127` 之间，而一个 `UInt8` 常量或变量可以存储的数字范围在 `0` 到 `255`之间。如果一个数字不适合存储到某类型的变量或常量中时，当编译代码时，会有相关错误提示：

```swift
let cannotBeNegative: UInt8 = -1
// UInt8 不能存储负数，所以此处将报错。
let tooBig: Int8 = Int8.max + 1
// Int8 不能存储大于其最大值的一个值，所以此处将报错。
```

由于每一种整型的存储范围都是不同的，

###整型和浮点型转换

<a name="Type_Aliases"></a>
##类型别名

<a name="Booleans"></a>
##布尔值

<a name="Tuples"></a>
##元组

<a name="Optionals"></a>
##可选

<a name="Assertions"></a>
##断言
