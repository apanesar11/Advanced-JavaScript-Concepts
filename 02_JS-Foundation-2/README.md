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