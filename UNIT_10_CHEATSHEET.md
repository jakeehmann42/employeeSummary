### Creating a constructor

```javascript
function Shape(width,height){
    this.width = width;
    this.height = height;

    this.area = () => {
        return this.width * this.height;
    }
}
```

Constructors are functions that return new objects. Quite simply, they are designed to make *repeatable* code and object creation easier; this way we can seperate the *blueprint* and the *instance*. Our constructor functions as the blueprint, in which we are defining how a shape behaves. 

Important rules:
* Capitalize your constructors. This is standard.
* Assign the values you want every *thingy* to have with ```this.property```, where property is the name of the property you are assigning to.

We then create new shapes:
```javascript
const square = new Shape(2,2);
console.log(square.area());

const rectangle = new Shape(4,2);
console.log(rectangle.area());
```
We first use the *new* key word, followed by calling the constructor function. We pass in arguments to match the parameters of the constructor, and then in the constructor function, we construct what a shape is. In ours, we have said that we take in two parameters, height and width, and then a 'Shape' is an object that has 3 keys; height, set to the given height, width, set to the given width, and then area, a function that returns height * width;

We can also attach functions to *all instances of Shape* by using the prototype interface. This is a nice feature in JavaScript that lets you modifying all existing Shapes *after* the constructor has been defined. We can do so by:

```javascript
Shape.prototype.perimeter = function(){
    return 2 * (this.width + this.height);
}
```

Important things to note:
* We assign to *Constructor*.prototype.*new Method Name*
* We *must* give it a function definition in the old way, not an arrow function. (Long story short, this predates arrow functions, kinda)
* We can still use ```this```!


### Classes

ES6 introduced a new way to make objects... Classes!

These are probably familiar to anyone who came from a class-based language like Java, and while they operate a little differently underneath the hood, at a surface level, they are similar.

Classes are in fact "special functions", and just as you can define function expressions and function declarations, the class syntax has two components: class expressions and class declarations.

One way to define a class is using a class declaration. To declare a class, you use the class keyword with the name of the class ("Rectangle" here).

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

A class expression is another way to define a class, but we can hold off on that!

The class has a body, the methods and properties, and most importantly, the constructor. The constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name "constructor" in a class. A SyntaxError will be thrown if the class contains more than one occurrence of a constructor method.

Also, a constructor can use the `super` keyword to call the constructor of the `super` class.

For example:

```javascript
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Getter
  get area() {
    return this.calcArea();
  }
  // Method
  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area); // 100
```

We can then, just the same as we did with constructor functions, use the new keyword, followed by a call to the Class definition, matching the arguments to the parameters in the constructor function.

#### Extending:

Sub classing with extends
The extends keyword is used in class declarations or class expressions to create a class as a child of another class.

```javascript
class Animal { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name); // call the super class constructor and pass in the name parameter
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}

let d = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```
If there is a constructor present in the subclass, it needs to first call super() before using "this".

### Running tests

- Jest, and other testing frameworks that mirror Jests, have tests that are organized into describe and it blocks. These are primarily for grouping tests by module, functionality, etc.

- Any file inside of the test folder ending with .test.js gets run by Jest automatically when we run the npm run test script.

- The expect function is used for assertions. Assertions are essentially statements that are used to verify that our code is doing what we "expect" it to do.

- The instanceof operator can be used to determine if an object was created with a given constructor function.

[Recommended Link: the Docs](https://jestjs.io/docs/en/getting-started)
[Matchers](https://jestjs.io/docs/en/using-matchers)

Writing a test:
```javascript
test("What I am testing ", () => {
    // My actual test
    let a = 2;
    let b = 2;
    expect(Math.pow(a,b)).toEqual(4);
});
```
We first write our test function, which takes to arguments:
- the name of the test, make it descriptive!
- a callback, which is our actual test

Then inside our callback, we write our test. We set up anything that needs setup, and then execute code, ending in one or more assertions:
- These assertions are the things we are evaluating for!
- In my example, I expect Math.pow, the power function, to return 4, because 2 squared is 4;.
- We write assertions using the ```expect.matcher.value``` in the most basic structure!