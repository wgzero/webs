# TypeScript文档

### 1.TypeScript组成部分

```
模块、函数、变量、语句、表达式、注释
```

### 2.基本类型

```tsx
1.any:任意类型
const mo: any = "mo"

2.number:数字类型
const num: number = 12

3.string: 字符串类型
const str: string = "hello TS"

4.boolean: 布尔类型
const isShow: boolean = true

5.数组类型
const arr: number[] = [1, 2]

6.元组: 用来已知数量和类型，并且一一对应, 用来存储不一样的数据类型
const x:[string, number] = ["hello", 1]

7.枚举: 用来定义数值集合
enum Color{
    Red,
    Green,
    Blue
}
const c: Color = Color.Blue
console.log(c) // 2

8.void: 表示该方法无返回值
function hello(): void{
    console.log("hello")
}

9.null: 表示对象值缺失

10.undefined: 用于初始化变量一个未定义的值

11.never:never是其他类型(包括null和undefined)的子类型，代表从不会出现的值

```

### 3.类型的最终定义

- 类型断言

  ```ts
  const str = "1"
  const str1 = "1" as any
  console.log(str1) // 1
  ```

- 类型推断: 由TypeScript编译器利用类型推断来推断类型

  ```ts
  const num = 2 // number类型
  console.log(num) // 2
  num = "12" // 编译报错
  ```

### 4.函数

```ts
// 无参数
function test(){
	const a:number = 10
	return a
}

// 有参数以及可以可选参数
function test1(x: number, y ?: string){
	return x + y
}

// lambda函数： 又称箭头函数
const show = (x: number) => 10 + x
console.log(show(10)) // 20

//剩余参数
function show1(...nums: number[]){
    console.log('--', nums.length)
}

console.log(show1(1,2,3)) // 3

```

### 5.联合类型： 

- 定义： 可以声明多个数据类型通过(|)

  ```ts
  // 联合类型
  let age: string | number = "18"
  age = "summer" // summer
  
  // 联合类型数组
  let age1: string[] | number[] = ["hello"]
  age1 = [1]
  console.log("age1", age1) // [1]
  ```



### 6.接口

- 定义： 通过去定义一个数据的类型扩展

  ```ts
  
  interface animalProps {
    name: string
    age?: number // 可选
    sayHi: () => string
    [propName: string]: any // 自定义类型传入
  }
  
  let animal: animalProps = {
    name: "dog",
    age: 1,
    sayHi: () => {
      return "summer"
    },
    height: ".5"
  }
  
  console.log("animal", animal, animal.sayHi()) // { name: 'dog', age: 1 } summer
  
  ```



### 7.类

- 定义:创建对象共同的属性和方法

  ```ts
  class Car {
    // 定义变量
    engine: string
    // 创建构造函数
    constructor(engine: string){
      this.engine = engine
    }
  
    running(): void{
      console.log("---", this.engine)
    }
  }
  
  // 创建对象
  let obj = new Car("宝马")
  console.log("obj", obj.engine) //宝马
  obj.running() // 宝马
  ```



### 8.对象

```ts

let obj = {
  name: "summer",
  age: 20
}
console.log("ob--", obj.name, obj.age) // summer 20
```

### 9.命名空间

### 10.模块

### 11.声明文件

```tsx
// 声明文件语法
declare var jQuery: (selector: string) => any;


let dom = document.createElement("div")
dom.className = "root"
jQuery(".root")

// 声明文件.d.ts
```

