# List the basic feature rightaway.

Following are very basic and simple example of new features of ES6. These are most used among others, just take a look and if you find anything missing please comment create issues.

## 1> Constants:
ES5:
```
Object.defineProperty(typeof global === "object" ? global : window, "PI", {
    value:        3.141593,
    enumerable:   true,
    writable:     false,
    configurable: false
})
PI > 3.0;
```
ES6:
```
const PI = 3.141593
PI > 3.0
```
---

## 2> Arrow functions :
### Expression Bodies
ES5:
```
odds  = evens.map(function (v) { return v + 1; });
nums  = evens.map(function (v, i) { return v + i; });
```
ES6:
```
odds  = evens.map(v => v + 1)
nums  = evens.map((v, i) => v + i)
```

### Statement Bodies
ES5:
```
nums.forEach(function (v) {
   if (v % 5 === 0)
       fives.push(v);
});
```
ES6:
```
nums.forEach(v => {
   if (v % 5 === 0)
       fives.push(v)
})
```
### Lexical this
ES5:
```
var self = this;
this.nums.forEach(function (v) {
    if (v % 5 === 0)
        self.fives.push(v);
});
```
ES6:
```
this.nums.forEach((v) => {
    if (v % 5 === 0)
        this.fives.push(v)
})
```
---

## Extended parameter handling
ES5:
```
function f (x, y, z) {
    if (y === undefined)
        y = 7;
    if (z === undefined)
        z = 42;
    return x + y + z;
};
f(1) === 50;
```
ES6:
```
function f (x, y = 7, z = 42) {
    return x + y + z
}
f(1) === 50
```
---
## String Interpolation:
ES5:
```
var customer = { name: "Foo" };
var card = { amount: 7, product: "Bar", unitprice: 42 };
var message = "Hello " + customer.name + ",\n" +
"want to buy " + card.amount + " " + card.product + " for\n" +
"a total of " + (card.amount * card.unitprice) + " bucks?";
```
ES6:
```
var customer = { name: "Foo" }
var card = { amount: 7, product: "Bar", unitprice: 42 }
var message = `Hello ${customer.name},
want to buy ${card.amount} ${card.product} for
a total of ${card.amount * card.unitprice} bucks?`
```
---
## Object properties:

### computed properties name:
ES5:
```
var obj = {
    foo: "bar"
};
obj[ "baz" + quux() ] = 42;
```
ES6:
```
let obj = {
    foo: "bar",
    [ "baz" + quux() ]: 42
}
```

### Method properties:
ES5:
```
obj = {
    foo: function (a, b) {
        …
    },
    bar: function (x, y) {
        …
    },
    //  quux: no equivalent in ES5
    …
};
```
ES6:
```
obj = {
    foo (a, b) {
        …
    },
    bar (x, y) {
        …
    },
    *quux (x, y) {
        …
    }
}
```
---
## Classes

### Defination:
ES5:
```
var Shape = function (id, x, y) {
    this.id = id;
    this.move(x, y);
};
Shape.prototype.move = function (x, y) {
    this.x = x;
    this.y = y;
};
```
ES6
```
class Shape {
    constructor (id, x, y) {
        this.id = id
        this.move(x, y)
    }
    move (x, y) {
        this.x = x
        this.y = y
    }
}
```
### Inheritance :
ES5:
```
var Rectangle = function (id, x, y, width, height) {
    Shape.call(this, id, x, y);
    this.width  = width;
    this.height = height;
};
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;
var Circle = function (id, x, y, radius) {
    Shape.call(this, id, x, y);
    this.radius = radius;
};
Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.constructor = Circle;
```
ES6:
```
class Rectangle extends Shape {
    constructor (id, x, y, width, height) {
        super(id, x, y)
        this.width  = width
        this.height = height
    }
}
class Circle extends Shape {
    constructor (id, x, y, radius) {
        super(id, x, y)
        this.radius = radius
    }
}
```
---
## Promise:
ES5:
```
function msgAfterTimeout (msg, who, timeout, onDone) {
    setTimeout(function () {
        onDone(msg + " Hello " + who + "!");
    }, timeout);
}
msgAfterTimeout("", "Foo", 100, function (msg) {
    msgAfterTimeout(msg, "Bar", 200, function (msg) {
        console.log("done after 300ms:" + msg);
    });
});
```
ES6:
```
function msgAfterTimeout (msg, who, timeout) {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${msg} Hello ${who}!`), timeout)
    })
}
msgAfterTimeout("", "Foo", 100).then((msg) =>
    msgAfterTimeout(msg, "Bar", 200)
).then((msg) => {
    console.log(`done after 300ms:${msg}`)
})
```
OR
```
function fetchAsync (url, timeout, onData, onError) {
    …
}
let fetchPromised = (url, timeout) => {
    return new Promise((resolve, reject) => {
        fetchAsync(url, timeout, resolve, reject)
    })
}
Promise.all([
    fetchPromised("http://backend/foo.txt", 500),
    fetchPromised("http://backend/bar.txt", 500),
    fetchPromised("http://backend/baz.txt", 500)
]).then((data) => {
    let [ foo, bar, baz ] = data
    console.log(`success: foo=${foo} bar=${bar} baz=${baz}`)
}, (err) => {
    console.log(`error: ${err}`)
})
```
---
