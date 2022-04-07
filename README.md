# Membuat Constructor Function

Sebelum javascript versi 6, pembuatan class biasaya dilakukan dengan menggunakan function. Hal ini dilakukan karena javascript bukanlah bahasa yang berfokus ke OOP. Dan function untuk membuat class tersebut yang dinamakan constructor funtion. Cara pembuatan constructor function juga sama dengan pembuatan function biasanya. Namun bedanya dalam best practice nya itu namanya diawali dengan huruf kapital dan kalau namanya lebih dari satu kata maka menggunakan camel case.

```js
// constructor function
function Person() {}
```

Setelah membuat constructor function, jika kita ingin membuat class dari constructor function tersebut maka kita bisa menggunakan **new** diikuti nama constructor function nya (class nya).

```js
function Person() {}

const ivan = new Person();
const rizky = new Person();
```

# Property di Constructor Function

Untuk menambahkan properti di constructor function kita bisa melakukanya dengan menggunakan keyword this lalu diikuti dengan nama parameter yang akan kita buat.

```js
function Person() {
  this.firstName = "";
  this.lastName = "";
}

const ivan = new Person();
// set firstName to Ivan
ivan.firstName = "Ivan";
```

# Method di Contructor Function

Jika kita membuat method di contructor function maaka object yang dibuat dari contructor function tersebut akan secara otomatis mempunyai method yang sama seperti di contructor function.

```js
function Person() {
  this.firstName = "";
  this.lastName = "";
  this.sayHello = function (name) {
    console.log(`Hello ${name} my name is ${this.firstName}`);
  };
}

// * pemanggilan method
const ivan = new Person();
ivan.firstName = "Ivan";
ivan.sayHello("Sayang");
```

# Parameter di Constructor Function

Karena constructor function sama seperti function biasa, maka hal tersebut membuat constructor function juga bisa kita kasih parameter. Hal ini bisa kita lakukan ketika pertama kali membuat object dan kita bisa langsung memasukkan parameter di constructor function.

```js
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.sayHello = function (name) {
    console.log(`Hello ${name} my name is ${this.firstName}`);
  };
}

// * pembuatan object dengan constructor funcion yang memiliki parameter
const ivan = new Person("Ivan", "Rizky Saputra");
```

# Constructor Inheritance

Di dalam constructor function, kita juga bisa melakukan pemanggilan constructor function lain dan mewarisi seluruh properti dan method dari constructor yang dipanggil tersebut. Hal semacam ini biasanya kita sebut dengan nama **Inheritance** (namun pada constructor function tidak murni inheritance melainkan hanya melakukan proses copy di belakangnya). Cara pemanggilan seperti ini bisa dilakukan dengan cara **NamaFunction.call(this, parameter)**.

```js
function Employee(firstName) {
  this.firstName = firstName;
  this.sayHello = function (name) {
    console.log(`Hi ${name} My name is ${this.firstName}`);
  };
}

function Manager(firstName, lastName) {
  // ini  digunakan untuk memanggil constructor function Employee
  Employee.call(this, firstName);
  this.lastName = lastName;
}
```

## Class

Sejak ES 6, ada kata kunci baru untuk membuat class di javascript dengan menggunakan kata kunci **class**, dengan kata kunci ini, kita tidak perlu lagi menggunakan contructor function untuk membuat class di javascript seperti versi sebelumnya. Namun untuk dibelakang layar juga masih akan dibuatkan prototype seperti yang terjadi di contructor function.

```js
class Person {}
const ivan = new Person();
console.log(ivan);
```

## Constructor di Class

Untuk membuat constructor di class maka kita bisa menggunakan kata kunci **constructr(parameter)**.

```js
class Person {
  constructor(name) {
    console.log(`Membuat Persn ${name}`);
  }
}
const ivan = new Person("ivan");
console.log(ivan);
```

## Property di Class

Kita juga bisa membuat property d class dengan men set nya di dalam constructor dengan menggunakan keyword **this.** diikuti nama dari property nya.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}
const ivan = new Person("ivan");
console.log(ivan);
console.log(ivan.name);
```

## Method di Class

Kita juga bisa menambahkan method di class dengan cara yang sama seperti di constructor function. Namun bedanya saat kita menambahkan method di class, itu akan secara otomatis menambahkan di constructor nya bukan di object instance nya. Dan hal itu sangat menguntungkan karena untuk membuat method yang direkomendasikan adalah membuatnya di prototype.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello(name) {
    console.log(`Hello ${name}, my name is ${this.name}`);
  }
}
const ivan = new Person("ivan");
console.log(ivan);
console.log(ivan.name);
ivan.sayHello("fikri");
```

## Class Inheritance

