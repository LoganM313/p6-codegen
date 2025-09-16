# Bach Compiler

This project is a full implementation of a compiler for a toy programming language called bach. It was made as part of my Introduction to Compilers course at UW-Madison. 

## How to Use
- Clone this repository
- Ensure Java and Make are installed on your machine
- Run make to compile the compiler
- Make a program in bach, our mini programming language! You can look at `test.bach` or `factorial.bach` to see syntax examples (or if you're really nerdy check out `bach.cup` for the full parser specification)
- Run the command `java -cp ./deps P6 <your-program> <output-file>` to generate assembly for your own program, or run `make test` to compile the included test programs
- If all goes well you should get MIPS assembly code for your program written to the output file
- Test out your program with a simulator like [this one] (https://shawnzhong.github.io/JsSpim/)

## How it Works
The compiler is broken down into sections that got implemented one at a time.
### Scanner
The scanner tokenizes the input program and sends these tokens to the parser, it recognizes keywords like integer, TRUE, FALSE, struct, etc. as well as recognizing valid IDs like variable names and creates corresponding tokens, it also detects valid String literals and fails at invalid String literals. We used a tool called JLex to generate the scanner with rules
### Parser
The parser recognizes the grammar of the language and is itself a pretty complicated program. We've defined our language's grammar in bach.cup and passed this to a program called JavaCUP to create our parser. The parser takes tokens from the scanner and discovers the program's structure. This allows us to work with the program from a heirarchical point of view, allowing recursive operations for the following phases. It also allows us to fix the formatting of an input program and make a pretty printed version of a program.
### Name Analysis
This phase goes through the program recursively to build symbol tables for the program, it also checks for bad names and multiply declared names.
### Type Checking
This phase also goes through the program recursively and type checks expressions throughout the program.
### Code Generation
This is the final phase of this compiler. It generates MIPS assembly code for the program using the structure discovered through the entire process.

