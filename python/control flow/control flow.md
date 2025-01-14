Control flow is the order in which the computer executes statements in a script.

By default, control flow is sequential: code is run in order from the first line in the file to the last line, in exactly the order specified.

Control structures such as conditions, loops, and function calls allow us to change and direct the flow of control i.e. the order of execution of the statements in a program.

There are 3 main types of control structures:

- **Sequential** — the default mode where statements are executed one after another.
- **Selection** — (also called “*conditional*” or “*decision*”) involves choosing between 2 or more alternative paths, based on a condition.
	- `if`
	- `if`-`else`
	- `if`-`elif`-`else`
- **Iteration** — (*loops*) allows a block of code to be repeated multiple times.
	- `while`
	- `for`

Note that Python does not have `do...while` loops.


Note that `if`, `while` and `for` are referred to as a *compound statement* in Python because it combines multiple other statements together. A compound statement comprises one or more _clauses_, each of which has a _header_ (like `if`) and a _suite_ (which is a list of statements, like the `if` body). The contents of the suite are delimited with indentation – we have to indent lines to the same level to put them in the same block.
