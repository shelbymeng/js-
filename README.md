## js高级程序设计笔记
### 一、js数据类型
基本类型为：Number,String,Boolen,Null.Undefined.
引用类型：Object,Array,Date,RegExp(正则),Function.
#### 数组方法
- 检测数组的方法
instance of 检测传入值的原型
Array.idArray()方法，确定某个值是不是数组
- 转换方法
所有对象都具有toLocaleString(),toString(),valueOf()方法
1. toString()方法会返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串
2. valueOf()返回的还是数组
3. toLocaleString()会创建一个数组值的以逗号分隔的字符串
- 栈方法
js中的数组可以像栈一样后进先出（LIFO），主要体现在pop()与push()方法，pop()方法可以将数组数组末尾的数移除，并返回移除的项。push()方法可以将任意数量的参数添加到数组末尾，返回修改后数组的长度。
- 队列方法
js的数组也可以模仿队列先进先出(FIFO)，主要体现在shift()与push()方法。shift()方法可以移除数组中的第一个数，并返回移除的项，数组长度减一。
- 重排序方法
分为sort()与reverse()方法。reverse()方法会反转数组的顺序，sort()方法默认升序排列，会默认调用toString()转型方法，比较得到的字符串排序。一般使用为
`
array.sort((a, b) => a - b)
`
- 操作方法
cancat()方法会创建一个当前数组的副本，然后将接收到的参数添加到副本数组的末尾并返回副本。
slice()方法会基于当前数组中的一个或多个项创建一个新数组。接收一或两个参数，start和end，即开始位置与结束位置，以数组序号为准。slice()方法并不会改变原数组。
splice()方法可以对原数组进行删除、插入、替换的操作，主要依据接受的参数个数。
1. 删除：指定两个参数即起始位置，删除的个数。
2. 插入：指定三个参数即起始位置，0，要插入的数据。
3. 替换：指定三个参数即起始位置，删除项数，要插入的数据。
splice()方法始终都会返回一个数组，包含从原数组中删除的项。
- 位置方法
indexOf()与lastIndexOf()方法，两个方法都接受两个参数：要查找的项和表示查找起点位置的索引。indexOf()方法会从数组的开头向后查找，lastIndexOf()会从数组末尾向前查找。
两个方法都会返回要查找的项在数组中的位置，没找到的情况下返回-1.在进行比较操作时，会使用全等操作符即类型与值的比较。
- 迭代方法
1. every(): 对数组中每一项运行给定的函数，若每一项都返回true，则返回true
2. filter(): 对数组中每一项运行给定函数，返回该函数会返回true的项组成的数组
3. forEach(): 对数组中每一项运行给定函数,没有返回值
4. map(): 对数组中每一项运行给定函数，返回每次函数调用结果组成的数组
5. some(): 对数组中每一项运行给定函数，如果该函数对任一项返回true，则返回true
以上方法都不会改变原数组的值。
- 归并方法
分别为reduce()与reduceRight()方法。这两个方法都会迭代数组中所有的项，然后构建一个最终返回的值。reduce()方法会从数组第一项开始，逐个遍历数组。reduceRight()方法则从数组的最后一项开始，向前遍历到第一项。
两个方法都接收两个参数，一个在数组中每一项调用的函数与作为归并基础的初始值，其中传给两个方法的函数接收4个参数，前一个值，当前值，项索引和数组对象。这个函数返回的任何值都会作为第一个参数自动的传给下一项。

#### Date类型
- 创建日期对象

 `var now = new Date();
Mon Jul 27 2020 20:29:24 GMT+0800 (中国标准时间)
 `

新创建的对象将自动获得当前时间和日期。  
ECMAScript提供两种方法
1. Date.parse()
2. Date.UTC()

Date.parse()方法接收一个表示字符串的参数，然后根据这个字符串返回相应日期的毫秒数。参数可以为一下几种：
1. 月/日/年 7/27/2020;
2. 英文月名 日，年 July 7,2020;
3. 英文星期几 英文月名 日 年 时：分：秒 时区 Mon July 27 2020 GMT+0800

若传入的字符串不能表示日期，则会返回NAN

