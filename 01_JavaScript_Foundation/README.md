# JavaScript Foundation

## JavaScript Engine
- is what allows the computer to understand a JS file
- there are many JS engines, a popular one is v8 which was released by Google in 2008 and written in C++
	- Google wanted their maps app to load faster so they created their own engine which introduced a compiler

### Interesting Facts
- Brendan Eich created the first JS engine and it was called Spider Monkey
- before the introduction of JS, the browser could only understand HTML and CSS

## Inside the Engine
- lexical analysis: breakage of syntax to a series of tokens which combine to form an AST (Abstract Syntax Tree)
	- makes it possible for the interpreter to understand the JS file

## Interpreters and Compilers
- Interpreter: directly executes instructions on the fly
- Compiler: compiles file to create an optimized form using a low level language
- it's very beneficial to use both together

## Babel + TypeScript
- 2 famous JS compilers

## Inside the v8 Engine