---
layout: post
title:  "OCA: Operators and statements"
date:   2018-11-02 11:33:27 +0100
categories: OCA Java 1.8
---
A year ago I succesfully obtained the Java 1.8 OCA certificate. I made some summaries to help me study for the accompanying exam. In this blog I'll share the summaries. This one is about operators and statements.

# Operators

- Special symbol
- Can be applied to set of
  - Variables
  - Values
  - Literals (referred to as operands)
- Returns result
- Three flavors:
  - Unary
    - Can be applied to 1 operand
  - Binary
    - Can be applied to 2 operands
  - Ternary
    - Can be applied to 3 operands
- Not necessarily evaluated from left-to-right order
  - Operators follow order of operation
  - Order can be overridden with parentheses
  - Operators have precedence
    - If same precedence: from left to right

| Operator | Symbols and examples |
| --- | --- |
| Post-unary operators | Expression++, expression-- |
| Pre-unary operators | ++expression, --expression |
| Other unary operators | -, ! |
| Multiplication/Division/modulus | \*, /, % |
| Addition/Subtraction | +, - |
| Relational operators | \&lt;, \&gt;, \&lt;=, \&gt;= |
| Equal to/not Equal to | ==, != |
| Logical operators | &amp;, ^, | |
| Short-circuit logical operators | &amp;&amp;, || |
| Ternary operators | Boolean expression ? expression1 : expression2 |
| Assignment operators | =, +=, -=, \*=, /=, %=, &amp;=, ^=, |=, <<=, >>=, >>>= |

Only operators that you should know for the OCA exam are listed. Be aware of the existence of unary operators ~ and +, shift operators <<, >> and >>>, relational operator instanceof, and assignment operators /=, %=, &amp;=, ^=, |=, <<=, >>= and >>>

# Binary arithmetic operators

Can be used to

- Perform mathematical operations on variables
- Create logical expressions
- Perform basic variable assignments

## Arithmetic operators

- Additive:
  - Operators:
    - Addition: +
    - Subtraction: -
  - Precedence:
    - Lower order: last evaluated
- Multiplicative:
  - Operators
    - Multiplication: \*
    - Division: /
      - For integers: floor value of nearest integer that fulfils the operation
    - Modulus: %
      - Remainder operator
      - Remainder when 2 numbers are divided
      - Positive dividends: For a given divisor y, the modulus operation results in a value between 0 and y – 1
      - Not limited to positive integer values:
        - Negative integers possible
        - Floating-point integers possible
      - Negative dividends: For a given divisor y, the modulus operation results in a value between –y + 1 and 0
  - Precedence
    - Higher order: first evaluated
- Order:
  - rules can be overridden by parentheses
  - Follow precedence rules
  - Then evaluate from left to right
- May be applied to:
  - Any Java primitives (or wrappers) except:
    - boolean (+ wrapper)
    - String
  - + and += may be applied to String values for concatenation.

## Numeric promotion

Each primitive has a bit-length

### Rules

- If 2 values have different data types, Java will automatically promote one of the values to the larger of the two data types.
- If one of the values is integral and the other is floating-point, Java will automatically promote the integral value to the floating-point value&#39;s data type.
  - floating-point literals are double, unless post-fixed with an f
- Smaller data types are first promoted to int any time they&#39;re used with a Java binary arithmetic operator, even if neither of the operands is int.
  - Smaller data types:
    - Byte
    - Short
    - Char
      - Ascii value of character is used when assigned with single quotes
      - Value of number is used when number is assigned without quotes
  - Unary operators are excluded from this rule.
- After all promotion has occurred and the operands have the same data type, the resulting value will have the same data as its promoted operands.

# Unary operators

A unary operator requires exactly one operand.

| Unary operator | Description |
| --- | --- |
| + | Indicates a number is positive, although numbers are assumed to be positive in Java unless accompanied by a negative unary operator |
| - | Indicates a literal number is a negative or negates an expression |
| ++ | Increments a value by 1 |
| -- | Decrements a value by 1 |
| ! | Inverts a Boolean&#39;s logical value |

## Logical complement and negation operators

Logical complement operator:

- Logical complement operator:
  - !
  - Flips value of a Boolean expression:
    - True becomes false
    - False becomes true
  - Can not be used on numeric expression
  - Can only be used on Boolean values
  - 1 and 0 are unrelated to true and false in Java
- Negation operator:
  - –
  - Reverses the sign of a numeric expression
  - Can not be used on boolean expression