Date.UTC()方法同样返回表示日期的毫秒数，但接收参数不同。分别为年份、基于0的年份(一月为0)、月中哪一天、小时数(0到23)、分钟、秒、毫秒数。只有前两个参数必填。若没指定月份的天数，则假设天数为1；若省略其他参数，则全部假设为0.

ECMAScript5后提供了Date.now()方法，返回当前时间与日期的毫秒数。

`var now = Date.now();1595855534138`

- 继承方法  
Date类型同样重写了toLocaleString()、toString(),和valueOf()方法。
- 日期格式化方法  
toDateString() ——显示星期、月、日、年;  
toTimeString() ——显示时、分、秒;  
toLocaleDateString() ——以特定地区的格式显示星期、月、日、年;  
toLocaleTimeString() ——以特定实现的格式显示时、分、秒;  
toUTCString() ——以特定于实现的格式完整的UTC日期；  
日期与时间的方法：  
| 方法 | 说明 |
| -- | -- |
| getTime() | 返回表示时间的毫秒数 |
| setTime(毫秒) | 以毫秒设置日期 |
| getFullYear() | 取得四位数的年份|
| setFullYear(年) | 设置日期的年份，传入值必须为四位数字|
| getMonth() | 返回日期中的月份，0表示一月，11十二月|
| setMonth(月) | 设置日期的月份，同上 |
| getDate() | 返回日期月份中的天数(1到31) |
| setDate(日) | 设置日期月份中的天数，若传的值超过了月中应有的天数，则相应增加一个月 |
| getDay() | 返回日期中的星期(0表示星期日，6表示星期六) |
| getHours() | 返回日期中的小时数(0-23) |
| setHours(时) | 设置日期中的小时数。若传入值超过23则增加月份中的天数 |
| getMinutes() | 返回日期中的分钟数(0-59) |
| setMinutes(分) | 设置日期中的分钟数。若传入值超过59则增加小时数 |
| getSeconds() | 返回日期中的秒数(0-59) |
| setSeconds(秒) | 设置日期中的秒数。若传入值超过59则增加分钟数 |
| getMilliseconds() | 返回日期中的毫秒数 |
| setMilliseconds(毫秒) | 设置日期中的毫秒数

#### RegExp类型
ECMAScript通过RegExp类型来支持正则表达式  
`var expression = / pattern / flag;`  
pattern是正则表达式，可以包含字符类，限定符，分组，向前查找以及反向引用。每个表达式可以带有一个或多个标志(flag)，用以表明正则表达式的行为。  
1. g：表示全局模式，该模式会被应用于所有字符串。
2. i：表示不区分大小写模式，匹配时忽略大小写。
3. m：表示多行模式，在匹配到末尾时继续向下一行查找。  
元字符必须要转义才能使用，包括  
`( [ { \ ^ $ | ) ？ * + . ] }`  
若想匹配这些字符串必须将其转义  
`var pattern = /\[bc\]at/i`匹配第一个[bc]at，不区分带小写。
也可以写为  
`var pattern = new RegExp("[bc]at", i)`  
- RegExp实例属性  
1. global：布尔值，表示是否设置g标志。
2. ignoreCase：布尔值，表示是否设置i标志。
3. lastIndex：整数，表示开始搜索下一个匹配项字符位置。
4. multiline：布尔值，表示是否设置i标志。
5. source：正则表达式字符串表示。  
`var pattern = /\[bc\]at/`  
`alert(pattern.global);` //false  
`alert(pattern.ignoreCase);` //true
- RegExp实例方法  
主要方法为exec(),专门为捕获组设计的。exec()接收一个参数，即要应用模式的字符串，然后返回第一个匹配信息的数组，在没有匹配项的情况下返回null。返回数组为array的实例，但包含两个额外的属性，index和input。index表示匹配项在字符串的位置索引，input表示应用正则表达式的字符串。

### 二、面向对象的程序设计
#### 1.理解对象
- 属性类型  
1. 数据类型  
数据类型包含一个数据值的位置，在此位置可以进行读写值。  
Configurable；表示能否delete删除属性重新定义属性，能否修改属性的特性，或者能否将属性修改为可访问属性。  
Enumerable：表示能否通过for-in循环返回属性。  
Writable：表示能否修改属性的数据值。  
Value：包含这个属性的数据值。  
`var person = {};`  
`Object.defineProperty(person, "name", {
    Writable: false;
    value: "aaa"
  });`
