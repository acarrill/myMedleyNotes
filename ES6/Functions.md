# **Functions**
## **Index**
1. **Arrow Functions**
  1. **'This' on regular functions**
  1. **'This' on arrow functions**
1. **Default Functions Parameters**
1. **Classes on JavaScript**
  1. **ES6 Classes**
  1. **Static Methods**
1. **JavaScript Subclases**
  1. **QUIZ**
### **1.Arrow Functions**
Regular functions can be either **function declarations** or **function expressions**, however arrow functions are always expressions. In fact, their full name is "arrow function expressions", so they can only be used where an expression is valid. This includes being:
- stored in a variable,
- passed as an argument to a function,
- and stored in an object's property.
One confusing syntax is when an arrow function is stored in a variable.
```javascript
const greet = name => `Hello ${name}!`;
```

**Parentheses and arrow function parameteres: **various parameter must  be passed through parentheses.

### ***1.1 'This' on regular functions***
To get a handle on how undefinedthisundefined works differently with arrow functions, let's do a quick recap of how undefinedthisundefined works in a standard function. If you have a solid grasp of how undefinedthisundefined works already, feel free to [**jump over this section**]([object Object]).
The value of the undefinedthisundefined keyword is based completely on how its function (or method) is called. undefinedthisundefined could be any of the following:
### A new object
If the function is called with undefinednewundefined:
```javascript
const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);

```
In the code above, the value of undefinedthisundefined inside the undefinedSundaeundefined constructor function is a new object because it was called with undefinednewundefined.
### A specified object
If the function is invoked with undefinedcallundefined/undefinedapplyundefined:
```javascript
const result = obj1.printName.call(obj2);

```
In the code above, the value of undefinedthisundefined inside undefinedprintName()undefined will refer to undefinedobj2undefined since the first parameter of undefinedcall()undefined is to explicitly set what undefinedthisundefined refers to.
### A context object
If the function is a method of an object:
```javascript
data.teleport();

```
In the code above, the value of undefinedthisundefined inside undefinedteleport()undefined will refer to undefineddataundefined.
### The global object or undefined
If the function is called with no context:
```javascript
teleport();

```
In the code above, the value of undefinedthisundefined inside undefinedteleport()undefined is either the global object or, if in strict mode, it's undefinedundefinedundefined.
### ***1.2 'This' on arrow functions***
With regular functions, the value of undefinedthisundefined is set based on *how the function is called*. With arrow functions, the value of undefinedthisundefined is based on *the function's surrounding context*. In other words, the value of undefinedthisundefined *inside* an arrow function is the same as the value of undefinedthisundefined *outside* the function.

### Examples of *this* scope; 1º Regular function 2º Closure 3º Arrow function:
### 1º
```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  setTimeout(function() {
    this.scoops++;
    console.log('scoop added!');
  }, 500);
};

const dessert = new IceCream();
dessert.addScoop();

```
undefinedResult: 0undefined
### 2º
```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  const cone = this; // sets `this` to the `cone` variable
  setTimeout(function() {
    cone.scoops++; // references the `cone` variable
    console.log('scoop added!');
  }, 0.5);
};

const dessert = new IceCream();
dessert.addScoop();
```
undefinedResult: 1undefined
### 3º
```javascript
// constructor
function IceCream() {
  this.scoops = 0;
}

// adds scoop to ice cream
IceCream.prototype.addScoop = function() {
  setTimeout(() => { // an arrow function is passed to setTimeout
    this.scoops++;
    console.log('scoop added!');
  }, 0.5);
};

const dessert = new IceCream();
dessert.addScoop();
```
undefinedResult: 1undefined

## **undefined2.Default Functions Parametersundefined**
### ***Default function parameters***
**Default function parameters** are quite easy to read since they're placed in the function's parameter list:
```javascript
function greet(name = 'Student', greeting = 'Welcome') {
  return `${greeting} ${name}!`;
}

greet(); // Welcome Student!
greet('James'); // Welcome James!
greet('Richard', 'Howdy'); // Howdy Richard!
```
### *undefinedExample using destructuring in default parametersundefined*
```javascript
/*
 * Programming Quiz: Using Default Function Parameters (2-2)
 */

// your code goes here
function buildHouse ({floors = 1, color = "red", walls = "brick"} = {}){
    return (`Your house has ${floors} floor(s) with ${color} ${walls} walls.`)   
}


console.log(buildHouse()); // Your house has 1 floor(s) with red brick walls.
console.log(buildHouse({})); // Your house has 1 floor(s) with red brick walls.
console.log(buildHouse({floors: 3, color: 'yellow'})); // Your house has 3 floor(s) with yellow brick walls.
```

