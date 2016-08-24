# C# Best practices
:+1: Consider ending the name of derived classes with the name of the base class.

_Make source code is readable and explans the relationship clearly_
```C#
# From .NET Framework 
public class KeyPressEventArgs : EventArgs
{
}

# From DQS project
public class UserController : BaseController
{
}
```

