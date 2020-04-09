# JavaScript Foundation 2

## Execution Context
- a part of creation phase
- JS creates a new execution context whenever we call another function
- the base execution context is **global execution context**
- this base execution context gets popped off when the final line of code runs
- all code in JS is a part of an execution context
- in global execution context, this === global object

## Lexical Environment
- is where you write something
- during lexical analysis, compiler checks to see where the words were written
- a function can be lexically inside another function
- determines our available variables
- where function is called is dynamic scope
- the very first lexical environment is **global lexical environment**

## Hoisting
- occurs between creation and execution phase
- is the movement of variables and function declarations to the top of respective environment during compilation
- allows us to call functions before they are defined
- JS engine allocates memory for variables and functions before the creation phase
- variables are partially hosted, we hoist it but not it's value
- make sure you don't put function inside (), example:
```js
(function fun() {
	// ...
})
```
- the new JS features **const** and **let** don't get hoisted
- function expression:
```js
var hello = function() {
	console.log('hello');
}
```
- function declaration:
```js
function hello() {
	console.log('hello');
}
```
- example: hoisting with function expression
```js
console.log(hello());

var hello = function() {
	console.log('hello');
}

// => undefined (hello is partially hosted)
```

### Hoisting Example(s) 1
- indicate which variable is lost during hoisting
```JS
var a = 1;
var a = 2;

// 

a = undefined
var a = 1;
var a = 2; // doesn't look right, I'll ignore you

//

a = undefined
var a = 1;
```
- now let's do the same for function declarations
```JS
a();
function a() {
	console.log('hi');
};
function b() {
	console.log('bye');
}

// => bye (function declarations get FULLY hoisted)
```

### Hoisting Example 2
- difficult question:
```JS
var favouriteFood = 'grapes';

var foodThoughts = function() {
	console.log('original', favouriteFood);
	var favouriteFood = "sushi";
	console.log('new', favouriteFood);
};

foodThoughts();

// => original undefined
// => new sushi
```
- favouriteFood gets hoisted inside of the function
- hoisting happens on EVERY execution context
- to avoid hoisting, use const and let

### Hoisting Example 3
```JS
function bigBrother() {
	function littleBrother() {
		return 'it is me!';
	};
	return littleBrother();
	function littleBrother() {
		return 'no me!';
	};
};

bigBrother();

// => no me!  
```

## Function Invocation
- instead of global context, we get local and arguments
- arguments is an object that contains the parameters that are passed in
- it is avilable when we create a new execution context

## arguments Keyword
- avoid using this, JS engine is less able to optimize our code because it doesn't return a legit object
- instead use:
```JS
Array.from(arguments);
```
- or
```JS
function func(...args) {
	console.log(args[0]);
}
```

## Variable Environment
- a place where variables live
- example:
```JS
function two() {
	var isValid;
}

function one() {
	var isValid = true;
	two();
}

var isValid = false;
one();

// stack

// two - undefined
// one - true
// global - false
```
- variables are stored either on call stack or as a reference to the memory heap

## Scope Chain
- each context has a link to it's parent
- all functions have global lexical environment
- scope chain gives access to variables in parent environment
- compiler looks at code and attatches all these scope chains before it even runs the code
- **function lexical environment**: function has access to the variable environment of the function that it's inside of
- we should avoid using **eval** because it changes the way scope works in JS

## [[scope]]
- leakage of global variables example:
```JS
function weird() {
	height = 40;
	return height;
}
weird();
```
- height hasn't been declared so it goes up a scope chain to global environment and creates it
- to prevent this from happening, we can use 'use strict'
- example:
```JS
var heyhey = function doodle() {
	return 'heyhey';
}

heyhey(); // => heyhey
doodle(); // => ReferenceError
```
- doodle is enclosed in it's own scope so we cannot access it from global execution context

## Function Scope vs Block Scope
- we create a new environment when there is a function
- most programming languages use block scope, JS allows us to use it though const and let

### Block Scope Example
```JS
function loop() {
	for (let i = 5; i < 5; i++) {
		console.log(i);
	}
	console.log('final', i);
}
loop();
```
- we get a reference error because we're trying to access i outside of it's environment

