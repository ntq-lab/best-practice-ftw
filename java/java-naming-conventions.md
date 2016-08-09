# Java naming conventions

Java naming conventions are a set of rules which were recommmended to follow as we devicde 
what to name identifiers such as class, method, package, variable, constant, etc.

## Class Name

A class name should always starts with **an uppercase** letter and and should be **a noun** or **a noun phrase**.  

### Best practices :smiley:
```java
public class Language {
}

public class AsyncHttpClient {
}
```

### Bad practices :angry:
```java
// From JDK1.2.
public class NO_RESPONSE {
}

// From Jodd libaries.
public class FindFile {
}

```

An abstract class should end with postfixes like: `Base`, `Support` or can start with the prefix: `Abstract`.

But bear in mind that we should be consitent with one convention throughout one project (at least).

### Best practices :smiley:
```java

// From Apache.
public abstract class LifecycleBase implements Lifecycle {
}

// Learned from Spring.
public abstract class FluentCollectionSupport<E> implements FluentCollection<E> {
}

// From JDK.
public abstract class AbstractCollection<E> implements Collection<E> {
}

```

A concrete class implementing an interface should have a specific name indicating its implementation strategy, otherwise class name can start with prefix `Default` or end with postfix `Impl`.

### Best practices :smiley:

```java

// From JDK, implementation class has a specific name with a specific implementation strategy.
public class ArrayBlockingQueue<E> extends AbstractQueue<E> implements BlockingQueue<E> {
}

public class LinkedBlockingDeque<E> extends AbstractQueue<E> implements BlockingDeque<E> {
}

// From Spring.
public final class DefaultSecurityFilterChain implements SecurityFilterChain {
}

// From Eclipse Collections.
public final class MutableBagFactoryImpl implements MutableBagFactory {
}

```
## Interface Name

An interface names should also start with **an uppercase letter** and be **a noun** or **a phrase noun** or an **adjective**
### Best practices :smiley:

```java

// From Spring.
public interface ApplicationContext {
}

// From JDK.
public interface Executor {
}

// Name is an adjective.
public interface Runnable {
}

public interface Iterable {
}

```

Interface name should never start or end with prefixes like `I` or postfixes like `Interface`.

### Bad practices :angry:

```java
// From Java Wordnet Interface Library (JWI) v2.4.0.
public interface IDictionary extends IHasVersion, IHasLifecycle, IHasCharset {
}

// From JDK.
public interface RepositoryIdInterface {
}
```
