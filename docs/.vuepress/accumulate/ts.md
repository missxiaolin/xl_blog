## ts保姆级教程，别再说你不会ts了

TypeScript，简称 ts，是微软开发的一种静态的编程语言，它是 JavaScript 的超集。 那么它有什么特别之处呢?

- 简单来说，js 有的 ts 都有，所有js 代码都可以在 ts 里面运行。
- ts 支持类型支持，ts = type +JavaScript。

### 那么 ts 和 js 有什么区别呢？

ts 的常用基础类型分为两种：js 已有类型

- 原始类型：number/string/boolean/null/undefined/symbol
- 对象类型：object（包括，数组、对象、函数等对象）

ts 新增类型

- 联合类型
- 自定义类型(类型别名)
- 接口
- 元组
- 字面量类型
- 枚举
- void
- any
……

原始类型：
number/string/boolean/null/undefined/symbol
语法比较简单，基本和 js 差别不大

~~~
// 数值类型
let age: number = 18

// 字符串类型
let myName: string = '小花'

// 布尔类型
let isLoading: boolean = false

// undefined
let un: undefined = undefined

// null
let timer:null = null

// symbol
let uniKey:symbol = Symbol()
~~~

### 函数

函数涉及的类型实际上指的是：函数参数和返回值的类型

#### 定义单个函数

~~~
// 普通函数
function 函数名(形参1： 类型=默认值， 形参2：类型=默认值,...): 返回值类型 { }
// 声明式实际写法:
function add(num1: number, num2: number): number {
  return num1 + num2
}

// 箭头函数
const 函数名（形参1： 类型=默认值， 形参2：类型=默认值, ...):返回值类型 => { }
const add2 = (a: number =100, b: number = 100): number =>{
   return a + b
 }
 // 注意： 箭头函数的返回值类型要写在参数小括号的后面
add（1,'1') // 报错
~~~

#### 统一定义函数格式

当函数的类型一致时，写多个就会显得代码冗余，所以需要统一定义函数的格式 如下所示：

~~~
const add2 = (a: number =100, b: number = 100): number => {
    return a + b
  }

function add1 (a:number = 100 , b: number = 200): number {
    return a + b
  }
// 这里的 add1 和 add2 的参数类型和返回值一致，
// 那么就可以统一定义一个函数类型
type Fn = (n1:number,n2:number) => number 
const add3 : Fn = (a,b)=>{return a+b }
// 这样书写起来就简单多啦
~~~ 

#### 函数返回值类型void

在 ts 中，如果一个函数没有返回值，应该使用 void 类型

~~~
function greet(name: string): void {  console.log('Hello', name)  //}
~~~

可以用到void 有以下几种情况

- 函数没写return
- 只写了 return， 没有具体的返回值
- return 的是 undefined

~~~
// 如果什么都不写，此时，add 函数的返回值类型为： void
const add = () => {}

// 如果return之后什么都不写，此时，add 函数的返回值类型为： void
const add = () => { return }

const add = (): void => {
  // 此处，返回的 undefined 是 JS 中的一个值
  return undefined
}
// 这种写法是明确指定函数返回值类型为 void，与上面不指定返回值类型相同
const add = (): void => {}
~~~

那么就有人好奇，既然return undefined，那么为什么不可以直接在返回值那里写 :undefined 呢？ 如果函数没有指定返回值，调用结束之后，值是undefined的，但是不能直接声明返回值是undefined

~~~
function add(a:number, b:number): undefined { // 这里会报错
  console.log(a,b)
}
~~~

#### 函数-可选参数

使用函数实现某个功能时，参数可以传也可以不传。

例如：数组的 slice 方法，可以 slice() 也可以 slice(1) 还可以 slice(1, 3) 那么就可以定义可选参数 语法：

~~~
可选参数：在可选参数名的后面添加 ?（问号）
function slice (a?: number, b?: number) {
    // ? 跟在参数名字的后面，表示可选的参数
    // 注意：可选参数只能在 必须参数的后面
    // 如果可选参数在必选参数的前面，会报错
    console.log(111);
    
  }
  slice()
  slice(1)
  slice(1,2)
}
~~~

### 对象类型-单独使用

格式： 方法有两种写法： 普通函数 和 箭头函数

const 对象名: {
  属性名1：类型1，
  属性名2?：类型2，
  方法名1(形参1: 类型1，形参2: 类型2)： 返回值类型,
  方法名2:(形参1: 类型1，形参2: 类型2) => 返回值类型
} = { 属性名1: 值1，属性名2：值2  }

#### 对象类型-类型别名

~~~
// 创建类型别名
type Person = {
  name: string，
  age: number
  sayHi(): void
}

// 使用类型别名作为对象的类型：
let person: Person = {
  name: '小花',
  age: 18
  sayHi() {}
}
~~~

### 接口

当一个对象类型被多次使用时，有如下两种方式来来描述对象的类型，以达到复用的目的：

- 类型别名，type
- 接口，interface
  
语法：

~~~
interface 接口名  {属性1: 类型1, 属性2: 类型2}
// 这里用 interface 关键字来声明接口
interface IGoodItem  {
	// 接口名称(比如，此处的 IPerson)，可以是任意合法的变量名称，推荐以 `I` 开头
   name: string, price: number, func: ()=>string
}

// 声明接口后，直接使用接口名称作为变量的类型
const good1: IGoodItem = {
   name: '手表',
   price: 200,
   func: function() {
       return '看时间'
   }
}
const good2: IGoodItem = {
    name: '手机',
    price: 2000,
    func: function() {
        return '打电话'
    }
}
~~~

接口和类型 的区别 interface（接口）和 type（类型别名）的对比：

- 相同点：都可以给对象指定类型
- 不同点:
1、接口，只能为对象指定类型。它可以继承。
2、类型别名，不仅可以为对象指定类型，实际上可以为任意类型指定别名

先有的 interface，后有的 type,推荐使用 type

~~~
// 接口的写法-------------
interface IPerson {
	name: string,
	age: number
}

const user1：IPerson = {
	name: 'a',
	age: 20
}

// type的写法-------------
type Person  = {
	name: string,
	age: number
}
const user2：Person = {
	name: 'b',
	age: 20
}
~~~

#### 接口继承

如果两个接口之间有相同的属性或方法，可以将公共的属性或方法抽离出来，通过继承来实现复用 语法：

~~~
interface 接口2 extends 接口1 {
 属性1： 类型1， // 接口2中特有的类型 
 }

interface a { x: number; y: number }
// 继承 a
// 使用 extends(继承)关键字实现了接口
interface b extends a {
  z: number
}
// 继承后，b 就有了 a 的所有属性和方法(此时，b 同时有 x、y、z 三个属性)
~~~

### 元组

元组是一种特殊的数组。有两点特殊之处

它约定了的元素个数

它约定了特定索引对应的数据类型


举个例子：

~~~
就拿 react 里面的 useState来举例：
function useState(n: number): [number, (number)=>void] {
        const setN = (n1) => {
            n = n1
        }
        return [n, setN]
    }

const [num ,setNum] = useState(10)
~~~
