# Java naming conventions

Java naming conventions are a set of rules which were standardized and recommmended by Sun Microsystems, Inc to follow as we devicde 
what to name identifiers such as class, method, package, variable, constant, etc.

## Class Name

A class name should always starts with **an uppercase** letter and and should be **a noun** or **a noun phrase**.

```java
// :thumbsup: Good names .
public class Employee {
}

public class AsyncHttpClient {
}

// Bad names.
// From JDK1.2.
public class NO_RESPONSE {
}

// From Jodd libaries.
public class FindFile {
}

```

An abstract class should end with postfixes like: `Base`, `Support` but should not start with the prefix: `Abstract` but still acceptable.

```
// Good names :
```

http://www.javatpoint.com/java-naming-conventions