## Increment and decrement operators

- Increment:
  - ++
- Decrement:
  - –
- Can be applied to numeric operands and have higher order or precedence compared to binary operators
- Placed before operand:
  - Pre-increment (or pre-decrement) operator
  - Applied first, return value is new value
- Placed after operand
  - Post-increment (or post-decrement) operator
  - Original value is returned, operator is applied after returning

# Using additional binary operators

Binary operators include operators that:

- Perform assignments
- Compare arithmetic values and return Boolean results
- Compare Boolean and object values and return Boolean results

## Assignment operators

- Binary operator
- Modifies or assigns the variable on the left-hand side of the operator with the result of the value on the right-hand side of the equation
- Example: =
  - Assigns value
- Java will automatically promote from smaller to larger data types
- Java throws a compiler exception if it detects an attempt to convert from larger to smaller data types

## Casting primitive values

- You can fix incompatible type by casting the results to a smaller data type
  - Required any time you are going from larger to smaller numerical data type
  - Or converting from floating-point to integral value
- Overflow:
  - When a number is too large for the data type
  - System &quot;wraps around&quot; to next lowest value and counts up from there
- Underflow
  - Analogous to overflow
  - When a number is too low for the data type
- Short values are automatically promoted to int when applying any arithmetic operator
  - Result is int
  - Compiler error when trying to fit int in short
  - Solve this with explicit cast to short: (short)
    - Instructing to ignore default behavior
- Boolean can not be assigned to String (compile error)

## Compound assignment operators

- Numerous compound statements
  - To know for the exam:
    - +=
    - -=
- Glorified forms of simple assignment operator with built-in arithmetic or logical operation
  - Applies left- and right-hand sides of the statement
  - Stores result in left-hand side
- Can only be applied to already defined variable, not to declare new variable
- Can be used to explicitly cast a value
  - No compiler exception
  - Example:
    - Long x = 10; int y = 5; y \*= x;
- Result of assignment is expression in and of itself, equal to the value of the assignment
  - Example:
    - Long x = 5; long y = (x=3);
      - Result: x = 3, y = 3
      - (x=3): assigns 3 to x and returns 3

## Relational operators

- Compare two expressions
- Return Boolean value
- Relational operators applied to numeric primitive data types only:
  - <
    - Strictly less than
  - <=
    - Less than or equal
  - >;
    - Strictly greater than
  - >=
    -  Greater than or equal to
- Instanceof operator:
  - A instanceof b
    - True if the reference that a points to is an instance of a class, subclass, or class that implements a particular interface, as named in b
- Comparing String reference with int results in compilation error

## Logical operators

- Operators:
  - &amp;
  - |
  - ^
- Logical operators:
  - applied to Boolean data types
- Bitwise operators:
  - Applied to numeric data types
  - Perform bitwise comparisons of the bits that compose the number
  - Not on exam

### Truth tables

x &amp; y (AND)

|   | Y = true | y = false |
| --- | --- | --- |
| x = true | True | False |
| x = false | False | False |

x | y (INCLUSIVE OR)

|   | Y = true | y = false |
| --- | --- | --- |
| x = true | True | True |
| x = false | True | False |

x ^ y (EXCLUSIVE OR)

|   | Y = true | y = false |
| --- | --- | --- |
| x = true | False | True |
| x = false | True | False |

- AND is only true if both operands are true.
- Inclusive OR is only false if both operands are false.
- Exclusive OR is only true if the operands are different.

### Conditional operators

- Short-circuit operators:
  - &amp;&amp;
    - Right-hand side does not get evaluated if left-hand side is false
  - ||
    - Right-hand side does not get evaluated if left-hand side is true
- Nearly identical to logical operators
- Right-hand side may never be evaluated if final result can be determined by left-hand side
- Handy for null checks
- If variables are be altered in the right-hand side in case it is never reached, the variables are not altered

## Equality operators

- Difference between &quot;two objects are the same&quot; and two objects are equivalent&quot;.
- No distinction between the same and equivalent for numeric and Boolean primitives.
- Operators:
  - ==
    - Equals
    - Can be used on
      - Numeric primitives
      - Boolesn values
      - Object references
  - !=
    - Not equals
- Used in and limited to three scenarios:
  - Comparing two numeric primitive types. If numeric values are of different data types, values are automatically promoted as previously described.
  - Comparing two Boolean values.
  - Comparing two objects, including null and String values.