`alert(person.name); //aaa`  
`person.name = "bbb";`  
`alert(person.name); // bbb`  
在调用Object.defineproperty()方法时，若不指定参数，则三个配置都为false。  
2. 访问器属性  
访问器属性不包括数据值，而是包含一对setter，getter函数(不必须)，在读取访问器属性的时候，会调用getter函数，这个函数会返回有效的值，在写入访问器属性的时候，会调用setter函数传入新值，这个函数负责处理数据。  
Configurable：同上。  
Enumerable： 同上。  
Get：在读取属性值时调用的函数，默认undefined。  
Set：在写入属性的时候调用的函数，默认为undefined。  
访问器属性不能直接定义，必须使用object.defineproperty()来定义。  
`var book = {
  _year: 2004,
  edition; 1
}`  
`Object.definepropety(book, "year", {
    get: function(){
      return this._year;
  },
    set: function(newValue){
      this._year = newValue;
      this.edition += newValue - 2004;
  }
});`  
`book.year = 2005;`  
`alert(book.edition); //2`  
不需要同时指定setter与getter，单独指定getter表示属性不可写入，单独指定setter表示属性不可读。  
- 定义多个属性  
ECMAScript定义一个Object.defineproperty()的方法，利用这个方法可以通过描述符一次定义多个属性。方法接收两个参数，第一个是要添加或修改其属性的对象，第二个对象的属性与第一个对象中要添加或修改的属性一一对应。  
`var book = {};`  
`object.defineProperty(book,
  {
    _year: {value: 2004},
    edition: {value: 1},
    year:
    {get: function(){return this._year},
    set: function(newValue)
    {if(newValue > 2004){this._year = newValue;this.edition +=newValue - 2004}}}});`  
以上代码在book对象上定义了两个数据属性(\_year和edition)和一个访问器属性(year)。  
- 读取属性的特性  
使用Object.getOwnPropertyDescriptor()方法，可以取得给定属性的描述符。方法接收两个参数，属性所在的对象和要读取器描述符的属性名称。返回值是一个对象，如果是访问器属性，这个对象的属性有Configurable、Enumerable、get、set；如果是数据属性，这个对象的属性有Configurable、enumerable、Writable、value。  
`var descriptor = Object.getOwnPropertyDescriptor(book, "_year");`  
`alert(descriptor.value); //2004`    
`alert(descriptor.configurable); //false`  

#### 2.创建对象  
使用object构造函数有明显的缺点就是使用同一个接口创建很多对象，会产生大量重复代码。  
##### 工厂模式  
这种模式抽象了创建具体对象的过程，用函数来封装以特定接口创建对象的细节。  
`function createPerson(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.say = function(){
    alert(this.name);
  };
  return o;
}`  
`var person1 = createPerson("aaa", 18, "aaaaa")`  
`var person2 = createPerson("bbb", 19, "bbbbb")`  
##### 构造函数模式  
构造函数可以用来创建特定类型的对象，可以创建自定义的构造函数从而定义自定义对象类型的属性和方法。  
`function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.say = function(){
    alert(this,name);
    };
}`  
`var person1 = new Person("aaa", 18, "aaaa")`  
`var person2 = new Person("bbb", 19, "bbbb")`  
在这个例子中，Person()函数取代了createPerson()函数。Person()中的代码与createPerson()存在部分不同之处；  
1. 没有显式的创建对象；
2. 直接将属性和方法赋给了this对象；
3. 没有return语句。  
要创建Person的新实例，必须使用new操作符。以这种方式调用构造函数实际上会有四个步骤：  
1. 创建一个新对象  
2. 将构造函数的作用域赋给新对象(this就指向了新对象)  
3. 执行构造函数中的代码(为这个新对象添加属性)  
4. 返回新对象  
在构造函数模式中，person1与person2分别保存着Person的一个不同实例，两个对象都有一个constructor(构造函数)属性，该属性指向Person  
`alert(person1.constructor == Person); //true`  
`alert(person2.constructor == Person); //true`  
创建自定义的构造函数意味着可以将它的实例标识为一种特定的类型。  
- 将构造函数当做函数  
构造函数与函数的不同之处就在于调用的方式不同。只要可以通过new操作符来使用，就可以称为构造函数。  
// 当做构造函数  
`var person = new Person("aa", 18, "aaa"); //构造函数`  
`person.say(); //aa`  
// 当做普通函数  
`Person("bb", 19, "bbb"); //作为普通函数`  
`window.say(); //bb`    
//在另一个对象的作用域中调用  
`var o = new Object();`  
`Person.call(o, "cc", 20, "ccc");`  
`o.say(); //cc`  
- 构造函数的问题  
每个方法都要在每个实例上重新创建一次。  
`function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.say = say;
  }`  
