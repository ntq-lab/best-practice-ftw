
## Meaningful Names

### Use Intention-Revealing Names

* The name of a variable, function, or class, should tell you why it exists, what it does, and how it is used. 

* If a name requires a comment, it does not reveal intention.

### Avoid Disinformation

* Programmers must avoid using names that obscure the meaning of the code.

    * For example, avoid using hp, aix, and sco because they are variants of Unix platforms. 

    * Another example is referring to a group of accounts as an accountList unless it’s actually a List.

### Make Meaningful Distinctions

* Number-series naming (a1, a2, .. aN) is not meaningful.

* If you have a Product class and other classes called ProductInfo or ProductData, you have made the names noisy because differences in meaning are not clear

### Use Pronounceable Name

* Make names pronounceable. A variable name of genymdhms (generation date, year, month, day, hour, minute, and second) is not pronounceable.

### Use Searchable Names

* The common practice of using single-letter names create a particular problem because they are not easy to locate by searching in code.

### Avoid Encodings

* Encoding names with type indicators such as String in a variable phoneString is unneeded and creates noise. 

* Type indicator encoding is especially unneeded in languages such as Java because Java is a strongly typed language and the compiler forces correct typing anyhow.

### Member Prefixes

* Prefixing member variables with conventions such as m_ is not needed anymore.

### Interfaces and Implementations

* Preceding and interface with letter I as seen in IShapeFactory for example is a distraction.

### Avoid Mental Mapping

* A problem arises from a choosing to use neither problem domain terms nor solution domain terms. It forces readers to mentally translate names. 

    * Example using the letter r to indicate a URL.

### Class Names

* Classes and objects should have noun or noun phrase names like Customer , WikiPage, Account , and AddressParser . 

* Avoid words like Manager , Processor , Data , or Info in the name of a class. A class name should not be a verb

### Method Names

* Use verbs in method names like postPayment, deletePage, or save.

### Don’t Be Cute

* If names are too clever, they will be memorable only to people who share the author’s sense of humor, so choose clarity over entertainment value.

### Don’t Pun

* Using the same name for two different purposes is essentially a pun and should be avoided. 

    * Example: using add that adds to a collection in one case, while in another, add concatenates a string to another string.

### Use Solution Domain Names

* People who read your code will be programmers, so use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth vs. problem domain names. The name AccountVisitor means more to a programmer familiar with the VISITOR pattern.

### Use Problem Domain Names

* Use problem domain names when solution domain names are not available, so at least the programmer who maintains your code can ask a domain expert what it means.

### Add Meaningful Context

* There are a few names which are meaningful in and of themselves - most are not. Instead,you need to place names in context for your reader by enclosing them in well-named classes, functions, or namespaces

### Don’t Add Gratuitous Context

* Add no more context to a name than is necessary and shorter names are usually better than longer ones, if they are clear

## Functions

### Small

* Lines should not be 150 characters long.	

* Functions should not be 100 lines long.	

* Functions should hardly ever be 20 lines long.

### Blocks and Indenting

* Blocks	within statements should be one line long.

* The indent level of a function should not  be greater than one or two.

### Do One Thing

* Functions should do only one thing and do it well.

### One Level of Abstraction per Function

* Make sure that the statements within our function are all at the same level of abstraction

* To determine abstraction level, use the "Step Down" rule. This rule is reading the program as though it were a set of TO paragraphs, each of which is describing the current level of abstraction and referencing subsequent TO paragraphs at the next level down

* Make the code read like a top-down set of TO paragraphs is a useful technique for keeping the abstraction level consistent

### Switch Statements

* Appear only once 

* Used to create polymorphic objects 

* Hidden behind an inheritance relationship so that the rest of the system can’t see them

### Use Descriptive Names

* Don’t be afraid of using long names 

* Don’t be afraid of spending time to choose a descriptive name 

* Be consistent in naming

### Function Arguments

* The ideal number of arguments is zero (niladic), followed by one (monadic), followed closely by two (dyadic). Avoid three arguments where possible and do not use more than three (polyadic)

* Do not use flag arguments such as booleans because it implies the function doing more than one thing 

* Two arguments make the function more complicated to understand and three arguments even more so 

* Wrap multiple arguments into a class of their own

### Have No Side Effects

* Ensure functions have no side effects and especially side effects that include temporal coupling. Temporal coupling creates dependencies between code and timing

### Command Query Separation

* Functions should either perform an action or answer a question, but not both

### Prefer Exceptions to Returning Error Codes

* And when using exceptions, it’s often preferable to extract try/catch block include into functions

### Don’t Repeat Yourself

* Avoid duplication

* [Rule of thre](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming))

## Comments

### Comments Key Factors:

* Comments Do Not Make Up for Bad Code 

* Explain Yourself in Code (not comments) 

## Good comments 

* Legal Comments (copyright, all rights reserved, etc.)  

* Informative Comments (example: comment for intention of regular expression matching because regular expression code can be confusing to some people.) 

* Clarification  

* Warning of Consequences

* TODO comments are sometimes reasonable, and IDEs can help find them  

* Amplification of importance 

* Javadocs  

## Bad comments

* Mumbling (take time to construct comments)  

* Redundant  

* Misleading  

* Mandated (re: rules declaring every function must have a comment)  

* Journaling (redundant with source code control systems)  

* Noise (re: documenting the default constructor when it’s obvious in code)  

* Scary Noise (blatantly incorrect)  

