---
layout: post
title:  "OCA: Java Building Blocks"
date:   2018-11-02 11:33:27 +0100
categories: OCA Java 1.8
---
A year ago I succesfully obtained the Java 1.8 OCA certificate. I made some summaries to help me study for the accompanying exam. In this blog I'll share the summaries. This one is about Java Building Blocks.

# Java Building Blocks

## Java class structure

- Classes = basic building blocks
- For most classes, object is needed
  - Object = runtme instance of a class in memory
- Various objects represent state of program
- Members of a class: fields, methods

Example:
~~~~
 public class Animal {
 
  String name;
 
  public String getName() {
   return name;
  }
 
  public void setName(String name) {
   this.name = name;
  }
}
~~~~
## Keywords

- keyword = word with special meaning in Java
  - public = class can be used by other classes
  - class = defining a class
  - void = no value gets returned

## Fields

- generally known as variables
- hold the state of program

## Methods

- = functions or procedures
- operate on the state of program
- has return type (sometimes void)
- can have parameters
- full declaration = signature

## Comments

- Not executable code
- can be placed anywhere
- Single line comment:
  - starts with //
  - anything after // on the same line is ignored by the compiler
- multiline or multiple-line comment:
  - starts with /\*
  - ends with \*/
  - /\*\* is for javadoc
  - \* at beginning of every line  not mandatory

## Classes vs. files

- 1 class in 1 file:
  - Most of the time, each class in its own \*.java file,
  - usually public but not required to be public
- Multiple classes in same file:
  - allowed
  - at most 1 class can be public
  - public class must match filename
  - A file without public classes is allowed

## main() method

## Java Virtual Machine

- Startup of Java process is managed by Java Virtual Machine
- JVM calls underlying system to allocate memory and CPU time, access files, etc…

## Main method

- Java program begins executing at main method
- Gateway between startup of Java process and beginning of code
- Hooks code into process, keeping it alive long enough to do the work
- If trying to execute class without main method, error is thrown, program terminates

example:
~~~~
public class Zoo {
 public static void main(String[] args) {}
}
~~~~
### main() method signature:

- Signature is always one of these:
  - public static void main (parameter list)
  - public static final void main (parameter list)

- keyword public:
  - access modifier
  - declares level of exposure to callers
- keyword static
  - binds method to its class and can be executed without making an object
  - non-static main is invisible for JVM
- keyword void:
  - return type (silent)
- parameter list:
  - Possible parameter list:
    - String[] args
    - String args[]
    - String… args
  - &quot;args&quot; can be replaced by any valid variable name
  - args are read when JVM starts
  - []:
    -- array
    -- fixed size
    -- index starts at 0
  - … :
    - varargs
  - When trying to access parameter that&#39;s not given when running application:
    - ArrayIndexOutOfBoundsException

## Compiling and executing

- compile:
  - javac Zoo.java
  - JDK is needed
- execute:
  - java Zoo
  - JRE or JDK is needed
  - Java classes run on JVM and run on any machine with Java
- To execute, file must have extension .java
- filename must match name of class, including case
- result of compilation is bytecode file with same name and extension .class
- Bytecode consists of instructions that JVM can execute
- omit .class extension to run
  - . has reserved meaning in JVM
- to run use _java_ with the classname as parameter

## Package declarations and imports

- Packages and imports: way to organize classes (logical groupings)
- Import statement:
  - tells Java which packages to look in for classes
    - Use class in unimported package:
      - error: cannot be resolved to a type
  - example: import java.util.Random
- package:
  - If it starts with java or javax: came with JDK
  - Child packages: longer = more specific
  - Naming rules: same as variable names, separated by dots

## Wildcards

- Shortcut to import all classes in package.

- Example: import java.util.\*;
- \* = wildcard
  - imports
    -- all classes in package
  - does not import:
    -- child packages
    -- fields
    -- methods
- Only 1 wildcard can be used and it should be at the end
- Importing many classes does not slow down program
- Static imports:
  - are an exception on this

## Redundant imports

- java.lang:

- Automatically imported
- Explicit import allowed, not necessary

- Specific class:

- Import of specific class is redundant:
  -  if all the classes in a package are already imported with a wildcard
- Import with wildcard is redundant
  - if the specific classes used in the program are already imported

- Class in same package as class importing it:
  - Import is redundant

- Java automatically looks in current package for other classes

## Naming conflicts

- Class names
  - Don&#39;t have to be unique across all of Java
  - When found in multiple imported packages:
    -- compiler error, type is ambiguous
  - Explicitly import class name: precedence over any wildcards
  - when 2 specific classes with same name imported:
    - compiler error, import collides with another import statement
  - When you want to use 2 classes with same name:
    - option 1:
      - use one in the import
      - use the other&#39;s fully qualified classname when using it
    - option 2:
      - Do not use an import and use fully qualified classname for both

## Creating a new package

### Default package

