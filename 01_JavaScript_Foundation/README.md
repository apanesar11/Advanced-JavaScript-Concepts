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
- interpreters
	- pro: interpreters are quick to get up running (JS used interpreters at the beginning)
	- con: gets very slow when running same code over and over again
- compilers:
	- pro: have the ability to simplify repetitive code (optimize)
- combining these 2 we get a JIT (just in time) compiler
- v8 engine uses the interpreter Ignition and compiler TurboFan
- interpreter spits out Bytecode which is interpreted by the JS engine
- profilers watch code and make notes on how it can be optimized
- with the aid of a JIT compiler, the execution speed gradually improves

## Comparing other languages
- other languages tend to have an .exe executable file (written in C++)
- java has JVM (java virtual machine) which converts java to bytecode

## Writing Optimized Code
- be careful when using any of the following
	- delete
	- for in
	- eval()
	- arguements
	- with
- the following makes our code less optimized and causes compiler to run slower
	- [hidden classes](https://richardartoul.github.io/jekyll/update/2015/04/26/hidden-classes.html)
		- must be careful with order
	- [inline caching](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments)
- write predictable code that doesn't confuse the compiler

## WebAssembly
- why don't we use machine code instead of JS?
	- compiler must be really fast
	- browsers must agree on a standard
- WebAssembly tackles this problem

## Call Stack and Memory Heap
- we store/write information on memory heap
- we keep track of what is happening on call stack (FILO)
	- starts at global executional context
	- stores data and pointers as code executes
- some variables are stored on call stack, data structures are stores on memory heap

## Stack Overflow
- commonly caused by recursion

## Garbage Collection
- JS is a garbage collected language
- in low level languages like C++, you control this
- JS uses a mark and sweep algorithm

## Memory Leaks
- 3 major causes
	- too many global variables
	- too many event listeners
	- setInterval

## Single Threaded
- JS is a synchronous language (one long process can cause delays)

## JavaScript Runtime
- 3 parts of event loop
	- call stack + memory heap
	- Web API
	- callback queue
- browser provides Web API (uses low-level languages like C++ to perform applications in background)
	- are asynchronous
- the event loop runs when call stack in empty
- callback queue returns to call stack when stack is empty and file has finished being read

## Node.js 
- also built on v8
- C++ program
- has global variable instead of window