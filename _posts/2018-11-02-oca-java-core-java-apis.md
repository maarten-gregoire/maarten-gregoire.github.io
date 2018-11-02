---
layout: post
title:  "OCA: Core Java APIs"
date:   2018-11-02 11:33:27 +0100
categories: OCA Java 1.8
---
A year ago I succesfully obtained the Java 1.8 OCA certificate. I made some summaries to help me study for the accompanying exam. In this blog I'll share the summaries. This one is about Core Java APIs.

# Creating and manipulating Strings

- String:
  - Sequence of characters
  - Reference type
  - &quot;new&quot; keyword not mandatory for instantiation

## Concatenation

- + operator:
  - combines two String objects = concatenation
  - can be used in two ways within same line
  - rules:
    - if both operands are numeric: + means numeric addition
    - if either operand is String: + means concatenation
    - evaluated left to right

## Immutability

- Immutable:
  - When a String is created, not allowed to change
    - Cannot be made larger
    - Cannot be made smaller
    - Characters inside of it cannot be changed
  - Opposite of Immutable = mutable = changeable
    - Strings are not mutable = immutable
- Concat does not change a String but returns a new String
  - Example: String s2 = s1.concat(&quot;2&quot;);
    - S1 is not changed

## String pool

- Common Strings are reused by Java
  - Because Strings use a lot of memory
- String pool = intern pool
  - Location in JVM
  - Collects all the Strings
  - Contains literal values that appear in the program
  - If a string is not a literal, it&#39;s not in the String pool
    - Example: myObject.toString()
    - Garbage collected just like any other object
  - New String(&quot;String&quot;) does not use String pool

## String methods

- String = sequence of characters
- Count from 0 when indexed
- 13 methods from String class
  - length()
    - Returns number of characters in String
    - Counts total size, does not start at 0
      - Example &quot;aap&quot;.length() = 3;
  - charAt()
    - find out character at specific index
    - 0 is first character
    - StringIndexOutOfBoundsException can be thrown if index is out of range
  - indexOf()
    - returns first index that matches desired value
    - individual character or whole String
      - first parameter
    - can start from requested position
      - second parameter is index to start (optional)
      - returns index starting form beginning of String
    - if no match is found returns -1
  - substring()
    - substring, not subString
    - looks for characters in String
    - returns parts of the String
    - first parameter:
      - index to start with for returned String
      - can be equal to length
        - returns empty string
      - if higher than length, throws exception
    - second (optional) parameter:
      - end index to stop
        - does not include index
          - Stopsright before index
        - can be 1 past the end of the sequence
          - stops at end
          - would be redundant
        - stops automatically at end if omitted
        - throws exception if lower than start index (first parameter)
        - throws exception if higher than length
    - starts counting at 0;
    - example:
      - &quot;animals&quot;.substring(3,4)
        -  m
      - &quot;animals&quot;.substring(3)
        - Mals
      - &quot;animals&quot;.substring(3,3)
        - Empty String
      - &quot;animals&quot;substring(3,2)
        - Throws exception
  - toLowerCase(), toUpperCase()
    - Convert to lowercase or uppercase
    - Leave alone any characters other than letters
    - Original string stays the same, returns converted string
  - equals() and equalsIgnoreCase()
    - check whether 2 String objects contain exactly same characters in same order
    - different from ==
      - == compares reference, not the characters
    - EqualsIgnoreCase()
      - Converts case if needed
  - startsWith() and endsWith()
    - look whether value matches end or beginning part of String
    - case-sensitive
  - contains()
    - looks for matches in the String
    - can be anywhere in String
    - case-sensitive
  - replace()
    - search and replace
    - can take char parameters
    - can take charSequence parameters
      - CharSequence = general way of representing several classes
        - including String
        - including StringBuilder
        - interface
      - signatures:
        - String replace(char oldChar, char newChar)
        - String replace(CharSequence oldChar, CharSequence newChar)
  - trim()
    - removes whitespace from beginning and end
      - whitespace:
        - spaces
        - \t (tab)
        - \n (newline)
        - \r (cariabe return)
        - Other whitespace characters
    - If no whitespace
      - Returns original string
    - Leaves spaces in the middle

## Method chaining

- When method called, return value is String
  - methods can be chained
    - to evaluate, start from left and evaluate untl semicolon
    - for each method String object is created, last one is returned

# Stringbuilder

- mutable
- less Objects created
  - does not store all interim String values