- Special unnamed package
- Only use for throwaway code
- No package name

### Creating a package

- Directory structure is related to package name
  - The package name represents any folders underneath the current path when compiling
  - package names are case sensitive

### Compile in package

- javac packagename/Classname.java

### Run in package

- java packagename.Classname

### Set classpath

- java -cp &quot;location&quot; packagename.Class
- example:
  - java -cp &quot;.;C:\temp\someOtherLocation;c:\temp\myJar.jar&quot; myPackage.MyClass

## Code formatting on the exam

- Not all questions include the imports
- If question is not asking about imports, imports are often omitted to save space
- If line numbers do not start at 1:
  - imagine ommited code is correct
- If line numbers start at 1:
  - make sure imports are not missing
- Code is sometimes merged on one line

## Creating Objects

- Object = instance of class

## Constructors

- create instance: new keyword
  - example: Random r = new Random
- Name of class + parentheses = constructor
  - constructor = special type of method that celates a new object
- Creating a constructor:
  - name matches name of class
  - no return type
    -- &quot;public void&quot; is not a constructor
    -- capital letter and return type: not a constructor but regular method
  - constructor is used to initialize fields
    -- other code is allowed
- Initializing fields can happen on the line on which they are declared instead of in constructor
- When no constructor is coded: compiler supplies &quot;do nothing&quot; default constructor
  - in most cases explicitly declared constructor not required
    -- in special case: required

## Reading and writing Object Fields

- Possible to read and write instance variables directly from caller.
- Reading variable = getting it
- Writing variable = setting it
- Reading and writing also possible on line of declaration

## Instance initializer blocks

- code between {} = code block
  - sometimes code is called being inside braces
  - sometimes code blocks are inside method
    -- run when method is called
  - can appear outside method
    -- instance initializers.
  - number of code blocks = number of pairs of braces
    -- if number of open braces is not equal to number of closed braces, code doesn&#39;t compile

## Order of initialization

- Fields and instance initializer blocks are run in the order in which they appear in the file.
- Constructor runs after all fields and instance initializer blocks have run
- When running a main method, the main method is executed without first initializing the fields (main is static)
- Order matters for the fields and blocks of code
  - You can&#39;t refer to a variable before it has been initialized

## Distinguishing between Object references and primitives

## Primitive types

- 8 built-in data types: primitive types
  - building blocks for Java objects
  - Java objectsare complex collections of primitive data types

| **Keyword** | **Type** | **Example** |
| --- | --- | --- |
| boolean | true or false | true |
| byte | 8-bit integral value | 123 |
| short | 16-bit integeral value | 123 |
| int | 32-bit integral value | 123 |
| long | 64-bit integral value | 123 |
| float | 32-bit floating-point value | 123.45f |
| double | 64-bit floating-point value | 123.456 |
| char | 16-bit Unicode value | &#39;a&#39; |

- float and double: floating point (decimal values)
- float requires letter f
- byte, short, int, long: numbers without decimal points
- each numeric type uses twice as many bits as the smaller similar type
- byte
  - can hold value from -128 to 127
  - 8 bits
- Integer.MAX\_VALUE gives maximum value of int
- number present in code = literal
  - Java assumes a literal is int
  - does not compile if too big
  - add L to number to make it long
- Java allows to specify digits in several other formats than decimal
  - octal (0-8): prefix = 0
    - example 017
  - hexadecimal (0-9 and A-F): prefix = 0x or 0X
    - example: 0xFF
  - binary (0-1): prefix is 0b or 0B
    - example 0b10
- underscores can be added for readabliity to numeric literals (java 7)
  - can be added anywhere except:
    - beginning
    - end
    - right before decimal point
    - right after decimal point

## Reference types

- refers to Object (instance of class)
- primitive types hold values in memory where variable is allocated
- references do not hold value of object they refer to, instead a reference (address) is stored
  - Java does not allow you to know the address
  - only reference can be used
- A value is assigned to a reference in one of 2 ways:
  - can be assigned to another object of same type
  - can be assigned to new object using new keyword

## Key differences

- reference types can be assigned null
  - do not currently refer to an object
- primitive types give compiler error when attempted to assign null
- reference types can be used to call methods when they do not point to null
- primitives do not have methods declared on them
- all primitive types have lowercase type names
- classes begin with uppercase (convention)

## Declaring and initializing variables

- variable = name for piece of memory that stores data
- declare variable:
  - type + name
- when declared, value can be given
  - initializing
    - variable name + equal sign + value
    - can be done right away when declaring

## Declaring multiple variables

- declare multiple variables in one statement
  - must be of same type
    - example: String s1 = &quot;yes&quot;, s2 = &quot;no&quot;;
    - example of compile error: int num, String value;
    - declaring multiple times same type not allowed:
      - example: double d1, double d2; // does not compile
  - multiple can be declared while only one may be initialized:
    - example: int i1, i2, i3 = 0;
      - only i3 is initialized
  - separated by comma = declaration of its own

