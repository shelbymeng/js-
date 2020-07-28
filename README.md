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
#### 创建对象
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
