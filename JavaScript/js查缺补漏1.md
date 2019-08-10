# 详细描述JavaScript的数据类型？

基本数据类型：```undefined```,```null```,```number```,```boolean```.```string```,```Symbol```

引用数据类型：```object```

``` NaN```也属于```number```类型，但是```NaN```不等于自身

# Typeof操作符
```typeof```对于基本类型而言，除了```null```以外，都能正确的显示类型，对``` typeof null```会返回```object```，可以理解为```null```是空对象的引
用,```typeof```对于引用类型而言，除了函数会显示```function```以外，都会显示```object```，在某些浏览器版本之前，``` typeof Regxp```会返回```fun
ction```。

若想正确的判断一个变量的类型，可以使用```Object.prototype.toString.call(x)```,可以得到一个类似```[object type]```的字符串。

# 类型转换
### 转```Boolean```

对于```Boolean()```来说，除了```null``` , ```undefined``` , ```0（包括-0）``` , ```空字符串``` , ```NaN``` , ```false``` 以外，其余的都会返回
```true```,包括所有的对象。

### 对象转基本类型

对象转换为基本类型时，首先要调用```valueof()```，然后调用```toString()```

### 加号运算符

只要有一方为字符串，另一方也会转换为字符串，只要有一方是数字，另外一方会转换为数字

```
1 + "1"    //"11"

"a" + + "b" //"aNaN" 因为 + "b"是NaN,再加a就是aNaN
```

# ``` == ```运算符

```undefined == null ``` 返回true

``` NaN == NaN ``` 返回false,NaN不和任何值相同

``` [] == ![] ```在有一方为``` Boolean```的情况下，会将其都转换为数字在进行比较

1. ![]为false，那么表达式变为 ``` [] == false ```，而根据规则，会将其转换为数字，于是 ``` [] == 0 ```。

2. 将[]转换为基本类型再与0进行比较

``` [].toString()```转换为``` " " ```，表达式变为 ``` "" == 0 ```。

3.```""```会被转换为 0，所以返回```true```

# ```new```操作符

在构造函数中，如果显示的返回一个基本类型的值，构造函数的返回值不会受到影响，仍然会返回对象实例，如果返回的是对象，那么就将该对象正常返回
1. 新生成了一个对象

2. 执行原型链接

3. 将该对象绑定到this上

4. 执行构造函数，如果返回的是原始值则将其忽略，如果返回的是对象，则需要将其正常处理

```
 function create(foo, ...reset){
     //1.创建空对象
     let obj = new Object();
     //2.链接原型，要让新创建的这个对象的原型变为Person.prototype
     Object.setPrototypeOf(obj,foo.prototype);
     //3.将该对象绑定到构造函数的this上并传入参数
     let result = foo.apply(obj,reset);
     //4.apply就已经执行了构造函数，返回结果时要判断执行构造函数会返回什么，如果返回的是原始值需要将其忽略，返回新创建的对象，如果返回的是对象，则需要将其结果返回
     return typeof result === "object" ? result : obj

 }

 function Person(name,age){
     this.name = name;
     this.age = age;
 }

 const me = create(Person,"张盛");
console.log(me);
```

# instanceof 

``` instanceof ```查找的原理是根据：判断对象的原型链中是不是能找到该类型，instanceof不能用来判断基本数据类型的，因为基本数据类型不是对象，
并且在js中所有的对象都会从Object中继承属性，所以对一个对象```instanceof Object```永远返回```true```。
```
let arr = [1, 2, 3, 4];

//在arr的原型链上查找Array类型
console.log(arr instanceof Array);
```

手动实现instanceof，思路是去查找右边变量的prototype属性是否在左边变量的原型链上即可
```
let arr = [1, 2, 3, 4];
function instan(left,right) {
    let right_prototype = right.prototype;
    left = left.__proto__;
    while (true) {
        //当查找到原型链的顶端即,Object.prototype.__proto__,也就是Null时,查找结束
        if(left === null){
            return false
            
        }
        if(right_prototype === left){
            return true;
        }
        left == left.__proto__;
    }
}
```
# 令我这个自学半年的前端大学生感到崩溃的this全解

this:是一个指针，指向调用函数的对象。

关于this的绑定规则有四种：

1. 默认绑定
2. 隐士绑定
3. 硬绑定
4. new绑定

### 默认绑定

独立调用函数时，eg:
```
var name ="二狗";
function getName(){
    return this.name;   //window
}
getName();   //函数getName()被全局对象调用，所以this指向全局对象，非严格模式下为window，严格模式下为undefined,undefined上没有this对象，报错
```

当使用let定义name时，因为let定义的变量不再作为全局对象的属性，所以查不到。

### 隐式绑定