- changes its own state and returns reference to itself
- three ways to construct:
  - no parameter
    - example
      - new StringBuilder()
    - empty sequence of parameters
    - Java manages implementation details
  - String parameter
    - example
      - new StringBuilder(&quot;text&quot;)
    - specific value
    - Java manages implementation details
  - int parameter
    - example
      - new StringBuilder(10);
    - reserve certain amount of slots for characters (initial capacity, can be enlarged)
- size: number of characters currently in sequence
- capacity:
  - number of characters the sequence can hold
  - when Stringbuilder is constructed
    - starts at default capacity (16)
    - r capacity chosen by programmer

## Important StringBuilder Methods

### charAt(), indexOf(), length(), substring()

- Same as String
- substring returns String, Stringbuilder is not changed

### append()

- appends String to StringBuilder
- returns Reference to current StringBuilder
- can be used on all types
  - types are automatically converted to String
- can be chained
- can be used directly after constructor

### insert()

- adds characters to StringBuilder at requisted index
- returns reference to current StringBuilder
- can be used on all types
- indexes can change when characters are inserted
- signature:
  - StringBuilder insert(int offset, String str)
- Invalid index:
  - Exception

### delete() and deleteCharAt()

- Opposite of insert
- Removes characters from sequence
- Returns reference to current StringBuilder
- deleteCharAt:
  - nly one character
  - signature
    - StringBuilder deleteCharAt(int index)
- delete
  - ne or multiple characters
  - signature
    - StringBuilder delete(int start, int end)
    - Stops right before end index
- Indexes change

### reverse()

- Reverses characters in sequence
- Returns reference to current StringBuilder
- Signature:
  - StringBuilder reverse()

### toString()

- Converts StringBuilder to String
- Signature:
  - String toString()

## StringBuffer

- StringBuilder
  - When writing new code that concatenates a lot of String objects together
  - Since Java 5
- StringBuffer
  - In old code (before Java 5)
  - More slowly
  - Thread safe
  - Works in same way as StringBuilder

# Equality

- ==
  - On numbers
    - Compare number
    - true when one is wrapper class and other one is primitive
    - false when both wrapper classes and one is using constructor and other one is not
    - False when different types
  - On Objects
    - Compare reference
  - On Strings
    - If assigned directly
      - Compare string (same object)
      - Pool is used
      - Only one literal was created in memory
    - If computed at runtime
      - New string is created
      - Are not equal
      - Different object
    - Do not use == on Strings
- .equals
  - On Strings
    - Compare String
    - Uses equals method
  - On StringBuilders
    - Equals not implemented
    - Compares reference
  - On Objects
    - If no equals method is implemented
      - Compare reference
      - Same as ==
    - If equals is implemented
      - Compare with equals method implementation
  - On numbers
    - primitive
      - Impossible
    - Wrapper class
      - Compares number
        - False when different type;
        - true when one is wrapper class and other one is primitive

# Arrays

- Stringbuilder
  - Sequence of characters / Array of characters
  - Array object is replaced with new bigger array object when out of space to store all characters
- String
  - Sequence of characters / Array of characters
  - With methods for dealing with characters
- Array
  - Area of memory on the heap
    - Space for a designated number of elements
  - Ordered list
  - Brackets are used
  - Can contain duplicates

## Array of primitives

- Structures:
  - Basic structure:
    - Type[] identifier = new type[size]
      - Example
        - Int[] numbers = new int[3];
    - All elements are set to default value for type
  - Initialized array
    - Type[] identifier = new identifier [] {element1, element2, …};
    - Alternative
      - Anonymous array
      - Type[] identifier = {element1, element2, …};
    - Illegal:
      - Type[] identifier = new identifier [size] {element1, element2, …};
      - Type[size] identifier;
- Reference variable pointing to array object
- Index starts at 0
- [] can appear before or after identifier
  - Examples:
    - int[] animals;
    - int [] animals;
    - int animals[];
    - int animals [];
- array and normal type can be declared on one line:
  - type identifier1[], identifier2;

## Array with reference variables

- Any type can be used for arrays
  - Includes self-created classes
