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
> 为了最佳编程体验，在 Xcode 中以 playground 方式打开本章内容。Playground 允许我们边写代码边看结果。
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

使用 `func` 来声明一个函数。通过在函数名称后面的括弧中跟上参数列表，就可以对函数进行调用。

```swift
func greet(name: String, day: String) -> String {
    return "Hello \(name), today is \(day)."
}
greet("Bob", "Tuesday")
```

> ####实验
> 移除掉上面代码中的 `day` 参数，然后添加一个参数，用来在问候中包含今天的午餐。

使用一个元祖 (tuple) 可以从一个函数中返回多个值。

```swift
func getGasPrices() -> (Double, Double, Double) {
    return (3.59, 3.69, 3.79)
}
getGasPrices()
```

函数同样可以接受可变参数，它会将这些参数封装进一个数组中。

```swift
func sumOf(numbers: Int...) -> Int {
    var sum = 0
    for number in numbers {
        sum += number
    }
    return sum
}
sumOf()
sumOf(42, 597, 12)
```

>####实验
> 写一个函数，用来计算出该函数中参数的平均值。

函数还可以嵌套。被嵌套的函数可以访问外部函数中定义的变量。我们可以用嵌套函数来编写长或复杂的代码。

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

swift 中的函数是 一等 (first-class) 类型。这就意味着一个函数可以将另外一个函数以值的方式返回。

```swift
func makeIncrementer() -> (Int -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

函数还可以当做参数传入到另外一个函数中。

```swift
func hasAnyMatches(list: [Int], condition: Int -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(numbers, lessThanTen)
```

函数实际上是一种特殊的闭包：可以在后面调用函数中的代码块。在闭包中的代码可以访问在创建闭包所在范围构建的内容，例如变量和函数，甚至是闭包在执行的时候可以访问不同范围的内容 — 例如上面介绍的嵌套函数。我们可以写没有名字的闭包，只需要将代码写在大括弧 (`{}`) 内即可。在闭包代码体内利用 `in` 关键字将参数和返回值与代码体分隔开。

```swift
numbers.map({
    (number: Int) -> Int in
    let result = 3 * number
    return result
    })
```

>####实验
> 重写上面的闭包代码，所有的奇数都返回 0。

有多种选择可以让编写的闭包代码更简洁。当已知闭包的类型时，例如调用一个 delegate，那么可以忽略掉它的参数和返回值。一行语句的闭包表示将返回语句的值。

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
mappedNumbers
```

对参数的引用可以用参数的位置来代替参数的名称 — 这种方法在很短的闭包中非常有用。一个闭包以最后一个参数传递给某个函数时，这个闭包可以立即跟在括弧后面。

```swift
let sortedNumbers = sorted(numbers) { $0 > $1 }
sortedNumbers
```

<a name="Objects_and_Classes"></a>
##对象和类

在 `class` 后面跟上类名就可以创建一个类。在类中，属性声明的写法与常量或者变量声明一样，唯一的区别就是它们的上下文处于类中。同样，函数和方法的声明也是一样的。

```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

>####实验
> 在上面的代码中用 `let` 添加一个常量属性，以及带一个参数的方法。

在类名后面跟上括弧就能创建一个类实例。使用 `.` 语法可以访问实例的属性和方法。

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

上面的 `Shape` 类缺少一些重要的内容：当创建类实例时所需要进行的初始化工作。我们使用 `init` 可以创建一个。

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

注意观察， `init` 中的 `self` 用来区分属性 `name` 和参数中的`name`。接收一个参数的初始化方法会在创建类的实例时被调用。每一个属性都需要被赋值 — 无论是在类中声明的 (例如 `numberOfSides`) 或者是在初始化方法中 (如 `name`)。

如果需要在对象销毁之前执行一些清理任务，可以利用实现一下 `deinit` 方法。

子类后面可以跟上父类，中间用冒号隔开。在 Swift 中不需要子类继承自某个标准的基类。所以根据需求，我们可以包含或者略去某个父类。

子类中的方法想要重写 (override) 父类中实现的方法，需要将其标记为 `override` — 如果重写了父类中的某个方法，但是没有 `override` 标记，编译器会检测出相关错误。另外如果在类中标记为 `override` 的方法，不存在于父类中，编译器同样会报错。

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() ->  Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

>####实验
> 构建另外一个基于 `NamedShape` 的子类：`Circle`，它的初始化方法接收两个参数：半径和姓名。并实现 `area` 和 `describe` 两个方法。

除了简单属性的存储外，属性还可以有 getter 和 setter。

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
    get {
        return 3.0 * sideLength
    }
    set {
        sideLength = newValue / 3.0
    }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
triangle.perimeter
triangle.perimeter = 9.9
triangle.sideLength
```

上面的代码中为 `perimeter` 编写了一个 setter，隐式的新值用命名为 `newValue`。在 `set` 后面可以写一个明确的名称在括号中。

注意 `EquilateralTriangle` 类的初始化方法中有 3 个不同的步骤：

1. 设置这个子类中声明属性的值。
2. 调用父类中的初始化方法。
3. 修改父类中定义的属性值。此处可以做一些额外的工作，例如使用方法，getters 或 setters。

如果你不需要对属性做计算，但是又想在属性设置新值之前和之后执行一些代码，那么请使用 `willSet` 和 `didSet`。例如，下面这个类总是能够确保三角形的边长与正方形的边长相等。

```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
    willSet {
        square.sideLength = newValue.sideLength
    }
    }
    var square: Square {
    willSet {
        triangle.sideLength = newValue.sideLength
    }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
triangleAndSquare.square.sideLength
triangleAndSquare.triangle.sideLength
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
triangleAndSquare.triangle.sideLength
```

类中的函数 (methods) 与普通方法 (functions) 有一个重要的区别。在普通方法中的参数名称只能用于方法内容，而类中函数的参数名称在调用该函数时需要用到 (除了第一个参数)。默认情况下，在调用函数或者函数内部时，，函数的参数名称与参数一样。当然，你可以指定另外一个名称，在函数内部使用。

```swift
class Counter {
    var count: Int = 0
    func incrementBy(amount: Int, numberOfTimes times: Int) {
        count += amount * times
    }
}
var counter = Counter()
counter.incrementBy(2, numberOfTimes: 7)
```

当使用可选值 (optional values) 时，可以在操作 (这些操作包括函数，属性和下标) 之前写一个 `?`。如果 `?` 前面的值是 `nil`，那么会忽略掉 `?` 后面的所有内容，并且整个表达式的值为 `nil`，否则可选值将被展开运行，所有 `?` 后面内容的运行结果将作为可选值。这两种情况下，整个表达式的值都是一个可选值。

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength

```


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