## ***undefined3.Classes on JavaScriptundefined***
### ***ES5 "Class" Recap***
Since ES6 classes are just a mirage and hide the fact that ***prototypal inheritance is actually going on under the hood***, let's quickly look at how to create a "class" with ES5 code:
```javascript
function Plane(numEngines) {
  this.numEngines = numEngines;
  this.enginesActive = false;
}

// methods "inherited" by all instances
Plane.prototype.startEngines = function () {
  console.log('starting engines...');
  this.enginesActive = true;
};

const richardsPlane = new Plane(1);
richardsPlane.startEngines();

const jamesPlane = new Plane(4);
jamesPlane.startEngines();
```
### ***ES6 Classes***
Here's what that same undefinedPlaneundefined class would look like if it were written using the new undefinedclassundefined syntax:
```javascript
class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}
```
> **⚠️ Where Are All The Commas? ⚠️**
Did you notice that there aren't any commas between the method definitions in the Class? Commas are not used to separate properties or methods in a Class. If you add them, you'll get a undefinedSyntaxErrorundefined of undefinedunexpected token ,undefined

### ***Static methods***
> Description
> Static method calls are made directly on the class and are not callable on instances of the class. Static methods are often used to create utility functions.

To add a static method, the keyword undefinedstaticundefined is placed in front of the method name. Look at the undefinedbadWeather()undefined method in the code below.
```javascript
class Plane {
  constructor(numEngines) {
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  static badWeather(planes) {
    for (plane of planes) {
      plane.enginesActive = false;
    }
  }

  startEngines() {
    console.log('starting engines…');
    this.enginesActive = true;
  }
}

```
See how undefinedbadWeather()undefined has the word undefinedstaticundefined in front of it while undefinedstartEngines()undefined doesn't? That makes undefinedbadWeather()undefined a method that's accessed directly on the undefinedPlaneundefined class, so you can call it like this:
undefinedPlane.badWeather([plane1, plane2, plane3]);undefined

> ***From class constructor and other methods***
> Static methods are not directly accessible using the [undefinedthisundefined]([object Object]) keyword from non-static methods. You need to call them using the class name: undefinedCLASSNAME.STATIC_METHOD_NAME()undefined or by calling the method as a property of the undefinedconstructorundefined: undefinedthis.constructor.STATIC_METHOD_NAME()undefined.

## **4.JavaScript Subclasses**
Now that we've looked at creating classes in JavaScript. Let's use the new undefinedsuperundefined and undefinedextendsundefined keywords to extend a class.
```javascript
class Tree {
  constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
    this.size = size;
    this.leaves = leaves;
    this.leafColor = null;
  }

  changeSeason(season) {
    this.leafColor = this.leaves[season];
    if (season === 'spring') {
      this.size += 1;
    }
  }
}

class Maple extends Tree {
  constructor(syrupQty = 15, size, leaves) {
    super(size, leaves);
    this.syrupQty = syrupQty;
  }

  changeSeason(season) {
    super.changeSeason(season);
    if (season === 'spring') {
      this.syrupQty += 1;
    }
  }

  gatherSyrup() {
    this.syrupQty -= 3;
  }
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');

```
Both undefinedTreeundefined and undefinedMapleundefined are JavaScript classes. The undefinedMapleundefined class is a "subclass" of undefinedTreeundefined and uses the undefinedextendsundefined keyword to set itself as a "subclass". To get from the "subclass" to the parent class, the undefinedsuperundefined keyword is used. Did you notice that undefinedsuperundefined was used in two different ways? In undefinedMapleundefined's constructor method, undefinedsuperundefined is used as a function. In undefinedMapleundefined's undefinedchangeSeason()undefined method, undefinedsuperundefined is used as an object!

## **4.1QUIZ**
### ***Directions:***
Create a undefinedBicycleundefined subclass that extends the undefinedVehicleundefined class. The undefinedBicycleundefined subclass should override undefinedVehicleundefined's constructor function by changing the default values for undefinedwheelsundefined from undefined4undefined to undefined2undefined and undefinedhornundefined from undefined'beep beep'undefined to undefined'honk honk'undefined.
### ***Your Code:***
```javascript
/*
 * Programming Quiz: Building Classes and Subclasses (2-3)
 */

class Vehicle {
	constructor(color = 'blue', wheels = 4, horn = 'beep beep') {
		this.color = color;
		this.wheels = wheels;
		this.horn = horn;
	}

	honkHorn() {
		console.log(this.horn);
	}
}

// your code goes here
class Bicycle extends Vehicle{
    constructor(color = 'blue', wheels = 2, horn = 'honk honk'){
        super(color, wheels, horn);
    }
}

/* tests
const myVehicle = new Vehicle();
myVehicle.honkHorn(); // beep beep
const myBike = new Bicycle();
myBike.honkHorn(); // honk honk
*/

```
