
## 小码哥swift进阶

   * [小码哥swift进阶](#小码哥swift进阶)
      * [1. 编译器](#1-编译器)
      * [2. switch 使用](#2-switch-使用)
      * [3. where 使用](#3-where-使用)
      * [4. 函数](#4-函数)
         * [4.1 隐式返回](#41-隐式返回)
         * [4.2 多返回值（元祖）](#42-多返回值元祖)
         * [4.3 参数标签](#43-参数标签)
         * [4.4 inout](#44-inout)
         * [4.5 函数重载](#45-函数重载)
         * [4.6 高阶函数](#46-高阶函数)
         * [4.7 @discardableResult](#47-discardableresult)
      * [5. 枚举（值类型）](#5-枚举值类型)
         * [5.1 未指定类型](#51-未指定类型)
         * [5.2 关联值](#52-关联值)
         * [5.3 指定类型、指定值](#53-指定类型指定值)
         * [5.4 默认值](#54-默认值)
      * [6. Optional](#6-optional)
         * [6.1 本质](#61-本质)
      * [7. 结构体和类](#7-结构体和类)
      * [8. 闭包](#8-闭包)
         * [8.1 自动闭包](#81-自动闭包)
         * [8.2 尾随闭包](#82-尾随闭包)
         * [8.3 逃逸闭包](#83-逃逸闭包)
      * [9. 属性](#9-属性)
      * [10. subscript](#10-subscript)
      * [11. 继承](#11-继承)
      * [12. 初始化](#12-初始化)
         * [12.1 调用规则：](#121-调用规则)
         * [12.2 两段初始化](#122-两段初始化)
         * [12.3 重写](#123-重写)
         * [12.4 自动继承](#124-自动继承)
         * [12.5 required](#125-required)
         * [12.6 可失败初始化器](#126-可失败初始化器)
         * [12.7 deinit](#127-deinit)
      * [13. 协议](#13-协议)
         * [13.1 定义属性和方法](#131-定义属性和方法)
         * [13.2 构造器](#132-构造器)
         * [13.3 限定类型](#133-限定类型)
         * [13.4 检验协议的一致性](#134-检验协议的一致性)
         * [13.5 可选协议](#135-可选协议)
         * [13.6 协议扩展](#136-协议扩展)
      * [14 错误处理](#14-错误处理)
         * [14.1 自定义错误](#141-自定义错误)
         * [14.2 处理错误](#142-处理错误)
      * [15 泛型](#15-泛型)
         * [15.1 泛型函数](#151-泛型函数)
         * [15.2 泛型类型](#152-泛型类型)
         * [15.3 关联类型](#153-关联类型)
         * [15.4 泛型约束](#154-泛型约束)
         * [15.5 类型擦除](#155-类型擦除)
      * [16 高级运算符](#16-高级运算符)
         * [16.1 溢出运算符](#161-溢出运算符)
         * [16.2 重载运算符](#162-重载运算符)
         * [16.3 Equatable](#163-equatable)
         * [16.4 Comparable](#164-comparable)
      * [17 swift 指针](#17-swift-指针)
      * [18 字面量](#18-字面量)
      * [19 更多](#19-更多)
         * [19.1 MARK、TODO、FIXME](#191-marktodofixme)
         * [19.2 条件编译](#192-条件编译)
         * [19.3 系统版本判断](#193-系统版本判断)
         * [19.4 API可用](#194-api可用)
         * [19.5 KVO、KVC](#195-kvokvc)
* [Swift Advance](#swift-advance)
   * [一、内建集合](#一内建集合)
      * [1. 数组](#1-数组)
         * [1.1 写时复制](#11-写时复制)
         * [1.2 高阶函数](#12-高阶函数)
         * [1.3 切片](#13-切片)
         * [1.4 数组字面量](#14-数组字面量)
      * [2.字典](#2字典)
         * [2.1 哈希表](#21-哈希表)
         * [2.2 字典字面量](#22-字典字面量)
   * [二、集合类型协议](#二集合类型协议)
      * [1. Sequence（序列）](#1-sequence序列)
         * [1.1 自定义一个序列](#11-自定义一个序列)
         * [1.2 for - in 与迭代器](#12-for---in-与迭代器)
      * [2. Collection（集合）](#2-collection集合)
         * [2.1 IndexingIterator](#21-indexingiterator)
         * [2.2 Slice（切片）](#22-slice切片)
      * [4. Codable协议](#4-codable协议)
         * [Codable 序列化与反序列化](#codable-序列化与反序列化)




### 1. 编译器

* 编译器架构

  > （前端(frontEnd)，优化器(Optimizer)、后端(backEnd)）

  ![img](https://tva1.sinaimg.cn/large/008i3skNgy1gw9x04nihcj30gw03aa9y.jpg)

* ***LLVM***架构

![img](https://tva1.sinaimg.cn/large/008i3skNgy1gw9x2cqc21j30hw0780sz.jpg)



> 1. 不同的前端后端使用统一的中间代码LLVM Intermediate Representation (LLVM IR)
> 2. 如果需要支持一种新的编程语言，那么只需要实现一个新的前端
> 3. 如果需要支持一种新的硬件设备，那么只需要实现一个新的后端
> 4. 优化阶段是一个通用的阶段，它针对的是统一的LLVM IR，不论是支持新的编程语言，还是支持新的硬件设备，都不需要对优化阶段做修改
> 5. 相比之下，GCC的前端和后端没分得太开，前端后端耦合在了一起。所以GCC为了支持一门新的语言，或者为了支持一个新的目标平台，就 变得特别困难
> 6. LLVM现在被作为实现各种静态和运行时编译语言的通用基础结构(GCC家族、Java、.NET、Python、Ruby、Scheme、Haskell、D等)



* ***Clang***

  > Clang是一个由Apple主导编写，基于LLVM的C/C++/Objective-C编译器（前端）



* ***swift***编译步骤

  swift源码经过`parse解析`、`ast编译`，生成`AST语法树` 

  > swiftc -dump-ast target.swift >> ast.swift

  通过`SIL生成器`生成`SIL源码`

  > swiftc -emit-sil target.swift >> ./target.sil

  生成`IR中间代码`

  > swiftc -emit-ir target.swift >> ir.swift

  输出`.o机器文件`

  > swiftc -emit-object target.swift

  

### 2. switch 使用

```swift
/// 单个条件
enum BOOL { case YES, NO, Other }
let a = BOOL.YES
switch a {
    case .YES:
        print("true")
    default: break
}

/// 多个条件
switch a {
		case .YES, .NO:
        print("true or false")
    default: break
}
```

```swift
/// 区间匹配
let a = 10
switch a {
case 0 ..< 60:
    print("不及格")
case 60 ... 100:
    print("及格")
default: break
}
```

```swift
/// 元祖匹配+值绑定
let a = (0, Data())
switch a {
case (let code, let response):
    print(code, response)
default: break
}

switch a {
case (_ , let response):
    print(response)
default: break
}

/// 指定值
switch a {
case (400 , let response):
    print(response)
default: break
}

/// 指区间
switch a {
case (200 ..< 300 , let response):
    print(response)
default: break
}

/// 使用 where 条件
let a = (0, Data())
switch a {
case (let code, let response) where response.count > 0 :
    print(response)
default: break
}
```



### 3. where 使用

> 可以在`switch` `for in` `泛型` `协议`中使用

```swift
/// 1.switch
var value:(Int,String) = (1,"小明")
switch value {
case let (x,_) where x < 60:
    print("不及格")
default:
    print("及格")
}

/// 2.for in
let arrayOne = [1,2,3,4,5]
let dictionary = [1:"hehe1",2:"hehe2"]
for i in arrayOne where dictionary[i] != nil {
    print(i)
}

/// 3.泛型
func genericFunction<S>(str:S) where S:ExpressibleByStringLiteral{
    print(str)
}
// 也可以不使用where语句，直接在尖括号中定义时做限制
func genericFunction2<S:ExpressibleByStringLiteral>(str:S){
    print(str)
}

/// 4.协议
protocol aProtocol{}
extension aProtocol where Self:UIView{
    //只给遵守myProtocol协议的UIView添加了扩展
    func getString() -> String{
        return "string"
    }
}
```



### 4. 函数

> 函数所有的参数、返回值都是let不可变类型



#### 4.1 隐式返回

> 单一表达式可以省略`return`

```swift
func sum(a:Int, b:Int) -> Int {
  a + b
}
```

#### 4.2 多返回值（元祖）

```swift
func sum(a:Int, b:Int) -> (String, String) {
 	(String(a), String(b))
}
```

#### 4.3 参数标签

```swift
/// 修改参数名
func check(with number:Int) {
    print(number)
}

/// 省略参数名
func check(_ name:String) {
    print(name)
}

check(with: 10)
check("xiaoming")
```

#### 4.4 inout

> 函数参数为结构体时，是以值传递的方式，函数内部不会修改变量值。使用**inout**修饰为传递地址，可修改外部变量

1. 调用函数是参数加 **&** 符号
2. 参数是不能有默认值的，有范围的参数集合也不能被修饰

* 如果实参有物理内存地址，且没有设置属性观察器口直接将实参的内存地址传入函数（实参进行弓｝用传递）
* 如果实参是计算属性或者设置了属性观察器 , 采取了***Copy In Copy Out*** 的做法了调用该函数时，先复制实参的值，产生副本 `get`  了将副本的内存地址传入函数（副本进行引用传递），在函数内部可以修改副本的值了函数返回后，再将副本的值覆盖实参的值 `set `

```swift
func check(with number:inout Int) {
   	number = number + 10
}

var num = 10
check(with: &num)
print(num)
/// 20
```

#### 4.5 函数重载

> 函数名相同的函数，在参数不同时的重载

* **重点：**函数重载只针对参数 

1. 参数个数不同
2. 参数类型不同
3. 参数标签不同

#### 4.6 高阶函数

> 返回值或参数是函数类型的函数，叫做高阶函数



#### 4.7 @discardableResult

> 消除函数调用后返回值未被使用的警告









### 5. 枚举（值类型）

> 1. 可以看成一个提供特定几种情况的实例，不同与结构体和类（提供初始化方法生成实例）
> 2. 作为值类型，枚举可以保存方法，不能保存存储属性

#### 5.1 未指定类型

```swift
enum PathType {
    case defaultPath, horizontal, vertical
}
```

#### 5.2 关联值

```swift
enum PathType {
    case defaultPath(String), horizontal(Int), vertical
}
```

#### 5.3 指定类型、指定值

```swift
enum PathType: String{
    case defaultPath = "defaultPath", horizontal = "horizontal", vertical = "vertical"
}
```

#### 5.4 默认值

```swift
///默认 defaultPath = "defaultPath", horizontal = "horizontal", vertical = "vertical"
enum PathType: String {
    case defaultPath, horizontal, vertical
}

/// 默认 defaultPath = 0, horizontal = 1, vertical= 2
enum PathType: Int {
    case defaultPath, horizontal, vertical
}
```



### 6. Optional

```swift
/// 多重可选
var a:Int? = 10
var b:Int?? = 10
/// 使用 frame variable -R 或者 fr v -R 查看结构
/// a -> (Swift.Optional<Swift.Int>) a = some 
/// b -> (Swift.Optional<Swift.Optional<Swift.Int>>) 

```

#### 6.1 本质

> 可选项的本质是**enum**类型

```swift
public enum Optional<Wrapped> : ExpressibleByNilLiteral { 
    case none 
  	case some(Wrapped)
  	public init(_ some:Wrapped)
}
```



### 7. 结构体和类

> 在 Swift 标准库中，绝大多数的公开类型都是结构体，而枚举和类只占很小一部分。

结构体和类的主要不同点:

* 结构体(和枚举)是值类型，而类是引用类型。在设计结构体时，我们可以要求编译器保证不可变性。而对于类来说，我们就得自己来确保这件事情。

- 内存的管理方式有所不同。结构体可以被直接持有及访问，但是类的实例只能通过引用 来间接地访问。结构体不会被引用，但是会被复制。也就是说，结构体的持有者是唯一 的，但是类却能有很多个持有者。
- 使用类，我们可以通过继承来共享代码。而结构体(以及枚举)是不能被继承的。想要在 不同的结构体或者枚举之间共享代码，我们需要使用不同的技术，比如像是组合、泛型 以及协议扩展等。
- 结构体作为值类型是不能被修改的，若要修改，必须加`mutating`

* ***结构体***和***类***的内存分配

  ```swift
  /// 函数调用，内存在栈中
  func test() {
    /// 结构体值类型，栈
    let size = Size()
    /// 对象，Point()在堆中分配内存，point在栈中持有Point()的内存地址
    let point = Point()
  }
  
  /// 类
  class Size {
    var width = 1
    var height = 1
  }
  
  /// 结构体
  struct Point {
    var x = 0
    var y = 0
  }
  ```

* 分配内存流程

  * Class.___allocating_inint()_
  * libswiftCore.dylib: ___swift_allocObject_
  * libswiftCore.dylib: _swift_slowAlloc_
  * libsystem_malloc.dylib: _malloc_



### 8. 闭包

> 要打破引用循环，我们需要确保其中一个引用要么是 **weak**，要么是 **unowned**

**weak** 引用表 示不增加引用计数，并且当被引用的对象被释放时，将该 weak 引用自身设置为 **nil**

对每个 **unowned** 的引用，Swift 运行时将为这个对象维护另外一个引用计数。当所有的 strong 引用消失时，对象将把它的资源 (比如对其他对象的引用) 释放掉。不过，这个对象本身的内存 将继续存在，直到所有的 **unowned** 引用也都消失。这部分内存将被标记为无效 (有时候我们也 把它叫做僵尸 (zombie) 内存)，当我们试图访问这样的 **unowned** 引用时，就会发生运行时错 误。

不过注意这其实并不是未定义的行为。我们还有第三种选择，那就是 **unowned**(unsafe)，它不 会做运行时的检查。当我们访问一个已经无效的 **unowned**(unsafe) 引用时，这时候结果将是未 定义的。

#### 8.1 自动闭包

```swift
/// 1. 传参类型和闭包返回值类型一致
/// 2. 闭包不能包含参数
func count(a:Int, b:@autoclosure ()-> String) -> Double {
		return Double(b().count + a)
}

/// 将"123"自动包装为闭包
print(count(a: 2, b: "123"))
```

#### 8.2 尾随闭包

```swift
/// 闭包作为最后一个参数, 可以书写在函数括号之后的闭包表达式
func count(b: (Int)-> Int) {
    print(b(5))
}
count{ $0 * $0 }
```

#### 8.3 逃逸闭包

```swift
/**  非逃逸闭包的生命周期：

1. 把闭包作为参数传递给函数。
2. 函数中运行该闭包。
3. 退出函数。

非逃逸闭包被限制在函数内，当函数退出时，该闭包的引用计数不会增加，也就是说其引用计数在进入函数和退出函数时保持不变。
*/

/** 逃逸闭包
当一个闭包作为参数传到一个函数中，但是这个闭包在函数返回之后才被执行，我们称该闭包从函数中逃逸。
逃逸闭包生命周期长于相关函数，当函数退出时，逃逸闭包的引用仍然被其他对象持有，不会再相关函数结束后释放。
闭包参数默认是非逃逸类型。如果需要其逃逸类型的闭包，可以使用关键字@escaping
*/
```



### 9. 属性

属性可分为2大类：

* 存储属性（stored property）
  * 存储在实例的内存中
  * 结构体、类可以定义存储属性，枚举不可以

* 计算属性（computed property）
  * 本质是函数
  * 不占用实例内存
  * 枚举、extension、结构体、类都可以定义计算属性
  * inout，因为计算属性不占用实例内存，使用inout时，会先复制一份属性值（get值）保存在内存中，将该内存地址传人函数，在函数内部可以修改内存中的数据，函数结束后，再将内存中的数据覆盖属性值（set值）

```swift
struct Student {
    /// 存储属性
    var name: String
    /// 存储属性 + 属性观察器(实例初始化函数中设置不会触发观察器、属性初始化不会触发观察器)
    var money:Double {
        didSet {
            print(money)
        }
    }
    /// 懒加载存储属性（Student的实例必须是var可变才能访问lazy属性，因为time会在懒加载时改变结构体内存）
    lazy var time:Date = Date()
    
    /// 计算属性
    var height: Double {
        get {
            180.0
        }
        set {
            print(newValue)
        }
    }
  	/// 计算属性（可以只有get方法，只有get方法时，可省略get）
    var age: Int {
        return 3
    }
}
```



* 单例模式

```swift
/// 将init私有化
class Student {
  	static let share = Student()
	  private init(){}
}
```



### 10. subscript

> 通过下标获取元素
>
> 可提供多个参数
>
> ***enum、protocol、extension、struct、class*** 都可以使用`subscript`提供下标功能

* `subscript `和计算属性类似，需要提供`get`(必须)，`set`(可选)方法
* `subscript`返回值的类型就是`set`方法`newValue`的类型，调用`set`也必须提供相同类型

```swift
extension Array{
    subscript(index value:Int) -> Element{
        get {
            guard count > value else { return self[count - 1] }
            return self[value]
        }
        set {
            guard count > value else {
                debugPrint("index out of range")
                return
            }
            self[value] = newValue
        }
    }
}

var array = [1,2,3,4]
print(array[index: 4])
array[index: 4] = 200

/// 4 
/// "index out of range"

```

 

* 我认为`subscript`主要用于***enum、protocol、extension、struct、class***包含***Collection***时通过***下标***访问元素更直观，比如`Alamofire`中的`HTTPHeader`

```swift
public struct HTTPHeaders {
    private var headers: [HTTPHeader] = []
    public init(_ headers: [HTTPHeader]) {
        self.init()

        headers.forEach { update($0) }
    }
    public subscript(_ name: String) -> String? {
        get { value(for: name) }
        set {
            if let value = newValue {
                update(name: name, value: value)
            } else {
                remove(name: name)
            }
        }
    }
}

/// HTTPHeaders将headers私有，直接使用下标访问headers元素
var headers = HTTPHeaders([HTTPHeader(name: "a", value: "100"), HTTPHeader(name: "b", value: "300")])
print(headers["a"])
headers["a"] = "200"
```



### 11. 继承

* 只有类支持继承，值类型（枚举、结构体）不支持
* 子类可以重写父类的**subscript、func、property **
* 如果不希望被继承可使用**final**修饰，不希望被重写使用**final、static**修饰，使用***class***修饰的**subscript、func、property(计算类型) **可以被重写
* 属性（存储、计算）可以重写为计算属性，不能重写为存储属性
* 只能重写**var**属性，不能重写**let**属性
* 父类的**readOnly**可以重写为**readWrite**，父类的**readWrite**不能重写为**readOnly**





### 12. 初始化

> 类、结构体、枚举都可以定义初始化器 
>
> 类有两种初始化器：**指定初始化器(designated initializer)**、**便捷初始化器(convenience initializer)**



#### 12.1 调用规则：

* 指定初始化器是类的主要初始化器， 每个类至少有一个。
* 指定初始化器必须调用父类的指定初始化器。
* 便捷初始化器非必需，但是每个便捷初始化器都必须调用一个本类中的指定初始化器。
* 便捷初始化器也可以调用本类中的其他便捷初始化器。

![截屏2021-12-16 下午4.47.49](https://tva1.sinaimg.cn/large/008i3skNly1gxfrs4dwb4j30ud0u041h.jpg)

#### 12.2 两段初始化

* 第一阶段：初始化所有存储属性
  * 当前类中指定初始化器确保所有存储属性都完成初始化
  * 当前类中指定初始化器调用父类指定初始化器，不断向上，确保所有父类的存储属性初始化完毕。

* 第二阶段：self初始化完毕，可以使用
  * 所有存储属性初始化完毕，可以使用`self`访问、修改属性，调用实例方法等。



#### 12.3 重写

* 重写父类指定初始化器时，必须加上`override`
* 重写父类的便捷初始化器，不用加`override`，因为子类不能调用父类的便捷初始化器，所以严格意义上不算重写



#### 12.4 自动继承

* 如果子类没有自定义任何指定初始化器，它会自动继承父类所有的指定初始化器

* 如果子类提供了父类所有指定初始化器的实现(要么通过方式1继承，要么重写) ，子类自动继承所有的父类便捷初始化器  
* 就算子类添加了更多的便捷初始化器，这些规则仍然适用  
* 子类以便捷初始化器的形式重写父类的指定初始化器，也可以作为满足规则2的一部分 



#### 12.5 required

* 用`required`修饰指定初始化器，表明其所有子类都必须实现该初始化器(通过继承或者重写实现) 
* 如果子类重写了`required`初始化器，也必须加上`required`，不用加`override`		 					 			



#### 12.6 可失败初始化器

* 类、结构体、枚举都可以使用init?定义可失败初始化器

* 不允许同时定义参数标签、参数个数、参数类型相同的可失败初始化器和非可失败初始化器  
* 可以用init!定义隐式解包的可失败初始化器  
* 可失败初始化器可以调用非可失败初始化器，非可失败初始化器调用可失败初始化器需要进行解包  
* 如果初始化器调用一个可失败初始化器导致初始化失败，那么整个初始化过程都失败，并且之后的代码都停止执行 
* 可以用一个非可失败初始化器重写一个可失败初始化器，但反过来是不行的 				



#### 12.7 deinit

* 父类的deinit能被子类继承  
* 子类的deinit实现执行完毕后会调用父类的deinit 							 					 		







### 13. 协议

> 协议规定了用来实现某一特定功能所必需的方法和属性。
>
> 任意能够满足协议要求的类型被称为遵循(conform)这个协议。
>
> 类，结构体或枚举类型都可以遵循协议，并提供具体实现来完成协议定义的方法和功能



#### 13.1 定义属性和方法

* **实例属性、类属性**不能确定是计算属性还是存储属性，由遵守协议的实现来决定。
* 协议中的通常用`var`来声明变量属性，必须指明是只读的还是可读可写的，`{ set get }`可读可写，`{ get }`只读。
* **类型方法、类型属性**只能使用`static`修饰
* **结构体、枚举**在方法的实现中修改**存储属性**，必须使用`mutating`修饰



```swift
protocol classa {
  	/// 读写
    var marks: Int { get set }
  	/// 只读
    var result: Bool { get }
    
  	/// 实例方法
    func attendance() -> String
    /// 类型方法
  	static func markssecured() -> String
}
```



#### 13.2 构造器

* 构造器实现必须使用`required`修饰
* 构造器实现可以为**指定构造器**或**便利构造器**

```swift
protocol dha {
    var name:String { get set }
    init(name:String)
}

class mada:dha {
    var name: String = "ddd"
    required convenience init(name: String) {
        self.init()
        self.name = name
    }
}
```

* 如果一个子类重写了父类的指定构造器，并且该构造器遵循了某个协议的规定，那么该构造器的实现需要被同时标示`required`和`override`修饰符

```swift
class Dama {
    init(name:String){
        
    }
}
class SubDama: Dama, dha {
    var name: String = ""
    required override init(name: String) {
        super.init(name: "")
        self.name = name
    }
}
```



#### 13.3 限定类型

>`Self`代表当前类型、`self`代表当前实例
>
>`Person.self`是一个元类型（metadata）的指针，存放着类型相关信息
>
>`Person.Type`是`Person.self`的类型 `var type: Person.Type = Person.self`, 一般用于类型传递

```swift
/// 仅支持类,不支持结构体、枚举，使用AnyObject
protocol dha: AnyObject{
}

/// 仅扩展实现该协议的UIView类型
extension dha where Self: UIView {
}

/// 仅扩展特定泛型协议
extension Collection where Element: Equatable {
}
```



#### 13.4 检验协议的一致性

使用is和as操作符来检查是否遵循某一协议或强制转化为某一类型。

- `is`操作符用来检查实例是否`遵循`了某个`协议`。
- `as?`返回一个可选值，当实例`遵循`协议时，返回该协议类型;否则返回`nil`。
- `as`用以强制向下转型，如果强转失败，会引起运行时错误。



#### 13.5 可选协议

- 使用关键字`optional`来指明
- 协议和可选需求都必须用`@objc`标记
- `@objc`协议只能由继承自Objective-C类或其他`@objc`类的类使用，结构体或枚举不能使用



#### 13.6 协议扩展

- 可以对协议进行扩展，为遵守协议的类型提供方法、构造器、下标和计算属性的实现。

```swift
extension dha {
    func sette() {
        print(name)
    }
}
```



### 14 错误处理

```swift
/// Error 协议
public protocol Error : Sendable {
}
```



#### 14.1 自定义错误

* 通过实现`Error`协议自定义错误

```swift
enum IntParsingError: Error {
	case overflow
	case invalidInput(Character)
}
```

* 通过`throw`抛出自定义`Error`，可能抛出错误的函数上加上`throws`声明

```swift
 extension Int {
	init(validating input: String) throws {
		let c = _nextCharacter(from: input)
		if !_isValid(c) {
			throw IntParsingError.invalidInput(c)
		}
	}
}
```



#### 14.2 处理错误

* 使用`try`调用可能抛出`Error`的函数
* 使用`do-catch`捕捉`Error`

```swift
 do {
     let price = try Int(validating: "$100")
 } catch IntParsingError.invalidInput(let invalid) {
     print("Invalid character: '\(invalid)'")
 } catch IntParsingError.overflow {
     print("Overflow error")
 } catch {
     print("Other error")
 }
 // Prints "Invalid character: '$'"
```

* 不捕捉`Error`, 在当前函数增加`throws`声明, 会自动抛给上层函数处理，如果顶层函数依然没有捕捉Error，那么程序将终止

```swift
func test() throws {
	try Int(validating: "$100")
}
```



* `try?、try!` 不处理`Error`
  * `try?` 返回一个可选值，当有错误出现时，返回`nil`
  * `try!`表明不会出现错误，当有错误抛出时，程序将终止

* 当函数内，调用闭包可能抛出错误时，函数需要加上`rethrows`

```swift
func test(fn:(Int) throws -> Int, num: Int) rethrows {
	try fn(num)
}
```



* `defer`: 定义任何方式（抛出错误、`return`）离开代码块前都必须要执行的代码
* `assert`断言
  * 不符合指定条件就抛出运行时错误，常用于调试阶段的条件判断
  * 只会在**Debug**模式下生效， **Release**模式会忽略

```swift
 func divide(_ v1: Int, _ v2: Int) -> Int {
    assert(v2 != 0, "除数不能为0")
		return v1 / v2
 }
 print(divide(20, 0))
```



* `fatalError`: 遇到严重错误，希望程序直接结束(`try-catch`无法捕捉)
  * 使用了`fatalError`就不用写`return`了
  * 在某些不得不实现、但不希望别人调用的方法，可以使用`fatalError`

```swift
class Person { required init() {} } class Student : Person {
required init() { fatalError("don't call Student.init") }
    init(score: Int) {}
}
var stu1 = Student(score: 98) var stu2 = Student()
```





### 15 泛型

> 通过泛型将类型参数化，抽取成为通用代码，提高代码复用率，减少代码量



#### 15.1 泛型函数

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```



#### 15.2 泛型类型

```swift
struct Stack<Element> {
    var items: [Element] = []
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
```



#### 15.3 关联类型

> 给协议中使用泛型需要用到`associatedtype`， 协议中可以拥有多个关联类型。

```swift
protocol Container {
    associatedtype Item: Equatable
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

```

为什么使用`associatedtype`, 而不是`<T>`?

* protocol Container<T> {} 代表了这是一个不确定类型的协议，遵循它的类可以实现多种`Container`, 这是没有必要的，而`associatedtype`代表了`Container`是唯一的泛型协议，遵循者只能实现一次。



#### 15.4 泛型约束

```swift
// 继承约束使用格式
func 函数名<泛型: 父类>(参数列表) -> 返回值 {
// 函数体，泛型类型是某个类的子类类型
}
// 协议约束使用格式
func 函数名<泛型: 协议>(参数列表) -> 返回值 {
// 函数体，泛型类型遵循某些协议
}

// 继承、协议组合
func 函数名<泛型: 父类&协议>(参数列表) -> 返回值 {
// 函数体，泛型类型遵循某些协议
}

// 条件约束使用格式
func 函数名<泛型1, 泛型2 where 条件>(参数列表) -> 返回值 {
// 函数体，泛型类型满足某些条件

```





#### 15.5 类型擦除

> 协议可以作为类型来使用，但是泛型协议却无法直接作为类型使用



```swift
protocol Generator {
    associatedtype AbstractType
    func generate() -> AbstractType
}

struct IntGenerator: Generator {
    typealias AbstractType = Int
    
    func generate() -> Int {
        return 0
    }
}

struct StringGenerator: Generator {
    typealias AbstractType = String
    
    func generate() -> String {
        return "zero"
    }
}

// 报错 Protocol 'Generator' can only be used as a generic constraint because it has Self or associated type requirements
let value: Generator = arc4random()%2 == 0 ? IntGenerator() : StringStore()
```





* 使用类型擦除

  > 把泛型协议封装成的具体类型，其本质就是对泛型协议进行了 **类型擦除（Type Erase）**，从而解决了泛型类型的存储问题。

```swift
struct GeneratorThunk<T>: Generator {
    private let _generate: () -> T
    
    init<G: Generator>(_ gen: G) where G.AbstractType == T {
        _generate = gen.generate
    }
    
    func generate() -> T {
        return _generate()
    }
}

let gens: GeneratorThunk<String> = GeneratorThunk(StringGenerator())
```



* 使用 **some** 声明不透明类型

```swift
let value: some Generator = arc4random()%2 == 0 ? IntGenerator() : StringStore()
```





### 16 高级运算符



#### 16.1 溢出运算符

> swift的算数运算出现溢出时会抛出运行时错误
>
> 使用`&+、&-、&*`, 支持溢出运算

```swift
var min = UInt8.min
var max = UInt8.max
/// 255
print(min &- 1)
/// 0
print(max &+ 1)
/// 254
print(max &* 2)
```



#### 16.2 重载运算符

> 类、结构体、枚举可以为现有运算符提供自定义实现

```swift
struct Point {  
	var x: Int, y: Int 
  static func + (p1: Point, p2: Point) -> Point { 	
	  	Point(x: p1.x + p2.x, y: p1.y + p2.y) 
  } 							
} 							 					 				
```



#### 16.3 Equatable 

> 遵循`Equatable`，并重载`==`就可以使用`==`判断2个实例是否等价，引用类型使用`===、!==`比较地址是否相同。
>
> 以下类型会提供`Equatable`默认实现
>
> 1. 没有关联类型的枚举
> 2. 只拥有遵循`Equatable`协议关联类型的枚举
> 3. 只拥有遵循`Equatable`协议存储属性的结构体



#### 16.4 Comparable

> 比较2个实例大小
>
> 1. 遵循`Comparable`协议
> 2. 重载比较运算符





### 17 swift 指针

Swift中也有专门的指针类型，这些都被定性为“Unsafe”(不安全的)，常见的有以下4种类型 ：

* `UnsafePointer<Pointee>` 类似于 `const Pointee * `
* `UnsafeMutablePointer<Pointee> `类似于 `Pointee *  `
* `UnsafeRawPointer` 类似于 `const void * 					`			
* `UnsafeMutableRawPointer` 类似于` void * 			`	



```swift
var age = 10 
func test1(_ ptr: UnsafeMutablePointer<Int>) { 							
  ptr.pointee += 10 
} 							

func test2(_ ptr: UnsafePointer<Int>) { 
  print(ptr.pointee) 			
}

test1(&age)
test2(&age) // 20		 
```



### 18 字面量

> Swift自带的绝大部分类型，都支持直接通过字面量进行初始化
> `Bool、Int、Float、Double、String、Array、Dictionary、Set、Optional`



```swift
var age = 10 
var isRed = false 
var name = "Jack"					 					 					
```

Swift自带类型之所以能够通过字面量初始化，是因为它们遵守了对应的协议  

* Bool : ExpressibleByBooleanLiteral 
* Int : ExpressibleByIntegerLiteral 
* Float、Double : ExpressibleByIntegerLiteral、ExpressibleByFloatLiteral
* Dictionary : ExpressibleByDictionaryLiteral 								
* String : ExpressibleByStringLiteral 
* Array、Set : ExpressibleByArrayLiteral
* Optional : ExpressibleByNilLiteral





### 19 更多

#### 19.1 MARK、TODO、FIXME

*  // MARK: - 类似于OC中的 #pragma mark - 
*  // TODO: 用于标记未完成的任务  
*  // FIXME: 用于标记待修复的问题 



#### 19.2 条件编译

```swift
// 操作系统:macOS\iOS\tvOS\watchOS\Linux\Android\Windows\FreeBSD
#if os(macOS) || os(iOS)  
// CPU架构:i386\x86_64\arm\arm64 
#elseif arch(x86_64) || arch(arm64) 							
// swift版本  
#elseif swift(<5) && swift(>=3)  
// 模拟器  
#elseif targetEnvironment(simulator) 
// 可以导入某模块  
#elseif canImport(Foundation)  
#else  
#endif 							 				
```



#### 19.3 系统版本判断

```swift
if #available(iOS 10, macOS 10.12, *) {
  // 对于iOS平台，只在iOS10及以上版本执行 
  // 对于macOS平台，只在macOS 10.12及以上版本执行 
  // 最后的*表示在其他所有平台都执行 					
} 							 
```



#### 19.4 API可用

```swift
@available(iOS 10, macOS 10.15, *)
class Person {}
struct Student {
    @available(*, unavailable, renamed: "study")
    func study_() {}
    func study() {}
    @available(iOS, deprecated: 11)
    @available(macOS, deprecated: 10.12)
    func run() {}
}
```



#### 19.5 KVO、KVC



> Swift 支持 KVC \ KVO 的条件 
>
> * 属性所在的类、监听器最终继承自 NSObject 
>
> * @objc dynamic 修饰对应的属性

```swift
 class Person: NSObject {  
   @objc dynamic var age: Int = 0   
   var observer: Observer = Observer()  
   override init() {
     super.init()      
     self.addObserver(observer,
                      forKeyPath: "age",       
                      options: .new,             
                      context: nil)} 
   deinit { 					
     self.removeObserver(observer,  
                         forKeyPath: "age") 
   } } 								

```

































# Swift Advance



## 一、内建集合

### 1. 数组

#### 1.1 写时复制

> 写时复制: 复制时用的是一个内存地址，当某一个集合改变时恰到好处的复制了一份出来

>  Swift 中，所有的基本类型，包括整数、浮点数、字符串、数组和字典等都是值类型，并且都以结构体的形式实现，那么每次赋值时都会复制，而Swift使用了写时复制来优化了内存



```swift
var x = [6,6,6]
// 浅拷贝
var y = x
// 深拷贝
y.append(6)
y // [6,6,6,6]
x // [6,6,6]
```

#### 1.2 高阶函数

>高阶函数：接受函数或闭包(匿名函数)作为参数，即：使用函数将行为参数化、不关心函数的实现（由调用者提供）
>
>map: 文档注释为 transformed elements，即元素变形
>
>flatMap：1. 一围数组遍历去除nil元素，已废弃，需使用compactMap， 2. 多维数组遍历为一围数组。
>
>compactMap：flatMap废弃，一围数组遍历去除nil元素。
>
>reduce：把数组元素组合计算为一个值，并且会接受一个初始值，这个初始值的类型可以和数组元素类型不同
>
>filter：根据条件筛选



> Closure(闭包) 可以捕获自身作用域之外的变量的函数

```swift
/// 闭包
let block = { value -> Int in
		return value * 2
}
/// 函数
func multiply(number:Int) -> Int{
		return number * 2
}
let multiply = multiply(number:)

/// multiply: (Int) -> Int 	
/// multiply.self (Function)

/// block: (Int) -> Int
/// block.self (Function)
```



```swift
/// 1. Map 接收一个 (Element) -> T 的函数
/// func map<T>(_ transform: (Element) throws -> T) rethrows -> [T]
let values = [10,20,30]
/// 传递一个闭包或函数
values.map(block)
values.map(multiply(number:))
/// 闭包简写
values.map{ $0 * 2 }
// [20, 40, 60]

/// 2. flatMap
let numbers = [[1, 2, 3], [4, 5], [6]]
let flatMapped = numbers.flatMap { $0 }
// [1, 2, 3, 4, 5, 6]

/// 3. compactMap
let possibleNumbers = ["1", "2", "three", "///4///", "5"]
let mapped: [Int?] = possibleNumbers.map { str in Int(str) }
// [1, 2, nil, nil, 5]
let compactMapped: [Int] = possibleNumbers.compactMap { Int($0) }
// [1, 2, 5]

/// 4. reduce
let sum = values.reduce(5,+)
// 5 + 10 + 20 + 30 = 65
```



```swift
/// for in 与 forEach 区别
/// 1. for in 可以添加条件语句
for idx in self.indices where self[idx] == element { return idx
}
/// 2. return 可以直接结束 for in循环，forEach不行。
/// 3. forEach是闭包
```



####  1.3 切片 

> 获取某个范围中的元素，我们可以使用`切片`
>
> 切片类型只是数组的一种表示方式，它背后的 数据仍然是原来的数组，只不过是用切片的方式来进行表示。这意味着原来的数组并不需要被 复制。ArraySlice 具有的方法和 Array 上定义的方法是一致的，因此你可以把它们当做数组来 进行处理。如果你需要将切片转换为数组的话，你可以通过将切片传递给 Array 的构建方法来 完成

```swift
let numbers = [1, 2, 3, 4, 5, 6]
let slice = numbers[2..<numbers.endIndex]
let slice = numbers[3...]
let slice = numbers[3<..]
let slice = numbers[3..<5]
/// [3, 4, 5, 6]
/// slice 的类型是 ArraySlice 而不是 Array
```

#### 1.4 数组字面量

```swift
public protocol ExpressibleByArrayLiteral {

    /// The type of the elements of an array literal.
    associatedtype ArrayLiteralElement

    /// Creates an instance initialized with the given elements.
    init(arrayLiteral elements: Self.ArrayLiteralElement...)
}
```



### 2.字典

> 字典的本质是哈希表（本质数组），通过键的hashValue来确定每个键的位置，所以key必须要准守Hashable协议, 如果要将对象存储到 `Dictionary` 中，就要遵循 `Hashable` 协议及其扩展协议 `Equatable`。

#### 2.1 哈希表

> 解决哈希冲突的三种方法（拉链「链表」）、开放地址法、再哈希法）

`Swift4.1` 之前， 要符合 `Equatable` 的要求，你需要提供一个 `==` 操作符的实现。要符合 `Hashable` 的要求，你需要提供⼀个名为 `hashValue` 的计算属性:

```swift
// Swift < 4.1
extension Color: Hashable {
    static func ==(lhs: Color, rhs: Color) -> Bool {
        return lhs.red == rhs.red &&
               lhs.green == rhs.green &&
               lhs.blue == rhs.blue
    }
  
    var hashValue: Int {
         return self.red.hashValue ^
      					self.green.hashValue ^
      					self.blue.hashValue
   	}
}

let cyan = Color(red: 0x00, green: 0xFF, blue: 0xFF)
let yellow = Color(red: 0xFF, green: 0xFF, blue: 0x00)
cyan.hashValue == yellow.hashValue // true, collision
```

`swift4.1`已经帮我们实现了上面的步骤

编译器会自动合成您的自定义类型的Hashable和要求：

- 对于结构，其所有存储的属性必须遵循Hashable。
- 对于枚举，其所有关联值必须遵循Hashable。 （即使没有声明，没有关联值的枚举也具有Hashable一致性。）

`Swift 4.2` 通过引入 `Hasher` 类型并采用新的通用哈希函数进一步优化 `Hashable`, 现在，如果你要自定义类型实现 `Hashable` 的方式，可以重写 `hash(into:)` 方法而不是 `hashValue`。`hash(into:)` 通过传递了一个 `Hasher` 引用对象，然后通过这个对象调用 `combine(_:)` 来添加类型的必要状态信息。`== `的实现通过调用`hash(into:)`，再通过`hasher.finalize()`获取`hashValue`对比判断是否相等。

```swift
// Swift >= 4.2
class Color: Hashable {
    let red: UInt8
    let green: UInt8
    let blue: UInt8

    // Synthesized by compiler
    func hash(into hasher: inout Hasher) {
        hasher.combine(self.red)
        hasher.combine(self.green)
        hasher.combine(self.blue)
    }
  
    static func == (lhs: Color, rhs: Color) -> Bool {
        var lhsHasher = Hasher()
        var rhsHasher = Hasher()
        lhs.hash(into: &lhsHasher)
        rhs.hash(into: &rhsHasher)
        return lhsHasher.finalize() == rhsHasher.finalize()
    }
}

let cyan = Color(red: 0x00, green: 0xFF, blue: 0xFF)
let yellow = Color(red: 0xFF, green: 0xFF, blue: 0x00)
cyan.hashValue == yellow.hashValue // false, no collision
```

#### 2.2 字典字面量

```swift
public protocol ExpressibleByDictionaryLiteral {
    /// The key type of a dictionary literal.
    associatedtype Key

    /// The value type of a dictionary literal.
    associatedtype Value

    /// Creates an instance initialized with the given key-value pairs.
    init(dictionaryLiteral elements: (Self.Key, Self.Value)...)
}
```



## 二、集合类型协议

> 1. Array，Dictionary 和 Set 这些内建集合都是实现Sequence 和 Collection(继承Sequence) 协议
> 2. sequence 对于 next 闭包的使用是被延迟的。也就是说， 序列的下一个值不会被预先计算，它只在调用者需要的时候生成
> 3. 对于序列和集合来说，它们之间的一个重要区别就是序列可以是无限的，而集合则不行



### 1. Sequence（序列）

> 一个序列 (sequence) 代表的是一系列具有相同类型的值，你可以对这些值进行迭代

```swift
/// 序列
protocol Sequence {
    /// A type representing the sequence's elements.
    associatedtype Element where Self.Element == Self.Iterator.Element

    /// A type that provides the sequence's iteration interface and
    /// encapsulates its iteration state.
    associatedtype Iterator : IteratorProtocol

    /// Returns an iterator over the elements of this sequence.
    func makeIterator() -> Self.Iterator
}

/// 迭代器
protocol IteratorProtocol {
    /// The type of element traversed by the iterator.
    associatedtype Element
  
    /// The following example shows how an iterator can be used explicitly to
    /// emulate a `for`-`in` loop. First, retrieve a sequence's iterator, and
    /// then call the iterator's `next()` method until it returns `nil`.
    ///
    ///     let numbers = [2, 3, 5, 7]
    ///     var numbersIterator = numbers.makeIterator()
    ///
    ///     while let num = numbersIterator.next() {
    ///         print(num)
    ///     }
    ///     // Prints "2"
    ///     // Prints "3"
    ///     // Prints "5"
    ///     // Prints "7"
    ///
    /// - Returns: The next element in the underlying sequence, if a next element
    ///   exists; otherwise, `nil`.
    mutating func next() -> Self.Element?
}
```



#### 1.1 自定义一个序列

```swift
/// 创建迭代器(Iterator)
struct XIterator:IteratorProtocol {
    typealias Element = String
    mutating func next() -> String? {
    }
}

/// 创建序列(sequence)
struct XSequence: Sequence {
    var string: String
    func makeIterator() -> XIterator {
        return XIterator()
    }
}

/// 使用迭代器
func use() {
  var iterator = XSequence().makeIterator()
  while let element = iterator.next() {
		doSomething(with: element) 
  }
}
```



#### 1.2 for - in 与迭代器

> `Swift` ` for-in` 实际使用`Iterator` 调用 `next()`来进行迭代

```swift
/// 迭代器复制了animals的元素保存在element中，在迭代过程中操作数组，不会产生任何影响
var animals = ["Antelope", "Butterfly", "Camel", "Dolphin"] 

var animalIterator = animals.makeIterator()
while let animal = animalIterator.next() {
  	print(animal)
  	animals.removeLast()
}
```

> ` for-in` 和 `forEach ` 区别

```swift
/// forEach 不会终止迭代，仅仅是从闭包中返回
(1..<10).forEach { number in print ( number)
		if number > 2 { return }
}
```

```swift
/// for-in return会终止迭代
for item in (1 ..< 10) {
    if item > 2{ return }
}

/// for-in 可以添加 where 条件
for item in (1 ..< 10) where item % 2 == 0  {
    print(item)
}
```



### 2. Collection（集合）

> Collection 协议是建立在 Sequence 协议上的，和Sequence不同的是Collection不能是无限的。
>
> 官方解释：`Collection`是一个`element`可以被多次遍历的`Sequence`，非破坏性，并通过索引下标访问。

 

```swift
/// To add `Collection` conformance to your type, you must declare at least the following requirements:
/// - The `startIndex` and `endIndex` properties
/// - A subscript that provides at least read-only access to your type's elements
/// - The `index(after:)` method for advancing an index into your collection
protocol Collection: Sequence { 
	/// 一个非空集合中首个元素的位置
	var startIndex: Index { get }
	/// 集合中超过末位的位置，也就是比最后一个有效下标值大 1 的位置 
  var endIndex: Index { get }
	/// 返回在给定索引之后的那个索引值
	func index(after i : Index) -> Index
	/// 访问特定位置的元素
	subscript(position: Index) -> Element { get }
}
```



#### 2.1 IndexingIterator

集合类型中的默认迭代器类型是 IndexingIterator<**Self**>

 ```swift
struct IndexingIterator<Elements: IndexableBase>: IteratorProtocol, Sequence { 
  private let _elements: Elements
	private var _position: Elements.Index
  
	init (_elements: Elements) { 
    self._elements = _elements 
    self._position = _elements.startIndex
	}
  
	mutating func next() -> Elements._Element? {
    guard _position < _elements.endIndex else {
			return nil
		}
		let element = _elements[_position]
    _elements.formIndex(after: &_position) 
    return element
	}
}
 ```



#### 2.2 Slice（切片）

> 1. 切片是Collection中的一部分元素组合
> 2. 切片保存了Collection的indices，即共享索引。
> 3. 切片不会复制Collection中的元素
> 4. 当Collection is mutable, Collection发生改变时，会出发切片复制元素，使得切片中保存了原有元素。

```swift
protocol Collection: Sequence { 
	  /// 切片申明
  	associatedtype SubSequence : Collection = Slice<Self>
  	/// 通过 Range<Self.Index> SubSequence
  	subscript(bounds: Range<Self.Index>) -> Self.SubSequence { get }
}

/// 通过提供的方法获取切片
extension Collection {
  
  	@inlinable public func dropFirst(_ k: Int = 1) -> Self.SubSequence

    @inlinable public func dropLast(_ k: Int = 1) -> Self.SubSequence

    @inlinable public func drop(while predicate: (Self.Element) throws -> Bool) rethrows -> Self.SubSequence

    @inlinable public func prefix(while predicate: (Self.Element) throws -> Bool) rethrows -> Self.SubSequence

    @inlinable public func suffix(_ maxLength: Int) -> Self.SubSequence

    @inlinable public func prefix(upTo end: Self.Index) -> Self.SubSequence

    @inlinable public func suffix(from start: Self.Index) -> Self.SubSequence

    @inlinable public func prefix(through position: Self.Index) -> Self.SubSequence

    @inlinable public func split(maxSplits: Int = Int.max, omittingEmptySubsequences: Bool = true, whereSeparator isSeparator: (Self.Element) throws -> Bool) rethrows -> [Self.SubSequence]
  
    @inlinable public func firstIndex(where predicate: (Self.Element) throws -> Bool) rethrows -> Self.Index?
  
    @inlinable public subscript<R>(r: R) -> Self.SubSequence where R : RangeExpression, Self.Index == R.Bound { get }

    @inlinable public subscript(x: (UnboundedRange_) -> ()) -> Self.SubSequence { get }
}
```



###  4. Codable协议

```swift
public typealias Codable = Decodable & Encodable

public protocol Encodable {
    public func encode(to encoder: Encoder) throws
}

public protocol Decodable {
    public init(from decoder: Decoder) throws
}
```

#### Codable 序列化与反序列化

```swift
/// 序列化与反序列化
struct Student: Codable {
    let name: String
    let age: Int
}

let stu = Student(name: "alice", age: 20)
/// 序列化
let object2JsonData = try? JSONEncoder().encode(stu)
/// 反序列化
let jsonData2Object = try? JSONDecoder().decode(Student.self, from: object2JsonData!)
```

```swift
/// Key不统一处理
struct Student: Codable {
    let name: String
    let age: Int
  	let bornIn: String

    enum CodingKeys: String, CodingKey {
        case name
        case age
        case bornIn = "born_in"
    }
}
```

```swift
/// 派生类需要实现Codable的两个方法
class Person: Codable {
    var name:String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}


class Student: Person {
    var stuNo: Int

    init(stuNo: Int, name: String, age: Int) {
        self.stuNo = stuNo
        super.init(name: name, age: age)
    }
    
    enum Key: String, CodingKey {
        case stuNo
    }

    override func encode(to encoder: Encoder) throws {
        var container = encoder.container(keyedBy: Key.self)
        try container.encode(stuNo, forKey: Key.stuNo)
        try super.encode(to: encoder)
    }

    required init(from decoder: Decoder) throws {
        let container = try decoder.container(keyedBy: Key.self)
        self.stuNo = try container.decode(Int.self, forKey: .stuNo)
        try super.init(from: decoder)
    }

}
```