- Mixing and matching is impossible and gives a compiler error.
- On the exam assignment and equality operators are mixed

# Java statements

- Java statement = complete unit of execution
- Terminated with a semicolon
- Control flow statements:
  - Break up flow of execution:
    - Decision making
    - Looping
    - Branching
  - Selectively execute segments of code
  - Can be applied to:
    - Single expressions
    - Block of Java code
      - Group of 0 or more statements
      - Between balanced braces {}
      - Can be used anywhere a single statement is allowed

## If-then statement

- Excecute block under certain circumstances
- Excecute block if Boolean expression evaluates to true
- Curly braces
  - required for block of multiple statements
  - ptional for single statement
- tabs are just whitespace without meaning:
  - watch out for misleading indentation

Structure:

If (booleanExpression) {

} else if {

} else {

}

## If-then-else statement

- else is optional
- possible to append if then statements to an else block
  - rder is important
- nly one branch is executed
- if the expression  inside if statement does not evaluate to Boolean:
  - Does not compile
  - 0 and 1 are not considered Boolean values
  - Be aware for assignment operators instead of equality operators
- New if can be chained with else
- 2 else statements cannot be chained without additional if

## Ternary operator

- Conditional operator
- Three operands
- Form:
  - BooleanExpression ? expression : expression
- Condensed form of if statement
- Parentheses are optional but not required
- Second and third expressions are not required to have same data types
  - Can come into play when combined with assignment operator
    - Does not compile if assigned to unmatching type
- Only one of the right-hand expressions will be evaluated at runtime
  - If a non-evaluated expression performs a side effect it may not be executed
- Can be nested
  - Compute from outside to inside

## Switch statement

- Complex decision-making structure
- Single value is evaluated
- Flow is redirected to first matching branch
- Optional default statement is called when no matching case is found
  - If no default is available and no matching case, switch is skipped

### Supported data types

- Before Java 5.0:
  - Only int
  - Values that could be promoted to int
- After 5.0
  - Enum added
- After 7.0
  - String values added
- After 8.0
- Any of the primitive numeric wrapper classes
  - Byte
  - Short
  - Character
  - Integer

#### Supported types Java 8.0:

- Byte, byte
- Short, short
- Character, char
- Integer, int
- String
- Enum values

#### Not supported:

- Boolean, Boolean
- Long, long

### Structure
~~~~
Switch(variableToTest) {
 case constantExpression1:
  Break;
 Case constantExpression2:
  Break;
 Default:
}
~~~~
- Parentheses around variableToTest are required
- Beginning and ending curly braces are required
- Break is optional
  - Terminate switch statement
  - Return flow control to enclosing statement
  - If you leave out the break statement
    - Flow will continue to the next proceeding case or default block automatically
- Default is optional
  - May appear anywhere (only once)
  - Order matters only when break is left out
  - case is executed when that value is evaluated, not the default, even If case comes after default
- 0 or more case branches

### Compile-time Constant values

- Values in each case statement must be compile-time constant values of same or compatible data type as switch value
  - Only
    - Literals
    - enum constants
    - final constant variables
      - must be marked final
      - initialized in same expression as declaration

## While statement

- repetition control structure
- loop
- executes statement of code multiple times
- By using non-constant variables each repetition of the statement may be different
- Boolean is evaluated before each iteration
  - If false, exits loop
    - May terminate after first evaluation and block never executes

### Structure
~~~~
While (booleanExpression) {
}
~~~~
- While keyword
- Parentheses are required
- Curly braces
  - Required for block of multiple statements
  - Optional for single statement

### Infinite loops

- Loops may never end
  - Loop variable must be modified to be able to end
  - Other condition is break statement

## Do-while statement

- repetition control structure
- loop
- executes statement of code multiple times
- always executes at least once
- variable declared inside block is not known in condition

### Structure
~~~~
Do {
} while (booleanExpression);
~~~~

- Do keyword
- While keyword
- Parentheses are required
- Curly braces
  - Required for block of multiple statements
  - Optional for single statement
- Semicolon
  - Required

## For-statement

### Basic for loop

#### Structure:
~~~~
for (initialization; booleanExpression; updateStatement) {
}
~~~~
- for keyword
  - required
- parentheses:
  - required
- semicolons:
  - required
  - Used to separate initialization, booleanExpression and updateStatement sections
- Commas
  - ptional
  - Initialization and update can contain multiple statements separated by commas
  - In initialization type should be declared only once
