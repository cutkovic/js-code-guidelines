# JS Code Guidelines
## The purpose of this document is to provide general coding and style guidelines that should be followed while producing javascript code. There could be some exceptions and situations that require shift from these rules but in general these rules should be followed as much as possible in order to have consistent, pragmatic code.

### Indentation
Each indentation level is made up of 4 spaces. Text editor should be configured to insert spaces when the tab is pressed. If you break a line, next line is indented for 2 levels or 8 spaces.
When declaring multiple variables with a single var statement, every variable declaration should be on a separate line, and declarations should be aligned by an equal operator.

### Line length
Avoid lines that are longer than 80 characters.
There are exceptions to this rule :
When the line contains URL with some long content
If the line contains a regex literal. This prevents having to use the regex constructor which requires otherwise unnecessary string escaping.
If you’re constructing HTML inside javascript and all the HTML markup is placed on a single line

### Statement termination
Always terminate statement with a semicolon, to avoid possible errors caused by Automatic Semicolon Insertion (ASI)

### Naming guidelines
Use naming convention that follows core language naming convention. In case of Javascript that is camel case.

Variable names are always cames case and should begin with a noun. Beginning with a noun helps to differentiate variables from functions, which should begin with a verb.

Try to make the variable name indicate the datatype of its value. For example, the names count, length and size suggest the data type is a number, and names such as name, title and message suggest that the data type is a string. Single character variable names such as i, j and k are usually reserved for use in loops.

For function names and method names, the first word should always be a verb and there are some conventions for that :

can Function returns a boolean
has     Function returns a boolean
is  Function returns a boolean
get     Function returns a non-boolean
set     Function is used to save a value

### Constants
Javascript has no formal concept of constants (had no prior to ECMAScript 6)
The convention for constants is to use all uppercase letters with underscores separating words as in :
var MAX_COUNT = 10;
var URL = "http://www.nczonline.net/";

### Constructors
Javascript constructor are simply a functions that are used to create objects via new operator. So constructors in Javascript are formatted using Pascal case.

### String literals
Use single quotes for string literals. There is no real functional difference between single quotes and double quotes, it is just a matter to choose one style and stick to it. Single quotes is preferable only because when using single quotes you don’t have to escape them like when using double quotes.

### Null value
The special value null is often misunderstood and confused with  undefined. This value
should be used in just a few cases:
To initialize a variable that may later be assigned an object value
To compare against an initialized variable that may or may not have an object value
To pass into a function where an object is expected
To return from a function where an object is expected
There are also some cases in which null should not be used:
Do not use null to test whether an argument was supplied.
Do not test an uninitialized variable for the value null.

The best way to think about null is as a placeholder for an object.

### Undefined
Variables that are not initialized have an initial value of undefined, which essentially
means the variable is waiting to have a real value.
Despite this working, I recommend avoiding the use of undefined in code. This value
is frequently confused with the typeof operator returning the string “undefined” for a
value. In fact, the behavior is quite confusing, because  typeof will return the string
“undefined” both for variables whose value is undefined and for undeclared variables.

// foo is not declared
var person;
console.log(typeof person); //"undefined"
console.log(typeof foo); //"undefined"

In this example, both person and foo cause typeof to return “undefined” even though
they behave very different in almost every other way (trying to use foo in a statement
will cause an error, but using person will not).

By avoiding the use of the special value undefined, you effectively keep the meaning of
typeof returning “undefined” to a single case: when a variable hasn’t been declared. If
you’re using a variable that may or may not be assigned an object value later on, initialize
it to null:

// Good
var person = null;
console.log(person === null); //true

Setting a variable to null initially indicates your intent for that variable; it should eventually contain an object. The  typeof operator returns “object” for a null value, so it can
be differentiated from undefined.

### Object creation
Use object literals instead of Object constructor.

### Array creation
Use array literals instead of Array constructor.

### Single Line Comments
Single-line comments are created by using two slashes and end at the end of the line:
// Single-line comment

Many prefer to include a space after the two slashes to offset the comment text. There
are three ways in which a single-line comment is used:
- On its own line, explaining the line following the comment. The line should always
be preceded by an empty line. The comment should be at the same indentation
level as the following line.
- As a trailing comment at the end of a line of code. There should be at least one
indent level between the code and the comment. The comment should not go
beyond the maximum line length. If it does, then move the comment above the
line of code.
- To comment out large portions of code (many editors automatically comment out
multiple lines).

