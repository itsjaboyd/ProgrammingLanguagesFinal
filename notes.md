# Programming Languages (Post-Midterm)
Funcitonal Programming Languages contain one thing - the function, often more mathematical.
* Perfectly orthogonal, functions reside within funcitons and calls.
* Not particularily practical, in this deep relationship with math,
* No side effects in functional languages: if it does anything else than return needed value, these are side effects.
    + Example: Fibbonacci in functional, no tree is formed as the implementation remembers fibonacci calculations.
| Problem | Monad | 
| -------- | -------- | 
| Error | Maybe |
| Non Determinism | List |
| Context | State |
| Destruction | IO |

## October 28, 2019
**Prolog Assignment**
Predicate - statement in prolog, ex. here(), door(), location() in adventure.pl
* If you want to write something to the screen, write() will do this.
* read_words(W) parses user input into a list of words.

A sample predicate for looking at details ofa location:
look(R):-name(R,N),
    write(N),
    write(":\n"),
    long_desc(R,D),
    write(D).
how the game will work -> play: input(Words), interpret(W,Action), run(A), win().
* the task is to write what the actions will do and how to interpret them. EC: Make a sidequest using different game data. 
    + C(A,B):-door(A,B).
       C(B,A):-door(B,A).

## Type and Abstraction 
Type System: Type constructors and descriptors (const) all create a "type algebra." 
* the graphs on board are called categories: C going to A, AB, and B and AB going to A or B is called record/product.
    + A goes to A+B or C, B goes to A+B or C, and A+B goes to C is called the union operator.
    + These are really the only two ways to combine types.

Encapsulation and Information Hiding
* Does the language support thinking at the right level/multiple levels of abstraction?
* Consider Float - its a structure! Nothing but integer arithmetic in floating point numbers.

# FINAL PAPER
1. Pick a programming language that is interesting and not regularly taught at the university.
2. Make an argument in the paper for some situation in which the language can be chosen for a given task.
3. Write a small program (couple hundred lines at least) of something simple.
4. Write your experience on the language, explaining the pros & cons, but focus on where the language is good.
5. Example languages: Rust, R, Scala, etc.
6. 2-3 pages, one true format: 10 pt font, single-spaced, two column.
7. Explain its readability, writability, etc.
8. Due Saturday of dead week.

## November 1, 2019
Primitive Types
* Integer, Floating Point, Complex, Decimal, Boolean, Character.  * Enumerations - type that takes on fixed number of values (usually very small) 
    + What types of coercion are allowed? Enumerations are certainly stored as integers, 
    + What is the scope of enums? Most languages it does. In c++, class enum does, while enum doesn't.
