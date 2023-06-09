---
author: C. Lawrence Wenham
source: http://www.yacoset.com/Home/signs-that-you-re-a-bad-programmer
---

# Signs that you're a bad programmer

## 1. Inability to reason about code

Reasoning about code means being able to follow the execution path ("running the program in your head") while knowing what the goal of the code is.

### Symptoms

1. The presence of "voodoo code", or code that has no effect on the goal of the program but is diligently maintained anyway (such as initializing variables that are never used, calling functions that are irrelevant to the goal, producing output that is not used, etc.)
2. Executing idempotent functions multiple times (eg: calling the save() function multiple times "just to be sure")
3. Fixing bugs by writing code that overwrites the result of the faulty code
4. "Yo-Yo code" that converts a value into a different representation, then converts it back to where it started (eg: converting a decimal into a string and then back into a decimal, or padding a string and then trimming it)
5. "Bulldozer code" that gives the appearance of refactoring by breaking out chunks into subroutines, but that are impossible to reuse in another context (very high cohesion)

### Remedies

To get over this deficiency a programmer can practice by using the IDE's own debugger as an aide, if it has the ability to step through the code one line at a time. In Visual Studio, for example, this means setting a breakpoint at the beginning of the problem area and stepping through with the 'F11' key, inspecting the value of variables--before and after they change--until you understand what the code is doing. If the target environment doesn't have such a feature, then do your practice-work in one that does.

The goal is to reach a point where you no longer need the debugger to be able to follow the flow of code in your head, and where you are patient enough to think about what the code is doing to the state of the program. The reward is the ability to identify redundant and unnecessary code, as well as how to find bugs in existing code without having to re-implement the whole routine from scratch.

## 2. Poor understanding of the language's programming model

Object Oriented Programming is an example of a language model, as is Functional or Declarative programming. They're each significantly different from procedural or imperative programming, just as procedural programming is significantly different from assembly or GOTO-based programming. Then there are languages which follow a major programming model (such as OOP) but introduce their own improvements such as list comprehensions, generics, duck-typing, etc.

### Symptoms

1. Using whatever syntax is necessary to break out of the model, then writing the remainder of the program in their familiar language's style
2. (OOP) Attempting to call non-static functions or variables in uninstantiated classes, and having difficulty understanding why it won't compile
3. (OOP) Writing lots of "xxxxxManager" classes that contain all of the methods for manipulating the fields of objects that have little or no methods of their own
4. (Relational) Treating a relational database as an object store and performing all joins and relation enforcement in client code
5. (Functional) Creating multiple versions of the same algorithm to handle different types or operators, rather than passing high-level functions to a generic implementation
6. (Functional) Manually caching the results of a deterministic function on platforms that do it automatically (such as SQL and Haskell)
7. Using cut-n-paste code from someone else's program to deal with I/O and Monads
8. (Declarative) Setting individual values in imperative code rather than using data-binding

### Remedies

If your skills deficiency is a product of ineffective teaching or studying, then an alternative teacher is the compiler itself. There is no more effective way of learning a new programming model than starting a new project and committing yourself to use whatever the new constructs are, intelligently or not. You also need to practice explaining the model's features in crude terms of whatever you are familiar with, then recursively building on your new vocabulary until you understand the subtleties as well. For example:

- Phase 1: "OOP is just records with methods"
- Phase 2: "OOP methods are just functions running in a mini-program with its own global variables"
- Phase 3: "The global variables are called fields, some of which are private and invisible from outside the mini-program"
- Phase 4: "The idea of having private and public elements is to hide implementation details and expose a clean interface, and this is called Encapsulation"
- Phase 5: "Encapsulation means my business logic doesn't need to be polluted with implementation details"

Phase 5 looks the same for all languages, since they are all really trying to get the programmer to the point where he can express the *intent* of the program without burying it in the specifics of *how*. Take functional programming as another example:

- Phase 1: "Functional programming is just doing everything by chaining deterministic functions together"
- Phase 2: "When the functions are deterministic the compiler can predict when it can cache results or skip evaluation, and even when it's safe to prematurely stop evaluation"
- Phase 3: "In order to support Lazy and Partial Evaluation, the compiler requires that functions are defined in terms of how to transform a single parameter, sometimes into another function. This is called Currying"
- Phase 4: "Sometimes the compiler can do the Currying for me"
- Phase 5: "By letting the compiler figure out the mundane details, I can write programs by describing *what* I want, rather than *how* to give it to me"