`function say(){
  alert(this.name);
  }`  
`var person1 = new Person("aa", 18, "aaa");`  
`var person2 = new Person("bb", 19, "bbb");`    
将say函数定义转到构造函数外部，在构造函数内部将say属性设置成等于全局的say函数，这样say包含的是一个指向函数的指针，因此在person1和person2对象就共享了在全局作用域中定义的一个say函数。但在全局作用域下定义的say函数实际上只能被某个对象调用，不符合全局的事实，自定义的引用类型就没有封装性。  

##### 原型模式
我们所创建的每个函数都有一个prototype(原型)属性，这个属性是一个指针，指向一个对象，这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。prototype就是通过调用构造函数而创建的那个对象实例的原型对象，那么使用原型对象的好处是可以让所有的对象实例共享它所包含的属性和方法。不必在构造函数中定义对象的实例信息，而是将这些信息添加到原型对象中。   
`function Person(){}`  
`Persoon.prototype.name = "aa";`  
`Person.prototype.age = 18;`  
`Person.prototype.job = "aaa";`  
`Person.prototype.say = function(){ alert(this.name)}`  
`var person1 = new Person();`  
`person1.say(); //aa`  
`var person2 = new Person();`  
`person2.say(); //aa`  
`alert(person1.say == person2.say); //true`  
- 1.理解原型对象  
新创建一个函数，就会为该函数创建一个prototype属性，这个属性指向函数的原型对象。默认情况下，所有的原型对象都会获得一个constructor属性，这个属性包含了一个指向prototype属性所在函数的指针。  
创建了自定义的构造函数后，原型对象默认只会获得constructor属性；其他方法都是从Object中继承而来，当调用一个构造函数创建一个新的实例后，实例内部将包含一个指针，指向构造函数的原型对象，这个连接只存在于实例与构造函数的原型对象之间，而不是在实例与构造函数之间。  
`person.prototype.constructor == person; //构造函数的prototype属性的constructor指针指回了构造函数`  
`person1.__proto__ == person.prototype; //构造函数的实例中的__proto__指向了构造函数的原型。`  
构造函数的实例中都包含一个内部属性，这个属性仅仅指向了person.prototype;换句话说，实例与构造函数之间没有直接的关系，虽然实例中不包含属性与方法，但是可以通过查找对象的属性来调用原型的属性与方法。  
isPrototypeOf()方法可以确定对象之间是否在村这种关系，如果实例对象中的__proto__属性指向了调用isPrototypeOf方法的对象(person.prototype)，那么这个方法返回true。  
`function person(){};
person.prototype.name = "aa";
person.prototype.say = function(){
	alert(this.name);
};
var person1 = new person;
person1.say(); //aa;
alert(person.prototype.isPrototypeOf(peron1)); //true`  
ECMAScript 5中新增一个Object.getPrototypeOf()方法，这个方法返回__proto__的值。  
`alert(Object.getPrototypeOf(person1) == person.prototype); //true`  
`alert(Object.getPrototypeOf(peron1).name);`  
第一行表示返回该实例的原型对象，第二行表示取得原型对象中的name值。当代码读取某个对象的属性时，就会执行一次搜索，目标是具有给定名字的属性，若在实例中找到，则返回属性值，若没有找到，则继续搜索指针指向的原型对象，若原型对象中存在该属性则返回。  
当实例中添加一个属性值与原型相同时，就会屏蔽原型对象中的相同属性值，但不会修改。也可以使用delete操作符将实例中的同名属性值删除，则可以重新访问原型中的该属性值。  
hasOwnPrototype()方法可以检测一个属性是存在于实例，还是在原型对象中。这个方法只在给定属性存在于对象的实例中时，才会返回true。  
- 2.原型与in操作符  
in操作符有两种使用形式：单独使用与在for in中循环使用。单独使用时，in操作符会在通过对象能够访问给定属性时返回true，无论该属性是在实例中还是在原型中。  
在使用for in循环时，返回的是所有能通过对象访问的、可枚举的属性，其中既包括实例中的属性也包括原型中的属性。屏蔽了原型中不可枚举的属性的实例属性也会在for in循环中返回。  
若要去的对象上所有可枚举的实例属性，可以使用ECMAScript 5中的Object.keys()方法。该方法接收一个对象作为参数，返回一个包含所有可枚举属性的字符串数组。  
`Object.keys(person.prototype); //["name", "say", "age"]`  
`Object.keys(person1); //["name"]`  
若想得到所有实例的属性，无论是否可以枚举，则可以使用Object.getOwnPrototypeNames()方法。  
`Object.getOwnPrototypeNames(person.prototype);`  
`Object.getOwnPrototypeNames(person1);`  
- 3.更简单的原型语法  
使用对象字面量的形式创建对象。  
`var o = {};`  
`var person.prototype = {
  name: "aa",
  age: 18
}`  
将person.prototype设置为等于一个以对象字面量形式创建的新对象，最终的结果相同，但是constructor属性不在指向原person，因为每次新建一个函数，就会同时创建它的prototype对象，这个对象会自动获得constructor属性，本质上将会重写默认的prototype对象，因此constructor属性就变为了新对象的constructor属性，指向了Object构造函数，而不是person函数。此时instanceof操作符仍会返回正确的结果，但是无法通过constructor确定对象的类型。但可以在创建新的对象字面量时将constructor属性指向原对象。  
`function person(){}`  
`person.prototype = {
  constructor: person,
  name: "aa",
  age: 18
  }`  