- curly braces:
  - required for block of multiple statements
  - ptional for single statement
- sections (optional)
  - initialization
    - scope of variables declared in initialization is limited to within for-loop
    - variables declared before for-loop and assigned a value in initialization may be used outside for-loop
  - booleanExpression
  - updateStatement

#### Flow:

1. Initialization statement executes
2. If booleanExpression is true continue, else exit loop
3. Body executes
4. Execute updateStatements
5. Return to Step 2

#### Infinite loop:
~~~~
for(;;) {
}
~~~~

- for (;;)
  - Compiles
  - Infinite
- For()
  - Does not compile

#### Adding multiple terms

- Different sections can include extra variables that do not reference each other
  - Example
    - Variable can be initialized in initialization, even if it&#39;s never used
- Update statement can modify multiple variables

#### Redeclaring variable in initialization block

- Redeclaring variable in initialization block
  - Compilation error
- Declaring variable before loop and assign in initialization block
  - No compilation error

#### Incompatible data types in initialization block

- Variables in initialization block must be of same type
  - If not, compile error
- If same type, but type is declared more than once
  - Compile error
  - Example : 
  ~~~~
  for (long i = 0, long j = 5; i\&lt; 10; i++) {}
  ~~~~
  - compile error

#### Using loop variables outside loop

- Variables declared in initialization, trying to use outside for
  - Does not compile

### Enhanced for loop (for-each)

- Since Java 5.0
- For iterating over
  - Arrays
  - Collection objects

#### Structure
~~~~
for (datatype instance : collection) {
}
~~~~
- for keyword
  - required
- parentheses
  - required
- colon
  - required
- curly braces:
  - required for block of multiple statements
  - ptional for single statement
- sections
  - initialization
    - datatype of collection member
      - required
      - type must be same type as members of array or collection in the right-hand side
    - instance
      - required
      - every iteration it gets assigned a new value from the array or collection on the right-hand side
  - object to be iterated over
    - iterable collection of objects
    - required
    - built-in Java array
    - bject whose class implements java.lang.Iterable (most of Java Colections framework)
    - right-hand side

#### Does not compile:

- Object to iterate over is not an array and does not implement Iterable
- Type of instance does not match items in object to iterate over
  - A subclass is not ok

# Advanced flow control

## Nested loops

- Loops can contain other loops
  - Example: two-dimensional arrays
- Can be
  - For
  - Enhanced for
  - While
  - Do while

## Adding optional labels

- If-then, switch, loops
- Label = optional pointer to the headof statement
  - Used to jump to or break from
  - Single word followed by colon
    - Example: `LOOP: for(;;){}`
  - Only before statements
    - Not before declarations
  - Often usd in loop structures
  - Can be added to control  and block structures
  - Formatting: same rules as identifiers
  - Commonly uppercase with underscores, but this is not mandatory

## Break statement

- Transfers flow of control out to enclosing statement in
  - Switch
  - While
  - Do-while
  - For
- Foor loops: end loop early

### Structure
~~~~
optionalLabel: while(booleanExpression) {
        break optionalLabel;
}
~~~~
- optionalLabel
  - optional
  - reference to head of loop
- colon
  - required if optionalLabel is present
- break
  - keyword
  - transfers control to enclosing statement
  - can take optional label parameter
    - with label parameter
      - possible to break out of higher level outer loop
    - without label parameter
      - break will terminate nearest inner loop
- semicolon
  - required for break statement

## Continue statement

- causes flow to finish execution current loop

### Structure
~~~~
optionalLabel: while(booleanExpression) {
 continue optionalLabel;
}
~~~~
- optionalLabel
  - optional
  - reference to head of loop
- colon
  - required if optionalLabel is present
- continue
  - keyword
  - transfers control to Boolean expression that determines if loopshould continue
    - ends current iteration
  - can take optional label parameter
    - with label parameter
      - possible to break out of higher level outer loop
    - without label parameter
      - break will terminate nearest inner loop
- semicolon
  - required for continue statement

## Advanced flow control usage

|   | Allows optional labels | allows unlabeled break | allows continue statement |
| --- | --- | --- | --- |
| if | Yes\* | No | No |
| while | Yes | Yes | Yes |
| do while | Yes | Yes | Yes |
| for | Yes | Yes | Yes |
| switch | Yes | Yes | No |
|   |   |   |   |

\*: Labels are allowed for any block statement, including those that are preceded with an if-then statement.
