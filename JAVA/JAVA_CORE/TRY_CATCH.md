# Exception Handling in Java

## Types of Error
- Syntax Error: Errors in the code that prevent it from compiling. eg. missing semicolon, misspelled keywords.
- Runtime Error: Errors that occur during the execution of the program. eg. division by zero, null pointer exceptions.
- Logical Error: Errors in the logic of the program that lead to incorrect results. eg. incorrect calculations, wrong conditions in loops.

## Syntax:
```
try {
    // Code that may throw an exception
} catch (ExceptionType1 e1) {
    // Handle ExceptionType1
} catch (ExceptionType2 e2) {
    // Handle ExceptionType2
} finally {
    // Code that will always execute, regardless of whether an exception occurred or not
}
```

Hierarchy of Exception classes:
- Throwable 
  - Error
  - Exception
    - Checked Exceptions (e.g., IOException, SQLException)
    - Unchecked Exceptions (e.g., RuntimeException, NullPointerException)  

Multiple Catch Blocks, Nested try-catch

Stack Trace: Provides information about the sequence of method calls that led to the exception.
- Syntax: 
    StackTraceElement[] stackTrace = e.getStackTrace();
- Commonly used method to print stack trace:
    `e.printStackTrace();`
    or `strackTrace[i]` to get specific element.

For file handling use of exceptions handling is mandatory, or add exception to method signature using `throws` keyword.

throw vs throws:
- throw: Used to explicitly throw an exception from a method or any block of code.  
- throws: Used in method signature to declare that a method may throw one or more exceptions.
all methods using the method must handle or declare the exception. like if we call fun() which is having throws IOException, then fun1() which is calling fun() must also handle or declare IOException.

Custom Exception:
- Create a user-defined exception by extending the Exception class.
```java 
class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}
```

Closing resources:
- Use try-with-resources statement to automatically close resources like files, database connections, etc. i.e use finally to close resources.
eg sc.close() in finally block.

try with resources:
```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
``` 
- Automatically closes the resource when the try block is exited, either normally or via an exception because it is implementing AutoCloseable interface.