- 4.原型的动态性  
原型的查找过程是一次搜索，因此对原型对象所做的任何修改都能够立即从实例上反映出来。  
`var person = new Person();`  
`Person.prototype.say = function(){
  alert("hi");
  }
  person.say(); //hi`  
在创建实例后为原型对象添加方法，实例仍可以访问到这个方法，原因为实例与原型之间的松散连接关系。  
但如果重写了整个原型对象，在调用构造函数的时候会为其添加一个指向最初原型的prototype指针，也就是__proto__,而把原型修改为另一个对象就等于切断了构造函数与最初原型之间的联系。实例中的指针指向原型，而不是构造函数。  
`function person(){};`  
`var person1 = new person();`  
`person.prototype = {`  
`	name: "aaaaa",`  
	`age: 19999,`  
	`say: function(){`  
	`console.log(this.name);`	  
	`}`  
`};`  
`person1.say(); //person1.say is not a function`  
`person1.__proto__ = person.prototype;`  
`person1.say(); //aaaaa `  
- 5.原生对象的原型   
所有原生引用类型(Object, Array, String等)都在其构造函数的原型上定义了方法，在Array.prototype中可以找到sort()方法，而且String.prototype中可以找到subString()方法。  
`alert(typeof Array.prototype.sort); //function`  
通过原生对象的原型，不仅可以取得默认方法的引用，也可以定义新方法。像修改自定义对象的原型一样修改原生对象的原型，随时添加方法。  
- 6.原型对象的问题  
首先原型对象省略了为构造函数传递初始化参数这一环节，所有实例在默认情况下将会取得相同的属性值。  
原型中所有的属性是被很多实例共享的这种共享对于函数来说非常适合，但对于引用类型值的属性来说就会有问题。  
- 7.组合使用构造函数模式和原型模式  
构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。结果每个实例自己都会有一份实例属性的副本，又同时共享着对方法的引用，最大限度节省内存。这种混合模式还支持向构造函数传递参数。  
`function person(name){  
  this.name = name;  
	this.friends = ["a", "b"];  
};
person.prototype = {  
	constructor: person,  
	say: function(){  
    alert(this.name);  
  }  
}`  
`var person1 = new person("aaa");`  
`person1.friends.push("ccccc");`  
`alert(person1.friends); //a,b,ccccc`  
`alert(person2.friends); //a,b`  
`alert(person1.say === person2.say); //true`  
在上述代码中，实例的属性是在构造函数中定义的，二所有实例共享的属性constructor和方法say都是在原型中定义的，当修改了person1.friends，并不会影响到person2实例中的属性。  

