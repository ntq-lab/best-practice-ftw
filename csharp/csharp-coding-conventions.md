# C# coding conventions

The C# Language Specification does not define a coding standard. However, the guidelines in this topic are used by Microsoft to develop samples and documentation.
Coding conventions serve the following purposes:
* They create a consistent look to the code, so that readers can focus on content, not layout.
* They enable readers to understand the code more quickly by making assumptions based on previous experience.
* They facilitate copying, changing, and maintaining the code.
* They demonstrate C# best practices.

## Naming conventions
|Identifier|Cases|Name rules|Example|
-----------|-------|---------|---
Assembly and DLLs|Pascal|Choose names for your assembly DLLs that suggest large chunks of functionality, such as System.Data.<br>CONSIDER naming DLLs according to the following pattern:<br>`<`Company`>`.`<`Component`>`.dll<br>Refer to MSDN [Names of Assemblies and DLLs](https://msdn.microsoft.com/en-us/library/ms229048(v=vs.110).aspx)|Ntq.Controls.dll
Namespace|Pascal|`<`Company`>`.(<Product`>|`<`Technology`>`)[.`<`Feature`>`][.`<`Subnamespace`>`]<br>Refer to MSDN: [Names of Namespaces](https://msdn.microsoft.com/en-us/library/ms229026(v=vs.110).aspx)|Fabrikam.Math, Microsoft.Build.Tasks
Class|Pascal|noun or noun phrases|ApplicationContext
Interface|Pascal|adjective phrases, nouns or noun phrases.<br>prefix interface names with the letter I, to indicate that the type is an interface.|IDisposable, ISessionChannel
Enumeration type|Pascal|noun or noun phrases.<br>DO NOT use an "Enum" suffix in enum type names.<br>DO NOT use "Flag" or “Flags" suffixes in enum type names.|Direction, ErrorLevel<br>
Event|Pascal|name events with a verb or a verb phrase.<br>name event handlers (delegates used as types of events) with the "EventHandler" suffix<br>use two parameters named sender and e in event handlers.|Clicked, Painting, ValueChanged<br><br>ClickedEventHandler
Event argument|Pascal|name event argument classes with the "EventArgs" suffix.|ClickedEventArgs
Method|Pascal|give methods names that are verbs or verb phrases.|Split, CompareTo
Property|Pascal|name properties using a noun, noun phrase, or adjective.<br>CONSIDER giving a property the same name as its type.|BackColor<br>public ConnectionStatus ConnectionStatus { get {...} set {...} }
Parameter|Camel|use descriptive parameter names, using names based on a parameter’s meaning rather than the parameter’s type.<br>use _**value**_ for parameter names if there is no meaning to the parameters.|userName<br>public static int ToInt32(string value) {...}
Private field|Camel|name fields using a noun, noun phrase, or adjective.<br>DO NOT use a prefix for field names.<br>DO NOT use "g_" or "s_" to indicate static fields.|backgroundTasks, connected
Public/Protected static field|Pascal|Similar to _**Private field**_|Empty, MinValue, MaxValue
Constant field|Pascal|Similar to _**Private field**_|MaxInt
Local variable|Camel|Similar to _**Private field**_|i, selectedColor

Refer MSND [Naming Guidelines](https://msdn.microsoft.com/en-us/library/ms229002(v=vs.110).aspx)

## Layout Conventions
* Use the default Code Editor settings (smart indenting, four-character indents, tabs saved as spaces).
* Write only one statement per line.
* Write only one declaration per line.
```C#
string firstName;
string lastName;
int age;
```
Above code snipet may be changed later to:
```C#
string firstName = GetFirstName(userName);
string lastName = GetLastName(userName);
int age;
```
* If continuation lines are not indented automatically, indent them one tab stop (four spaces).
* Add at least one blank line between code blocks.
```C#
if (connected)
{
    ...
}

if (bytesSent > 0)
{
    ...
}
````
* Use parentheses to make clauses in an expression apparent, as shown in the following code.
```C#
if ((val1 > val2) && (val1 > val3))
{
    // Take appropriate action.
}
```

## Commenting Conventions
* Place the comment on a separate line, not at the end of a line of code.
* Begin comment text with an uppercase letter.
* End comment text with a period.
* Insert one space between the comment delimiter (//) and the comment text, as shown in the following example.
```C#
// The following declaration creates a query.
// It does not run the query.
```
* :-1: DO NOT create formatted blocks of asterisks around comments.
```C#
/*
* The following declaration creates a query.
* It does not run the query.
*/ 
```
## 