## Global Variables
- why not use these all the time? 
	- it pollutes our namespace by having to much data on global execution scope
	- having more than 1 JS file can cause complications (repition of same variable names)
- in html all scripts get combines to form one global execution context

## IIFE
- immediately invoked function expression
- places all code inside local scope to avoid namespace collisions
- 2 ways we can do this:
```JS
(function() {
	console.log('hello');
})();
(function() {
	console.log('hello');
}());
```
- we can take this a step further and pass in parameters so we don't have to go up a scope chain 
```JS
var script = (function($) {
	$('h1').click(() => console.log('click'));
})(jQuery);
```

## this Keyword
- "the object that the function is a property of"
- basic example:
```JS
obj.someFunc(this);
```
- with 'use strict' we can override this showing as window object
- useful example:
```JS
const obj = {
	name: 'Arashdeep',
	sing: function() {
		return 'hello ' + this.name;
	}
};
obj.sing();
```
- you can now read it as: "this is the object the function **sing** is a properly of"
- this gives methods access to their object

### Example: Dynamic vs Lexical Scope
- example:
```JS
const a = function() {
	console.log(this); // window
	const b = function() {
		console.log(this); // window
		const c = {
			hi: function() {
				console.log(this); // c
			}
		}
		c.hi();
	}
	b();
}
```
- b prints out window because there's nothing to the left of it
```JS
window.a(b());
```
- dynamic scope is at work here
- another example:
```JS
const obj = {
	name: 'Arashdeep',
	sing() {
		console.log(this) // obj
		var anotherFunc = function() {
			console.log(this); // window
		};
		anotherFunc();
	}
}
obj.sing();
```
- this keyword is not lexically scoped, it doesn't matter where it's written, it matters where it's called
- in JS, lexical and dynamic scope determines what variables are available
- this is dynamically scoped
- when can use arrow functions to force this to be lexically scoped
- a way to solve issue above:
```JS
const obj = {
	name: 'Arashdeep',
	sing() {
		console.log(this) // obj
		var anotherFunc = function() {
			console.log(this); // obj
		};
		return anotherFunc.bind(this);
	}
}
obj.sing();
```
- another approach
```JS
const obj = {
	name: 'Arashdeep',
	sing() {
		console.log(this) // obj
		var self = this;
		var anotherFunc = function() {
			console.log(self); // obj
		};
		return anotherFunc
	}
}
obj.sing()();
```

## call(), apply(), bind()
- all function use call() when being invoked
- the shorthand for call() is ()
- apply() does the same thing
- what does call() specifically do?
```JS
const wizard = {
	name: 'Merlin',
	health: 50,
	heal() {
		return this.health = 100;
	}
}

const archer = {
	name: 'Robin Hood',
	health: 30
}

console.log(archer);
wizard.heal.call(archer);
console.log(archer);

// archers health increases from 30 to 100
```
- calls method of an object, substituting another object for the current object
- we can pass in parameters that the method requires like:
```JS
wizard.heal.call(archer, 50, 100);
```
- what's the different between call and apply now? in apply you pass in arguments differntly
```JS
wizard.heal.apply(archer, [50, 100]);
```
- on the other hand, bind allows us to store a function for later use
```JS
const wizard = {
	name: 'Merlin',
	health: 50,
	heal(num1, num2) {
		return this.health += num1 + num2;
	}
}

const archer = {
	name: 'Robin Hood',
	health: 30
}

console.log(archer);
const healArcher = wizard.heal.bind(archer, 100, 30);
healArcher();
console.log(archer);
```
- call and apply are good for borrowing methods, bind allows us to call function later with a certain context

## bind() and currying
- you can use bind for function currying
```JS
function multiply(a, b) {
	return a*b;
}

let multiplyByTwo = multiply.bind(this, 2);
let multiplyByTen = multiply.bind(this, 10);
```

## Exercise: this keyword
```JS
var b = {
	name: 'Jay',
	say() {
		console.log(this); // b
	}
}

var c = {
	name: 'Jay',
	say() {
		return function() {
			console.log(this); // global
		}
	}
}

var d = {
	name: 'Jay',
	say() {
		return () => console.log(this); // d
	}
}
```

## Context vs Scope
- scope is function based, it tells us what variables the function has access to
- context is object based, what's the value of **this** keyword