#####  动态原型模式  
将所有的信息全部封装在构造函数中，通过在构造函数中初始化原型，又保持了同时使用构造函数和原型的优点。简而言之可以通过检查某个应该存在的方法是否有效，来决定是否需要初始化原型。  
`function person(name){
  this.name = name;
  if(typeof this.say != "function"){
		person.prototype.say = function({
			alert(this.name);
		};
	};
};`
`var person1 = new person("aaa");`  
`person1.say();`  
在say()不存在时才会将其添加到原型中，这段代码只会在初次调用构造函数时才会执行。
if语句检查的可以是初始化之后应该存在的属性或者方法，不需要将
所有的属性和方法全部检查。对于采用这种模式创建的对象，
可以使用instanceof操作符检查它的类型。  
##### 寄生构造函数模式  
这种模式的基本思想是创建一个函数，该函数的作用仅仅是封装创建对象的代码，
然后再返回新创建的对象。  
`function person(name){
    var o = new Object();
    o.name = name;
    o.say = function(){
        alert(this.name);
    }
    return o;  
}`  
`var person1 = new person("aaa");`  
`person1.say(); //aaa`  
##### 稳妥构造函数模式  
所谓稳妥对象，指的是没有公共属性，而且其方法也不引用this对象。稳妥构造函数遵循与寄生构造函数类似的模式，有两点不同：一是新创建对象的实例方法不引用this；二是不使用new操作符调用构造函数。  
#### 3.继承  
##### 原型链  
ECMAScript中描述了原型链的概念，将原型链作为实现继承的主要方法。基本思想是利用原型链让一个引用类型继承另一个引用类型的属性和方法。每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象内部的指针。假如让原型对象等于另一个类型的实例，此时的原型对象将包含一个指向另一个原型的指针，相应另一个原型对象中也包含着指向另一个够赞函数的指针。若另一个原型又是另一个类型的实例，上述关系成立，就构成了实例与原型的链条。  
实现原型链有一种基本模式：  
`function SuperType(){
  this.property = true;
}`  
`SuperType.prototype.getSuperValue = function(){
    return this.property;
}`  
`function SubType(){
  this.subproperty = false;
}`  
`SubType.prototype = new SuperType();`  
`SubType.prototype.getSubValue = function(){
  return this.subproperty;
}`  
`var instance = new SubType();`  
`alert(instance.getSuperValue); //true`  
1. 不要忘记默认的原型  
代码中创建了两个类型，SuperType与SubType，每个类型都有一个属性和方法，主要区别是SubType继承了SuperType，继承是通过创建SuperType的实例，并将实例赋给SubType.prototype实现的，相当于SubType的原型将作为SuperType的实例，实例中有一个指向SuperType原型的指针。这个实现的本质是重写原型对象，代之以一个新类型的实例。原来存在于SuperType的实例中的所有属性和方法，现在也存在于SubType.prototype中。但是没有使用SubType默认提供的原型，而是给它换了一个原型，这个新原型就是SuperType的实例。所以心源性不仅具有作为一个SuperType的实例所拥有的的全部属性和方法，其内部还有一个指向SuperType原型的指针。所以instance指向SubType的原型，SubType的原型又指向了SuperType的原型。getSuperValue方法依然在SuperType.prototype中，但是property则位于SubType.prototype中。这是因为property是一个实例的属性，而getSuperValue则是一个原型方法。那么SubType.prototype现在是SuperType的实例，那么property当然位于该实例中。  
2. 确定原型与实例的关系  
两种方式：instanceof操作符与isPrototypeOf操作符。  
`instance instanceof Object`  
`instance instanceof SuperType`  
`instance instanceof SubType`  
由于原型链的关系，可以说instance是以上三种类型中的任何一种类型的实例，所以三个构造函数都返回true。  
只有是原型链中出现过的原型，都可以说是该原型链所派生的实例的原型。  
`Object.prototype.isPrototypeOf(instance)`    
`SuperType.prototype.isPrototypeOf(instance)`    
`SubType.prototype.isPrototypeOf(instance)`    
以上代码都会返回true。  
3. 谨慎定义方法  
子类中有时需要重写超类型中的某个方法，或者添加超类型中不存在的某个方法，但给原型添加方法的代码一定要放在替换原型的语句之后。  
在通过原型链实现继承时，不能使用对象字面量创建原型方法，因为这样就会重写原型链。  
4. 原型链的问题  
最主要的问题是包含来自引用类性值的原型。包含引用类型值的原型属性会被所有的实例共享，这正是为什么要在构造函数中，而不是在原型对象中定义属性的原因。在通过原型来实现继承时，原型实际上会变为另一个类型的实例。于是，原来的实例属性就变成了现在的原型属性。  
第二个问题是：在创建子类型的实例时，不能向超类型的构造函数中传递参数。实际上应该说是没有办法在不影响所有对象的实例的情况下，给超类型的构造函数传递参数。  

