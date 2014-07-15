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

如果可选值是 `nil'，条件表达式将是 `false`，就不会执行括弧中的代码。否则，将会把值展开，并赋给 `let` 后面的常量，可以在后面的代码块中使用这个常量值。

switch 支持任意类型的数据，以及各种各样的比较操作 — 不限于整型和相等性检测。

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    let vegetableComment = "Add some raisins and make ants on a log."
case "cucumber", "watercress":
    let vegetableComment = "That would make a good tea sandwich."
case let x where x.hasSuffix("pepper"):
    let vegetableComment = "Is it a spicy \(x)?"
default:
    let vegetableComment = "Everything tastes good in soup."
}
```

> ####实验
> 移除上面代码中的 default 分支。观察一下会发生什么？

在执行完匹配上的 case 之后，程序会退出 switch 语句，并不会接着执行后续的 case。所以在 case 语句代码的尾部不需要明确写上 break。

使用 `for-in` 可以迭代字典中的每一项，每次可以获得一对键值。

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (kind, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
largest
```

> ####实验
> 添加另外一个变量来记录最大数字的类型。

使用 `while` 来重复执行代码块，直到条件发生改变。循环条件可以放在尾部，这样可以确保代码块至少运行一次。

```swift
var n = 2
while n < 100 {
    n = n * 2
}
n

var m = 2
do {
    m = m * 2
} while m < 100
m
```

在循环中可以使用索引 — 通过 `..<` 设置索引的范围或明确的写出初始值、条件和增量。下面的两个循环结果是一样的：

```swift
var firstForLoop = 0
for i in 0..<4 {
    firstForLoop += i
}
firstForLoop

var secondForLoop = 0
for var i = 0; i < 4; ++i {
    secondForLoop += i
}
secondForLoop
```

使用 `..<` 构建的范围忽略了上限值，而使用 `...<`构建的范围则包括上限和下限值。

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

在尖括弧里面写一个名称就能构建一个泛型函数或类型。

```swift
func repeat<ItemType>(item: ItemType, times: Int) -> [ItemType] {
    var result = [ItemType]()
    for i in 0..<times {
        result += item
    }
    return result
}
repeat("knock", 4)
```

我们不仅可以构建泛型函数和方法，还可以是泛型类、枚举和结构体。

```swift
// 重新实现了 Swift 标准库中的可选类型
enum OptionalValue<T> {
    case None
    case Some(T)
}
var possibleInteger: OptionalValue<Int> = .None
possibleInteger = .Some(100)
```

在类型名称后面可以使用 `where` 指定需求列表 — 例如，要求类型实现一个协议，要求两个类型都是相同的，或者要求一个类是继承自某个特定的类。

```swift
func anyCommonElements <T, U where T: Sequence, U: Sequence, T.GeneratorType.Element: Equatable, T.GeneratorType.Element == U.GeneratorType.Element> (lhs: T, rhs: U) -> Bool {
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])
```

> ####实验
> 修改 `anyCommonElements` 方法，让其返回一个数组，该数组中的值同时存在于两个序列中。

在编写简单的类时，可以忽略掉 `where` 关键字，只需要将协议或类名跟在一个冒号后面即可。例如 `<T: Equatable> ` 的写法与 `<T where T: Equatable>` 一样。
