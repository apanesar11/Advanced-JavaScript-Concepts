## JS Types
- numbers, booleans, string, undefined, null, symbol, object
- typeof null gives an obejct (this is a mistake)
- Symbols allow object properties to be unique
- undefined is the absence of a definition, null is absence of a value
- arrays and functions are objects (underneath the hood)
- 2 distinctions
	- primitive: data that only represents a single value
		- number
		- boolean
		- string
		- undefined
		- null
		- symbol
	- non-primitive: doesn't contain value directly, it has a reference to where object is held
		- object
		- array
		- function
- primitives get complicated because they can be used like objects, for example: true.toString() calls a wrapper object like this: Boolean(true) before executing code

## Array.isArray()
- JS does this to arrays:
```JS
var array = ['1', '2', '3'];

var array = {
	0: '1',
	1: '2',
	2: '3'
}
```
- Array.isArray allows us to check if object is an array

## Pass by value vs reference
- primitive types are passed by value
- non-prmitive types are passed by reference
- pass by value basically means we copy the value and place it somehwere else in memory
- pass by reference allows us to save a lot of memory space

## Type Coercion
- 

## JTS: Dynamic vs Static Typing

## JTS: Weakly vs Strongly Typed

## JTS: Static Typing in JS