## Identifiers

- Rules for identifier names
- same rules apply to anything you are free to name
  - variables
  - methods
  - classes
  - fields
- rules
  - name must begin with letter or $ or \_
  - subsequent characters may also be numbers
  - can not be Java reserved word
    - keyword that Java has reserved
    - case sensitive
      - keywords that differ in case are allowed
- reserved words:
  - abstract, assert, boolean break, byte, case, catch, char, class, continue, default, do, double, else, enum, extends, false, final, finally, float, for, if, implements, import, istanceof, int, interface, long, native, new, null, package, private, protected, public, return, short, static, strictfp, super, switch, synchonized, this, throw, throws, transient, true, try, void, volatile, while
  - const, goto
    - not actually used in Java but reserved
- Java supports unicode characters

## Default initialization

- Before a variable can be used it needs a value
  - some types get value automatically
  - some require programmer to specify value

## Local variables

- defined within a method
- must be initialized before use
- do not have default value
- contain garbage date until initialized
- compiler doesn&#39;t allow reading uninitialized value
- keep conditional statements in mind

## Instance and class variables

- not local
  - class variables
    - shared across multiple objects
    - keyword static
  - instance variables
    - = fields
- Initialization not required
  - have default value when declared

### Default initialization values by type

| **Variable type** | **Default initialization value** |
| --- | --- |
| boolean | false |
| byte, short, int, long | 0 (in the type&#39;s bit length) |
| float, double | 0.0 (in the type&#39;s bit  length) |
| char | &#39;\u000&#39; (NUL) |
| Object references (everything else), including String | null |

Remark: When a String which is null is printed with System.out.println, the word _null_ is printed.

## Variable scope

- scope local to the method
  - can not be used outside method
    - method parameter
      - scope = entire method
    - variable declared inside method
      - when declared in block, not available outisde block
        - compiler error
      - are in scope only after declaration, not before
  - can never have scope larger than method
- instance variables
  - available as soon as they are defined
  - last for lifetime of object
- static variables
  - go into scope when declared
  - stay in scope entire lifetime of program
  - non-static methods in same class have access to static variables and methods

## Ordering elements in a class

| **Element** | **Example** | **Required?** | **Where does it go?** |
| --- | --- | --- | --- |
| Package declaration | package abc; | No | First line in file |
| Import statements | import java.util.\*; | No | Immediately after the package |
| Class declaration | publc class C | Yes | Immediately after the import |
| Field declarations | int value; | No | Anywhere inside a class |
| Method declarations | void method() | No | Anywhere inside a class |
| Comments | /\* 444 \*/ | No | Anywhere |

PIC: Package, import, class

## Destroying objects

- Java automatically takes care of destroying objects
- Garbage collector
  - looks automatically for objects that aren&#39;t needed anymore
- Java objects are stored in program memory&#39;s heap:
  - heap = free store
    - large pool of unused memory allocated to Java application
    - may be quite large depending on environment
    - always a limit to it&#39;s size
    - if objects stay on heap while new ones keep being made, program runs out of memory

## Garbage collection

- Garbage collection
  - process of automatically freeing memory on the heap by deleting objects that are no longer reachable
  - many algorithms
  - System.gc():
    - not guaranteed to run
    - method provided by Java
    - does not run garbage collection
    - only suggests that it&#39;s a good time to kick off a garbage collection run
    - Java can ignore the request
  - Object will remain on heap until no longer available
    - object no longer reachable when one of these occurs
      - object no longer has any references pointing to it
      - all references of object have gone out of scope
  - The end of a program does not mean garbage collection is run
- objects
  - come in all different shapes and sizes
  - consume varying amounts of memory
  - cannot be assigned to another object
  - can not be passed to or returned from a method
  - object gets garbage collected, not the reference
- references are same size
- reference may or may not be created on heap

## finalize()

- objects are allowed to implement finalize() that might get called
- gets called if garbage collector tries to collect the objecct
- if garbage collector not run, method is not called
- if garbage collector fails to collect and tries again
  - method doesn&#39;t get called second time
- might get called
- wil not be called twice

## Benefits

- Object oriented
  - code is defined in classes
  - most classes can be instantiated into objects
  - Java is an oject-oriented language
    - not a procedural language
    - not a functional programming language
- access modifiers are provided to protect date from unintended access and modification
- Platform independent
  - interpreted language
  - gets compiled to bytecode
  - Java gets compiled once
  - write once, run everywhere
  - Java code compiled on Windows can run on Linux
- Robust
  - prevents memory leaks
  - Java manages memory on it&#39;s own
  - garbage collection automatically
- Simple
  - intended to be simpler than c++
  - eliminated pointers
  - no operator overloading
- Secure
  - runs inside JVM
    - creates sandbox that makes it hard for java code to do evil things to computer