函数的调用是在某个对象上触发的，典型的形式为obj.fun()，这种时候，this指向obj
```
function getName() {
    return `hello ${this.name}`;
}
var name = "全局name";
var person ={
    name: "person对象的Name",
    sayName: getName
}
//在全局环境上调用getName()方法
console.log(getName()); //hello 全局name
//在对象person上调用getName()方法
console.log(person.sayName()); //hello person对象的name
```
但是这种方式只有最后一层会影响到调用的位置
```
function sayHi(){
    console.log('Hello,', this.name);
}
var person2 = {
    name: 'person2上的Name',
    sayHi: sayHi
}
var person1 = {
    name: 'person1上的name',
    friend: person2
}
person1.friend.sayHi(); //friend属性是person2对象，相当于 person1.friend.person2.sayHi(),只关注最后一层，所以结果为person2上的Name

```
绑定丢失：
```
function sayHi(){
    console.log('Hello,', this.name);
}
var person2 = {
    name: 'person2上的Name',
    sayHi: sayHi
}
var name ="全局上的Name";
var foo = person2.sayHi;
foo();
```
这里直接将foo指向了person2对象的sayHi()函数，此时的变量foo = sayHi(){ console.log('Hello',this.name)}，随后又在全局环境中被调用

第二种绑定丢失发生在回调函数上
```
function sayHi(){
    console.log('Hello,', this.name);
}
var person1 = {
    name: 'YvetteLau',
    sayHi: function(){
        setTimeout(function(){
            console.log('Hello,',this.name);
        })
    }
}
var person2 = {
    name: 'Christina',
    sayHi: sayHi
}
var name='Wiliam';
person1.sayHi();
setTimeout(person2.sayHi,100);
setTimeout(function(){
    person2.sayHi();
},200);

```
结果为：
```
Hello, Wiliam
Hello, Wiliam
Hello, Christina
```
分析过程：
第一个输出：在setTimeout()中是一个回调函数，可以将该函数单独拿出来，它其实是在全局环境中运行的。

第二个输出：setTimeout(person2.sayHi,100);这里其实是在将person2.sayHi作为一个参数给setTimeout,而setTimeout执行了回调函数后，person2.sayHi()
中的this已经与person2没有关系了，也可以将该语句变为:
```
setTimeout(function(){
  console.log('Hello,', this.name);
},100)
```
其实与第一个输出没有区别

第三个输出：
```
setTimeout(function(){
    person2.sayHi(); //这里直接执行了函数
},200);
```

其实可以理解为：第三个输出中直接执行了函数，而第一个和第二个中只是指向了引用，并没有调用，调用他们的其实是全局环境。

### 显式绑定

其实就是通过Javascript的```apply```,```call```,```bind```显示的指定this所指向的对象，他们的第一个参数就是this所要指向的对象，call和apply的作用一样，只是在传参过程中:apply接收的是一个数组，而call接收的是一个一个的参数,同时call和apply都会执行函数，但是bind不会。但是当我们将```null```或者```undefined```作为参数传入```apply```,```call```,```bind```时，这些值将被忽略，实际上应用的是默认绑定规则

绑定丢失的又一个例子：
```
function sayHi(){
    console.log('Hello,', this.name);
}
var person = {
    name: 'YvetteLau',
    sayHi: sayHi
}
var name = 'Wiliam';
var Hi = function(fn) {
    fn();
}
Hi.call(person, person.sayHi); 
```
在最后一步可以看到，通过call将Hi这个函数中的this指向明确的绑定到了person对象上并且将person.sayHi作为参数传进去，然而可以来看一下此时Hi函数：
```
var Hi = function(fn){
//这里可以打印下这里的this更直观:
  console.log(this);    //person对象
 ！！这里直接执行了fn()函数，同时由于person.sayHi已经被赋值给了fn这个变量，所以隐式绑定丢失了，所以为默认绑定
 fn()
}

```

### new绑定

当我们使用new来调用函数时，就会把new创建的新对象绑定到这个函数的this上，前提是构造函数没有返回对象或者function，否则this就指向返回的这个对象或function

### 绑定优先级：new绑定>显式绑定>隐式绑定>默认绑定

### 箭头函数

箭头函数没有自己的this，它的this继承于外层中的this

```
var obj = {
    hi: function(){
        console.log(this);
        return ()=>{
            console.log(this);
        }
    },
    sayHi: function(){
        return function() {
            console.log(this);
            return ()=>{
                console.log(this);
            }
        }
    },
    say: ()=>{
        console.log(this);
    }
}
let hi = obj.hi();  //输出obj对象
hi();               //输出obj对象
let sayHi = obj.sayHi();
let fun1 = sayHi(); //输出window
fun1();             //输出window
obj.say();          //输出window

```
逐步分析：
1. let hi = obj.hi();将obj对象的hi方法的执行结果赋值给变量hi，在执行时,hi方法中的this由于隐式绑定，指向的是obj

