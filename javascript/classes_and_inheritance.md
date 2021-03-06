[back](README.md)

# Classes & Inheritance

## Prototypes
  - Every function has a `prototype` property that points to an object
  - Functions can either be invoked as a constructor using the `new` keyword, or
      normally
  - If a function is invoked normally, the prototype is ignored
  - If a function is invoked as a constructor,
      - a new object is created
      - the new object delegates failed property lookups to the constructor
          function's prototype object
      - `this` inside the constructor function body is set to the new object
      - the new object is returned after the function executes
  - A 'class' in Javascript is represented as constructor function with instance
      methods attached to its prototype object
  - By convention, constructor function names should start with a capital letter
  - Arrow functions can’t be used as constructor functions, because they don’t have a
    prototype property

## Class Syntax ES5

```js
// Class
// =======

// constructor function
function Dog (name) {
  this.name = name
}

// class property
Dog.breed = ‘Mutt’

// class method
Dog.printBread = function () {
  console.log(this.breed)
}

// instance method
Dog.prototype.bark = function () {
  console.log(‘woof’)
}

// private instance method
// (this is just a naming convention, privacy is not enforced)
Dog.prototype._poop = function () {
}

// Subclass
// ========

function Poodle (name, size) {
  // call superclass's constructor on `this`
  Dog.call(this, name)
  this.size = size
}

// delegate missed property lookups to the Dog prototype
Poodle.prototype = Object.create(Dog.prototype)

// update constructor property to point to Poodle
Poodle.prototype.constructor = Poodle

Poodle.prototype.doTrick = function() {
  console.log(‘<plays dead>’)
}
```

## Class Syntax ES6

ES6 adds some sugar over this mess.

```js
// Class
// =======

// constructor
class Dog {
  constructor (name) {
    this.name = name
  }

  // class properties
  static breed = ‘Mutt'

  // class method
  static printBreed () {
    console.log(this.breed)
  }

  // instance method
  bark () {
    console.log(‘woof’)
  }

  // private instance method
  #poop() {
  }
}

// Subclass
// ========

class Poodle extends Dog {
  constructor(name, size) {
    super(name)
    this.size = size
  }

  doTrick () {
    console.log(‘<plays dead>’)
  }
}
```