Kita bisa melakukan pewarisan terhadap suatu class ke kelas lain dengan menggunakan kata kunci **extends**. Di javascript class inherintance itu sama dengan prototype inheritance.

```js
class Employee {
  sayHello(name) {
    console.log(`Hello ${name} my name is ${this.name}`);
  }
}
class Manager extends Employee {
  sayHello(name) {
    console.log(`Hello ${name} my name is ${this.name}`);
  }
}

const ivan = new Employee();
ivan.name = "Ivan";
ivan.sayHello("Vera");
const rizky = new Manager();
rizky.name = "Rizky";
rizky.sayHello("Viola");
```

## Super Constructor

Jika kita dari child class ingin mengakses constructor dari parent class maka kita bisa melakukanya dengan menggunakan keyword **super** namun secara default hal ini sudah dilakukan. Selain itu jika kita membuat constructor di child class maka kita wajis untuk menjalankan constructor di parent walaupun di parent tidak ada constructor.

```js
class Employee {
  constructor(firstName) {
    this.firstName = firstName;
  }

  sayHello(name) {
    console.log(`Hello ${name} my name is ${this.firstName}`);
  }
}
class Manager extends Employee {
  constructor(firstName, lastName) {
    super(firstName);
    this.lastName = lastName;
  }
  sayHello(name) {
    console.log(`Hello ${name} my name is ${this.lastName}`);
  }
}

const ivan = new Employee("Ivan");
ivan.sayHello("Vera");
const rizky = new Manager("Ivan", "Rizky");
rizky.sayHello("Viola");
```

## Super Method

Untuk memanggil method di parent dari child kita bisa melakukanya dengan menggunakan perintah super

```js
class Shape {
  paint() {
    console.log("Paint Shape");
  }
}
class Circle extends Shape {
  paint() {
    super.paint();
    console.log("Paint Circle");
  }
}

const one = new Shape();
one.paint();
const two = new Circle();
two.paint();
```

## Geter dan Seter

Class juga mendukung geter dan seter, namun geter dan seter di sini berada di protorype bukan di object instance nya

```js
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }

  set fullName(value) {
    const result = value.split(" ");
    this.firstName = result[0];
    this.lastName = result[1];
  }
}

const one = new Person("Ivan", "Rizky");
console.log(one);
console.log(one.fullName);

one.fullName = "Ivan Saputra";
console.log(one);
```

## Public Class Field

Kita bisa membuat public class field dengan cara langsung membuat nama field dan value selevel dengan method. Jika kita tidak memberikan value maka nilai field akan undefined.

```js
class Customer {
  firstName;
  lastName;
  balance = 0;

  constructor() {}

  sayHello() {}
}

const ivan = new Customer();
console.log(ivan);
// * kita bisa melakukan seperti ini karena balance bersifat public
console.log(ivan.balance);
```

## Private Class Field

Untuk membuat private class field kita bisa menggunakan tanda **#** sebelum nama field.

```js
class Counter {
  #counter = 0;

  increment() {
    this.#counter++;
  }

  decrement() {
    this.#counter--;
  }
  getCounter() {
    return this.#counter;
  }
}

const counter = new Counter();
counter.increment();
counter.increment();
console.log(counter.getCounter());
// * kode dibawah ini akan error
// console.log(counter.#counter)
```

## Private Method

Sama seperti field, kita juga bisa menambahkan privae method dengan menggunakan tanda **#** sebelum pemberian nama method.

```js
class Name {
  say(name) {
    if (name) {
      this.#sayWithName(name);
    } else {
      this.#sayWithoutName();
    }
  }

  #sayWithName(name) {
    console.log(`Hallo ${name}`);
  }

  #sayWithoutName() {
    console.log("hallo");
  }
}

const person = new Name();
person.say("ivan");
person.say();
```

## Static Class Field

Kita bisa membuat field yang sifatnya global tanpa bergantung kepada object instance dengan menggunakan keywoord statis sebelum penamaan field. Hai ini juga membuat field seolah olah menjadi variable global yang bisa di akses di mana saja

```js
class Configuration {
  static name = "Ivan Rizky Saputra";
  static age = 19;
}

console.log(Configuration.name);
console.log(Configuration.age);
```

## Static Class Method

Selain itu kita juga bisa membuat static method agar bisa diakses dimana saja dan tidak bergantung pada object instance nya.

```js
class Logger {
  static log() {
    return "Hai sayang";
  }
}
console.log(Logger.log());
```

## Membuat Class Erroor

Kita bisa dengan mudah membuat custom class error di javascript dengan membuat turunan dari class Error yang merupakan defaul dari javascript sendiri.

```js
class ValidationError extends Error {
  constructor(message, field) {
    super(message);
    this.field = field;
  }
}
```