- Equals can be called on array
  - Compares reference
  - Does not look at elements
  - Works on arrays of primitives too
  - toString on array results in something liker [Ljava.lang.String;@160bc7c0
  - since java 5: java.util.Arrays.toString(array) prints array nicely
- array does not allocate space for objects, but for references to objects
- uninstantiated array references null
- assigning StringBuilder to String element in array does not compile
- assigning StringBuilder to Object element in array does throw ArrayStoreException
- casting:
  - example
    - String[] strings = (String[]) objects;

## Using an array

- length property
  - length of array
  - number of slots allocated (even when they are null)
  - size() method does not exist on array
- element at &quot;length&quot; position does not exist because of index starts at 0

## Sorting an array

- array has sort methods
  - sort()
    - Example
      - sort(numbers);
        - Order of numbers is changed
        - Small to large on numbers
        - Alphabetic order for strings
          - Be aware of numbers inside strings
            - Example: 10 100 9
              - 1 comes before 9
          - Numbers before characters
          - Uppercase before lowercase
  - Arrays needs one of these imports
    - Import java.util.\*;
    - Import java.util.Arrays;

## Searching in arrays

- Search only works if array is sorted
  - Not necessarily through sort function
- binarySearch(array, itemToFind));
- binarySearch splits array in 2 equal pieces and determines which half the target is. It repeats this process until only one element is left.

### Binary search rules

| Scenario | Result |
| --- | --- |
| Target element found in sorted array | Index of match |
| Target element not found in sorted array | Negative value showing one smaller than the negative of index, where a match needs to be inserted to preserve sorted order. (Negate and subtract one) |
| Unsorted Array | A surprise, not predictable |

#### Example:

int[] numbers = {2,4,6,8};
Arrays.binarySearch(numbers, 2) -\&gt; 0
Arrays.binarySearch(numbers, 4) -\&gt; 1
Arrays.binarySearch(numbers, 1) -\&gt; -1
Arrays.binarySearch(numbers, 3) -\&gt; -2
Arrays.binarySearch(numbers, 5) -\&gt; -5

## Varargs

- varargs can be used as if it were a normal array

## Multidimensional arrays

### Creating a multidimensional array

- example structures:
  - type[][] identifier;
  - type identifier[][];
  - type[] identifier[]; (2D array)
  - type[] identifier[][]; (3D array)
  - type[] identifier1 [], identifier2[][]; (2D array and 3D array)
- the arrays on the next level can have different sizes (= can be assmetric)
-
- initializing
  - examples
    - String[][] rectangle = new String[3][2]:
    - Int[][] differentsizes = {{1, 4}, {3}, {9, 8, 7}};
- Setting
  - Example
    - Reclangle[0][1] = &quot;set&quot;;

# ArrayList

- Can change size at runtime
- Ordered sequence
  - Allows duplicates
- One of these imports required
  - Import java.util.\*;
  - Import java.util.ArrayList;

## Creating

- Before Java 5: 3 ways
  - ArrayList list1 = new ArrayList();
    - Containing space for default number of elements
    - Not fill slots yet
  - ArrayList list2 = new ArrayList(10);
    - Specific number of slots
    - Not assign slots yet
  - ArrayList list3 = new ArrayList(list2);
    - Copy of another ArrayList;
      - Size
      - Contents
- Since Java 5: new ways added
  - ArrayList\&lt;String\&gt; list = new ArrayList\&lt;String\&gt;();
  - ArrayList\&lt;String\&gt; list = new ArrayList\&lt;\&gt;(); (since Jave 7)
- Implements interface List
  - Example
    - List\&lt;String\&gt; list = new ArrayList\&lt;\&gt;();

## Using

- Many methods
- E
  - Not really a class
  - Convention in generics
  - Any class that this array can hold (type between \&lt;\&gt;)
  - If no type specified: E = Object
  - toString() is implemented to print out easily

### add()

- insert new value in ArrayList
- signatures:
  - boolean add(E element)
    - always returns true
  - void add(int index, E element)
- if no type is specified for ArrayList,
  - all objects can be added
  - primitives cannot be added
- you can insert an element at a certain position (adds before existing element)
  - unexisting index: indexOutOfBoundException
    - at end of list is ok

### remove()

- removes first matching element
- signatures
  - Boolean remove(Object object)
    - Boolean true if element removed
  - E remove(int index)
    - Return value is element that was removed
    - Unexisting index: exception

### set()

- Changes one of the elements of ArrayList without changing size
- Signature
  - E set(int index, E newElement)
    - Returns old (replaced) element
- Unexisting index
  - Indexoutofboundexception
  - Adding one element at the end this way does not work

### isEmpty() and size()

- ArrayList does not have .length property
- Look how many slots are in use
  - Slot with null counts as slot
- Signatures
  - Boolean isEmpty()
  - int size()
    - size is one bigger than maximum index

### clear()

- discard all elements
- signature
  - void clear()
- ArrayList has size 0 after method;

