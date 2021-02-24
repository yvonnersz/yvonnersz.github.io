Here are some of the common types of errors that I have come across as I code my projects:

## ReferenceError
> The ReferenceError object represents an error when a non-existent variable is referenced.

In other words, this happens when you call a variable that has not been declared yet. For example:

```
$ variable

VM217:1 Uncaught ReferenceError: variable is not defined
    at <anonymous>:1:1
```

To fix this, we would just have to declare the variable before calling on it.

```
$ let variable = 'hi'
$ variable // 'hi'
```

## SyntaxError
> The SyntaxError object represents an error when trying to interpret syntactically invalid code.

Pretty self-explanatory! This error occurs when the syntax of your code isn't correct. For example:

## TypeError
> The TypeError object represents an error when an operation could not be performed, typically (but not exclusively) when a value is not of the expected type.

For example, this error could be thrown if:
1. an operand or argument passed to a function is incompatible with the type expected by that operator or function; or
2. when attempting to modify a value that cannot be changed; or
3. when attempting to use a value in an inappropriate way.