* When the comment could be avoided by better naming or succinctly written code

* Position markers (example: declaring a section of particular kinds of functions)

* Closing Brace Comments (re: try to shorten your functions instead)

* Attributions and Bylines (again, redundant with source code control systems)

* Commented out code

* HTML comments. Do not use HTML in comments

* Nonlocal Information

* No Obvious Connection (re: the connection between the comment and the code should

* be obvious)

* Function Headers (short functions do not need much description)

* Javadocs in Nonpublic Code  

## Formatting  

### Purpose of Code Formatting

* In essence, code formatting is about professional communication  

### Vertical Formatting

* File size consistency

* Openness Between Concepts (example: line breaks between the end of one function and beginning of new)

* Density (tightly related code should appear together)

* Distance (closely related concepts should vertically close to each other to avoid jumping around)

* Ordering (generally speaking, function call dependencies should point in the downward direction)  

### Horizontal Formatting

*  Openness and Density (example: spaces around assignment operators)

*  Alignment (horizontal length can imply need to refactor into more succinct code such as extracting new methods)

* Indentation (indent to signify hierarchy of scoping; re: methods should be indented to first level)

*  Dummy scores (example: a while code block should be broken into lines rather than consolidating into one line)

### Team Rules

* Teams should agree on formatting rules.  

## Objects and Data Structures 

### Data Abstraction

* Hiding implementation is about abstractions and not just a matter of putting a layer of functions between the variables. 

* Abstractions through layers allows the manipulation of the essence of data rather than requiring to know and expose the implementation.  

### Data/Object Anti-Symmetry

* Objects hide their data behind abstractions and expose functions to operate on their data 

* While data structures expose their data for convenience and contain no meaningful functions. Those data structures are processed by separated functions

* Avoid mixing these two constructs together into a structure

### The Law of Demeter

* A module should not know about the innards of the objects it manipulates  or talk to friends not strangers

* A method f of class C should only call the methods of these:

    * C

    * An object created by f

    * An object passed as an argument to f

    * An object held in an instance variable of C

### Conclusion

* Objects should hide data and expose behavior:

    * This makes it easy to add new kinds of objects without changing existing behaviors 

    * But makes it hard to new behavior to existing objects

* Data structures expose data but no significant behavior:

    * This makes it easy to add new behavior to existing data structures

    * But makes it hard to add new data structures to existing functions

## Error Handling 

### Use Exceptions Rather Than Return Codes

* Take advantage of exception handling in languages that support them

## Use Unchecked Exceptions

* The debate of unchecked vs. checked exceptions is over  

## Provide Context with Exceptions

* Provide enough context to determine the source and location of the error.

### Define Exception Classes in Terms of a Caller’s Needs

* The most important concern should be how exceptions are caught

*  Wrapping code to throw your own exceptions rather than coding to specific third-party API exceptions is a good practice  

### Define the Normal Flow

* Don’t use exceptions which clutters the business logic 

* Apply special case pattern

### Don’t Return Null

* If you are tempted to return null from a method, consider throwing an exception or returning a special case object instead  

### Don’t Pass Null

* Returning null from methods is bad, but passing null into methods is worse.  

## Boundaries  

*It’s rare to be in control of all software in our systems. Therefore, we need practices for*

*keeping software clean when crossing software boundaries.*

### Using Third-Party Code

* Avoid passing 3rd-party interfaces at boundaries in your system. Use wrapper code instead  

### Using Code That Does Not Yet Exist

* To keep from being blocked, explore writing your own interface for working with boundaries of code that does not exist yet  

### Clean Boundaries

* When using code outside our control, special care must be taken to ensure possible future change is not too costly. 

* Boundary code needs clear separation through wrappers/adapters and tests that define expectations  

## Unit Tests

### The Three Laws of TDD

* No writing production code until you have written a failing unit test

* No writing more of a unit test than is sufficient to fail. Not compiling is failing

* No writing more production code than is sufficient to pass the currently failing test

### Keeping Tests Clean

* Do not fall into the trap of having different quality standards for test code vs. production code  

### Clean Tests

Three factors to make tests clean:

* Readability  

* Readability  

* Readability  

### One Assert Per Test

* Although it may seem draconian, many believe unit tests should only have one assert per test 

### Five Rules of Clean Tests

* Fast

* Independent

* Repeatable

* Self-Validating (means boolean output)

* Timely  

## Classes 

### Class Organization Ordering (if present)

1. Public static constants

2. Private static variables

3. Private instance variables

4. Public functions

5. Private functions

### Encapsulation  

* Keep variables and utility functions private, but do not be fanatic about it

* Make protected if needed by the test in the same package  

### Classes Should Be Small!

* As already noted with functions, smaller is the primary rule when it comes to designing classes  

### The Single Responsibility Principle

* The Single Responsibility Principle  states that a class or module should have only one reason to change. 

* By trying to identify reasons to change (aka: responsibilities) we recognize and create better abstractions in code.  

### Cohesion  

* Classes should have a small number of instance variables, and each method of a class should manipulate one or more of those variables.

*  Maintaining this cohesion results in many small classes  

### Organizing for Change

* One way to organize for change is to support an object oriented design principle called "Open-Closed Principle" 

* Design classes to be open for extension but closed for modification

* Isolate from change by utilizing concrete classes of implementation details with abstract concept classes and interfaces

* Classes should depend upon abstractions, not on concrete details - Dependency Inversion Principle



##   