##### 借用构造函数  
在子类型构造函数的内部调用超类型构造函数，函数只是在特定环境下执行代码的对象，因此通过使用apply和call方法也可以再新创建的对象上执行构造函数。  
`function SuperType(){
  this.color = ["red", "green"];
}`  
`function SubType(){
  SuperType.call(this);
}`  
`var instance1 = new SubType();`  
`instance1.color.push("black");`  
`alert(instance1.color); //["red", "green", "black"]`  
`var instace2 = new SubType();`  
`alert(instace2.color); //["red", "green"]`  
1. 传递参数  
相较于原型链而言，借用构造函数可以在子类型构造函数中向超类型构造函数传递参数。  
`function SuperType(name){
  this.name = name;
}`  
`function SubType(){
  //继承了SuperType，同时传递了参数  
  SuperType.call(this, "aaa");
  //实例属性  
  this.age = 23;
}`  
`var instance = new SubType();`  
`alert(instance.name); //aaa`    
`alert(instance.age); //23`  
2. 借用构造函数的问题  
如果仅仅是借用构造函数那么将无法避免构造函数模式存在的问题——方法都在构造函数中定义，因此函数复用无从谈起。并且在超类型的原型中定义的方法，对于子类型而言也是不可见的，结果就是所有的类型只能通过构造函数模式。  

##### 组合继承  
指的是将原型链和借用构造函数的技术组合在一起。其思路是使用原型链实现对原型属性的和方法的继承，而通过借用构造函数来实现对实例属性的继承，这样既通过在原型上定义方法实现了函数复用，又能够保证每个实例都有它自己的属性。  
`function SuperType(name){
  this.name = name;
  this.color = ["red", "green"];
}`  
`SuperType.prototype.sayName = function(){
  alert(this.name);
}`    
`function SubType(name,age){
  //继承属性  
  SuperType.call(this,name);
  this.age = age;
}`  
`SubType.property = new SuperType();`  
`SubType.property.constructor = SubType;`  
`SubType.prototype.sayAge = function(){
  alert(this.age);
}`  
`var instance1 = new SubType("aaa", 23);`  
`instance1.color.push("black");`  
`alert(instance1.color); //["red", "green", "black"]`  
`instance1.sayName();  //aaa`  
`instance1.sayAge(); //23`  
`var instace2 = new SubType("bbb", 22)`  
`alert(instace2.color); //["red", "green"]`  
`instace2.sayName(); //bbb`  
`instace2.sayAge(); //22`  
例子中，SuperType构造函数定义了两个属性，name和color。SuperType的原型定义了一个方法sayName。SubType构造函数在调用SuperType构造函数时传入了name参数，又继续定义了自己的属性age。然后将SuperType的实例赋值给SubType的原型，然后又在该原型上定义了自己的方法sayAge。这样就可以让两个不同的SubType实例分别拥有自己的属性——包括color属性，又可以使用相同的方法。  
组合继承避免了原型链和借用构造函数的缺陷，融合二者优点，是js中最常用的继承模式，并且通过instanceof和isPrototypeOf方法可以识别基于组合继承创建的对象。  