### contains()

- Check if value is in ArrayList
- Signature
  - Boolean contains(Object object)
- Calls equals on each element()

### equals()

- Custom implementation of equals
  - Same elements in same order
- Signature
  - boolean equals(Object object)

## Wrapper Classes

- wrapper class is object type that corresponds to primitive
- each primitive type has wrapper class
- wrapper classes have a method that converts back to primitive
  - autoboxing has removed need for this

| Primitive type | Wrapper class | Example of constructing |
| --- | --- | --- |
| Boolean | Boolean | New Boolean(true) |
| Byte | Byte | New Byte((byte) 1) |
| short | Short | New Short((short) 1) |
| Int | Integer | New Integer(1) |
| Long | Long | New Long(1) |
| Float | Float | New Float(1.0) |
| Double | Souble | New Double(1.0) |
| Char | Character | New Character(&#39;c&#39;) |

- converting String to int
  - parseInt()
    - returns primitive
  - valueOf()
    - returns wrapper class

| Wrapper class | Converting String to primitive | Converting String to Wrapper class |
| --- | --- | --- |
| Boolean | Boolean.parseBoolean(&quot;true&quot;); | Boolean.valueOf(&quot;TRUE&quot;); |
| Byte | Byte.parseByte(&quot;1&quot;); | Byte.valueOf(&quot;2&quot;); |
| Short | Short.parseShort(&quot;1&quot;); | Short.valueOf(&quot;2&quot;); |
| Integer | Integer.parseInt(&quot;1&quot;); | Integer.valueOf(&quot;2&quot;); |
| Long | Long.parseLong(&quot;1&quot;); | Long.valueOf(&quot;2&quot;); |
| Float | Float.parseFloat(&quot;1&quot;); | Float.valueOf(&quot;2.2&quot;); |
| Double | Double.parseDouble(&quot;1&quot;); | Double.valueOf(&quot;2.2&quot;); |
| Character | None | None |

## Autoboxing

- Since Java 5
  - Java converts primitive value automatically yo relevant wrapper class
- When unboxing null
  - NullPointerException
- Remove Integer from List
  - When passing int to remove index is used
  - Use new Integer to solve this

## Converting between array and List

- From ArrayList to array
  - Call toArray on object
  - Default: array of class Object
  - Specify type as parameter
    - Example
      - toArray(new String[0]);
    - Size 0 means array with proper size is created
- From array to List
  - asList
    - Takes array or just the values typed out
  - Linked (backed)
    - When array changes, List changes too
    - When List changes, array changes
    - Fixed size
      - Add or Remove throws UnsupportedOperation Exception
      - Changing size is not possible
    - != java.util.ArrayList
  - When coming from int array, toString of this type of list returns something like: [[I@74a14482]

## Sorting

- Similar to sorting Array
- Use helper class
  - example
    - sort(numbers);

# Dates and Times

- Import is needed
  - Import java.time.\*;

## Creating dates and times

- Three choices:
  - LocalDate
    - Just a date
    - No time
    - No time zone
    - Example:
      - birthday this year
  - LocalTime
    - Just a time
    - No date
    - No time zone
    - Example:
      - Midnight
  - LocalDateTime
    - Date
    - Time
    - No time zone
    - Example:
      - Stroke of midnight on New Year&#39;s
- Avoid time zones unless necessary
  - ZonedDateTime if necessary
- now():
  - examples:
    - now();
      - 2015-01-20
      - Month before day
    - now();
      - 12:45:18.401
        - Hours, minutes, seconds, nanoseconds
    - now();
      - 2015-01-20T12:45:18.401
        - T separates date and time
- Of()
  - Examples:
    - of(2015, Month.JANUARY, 20);
    - of(2015, 1, 20);
      - Months start at 1
  - Signatures
    - Public static LocalDate of(int year, int month, int dayOfMonth)
    - Public static LocalDate of(int year, Month month, int dayOfMonth)
  - Month: enum
  - For time, choose precision:
    - Examples:
      - of(6, 15); // hour and minute
      - of(6, 15, 30); // + seconds
      - of(6, 15, 30, 200); // + nanoseconds
    - Signatures
      - public static LocalTime of(int hour, int minute);
      - public static LocalTime of(int hour, int minute, int seconds);
      - public static LocalTime of(int hour, int minute, int seconds, int nanos);
    - DateTimeException when impossible values
  - combination of date and time
    -
      - first date, then time
      - possible to give separate values with any precision
        - at least hour and minute for time
      - possible to give a LocalDate and a LocalTime
      - do not combine LocalDate or LocalDateTime with separate values, does not compile
  - not allowed to create LocalDate, LocalDateTime or LocalTime through constructor
    - does not compile
    - always use static methods (of)

## Manipulating dates and times

- date and time classes are immutable
  - need to be assigned to remember value
  - are not changed by a method
- methods:
  - plusDays()
    - example
      - date = date.plusDays(2);
    - adds number of days
  - plusWeeks
    - example
      - date = date.plusWeeks(1-:
    - adds 7 days \* number of weeks
  - plusMonths
    - adds number of months
    - Java knows leap years
      - If day does not exist in month, last day of month is used
  - plusYears
    - adds number of years
- methods can be chained
- doing time manipulations on LocalDate does not compile
- doing date manipulation on LocalTime does not compile

|   | Can call on LocalDate | Can call on LocalTime | Can call on LocalDateTime |
| --- | --- | --- | --- |
| plusYears/minusYears | yes | no | yes |
| plusMonths/minusMonths | yes | no | yes |
| plusWeeks/minusWeeks | yes | no | yes |
| plusDays/minusDays | yes | no | yes |
| plusHours/minusHours | no | yes | yes |
| plusMinutes/minusMinutes | no | yes | yes |
| plusSeconds/minusSeconds | no | yes | yes |
| plusNanos/minusNanos | np | yes | Yes |

## Periods

- converting date to long
  - LocalDate.toEpochDay()
    - Number of days since January 1, 1970
  - LocalDateTime.toEpochSecond()
    - Number of seconds since January 1, 1970
  - LocalTime does not have epoch method
  - Timezone: GMT
- Period class
  - Examples
    - period.ofYears(1);
    - period.ofMonths(3);
    - period.ofWeeks(3);
    - period.ofDays(2);
    - period.of(1, 0, 7); // every year and 7 days
  - methods cannot be chained
    - does compile but does not do what expected
    - gives compiler warning
  - plus method on LocalDate LocalDateTime, LocalTime
    - adding month to LocalTime does not work
      - UnsupportedTemporalTypeException

## Formatting dates and times

- Many methods to get information from date or time
  - Examples
    - date.getDayOfWeek();
    - date.getMonth();
    - date.getYear();
    - date.getDayOfYear();
- DateTimeFormatter
  - Examples
    - date.format(DateTimeFormatter.ISO\_LOCAL\_DATE));
    - time.format(DateTimeFormatter.ISO\_LOCAL\_TIME));
    - dateTime.format(DateTimeFormatter.ISO\_LOCAL\_DATE\_TIME));
  - ISO is standard for dates
  - Do not apply time formatters on dates or date formatters on time
  - Predefined formats:
    - Example
      - DateTimeformatter shortDateTime = DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT);
    - Usage example
      - shortDateTime.format(dateTime);
      - dateTime.format(shortDateTime);
    - exception when formatting is not possible