* Arrays - Data structure, generally contiguous in memory where order matters.
    + What legal subscripts? Integer is basically all allowed; some languages allow characters, even negative numbers.
    + Is the array range checked? Usually yes, but checks take a considerable amount of time and resources.
    + What operations are allowed? Low level languages usually don't implement such features:
        - slicing: gaining sub-arrays from existing arrays or alternating elements in patterns
        - membership: Is this element in the array? Linear search is the typical method
        - transposition: arrays holding themselves: 2-nD arrays can change their ordering
        - concatenation: can you stick arrays together (don't use the plus operator)
    + Static arrays must be held in a constant location (global).

# Expressions
## November 4, 2019
Expressions - Means of expressing computation, a combination of values and operators that has a value.
* Some languages don't overload operators such as lisp,
* Why would someone overload operators? Gives users ability to write code they want!
    + Disadvantages: misuse of operators is better than not at all, a sort of programming philosophy of protecting the user from themselves.
Side effects of Function Called Expressions 
* An observable change of global state made by a function call, i.e. output parameters, global & class variables, and IO.
Referential Transparency - If expression has no side effects, it can be thought of as a reference to its value.
* Functions are called *pure* if they have this property.
    + Four major causes of impurity: Error, Non-Determinism, Context, Destruction
Short Circuit Evaluation of Expression - if the value of an expression can be determined without evaluating the entire expression, common with boolean algebra.
Lazy vs Eager Evaluation:
* Lazy Evaluation - Expressions become values at the latest possible moment, very common in functional languages, allows expressions of infinite objects (not their evaluation)
* Eager Evaluation - Expressions become values at earliest opportunity.
Arithmetic Operations
* Unary
* Binary
    + Infix: a + b, tougher on the compiler, but worth it since that's how arithmetic is taught. Requires operator preference.
    + Prefix: add a b
    + Postfix: a b add, like postscript
Boolean Expressions - Two and Three way comparisons.
* Two way comparison: compare a and b and get true or false.
* Three way comparison: compare a and b and the result can be less than, equal then, or greater than.
Assignment
* Procedural Languages - write to memory, always has a side effect.
* Functional and Logic - create a new name binding to a constant value. There's no state in functional programming
Type Conversions
* Narrowing - type to new type that can't represent all new values, chance of losing information.
* Widening - type to new type that can represent all new values, no data could be lost.
* Casting - explicitly changing one type to another. 


## November 8, 2019
Prolog1 Homework: you can also turn in the look everywhere version of the assignment.
Write the assignment in a different file; include adventure.pl with [adventure]


## November 11, 2019
Control Statements: statements that allow conditional execution, i.e. ifs, case, switch, etc.
In different languages there can be various control expressions such as booleans, integers, (the form of the clause).
Multiple Selection: switch & case statements (also pattern matching)
    * How is multiple selection implemented? Possibly nested ifs, a tree statement, even jump tables.
Iteration: used for repetition
Unconditional Branch: most flexible and powerful of statements, other control structures can be implemented in terms of goto.


## November 13, 2019
Guarded Commands: introduced by Dijkstra
* Block of statements with boolean guards, one expression whos guard is true is executed.
Online Quiz during dead week, counts towards grade.

Subprograms
Basic Subprograms have: single entry point, suspends the caller.
Multiple entry points gives coroutines, avoiding suspension gives concurrency.
The definition of a subprogram includes the interface and its actions.
    * Call - the request to enter a sub program
    * Return - the resumption of the calling program
Procedures don't return values, intended as extension points for statements in language
Functions return values, modeled on math functions and generally shouldn't have side effects.
Coroutines include Yield and Resume, returns a value but maintains current state.
    * Resume restarts coroutine after last yield.
Side Effects are bad!
1. Context - global variables and static local variables
2. Error
3. Non-determinism
4. Destruction - I/O, out parameter

Referencing Environments - Set of bindings visible to a subprogram
Closures - subprogram and its referencing environment.

Formal and Actual
The parameter definitions in the header are called formal

Positional and Keyword Parameters
If the matching between formal and actual parameters is based only on order then the language uses positional parameters
If each actual parameter can be associated with a formal parameter name in any order the language used keyword parameters (ie foo(bar = 42)).

Parameter Passing
1. Pass by Value: only the value is passed (a copy)
2. Pass by result: local variable is created, value (result) is copied into caller at the end of function
3. Pass by value result: copy passed to function, value copied back into caller, also "passed by copy"
4. Pass by reference: create and copy an alias
5. Pass by name: as if parameter was textually substituted, referencing environment must also be included for name lookups


## November 15, 2019
### FINAL is on November 25, 2019, allowed one sheet of paper.
Multidimensional Arrays as Parameters
* Language needs to able to build the array mapping.
    + this complicates passing arrays: pointer arithmetic, less flexible functions, and more complex built in arrays.
* How can subprograms be passed? What is the referencing environment?
    + Call statement - shallow binding (take referencing environment right at the call)
    + passed funciton definition - deep binding
    + specified at call site - ad hoc binding
Indirect Subprograms
* Function pointers delegates a callable and assignable object.
* Viritual functions are implemented in terms of indirect subprograms

Overloaded Functions - Subprograms with the same name and referencing environment
* Each must have a different protocol (number, type, and order of arguments).
Overloaded Operators - usually there is some special function name that is invoked by operator syntax.
Generic Subprograms - work on multiple types, concept of parameter is what generic subprogram expects.
* A type is said to model the concept in it meets the requirements
* Generic programs work on all types that model their concept


## November 18, 2019
Assignment help: asserta/z(predicate asserting to be true), i.e. asserta(inv(obj)), opposite of this is retract().
    * to list out all locations: printList:-list(x).write(x).fail printList.

**Language Features in Support of OOP**
* Roots in SIMULA 67 and the lambda calculus, although considered to begin with SmallTalk80
* Currently the dominant practice within the field; too many people think that OO is synonym for 'good.'
OOP is about abstraction (NOT reuse!)
---Three Key Features for Languages---
1. Abstract Data Types (user defined)
2. Inheritance
3. Dynamic Binding (almost all OO relies on virtual functions)

Multiple Inheritance - If a language allows more than one parent class
* Makes dependence relations a graph rather than just a tree
Subtypes - does the language support the principle of substitution?
* Is the derived class an instance of the base?
* Substitution and extension require dynamic (run-time) binding of functions.

Do we allow user defined types that aren't objects?
Do all objects inherit from one primordial Object class? Java does, c++ doesn't
Alexander Stepanov - OOP is technically, philosophically, and methodoligically unsound. Real world problems overlap!
Slicing - derived class is omitted and only the base class and virtual function table is kept with pointer to derived; program will crash.
Reflection - Routine that looks at every data type within the class and operates (serializes) on that type

**Concurrency**: doing two unrelated things at the same time
* Exploit concurrent hardware with multi-core systems and IO bound processing. Concurrent design fits some domains very well, distributed processing
If you don't write for concurrency, then you simply don't get it. Compilers will try to implement concurrency, however they aren't very good at it.


## November 20, 2019
Final Exam is cumulative, due on Monday so start studying now! Allowed a single paper as a cheat sheet.
Threads and Processes
A thread is a sequence of executed statements.
There has to be some way of synchronization between races (data races can happen) two threads are accessing the same resource, one of those threads changes that resource.
* Co-operative (producer-consumer) - one thread is making something and the other thread uses, usually done with a queue of some sort.
* Competitive (resource contention) - when two threads require the same resource, done through mutual exclusion (mutex) only one thread can access the resource at once.
Synchronization Quadrants - multithreaded programming is hard!
Liveness and Deadlock
Semaphores - the Anti Thread
Monitors - mandatory mutexes, language inserts locks as needed & is genearlly conservative
Message Passing - relies on a thread safe queue, no shared state outside of queue.
Statement level Concurrency - statements that express parallelism, such statements can be automatically mapped to concurrent forms.


## November 22, 2019
FINAL REVIEW
Short Circuit Evaluation - there are mathematical identities, especially in boolean logic.
    * The evaluation of the entire expression doesn't matter when with parts such as False &&, True &&, True || 
The Unconditional Branch is goto, break, continue, etc.
Coroutine vs. Function: a coroutine is a type of subprogram, "funcitonal procedure" is a type of subprogram.
    * Functions have a call & return. They suspend their caller!
    * Coroutines suspend and return their caller, but they also have weight & yeild, which is similar to call and return but both are available at the same time.
Logic: A implies (->) B. Evidence/Conclusion can be replaced with some other conclusion from other evidence.
    Lambda Calculus - f(...) can replace that function with the result of the function. f(evidence) -> result. A function is proof for a result, so it can be replaced
Pattern Matching: Nothing | Tree Value Tree 
    * insert(Nothing, Value) = Nothing Value Nothing
    * insert(L x R, V : v < x) = insert(L, V) x R
        otherwise L X insert(R, V)
Type
Expressions
Abstractions
Subprograms
Concurrency
OOP

play :- read_words(W),command(C,W),P=..C,P,win.

read_words(W):-read_string(user_input,"\n\r","\n\r",_,L),split_string(L












