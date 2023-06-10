# TinyBasicPHP
Tiny Basic in PHP. Learn about building Basic interpreters from this simple working model.

Feel free to help improve this here or just get the code for your own use.


The code you provided is a PHP implementation of a Tiny BASIC interpreter. It allows you to run and execute programs written in Tiny BASIC, a simplified version of the BASIC programming language.

Here's an overview of how the interpreter works:

1. The code defines a class called `TinyBasicInterpreter` that encapsulates the functionality of the interpreter.

2. The `TinyBasicInterpreter` class has several properties, including `$program` (an array to store the parsed program lines), `$variables` (an array to store variable values), `$input` (to store user input), and `$forStack` and `$gosubStack` (to handle loops and subroutines).

3. The `run($code)` method is responsible for executing the Tiny BASIC program. It first parses the program code into individual lines and statements using the `parseProgram($code)` method.

4. The `executeProgram()` method is called to execute the parsed program. It iterates over the program lines in ascending order and executes each statement by calling the `executeStatement($statement)` method.

5. The `executeStatement($statement)` method handles different Tiny BASIC statements based on the command. It supports commands like `PRINT`, `LET`, `INPUT`, `GOTO`, `IF`, `GOSUB`, `RETURN`, `FOR`, `NEXT`, `REM`, `LIST`, `ABS`, `INT`, `RND`, and `SIZE`. The implementation of each command varies, but they generally involve printing output, assigning values to variables, performing arithmetic operations, controlling program flow, or executing subroutines.

6. The `evaluateExpression($expression)` method is used to evaluate mathematical expressions within the Tiny BASIC program. It replaces variables with their corresponding values and uses the `eval()` function to compute the expression result.

7. The interpreter executes the program line by line until there are no more lines to execute, or until a control flow statement like `GOTO`, `THEN`, or `RETURN` changes the program execution flow.

It's important to note that while the provided code attempts to implement a Tiny BASIC interpreter, it contains some issues and potential improvements. For example, there are variable scoping concerns, potential security risks when using `eval()`, and other possible edge cases that may not be handled correctly. Care should be taken when using this code, and it is advisable to review and test it thoroughly to ensure it meets your specific requirements.