| DateTimeFormatter f = DateTimeFormatter.\_\_\_ (FormatStyle.SHORT); | Calling f.format(localDate) | Calling f.format(localDateTime) | Calling f.format(localTime) |
| --- | --- | --- | --- |
| ofLocalizedDate | Legal, shows whole object | Logal – shows date part | Runtime exception |
| ofLocalizedDateTime | Throws runtime exception | Legal – shows whole object | Runtime exception |
| ofLocalizedTime | Throws runtime exception | Legal – shows time part | Legal – shows whole opbject |

- Predefined formats:
  - SHORT
    - Example
      - 1/20/20 11:12 AM
  - MEDIUM
    - Example
      - Jan 20, 2020 11:12:34 AM
- You can create your own
  - Example
    - DateTimeFormatter.ofPattern(&quot;MMMM dd, yyyy, hh:mm&quot;);
  - Syntax
    - MMMM
      - Example: January
    - MMM
      - Example Jan
    - MM
      - Example: 01
    - M
      - example: 1
      - example: 12
    - d or dd
      - day of month
    - ,
      - Output comma
    - yy or yyyy
      - year
    - h or hh
      - hour
    - :
      - Output colon
    - mm
      - minute

## Parsing dates and times

- convert String to date or time with formatter or without
  - examples
    - DateTimeFormatter f = DateTimeFormatter.ofPattern(&quot;MM dd yyyy&quot;);
LocalDate.parse(&quot;01 02 2015, f);
    - LocalTime time = LocalTime.parse(&quot;11:22&quot;);