Single-line comments should not be used on consecutive lines unless you’re commenting out large portions of code. Multiline comments should be used when long comment
text is required.

Here are some examples:

    // Good
    if (condition) {

        // if you made it here, then all security checks passed
        allowed();
    }

    // Bad: No empty line preceding comment
    if (condition) {
        // if you made it here, then all security checks passed
        allowed();
    }

    // Bad: Wrong indentation
    if (condition) {

    // if you made it here, then all security checks passed
        allowed();
    }

    // Good
    var result = something + somethingElse; // somethingElse will never be null

    // Bad: Not enough space between code and comment
    var result = something + somethingElse;// somethingElse will never be null

    // Good
    // if (condition) {
    // doSomething();
    // thenDoSomethingElse();
    // }

    // Bad: This should be a multiline comment
    // This next piece of code is quite difficult, so let me explain.
    // What you want to do is determine whether the condition is true
    // and only then allow the user in. The condition is calculated
    // from several different functions and may change during the
    // lifetime of the session.
    if (condition) {
        // if you made it here, then all security checks passed
        allowed();
    }

Multiline comments
I prefer the Java-style multiline comment pattern. The Java style is to have at least three lines: one for the  /*, one or more lines beginning with a *that is aligned with the  *on the previous line, and the last line for */. The resulting comment looks like this:
```javascript
/*
 * Yet another comment.
 * Also goes to a second line.
 */
```
Here are some examples:
```javascript
    // Good
    if (condition) {

        /*
         * if you made it here,
         * then all security checks passed
         */
        allowed();
    }

    // Bad: No empty line preceding comment
    if (condition) {
        /*
        * if you made it here,
        * then all security checks passed
        */
        allowed();
    }

    // Bad: Missing a space after asterisk
    if (condition) {

        /*
        *if you made it here,
        *then all security checks passed
        */
        allowed();
    }

    // Bad: Wrong indentation
    if (condition) {

    /*
     * if you made it here,
     * then all security checks passed
     */
        allowed();
    }

    // Bad: Don't use multiline comments for trailing comments
    var result = something + somethingElse; /*somethingElse will never be null*/
```

### Documentation comments

Document comments may take many forms, but the most popular
is the form that matches JavaDoc documentation format: a multiline comment with an
extra asterisk at the beginning (/**) followed by a description, followed by one or more
attributes indicated by the @sign. Here’s an example from YUI:
```javascript
    /**
    Returns a new object containing all of the properties of all the supplied
    objects. The properties from later objects will overwrite those in earlier
    objects.

    Passing in a single object will create a shallow copy of it. For a deep copy,
    use `clone()`.

    @method merge
    @param {Object} objects* One or more objects to merge.
    @return {Object} A new merged object.
    **/
    Y.merge = function () {
        var args = arguments,
            i = 0,
            len = args.length,
            result = {};

        for (; i < len; ++i) {
            Y.mix(result, args[i], true);
        }
        return result;
    };
```

### Statements and Expressions

Statements such as if/else/for/while/try should always span multiple lines.
```javascript
    // Bad, though technically valid JavaScript
    if(condition)
        doSomething();

    // Bad, though technically valid JavaScript
    if(condition) doSomething();

    // Good
    if (condition) {
        doSomething();
    }

    // Bad, though technically valid JavaScript
    if (condition) { doSomething(); }
```
Braces should be used for all block statements, including:

- if
- for
- while
- do...while
- try...catch...finally

### Brace Alignment

The opening brace should be on the same line as the beginning of the block statement, as in this example :

```javascript
    if (condition) {
        doSomething();
    } else {
        doSomethingElse();
    }
```

### Block Statement Spacing

Use space separation begore the opening parenthesis and after the closing parenthesis, such as :
```javascript
if (condition) {
        doSomething();
    }
```

### The switch Statement
Each case statement is indented one level from the switch keyword.
```javascript
    switch(condition) {
        case "first":
            // code
            break;
        case "second":
            // code
            break;
        case "third":
            // code
        break;
        default:
        // code
    }
```
Falling Through is acceptable method of programming, as long as it is clearly indicated, such as :
```javascript
    switch(condition) {
        // obvious fall through
        case "first":
        case "second":
            // code
            break;
        case "third":
            // code

            /*falls through*/
        default:
            // code
    }
```