## 3. Deficient research skills / Chronically poor knowledge of the platform's features

Modern languages and frameworks now come with an awesome breadth and depth of built-in commands and features, with some leading frameworks (Java, .Net, Cocoa) being too large to expect any programmer, even a good one, to learn in anything less than a few years. But a good programmer will search for a built-in function that does what they need before they begin to roll their own, and excellent programmers have the skill to break-down and identify the abstract problems in their task, then search for existing frameworks, patterns, models and languages that can be adapted before they even begin to design the program.

### Symptoms

These are only indicative of the problem if they continue to appear in the programmer's work long after he should have mastered the new platform.

1. Re-inventing or laboring without basic mechanisms that are built-into the language, such as events-and-handlers or regular expressions
2. Re-inventing classes and functions that are built-into the framework (eg: timers, collections, sorting and searching algorithms) \*
3. "Email me teh code, plz" messages posted to help forums
4. "Roundabout code" that accomplishes in many instructions what could be done with far fewer (eg: rounding a number by converting a decimal into a formatted string, then converting the string back into a decimal)
5. Persistently using old-fashioned techniques even when new techniques are better in those situations (eg: still writes named delegate functions instead of using lambda expressions)
6. Having a stark "comfort zone", and going to extreme lengths to solve complex problems with primitives

\* - Accidental duplication will also happen, proportionate to the size of the framework, so judge by degree. Someone who hand-rolls a linked list _might_ Know What They Are Doing, but someone who hand-rolls their own StrCpy() probably does not.

### Remedies

A programmer can't acquire this kind of knowledge without slowing down, and it's likely that he's been in a rush to get each function working by whatever means necessary. He needs to have the platform's technical reference handy and be able to look through it with minimal effort, which can mean either having a hard copy of it on the desk right next to the keyboard, or having a second monitor dedicated to a browser. To get into the habit initially, he should refactor his old code with the goal of reducing its instruction count by 10:1 or more.

## 4. Inability to comprehend pointers

If you don't understand pointers then there is a very shallow ceiling on the types of programs you can write, as the concept of pointers enables the creation of complex data structures and efficient APIs. Managed languages use references instead of pointers, which are similar but add automatic dereferencing and prohibit pointer arithmetic to eliminate certain classes of bugs. They are still similar enough, however, that a failure to grasp the concept will be reflected in poor data-structure design and bugs that trace back to the difference between pass-by-value and pass-by-reference in method calls.

### Symptoms

1. Failure to implement a linked list, or write code that inserts/deletes nodes from linked list or tree without losing data
2. Allocating arbitrarily big arrays for variable-length collections and maintaining a separate collection-size counter, rather than using a dynamic data structure
3. Inability to find or fix bugs caused by mistakenly performing arithmetic on pointers
4. Modifying the dereferenced values from pointers passed as the parameters to a function, and not expecting it to change the values in the scope outside the function
5. Making a copy of a pointer, changing the dereferenced value via the copy, then assuming the original pointer still points to the old value
6. Serializing a pointer to the disk or network when it should have been the dereferenced value
7. Sorting an array of pointers by performing the comparison on the pointers themselves

### Remedies

> "A friend of mine named Joe was staying somewhere else in the hotel and I didn't know his room number. But I did know which room his acquaintance, Frank, was staying in. So I went up there and knocked on his door and asked him, 'Where's Joe staying?' Frank didn't know, but he did know which room Joe's co-worker, Theodore, was staying in, and gave me that room number instead. So I went to Theodore's room and asked him where Joe was staying, and Theodore told me that Joe was in Room 414. And that, in fact, is where Joe was."

Pointers can be described with many different metaphors, and data structures into many analogies. The above is a simple analogy for a linked list, and anybody can invent their own, even if they aren't programmers. The comprehension failure doesn't occur when pointers are described, so you can't describe them any more thoroughly than they already have been. It fails when the programmer then tries to visualize what's going on in the computer's memory and gets it conflated with their understanding of regular variables, which are very similar. It may help to translate the code into a simple story to help reason about what's going on, until the distinction clicks and the programmer can visualize pointers and the data structures they enable as intuitively as scalar values and arrays.