##### 原型式继承  
`function object(o){
  function F(){}  
  F.property = o;
  return new F();
}`  
在object函数内部先创建了一个临时性的构造函数，然后将传入的对象作为这个构造函数的原型，最后返回了这个临时函数的一个新实例。从本质上说，object对传入其中的对象执行了一次浅复制。  
原型式继承，要求必须有一个对象可以作为另一个对象的基础。如果有这样一个对象，可以把它传递给object函数，然后再根据具体需求对得到的对象加以修改即可。  
ECMAScript5通过新增Object.create()方法规范了原型式继承。这个方法接收两个参数：一个用作新对象原型的对象和（可选）一个为新对象定义额外属性的对象。在传入一个参数的情况下，Object.create()与 Object()方法行为相同。  
`var person = {
  name: "aaa",
  friend: ["a", "b"]
}`  
`var anotherPerson = Object.create(person);`  
`anotherPerson.name = "bbb";`  
`anotherPerson.friend.push("ccc");`  
Object.create()方法的第二个参数，每个属性都是通过自己的描述符定义的，以这种方式指定的任何属性都会覆盖原型对象上的同名属性。  
但是引用类型值的属性始终都会共享相应的值，就像使用原型模式继承一样。  

##### 寄生式继承  
寄生式继承是与原型式继承紧密相关的一种思路。寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后返回对象 。  
`function createAnother(original){
  var clone = onject(original);
  clone.sayHi = function(){
    alert("hi");
  };
  return clone;
}`  
本例中，createAnother()函数接收了一个参数，也就是将要作为新对象基础的对象。然后把这个对象(original)传递给Object()函数，将返回的结果赋给clone，再为clone对象添加一个新方法sayHi，最后返回clone对象。  
##### 寄生组合式继承  
组合继承最大的问题就是在任何情况下都会调用两次超类型构造函数：一次是在创建子类型的原型的时候，另一次是在子类型构造函数内部，子类型最终会包含超类型对象的全部实例属性，但我们不得不在调用子类型构造函数时重写这些属性。  
`function SuperType(name){
  this.name = name;
  this.color = ["red", "green"];
}`  
`SuperType.prototype.sayName = function(){
  alert(this.name);
}`  
`function SubType(name, age){
  SubType.call(this,name); //第二次调用
  this.age = age;
}`  
`SubType.prototype = new SuperType(); //第一次调用SuperType()`  
`SubType.prototype.constructor = SubType;`  
`SubType.prototype.sayAge = function(){
  alert(this.age);
}`  
在第一次调用SuperType构造函数时，SubType.prototype会得到两个属性：name和color；它们都是SuperType的实例属性，只不过现在位于SubType的原型中。当调用SubType构造函数时，又会调用一次SuperType构造函数，这一次又在新对象上创建了两个实例属性，name和coloe。于是这两个属性就屏蔽了原型中的两个同名属性。  
寄生组合式继承的基本模式：  
`function inheritPrototype(subType,superType){
  //创建对象  
  var prototype = object(superType);  
  //增强对象  
  prototype.constructor = subType;  
  //指定对象  
  subType.prototype = prototype;
}`  
这个函数接收两个参数：子类型构造函数和超类型构造函数。在函数内部，第一步创建超类型原型的一个副本。第二步为创建的副本添加constructor属性，从而弥补因为重写原型而失去默认的constructor属性。最后将新创建的对象赋值给子类型的原型。  
这个例子高效率体现在只调用了一次SuperType构造函数，并且避免了在SubType.prototype上创建不必要的属性。与此同时原型链还能保持不变，因此可以正常使用instanceof和isPrototypeOf方法。寄生组合式继承是引用类型最理想的继承范式。  
