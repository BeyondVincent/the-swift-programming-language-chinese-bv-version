# Swift 概述

>本节[苹果官方原文](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html)

---
本节目录
 * [简单的值](#simple_values)
 * [流程控制](#Control_Flow)
 * [函数和闭包](#Functions_and_Closures)
 * [对象和类](#Objects_and_Classes)
 * [枚举和结构体](#Enumerations_and_Structures)
 * [协议和扩展](#Protocols_and_Extensions)
 * [泛型](#Generics)
---

按照惯例，学习一门新的编程语言，写的第一个程序就是在屏幕中打印出 "Hello, World"。在 Swift 中，只需要一行代码就可以搞定：

```swift
println("Hello, world")
```

如果你写过 C 或 Objective-C 代码，那么上面用 Swift 写的代码你看起来应该眼熟，上面这行代码就是一个完整的程序。不需要 import 某个库来处理输入 / 输出，或做字符处理。写在全局范围的代码会被认作程序的入口点，所以 main 函数不是必须的。在语句尾部也不需要写分号。

这里的概述通过向你展示如何完成各种编程任务，提供足够多的信息来开始写 Swift 代码。本节中介绍的某些内容如果你不理解，也不用担心，在本书的后续章节中会做详细的解释。

> ####注意
> 为了最佳编程体验，在 Xcode 中以 playground 方式打开本章内容。Playground 允许我们编写代码边看结果。
>
> 打开 [Playground](https://github.com/BeyondVincent/the-swift-programming-language-chinese-bv-version/blob/master/1_welcome_to_swift/GuidedTour.playground.zip?raw=true)


<a name="simple_values"></a>
##简单的值

使用 `let` 关键字声明一个常量，而变量的声明则用 `var`。虽然不需要知道常量在编译时期的值，但是需要给常量做一次确定的赋值。这意味着用常量来命名一个值时只能一次完成，不过可以在多个地方使用。

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

一个常量或变量的类型必须与你希望给其赋值的类型相同。不过我们不需要总是把类型明确的标示出来。当创建一个常量或变量时，编译器会推断出所提供值的类型。在上面的示例中，编译器推断出 `myVariable` 的类型是一个整型。因为它的初始值是整型。

如果初始值不能提供足够多的信息 (或者没有初始值)，可以在变量名后面指定具体的类型，类型与变量名之间用冒号分开。

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

> ####实验
> 创建一个常量，其类型明确指定为 `Float`，并且初始值为 `4`。

值永远不会隐式的转换为另外一种类型。如果需要将值转换为另外一种不同的类型，需要根据所需类型创建一个实例。

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

> ####实验
> 将上面最后一行代码中的 `String` 移除，看看会出现什么错误？

在字符串中包含一个值还有更简单的方法：将值写在括弧中，然后在括弧前面写一个反斜线(\\)。例如：

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

> ####实验
> 在一个字符串中利用 `\\()` 包含一个浮点计算，以及对某人的问候。

使用括号 ([]) 创建一个数组和字典，并通过索引或括号中的 key 来访问里面的元素。

```swift
var shoppingList = ["catfish", "water", "tulips", "blue paint"]
shoppingList[1] = "bottle of water"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

要创建一个空数组或字典，可以使用初始化语法。

```swift
let emptyArray = [String]()
let emptyDictionary = Dictionary<String, Float>()
```

如果编译器能够推断出相关的类型，那么可以用 `[]` 代表空数组，`[:]` 代表空字典 — 例如，当你要给一个变量设置新的值，或给函数传递一个参数时。

```
shoppingList = []   // 去购物吧
```

<a name="Control_Flow"></a>
##流程控制

条件表达式使用 `if` 和 `switch` 关键字，而循环语句可以使用关键字`for-in`, `for`, `while` 和 `do-while`。条件表达式和循环语句附近的扩或是可选的，而里面的内容则必须要使用括弧。

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
teamScore
```

在 `if` 语句中，条件必须是布尔表达式 — 也就是说这样的代码 `if score { ... }` 是错误的，并不会隐式的比较为 0。

可以结合 `if` 和 `let` 一起使用，表示相关的值可能会缺失。这些相关的值表示可选的 (optional)。一个可选的值可以包含一个值，或者包含一个 `nil` (表示这个值缺失)。在值的类型后面写一个问号 (?) 表示这个值是可选的。

```swift
var optionalString: String? = "Hello"
optionalString == nil

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

> ####实验
> 将 `optionalName` 的值修改为 `nil`。看看得到什么结果？添加一个 `else` 分支，如果 `optionalName` 是 `nil` 时，设置不同的问候。


<a name="Functions_and_Closures"></a>
##函数和闭包

<a name="Objects_and_Classes"></a>
##对象和类


<a name="Enumerations_and_Structures"></a>
##枚举和结构体

<a name="Protocols_and_Extensions"></a>
##协议和扩展

<a name="Generics"></a>
##泛型