2. hi();hi变量此时是obj.hi()的返回值，也就是箭头函数，而箭头函数的this继承的是上一个代码库中的this,也就是obj，所以输出obj

3. let sayHi = obj.sayHi(); 将obj对象的sayHi()方法的执行结果赋值给变量sayHi

4. 将sayHi的返回值赋值给fun1变量，而在sayHi()函数执行的是时候，其中的this由于默认绑定，指向了全局环境，因为它是在全局环境中被调用的。
此时的：
```
sayHi = function(){
 console.log(this);
 return ()=>{
  console.log(this);
 }
}
```
5. 将sayHi的返回值赋值给fun1变量，此时的
```
fun1 = () =>{
 console.log(this)
}
```
由于箭头函数中的this继承于上一个外层代码库的this,所以执行fun1()会输出window

6. obj.say()：调用obj的say()方法，该方法是一个箭头函数，指向外层，所以输出window

##### 再来一个例子
```
var obj = {
    hi: function(){
        console.log(this);
        return ()=>{
            console.log(this);
        }
    },
    sayHi: function(){
        return function() {
            console.log(this);
            return ()=>{
                console.log(this);
            }
        }
    },
    say: ()=>{
        console.log(this);
    }
}
let sayHi = obj.sayHi();
let fun1 = sayHi(); //输出window
fun1();             //输出window

let fun2 = sayHi.bind(obj)();//输出obj
fun2();                      //输出obj
```
逐行分析：

1.let sayHi = obj.sayHi(); 此时的
```
sayHi = function(){
 console.log(this);
 return ()=>{
  console.log(this);
 }
}
```
2. let fun1 = sayHi();fun1变量等于sayHi()函数的返回值，在sayHi()执行过程中，它是在全局环境中被调用的，所以其中的this指向window对象

3. fun1(),此时fun1是一个箭头函数，继承于刚才的外层，为window

4.let fun2 = sayHi.bind(obj)();此时fun2变量等于 sayHi中的this被绑定到obj对象后并执行的返回值，也就是fun2为：
```
fun2 = () =>{
 console.log(this)
}
```
由于this被绑定到了obj对象上，所以fun2()箭头函数中的this继承自上一个代码库，也就指向了obj


# 关于this的总结：

1. 当函数在new中调用时，this绑定的便是新对象

2. 函数是否被apply、bind、call等显式绑定，如果是，则指向绑定的对象

3. 函数是否被隐式绑定xxx.foo()，如果是，则指向最深层的那个对象

4.如果都没有，则为默认绑定

5.如果给apply、call、bind传入的参数是null或者undefined，则指向全局对象

6. 如果是箭头函数，则继承的是外层的this

# 超大题分析：
```
var number = 5;
var obj = {
    number: 3,
    fn: (function () {
        var number;
        this.number *= 2;
        number = number * 2;
        number = 3;
        return function () {
            var num = this.number;
            this.number *= 2;
            console.log(num);
            number *= 3;
            console.log(number);
        }
    })()
}
var myFun = obj.fn;
myFun.call(null);
obj.fn();
console.log(window.number);
```

第一步：将obj.fn的执行结果赋值给myFun变量，但是请注意：fn所对应的属性值是一个立即执行函数，在定义的时候就已经执行了，所以，此处的
```
myFun = function () {
            var num = this.number;
            this.number *= 2;
            console.log(num);
            number *= 3;
            console.log(number);
        }
```
而且，该函数在执行时，采用的是默认绑定，所以外层的this指向window，而且还在外层定义了一个局部的number变量，结果等于3，而由于this指向window
，全局环境下的number被修改为this.number *=2;所以window.number =10;

第二步：myFun.call(null);将myFun函数绑定到了全局作用域上，所以在myFun函数内的运算过程如下
```
var num = window.number; //10;
window.number = 20; //window.number变为了20
console.log(num);  //10
number *=3 ;  //这里的number指的是外层定义的number为3，所以这里计算后的number为9
console.log(number); //这里的number为
```

第三步：obj.fn()：执行obj对象上的fn()函数，此时采用了隐式绑定，将this绑定到了obj对象上,运算过程如下:
```
var num = obj.number; //3
obj.number *=2; //obj上的number变为6
console.log(num); //3
number *=3 ;//指的是外城的number，在第二步中已经变为9，所以这里为27
console.log(number);//27
```

第四步：输出window.number，第二步中已经被改为20，所以最终结果为:

10

9

3

27

20

😶😑😔😲😀我感觉我疯了，去做这道题，但是挺爽的🚑🚑🚑🚑🚑🚑🚑
