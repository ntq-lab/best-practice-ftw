# C# coding conventions

The C# Language Specification does not define a coding standard. However, the guidelines in this topic are used by Microsoft to develop samples and documentation.
Coding conventions serve the following purposes:
* They create a consistent look to the code, so that readers can focus on content, not layout.
* They enable readers to understand the code more quickly by making assumptions based on previous experience.
* They facilitate copying, changing, and maintaining the code.
* They demonstrate C# best practices.

:+1: **DO**
:-1: **DO NOT**
:ok_hand: **CONSIDER**

# Naming conventions
|Identifier|Cases|Name rules|Example|
-----------|-------|---------|---
Class|Pascal|noun or noun phrases|ApplicationContext
Interface|Pascal|adjective phrases, nouns or noun phrases.<br>prefix interface names with the letter I, to indicate that the type is an interface.|IDisposable, ISessionChannel
Enumeration type|Pascal|noun or noun phrases.<br>DO NOT use an "Enum" suffix in enum type names.<br>DO NOT use "Flag" or “Flags" suffixes in enum type names.|Direction, ErrorLevel<br>
Event|Pascal|name events with a verb or a verb phrase.<br>name event handlers (delegates used as types of events) with the "EventHandler" suffix<br>use two parameters named sender and e in event handlers.|Clicked, Painting, ValueChanged<br><br>ClickedEventHandler
Event argument|Pascal|name event argument classes with the "EventArgs" suffix.|ClickedEventArgs
Method|Pascal|give methods names that are verbs or verb phrases.|Split, CompareTo
Property|Pascal|name properties using a noun, noun phrase, or adjective.<br>CONSIDER giving a property the same name as its type.|BackColor<br>public ConnectionStatus ConnectionStatus { get {...} set {...} }
Parameter|Camel|use descriptive parameter names, using names based on a parameter’s meaning rather than the parameter’s type.<br>use _**value**_ for parameter names if there is no meaning to the parameters.|userName<br>public static int ToInt32(string value) {...}
Private field|Camel|name fields using a noun, noun phrase, or adjective.<br>DO NOT use a prefix for field names.<br>DO NOT use "g_" or "s_" to indicate static fields.|backgroundTasks
Public/Protected static field|Pascal|Similar to _**Private field**_|Empty, MinValue, MaxValue
Constant field|Pascal|Similar to _**Private field**_|MaxInt
Local variable|Camel|Similar to _**Private field**_|i, selectedColor

## Class

**DO** Name classes and structs with **nouns** or **noun phrases**

### :+1: Best practices
```C#
public class String 
{
}

public class HttpClient
{
}
```

### :-1: Bad practices
```C#
// From DQS project
public class ResetPassword
{
}

public static class TransferData
{
}
```

**DO** An abstract class should end with postfixes like: `Base` or can start with the prefix: `Abstract`.

But bear in mind that we should be consitent with one convention throughout one project (at least).

### Best practices :smiley:
```C#

// From DQS project.
public abstract class BaseController
{
}
```

A concrete class implementing an interface should have a specific name indicating its implementation strategy.

### Best practices :smiley:

```C#

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

An interface name should also start with **an uppercase letter** and be **a noun** or **a phrase noun** or an **adjective**
### Best practices :smiley:

```C#

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

Interface names should never start or end with prefixes like `I` or postfixes like `Interface`.

### Bad practices :angry:

```C#
// From C# Wordnet Interface Library (JWI) v2.4.0.
public interface IDictionary extends IHasVersion, IHasLifecycle, IHasCharset {
}

// From JDK.
public interface RepositoryIdInterface {
}
```