## 5. Difficulty seeing through recursion

The idea of recursion is easy enough to understand, but programmers often have problems imagining the result of a recursive operation in their minds, or how a complex result can be computed with a simple function. This makes it harder to design a recursive function because you have trouble picturing "where you are" when you come to writing the test for the base condition or the parameters for the recursive call.

### Symptoms

1. Hideously complex iterative algorithms for problems that can be solved recursively (eg: traversing a filesystem tree), especially where memory and performance is not a premium
2. Recursive functions that check the same base condition both before and after the recursive call
3. Recursive functions that don't test for a base condition
4. Recursive subroutines that concatenate/sum to a global variable or a carry-along output variable
5. Apparent confusion about what to pass as the parameter in the recursive call, or recursive calls that pass the parameter unmodified
6. Thinking that the number of iterations is going to be passed as a parameter

### Remedies

Get your feet wet and be prepared for some stack overflows. Begin by writing code with only one base-condition check and one recursive call that uses the same, unmodified parameter that was passed. Stop coding even if you have the feeling that it's not enough, and run it anyway. It throws a stack-overflow exception, so now go back and pass a modified copy of the parameter in the recursive call. More stack overflows? Excessive output? Then do more code-and-run iterations, switching from tweaking your base-condition test to tweaking your recursive call until you start to intuit how the function is transforming its input. Resist the urge to use more than one base-condition test or recursive call unless you really Know What You're Doing.

Your goal is to have the confidence to jump in, even if you don't have a complete sense of "where you are" in the imaginary recursive path. Then when you need to write a function for a real project you'd begin by writing a unit test first, and proceeding with the same technique above.

## 6. Distrust of code

### Symptoms

1. Writing IsNull() and IsNotNull(), or IsTrue(bool) and IsFalse(bool) functions
2. Checking to see if a boolean-typed variable is something other than true or false

### Remedies

Are you being paid by the line? Are you carrying over old habits from a language with a weak type system? If neither, then this condition is similar to the inability to reason about code, but it seems that it isn't reasoning that's impaired, but trust and comfort with the language. Some of the symptoms are more like "comfort code" that doesn't survive logical analysis, but that the programmer felt compelled to write anyway. The only remedy may be more time to build up familiarity.

## Signs that you are a mediocre programmer

### 1. Inability to think in sets

Transitioning from imperative programming to functional and declarative programming will immediately require you to think about operating on *sets* of data as your primitive, not scalar values. The transition is required whenever you use SQL with a relational database (and not as an object store), whenever you design programs that will scale linearly with multiple processors, and whenever you write code that has to execute on a SIMD-capable chip (such as modern graphics cards and video game consoles).

#### Symptoms

The following count only when they're seen on a platform with Declarative or Functional programming features that the programmer should be aware of.

1. Performing atomic operations on the elements of a collection within a *for* or *foreach* loop
2. Writing Map or Reduce functions that contain their own loop for iterating through the dataset
3. Fetching large datasets from the server and computing sums on the client, instead of using aggregate functions in the query
4. Functions acting on elements in a collection that begin by performing a new database query to fetch a related record
5. Writing business-logic functions with tragically compromising side-effects, such as updating a user interface or performing file I/O
6. Entity classes that open their own database connections or file handles and keep them open for the lifespan of each object

#### Remedies

Funny enough, visualizing a card dealer cutting a deck of cards and interleaving the two stacks together by flipping through them with his thumbs can jolt the mind into thinking about sets and how you can operate on them in bulk. Other stimulating visualizations are:

- freeway traffic passing through an array of toll booths (parallel processing)
- springs joining to form streams joining to form creeks joining to form rivers (parallel reduce/aggregate functions)
- a newspaper printing press (coroutines, pipelines)
- the zipper tag on a jacket pulling the zipper teeth together (simple joins)
- transfer RNA picking up amino acids and joining messenger RNA within a ribosome to become a protein (multi-stage function-driven joins, [see animation](https://web.archive.org/web/20230405060440/http://www.dnai.org/text/mediashowcase/index2.html?id=586))
- the above happening simultaneously in billions of cells in an orange tree to convert air, water and sunlight into orange juice (Map/Reduce on large distributed clusters)

If you are writing a program that works with collections, think about all the supplemental data and records that your functions need to work on each element and use Map functions to join them together in pairs before you have your Reduce function applied to each pair.

### 2. Lack of critical thinking

Unless you criticize your own ideas and look for flaws in your own thinking, you will miss problems that can be fixed before you even start coding. If you also fail to criticize your own code once written, you will only learn at the vastly slower pace of trial and error. This problem originates in both lazy thinking and egocentric thinking, so its symptoms seem to come from two different directions.

#### Symptoms

1. Homebrew "Business Rule Engines"
2. Fat static utility classes, or multi-disciplinary libraries with only one namespace
3. Conglomerate applications, or attaching unrelated features to an existing application to avoid the overhead of starting a new project
4. Architectures that have begun to require [epicycles](https://web.archive.org/web/20230405060440/http://en.wikipedia.org/wiki/Epicycle)
5. Adding columns to tables for tangential data (eg: putting a "# cars owned" column on your address-book table)
6. Inconsistent naming conventions
7. "Man with a hammer" mentality, or changing the definitions of problems so they can all be solved with one particular technology
8. Programs that dwarf the complexity of the problem they solve
9. Pathologically and redundantly defensive programming ("Enterprisey code")
10. Re-inventing LISP in XML

#### Remedies

Start with a book like [Critical Thinking](https://web.archive.org/web/20230405060440/http://www.amazon.com/gp/product/0130647608/ref=as_li_ss_tl?ie=UTF8&tag=synesmedia-20&linkCode=as2&camp=217145&creative=399369&creativeASIN=0130647608) by Paul and Elder, work on controlling your ego, and practice resisting the urge to defend yourself as you submit your ideas to friends and colleagues for criticism.

Once you get used to other people examining your ideas, start examining your own ideas yourself and practice imagining the consequences of them. In addition, you also need to develop a sense of proportion (to have a feel for how much design is appropriate for the size of the problem), a habit of fact-checking assumptions (so you don't overestimate the size of the problem), and a healthy attitude towards failure (even Isaac Newton was wrong about gravity, but we still love him and needed him to try anyway).

Finally, you must have discipline. Being aware of flaws in your plan will not make you more productive unless you can muster the willpower to correct and rebuild what you're working on.

### 3. Pinball Programming

When you tilt the board just right, pull back the pin to just the right distance, and hit the flipper buttons in the right sequence, then the program runs flawlessly with the flow of execution bouncing off conditionals and careening unchecked toward the next state transition.

#### Symptoms

1. One Try-Catch block wrapping the entire body of Main() and resetting the program in the Catch clause (the pinball gutter)
2. Using strings/integers for values that have (or could be given) more appropriate wrapper types in a strongly-typed language
3. Packing complex data into delimited strings and parsing it out in every function that uses it
4. Failing to use assertions or method contracts on functions that take ambiguous input
5. The use of Sleep() to wait for another thread to finish its task
6. Switch statements on non-enumerated values that don't have an "Otherwise" clause
7. Using Automethods or Reflection to invoke methods that are named in unqualified user input
8. Setting global variables in functions as a way to return multiple values
9. Classes with one method and a couple of fields, where you have to set the fields as the way of passing parameters to the method
10. Multi-row database updates without a transaction
11. Hail-Mary passes (eg: trying to restore the state of a database without a transaction and ROLLBACK)

#### Remedies

Imagine your program's input is water. It's going to fall through every crack and fill every pocket, so you need to think about what the consequences are when it flows somewhere other than where you've explicitly built something to catch it.

You will need to make yourself familiar with the mechanisms on your platform that help make programs robust and ductile. There are three basic kinds:

1. those which stop the program before any damage is done when something unexpected happens, then helps you identify what went wrong (type systems, assertions, exceptions, etc.),
2. those which direct program flow to whatever code best handles the contingency (try-catch blocks, multiple dispatch, event driven programming, etc.),
3. those which pause the thread until all your ducks are in a row (WaitUntil commands, mutexes and semaphores, SyncLocks, etc.)

There is also a fourth, Unit Testing, which you use at design time.

Using these ought to become second nature to you, like putting commas and periods in sentences. To get there, go through the above mechanisms (the ones in parenthesis) one at a time and refactor an old program to use them wherever you can cram them, even if it doesn't turn out to be appropriate (especially when they don't seem appropriate, so you also begin to understand why).

### 4. Unfamiliar with the principles of security

If the following symptoms weren't so dangerous they'd be little more than an issue of fit-n-finish for most programs, meaning they don't make you a bad programmer, just a programmer who shouldn't work on network programs or secure systems until he's done a bit of homework.

#### Symptoms

1. Storing exploitable information (names, card numbers, passwords, etc.) in plaintext
2. Storing exploitable information with ineffective encryption (symmetric ciphers with the password compiled into the program; trivial passwords; any "decoder-ring", homebrew, proprietary or unproven ciphers)
3. Programs or installations that don't limit their privileges before accepting network connections or interpreting input from untrusted sources
4. Not performing bounds checking or input validation, especially when using unmanaged languages
5. Constructing SQL queries by string concatenation with unvalidated or unescaped input
6. Invoking programs named by user input
7. Code that tries to prevent an exploit from working by searching for the exploit's signature
8. Credit card numbers or passwords that are stored in an unsalted hash

#### Remedies

The following only covers basic principles, but they'll avoid most of the egregious errors that can compromise an entire system. For any system that handles or stores information of value to you or its users, or that controls a valuable resource, **always have a security professional review the design and implementation**.

Begin by auditing your programs for code that stores input in an array or other kind of allocated memory and make sure it checks that the size of the input doesn't exceed the memory allocated for storing it. No other class of bug has caused more exploitable security holes than the buffer overflow, and to such an extent that you should seriously consider a memory-managed language when writing network programs, or anywhere security is a priority.

Next, audit for database queries that concatenate unmodified input into the body of a SQL query and switch to using parameterized queries if the platform supports it, or filter/escape all input if not. This is to prevent SQL-injection attacks.

After you've de-fanged the two most infamous classes of security bug you should continue thinking about all program input as completely untrustworthy and potentially malicious. It's important to define your program's acceptable input in the form of working validation code, and your program should reject input unless it passes validation so that you can fix exploitable holes by fixing the validation and making it more specific, rather than scanning for the signatures of known exploits.

Going further, you should always think about what operations your program needs to perform and the privileges it'll need from the host to do them before you even begin designing it, because this is the best opportunity to figure out how to write the program to use the fewest privileges possible. The principle behind this is to limit the damage that could be caused to the rest of the system if an exploitable bug was found in your code. In other words: after you've learned not to trust your input you should also learn not to trust your own programs.

The last you should learn are the basics of encryption, beginning with [Kerckhoff's principle](https://web.archive.org/web/20230405060440/http://en.wikipedia.org/wiki/Kerckhoffs%27_principle). It can be expressed as "the security should be in the key", and there are a couple of interesting points to derive from it.

The first is that you should never trust a cipher or other crypto primitive unless it is published openly and has been analyzed and tested extensively by the greater security community. There is no security in obscurity, proprietary, or newness, as far as cryptography goes. Even implementations of trusted crypto primitives can have flaws, so avoid implementations you aren't sure have been thoroughly reviewed (including your own). All new cryptosystems enter a pipeline of scrutiny that can be a decade long or more, and you want to limit yourself to the ones that come out of the end with all their known faults fixed.

The second is that if the key is weak, or stored improperly, then it's as bad as having no encryption at all. If your program needs to encrypt data, but not decrypt it, or decrypt only on rare occasions, then consider giving it only the public key of an asymmetric cipher key pair and making the decryption stage run separately with the private key secured with a good passphrase that the user must enter each time.

The more is at stake, then the more homework you need to do and the more thought you must put into the design phase of the program, all because security is the one feature that dozens, sometimes millions of uninvited people will try to break after your program has been deployed.

The vast majority of security failures traceable to code have been due to silly mistakes, most of which can be avoided by screening input, using resources conservatively, using common sense, and writing code no faster than you can think and reason about it.

### 5. Code is a mess

#### Symptoms

1. Doesn't follow a consistent naming convention
2. Doesn't use indentation, or uses inconsistent indentation
3. Doesn't make use of whitespace elsewhere, such as between methods (or expressions, see "[ANDY=NO](https://web.archive.org/web/20230405060440/http://thedailywtf.com/Articles/ANDYNO.aspx)")
4. Large chunks of code are left commented-out

#### Remedies

Programmers in a hurry (or The Zone) commit all these crimes and come back to clean it up later, but a bad programmer is just sloppy. Sometimes it helps to use an IDE that can fix indentation and whitespace ("pretty print") with a shortcut key, but I've seen programmers who can even bludgeon Visual Studio's insistence on proper indentation by messing around with the code too much.

## Signs that you shouldn't be a programmer

The following may not have any remedies if you still suffer from them after taking a programming course in school, so you will stand a better chance of advancing your career by choosing another profession.

### 1. Inability to determine the order of program execution

#### Symptoms

    a = 5
    b = 10
    a = b

    print a

1. You look at the code above and aren't sure what number gets printed out at the end

#### Alternative careers

1. Electrician
2. Plumber
3. Architect
4. Civil engineer
5. Artist

### 2. Insufficient ability to think abstractly

#### Symptoms

1. Difficulty comprehending the difference between objects and classes
2. Difficulty implementing design patterns for your program
3. Difficulty writing functions with low cohesion
4. Incompetence with Regular Expressions
5. Lisp is opaque to you
6. Cannot fathom the Church-Turing Thesis

#### Alternative careers

1. Contract negotiator
2. Method actor

### 3. Collyer Brothers syndrome

#### Symptoms

1. Unwilling to throw away anything, including garbage
2. Unwilling to delete anything, be it code or comments
3. The urge to build booby-traps for defense against trespassers
4. Unwilling to communicate with other people
5. Poor organization skills

#### Alternative careers

1. Antique dealer
2. Bag lady

### 4. Dysfunctional sense of causality

#### Symptoms

1. You seriously consider malice to be a reason why the compiler rejects your program
2. When called on to fix a bug in a deployed program, you try prayer
3. You take hidden variables for granted and don't think twice about blaming them for a program's misbehavior
4. You think the presence of code in a program will affect its runtime behavior, even if it is never invoked \*
5. Your debugging repertoire includes rituals like shining your lucky golf ball, twisting your wedding ring, and tapping the nodding-dog toy on your monitor. And when the debugging doesn't work, you think it might be because you missed one or didn't do them in the right order

\* - Memory constraints, shifted offsets, and compiler peculiarities notwithstanding. See discussion on [Reddit](https://web.archive.org/web/20230405060440/http://www.reddit.com/r/programming/comments/98c14/signs_you_may_be_a_bad_programmer/c0bs8jh). Judge accordingly.

#### Alternative careers

1. Playing the slot machines in Vegas

### 5. Indifference to outcomes

Programming could still be a hobby for you, but it would be in society's best interests to defend itself against your entry into the world of professional software development.

#### Symptoms

1. You aren't interested in fixing a bug that can be worked around by rebooting the computer
2. Your installation program silently deploys unsolicited third party programs that are unrelated to the function of yours \*
3. You don't use any ergonomic model when designing user interfaces, nor do you have any interest in usability studies
4. Your program exhibits pretension and grandeur beyond its utility, eg: displaying splash screens over active programs while loading in the background, or placing multiple launch icons in premium desktop locations \*
5. Your program produces output to be read by another (eg: a browser), or implements a network protocol, and relies on the other party's software to be significantly tolerant to spec violations
6. You write busy-wait loops even when the platform offers event-driven programming
7. You don't use managed languages and can't be bothered to do bounds checking or input validation
8. Your user interfaces do not make the difficulty of accidentally invoking a function proportionate to its destructiveness (eg: the "Delete Database" button is next to "Save", just as big, has no confirmation step and no undo)
9. You don't use whitespace, indentation or comments

\* - These are actually imposed by management more often than by the programmer, who only implements them. We'd still group them together for the sake of this self-test, though, and at the most suggest that one seek employment at a better firm, while the other goes back to business school to learn less destructive ways of making a profit.

#### Alternative careers

1. Debt collection
2. Telemarketing

## Further Reading

This article was published in the [May 2012 issue (Issue #24) of Hacker Monthly](https://web.archive.org/web/20230405060440/http://hackermonthly.com/issue-24.html), which compelled the author to write its antithesis: [Signs you're a good programmer](https://web.archive.org/web/20230405060440/http://www.yacoset.com/Home/signs-that-you-re-a-good-programmer).
