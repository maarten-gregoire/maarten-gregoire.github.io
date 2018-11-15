A while ago I succesfully obtained the Java 1.8 OCA certificate. I made some summaries to help me study for the accompanying exam. In this blog I'll share the summaries. This one is about exceptions.

# Exceptions

An exception is an event that alters program flow. Java has a Throwable superclass for all objects that represents these events. Not all of them have the word exception in their classname, which can be confusing.

- lang.Object
  - lang.Throwable
    - lang.Exception
      - lang.RuntimeException
    - lang.Error

For search: common use: return codes instead of exceptions. In other methods, use exception.

# 3 Types

- Runtime exceptions (unchecked)
  - RuntimeException class and subclasses.
  - Unexpected but not necessarily fatal
  - Occur when program is run (alternative = compile time)
  - Don&#39;t have to be handled or declared
  - Can be thrown by programmer or JVM
  - Examples:
    - ArithmeticException
      - Thrown by the JVM when code attempts to divide by zero
    - ArrayIndexOutOfBoudsException
      - Thrown by the JVM when code uses an illegal index to access an array
    - ClassCastException
      - Thrown by the JVM when an attempt is made to cast an object to a subclass of which it is not an instance
    - IllegalArgumentException
      - Thrown by programmer to indicate that a method has been passed an illegal or inappropriate argument
    - NullPointerException
      - Thrown by the JVM when there is a null reference where an object is required
    - NumberFormatException
      - Thrown by the programmer when an attempt is made to convert a string to a numeric type but the string doesn&#39;t have an appropriate format
- Checked exceptions
  - Includes Exception and all subclasses that do not extend RuntimeException.
  - More anticipated
  - Handle or declare: Java requires the code to either handle them or declare them in the method signature
  - Declare in method signature: throws
    - Throws means: it might throw an Exception, it also might not.
  - Must be handled or declared
  - Can be thrown by programmer or JVM
  - Examples:
    - FileNotFoundException
      - Thrown programmatically when code tries to reference a file that does not exist
      - Subclass of IOException
    - IOException
      - Thrown programmatically when there&#39;s a problem reading or writing a file
- Errors
  - something went horribly wrong, program should not attempt to recover.
  - lang.Error subclasses
  - Extend the Error class
  - Thrown by JVM
  - Should not be handled or declared (but can be)
  - Examples:
    - ExceptionInInitializerError
      - Thrown by JVM when a static initializer throws an exception and doesn&#39;t handle it
      - Java also mentions original cause of problem (original exception thrown in static initializer)
    - StackOverflowError
      - Thrown by the JVM when a method calls itself too many times (infinite recursion)
    - NoClassDefFoundError
      - Thrown by the JVM when a class that the code uses is not available at compile time

| Type | How to recognize | Ok to catch? | Required to handle or declare? |
| --- | --- | --- | --- |
| Runtime Exception (Unchecked) | Subclass of RuntimeException | Yes | No |
| Checked exception | Subclass of Exception but not subclass of RuntimeException | Yes | Yes |
| Error | Subclass of Error | No | No |

# Throwing an exception

- An exception can by thrown:
  - By code that&#39;s wrong:
    - Example: _String[] animals = new String[0]; System.out.println(animals[0]);_
  - Explicitly:
    - Example: _Throw new Exception;_
    - Example: _Throw new RuntimeException(&quot;Oh no!&quot;);_
    - Convention: passing String parameter is possible.
- All subclasses of java.lang.Throwable can be thrown.

# Handling an exception

## Try statement

_Try {_

_        // The try block is also referred to as protected code_

_} catch (exception\_type identifier) {_

_        // exception handler_

_}_

- Try keyword (required)
- If an exception is thrown in a try statement, the catch clauses attempt to catch it
- The identifier refers to the caught exception object
- The type of exception you are trying to catch
- The catch keyword
- Curly braces are required
- At least one of these two is required: catch, finally

&quot;Catch block&quot; = &quot;catch clause&quot;

## Finally Block

_Try {_

_        //protected code_

_} catch (exceptiontype identifier) {_

_        //exception handler_

_} finally {_

_        //finally block_

_}_

- _A finally block can only appear as part of a try statement_

- _The finally block_ _always __executes__ , whether or not an exception occurs in the try block_
- When there is no catch clause, the finally block is required
- The finally block is always the last block

## Flow of try catch exception:

- Code in the try block: run normally
- When the statement in try block throws exception:
  - type listed in catch block: try block stops running and catch block is executed
  - not listed in catch block: catch block not run
- Finally: is run at the end:
  - Regardless of whether exception is thrown
  - When exception is thrown finally is run after catch block
  - When no exception is thrown finally is run after try block
- The only reason why a finally block would not be excecuted if System.exit is actually called in try or catch.

# Catching various types of exceptions

## Hierarchy

When different types of exceptions are thrown by the same method, for determining the hierarchy this is important:

- Whether the exception is a checked or unchecked exception
- Whether the exceptions are subclasses of the others.

To determine which catch gets executed, the following rules apply:

- Java looks at them in the order they appear
- If it is impossible for one of the catch blocks to be executed, a compiler error about unreachable code occurs. (superclass is caught before subclass)
- At most one catch block will run, and it will be the first catch block that can handle it.

Multiple catch blocks with the same exception are not allowed. A checked exception can&#39;t be caught if the methods in the try block do not declare this exception, because the code is unreachable.

# Multiple try statements

- A catch or finally block can contain try statements
- Only the last exception to be thrown matters
- If the finally block and the catch block both throw an exception, the one in the catch block is forgotten about and the one in the finally block gets thrown
- Exception thrown in finally block can be masked with a new try statement inside the finally block

# Calling methods that throw Exceptions

- Calling method that throws exception:
  - Rules are same as within method
    - When method declares checked exception: should be handled or declared in method that calls method, even when exception is not actually thrown
    - Unreachable code = does not compile:
      - Example:
        - Checked exception caught by calling method
        - Called method does not declare this checked exception

# Subclasses

- When class overrides a method from a superclass or implements a method from an interface:
  - Not allowed to add checked exceptions to the method signature
  - Allowed to declare fewer checked exceptions than the superclass or interface
  - Allowed to declare a subclass of the checked exception in superclass or interface
  - Allowed to declare new runtime exceptions in a subclass method.
  - Methods are free to throw any runtime exceptions they want without mentioning them in the method declaration.

# Printing an exception

- Catch (Exception e)
  - out.println(e);
    - Prints type + message
  - out.println(e.getMessage);
    - Prints message
  - printStackTrace();
    - Prints stacktrace
    - Stacktrace:
      - Shows all methods on the stack
      - Everytime a method is called, Java adds it to the stack until it completes

# Returning an exception

Any Java type, including Exception can be declared as return type. It will simply return it and not throw it.
