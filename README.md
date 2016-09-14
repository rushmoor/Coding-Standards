# Rushmoor Borough Council - Coding Standards

1. [Introduction](#introduction)
2. [Naming Conventions and Style](#naming-conventions-and-style)
3. [Coding Practices](#coding-practices)
4. [References](#references)

## Introduction

This document provides a set of coding standards for developers working on .NET C# projects at Rushmoor Borough Council. 
These guidelines are in place to encourage consistency, maintainability and best practice across all application development 
at the council.

## Naming Conventions and Style

1\. Use Pascal casing for type and method names

```csharp
public class SomeClass
{
    public SomeMethod(){}
}
```

2\. Use camel casing for local variable names and method arguments

```csharp
int number;
void myMethod(int someNumber)
{}
```

3\. Prefix interface name with **I**
```csharp
interface IMyInterface
{}
```

4\. Prefix private member variables with **_**
```csharp
public class SomeClass
{
    private int _myNumber;
}
```

5\. Suffix custom attribute classes with **Attribute**.

6\. Suffix custom exception classes with **Exception**.

7\. Name methods using verb-object pair, such as **ShowDialog()**.

8\. Methods with return values should have a name describing the value returned, such as **GetObjectState()**.

9\. Use descriptive variable names.
* Avoid single character variable names, such as **i** or **t**. Use 
**index** or **temp** instead.
* Avoid using Hungarian notation for public or protected members.
* Do not abbreviate words (such as **num** instead of **number**).

10\. Always use C# predefined types rather than the aliases in the **System** namespace. 
For example:
```csharp
object NOT Object
string NOT String
int NOT Int32
```

11\. With generics, use capital letters for types. Reserve suffixing **Type** when dealing 
with the .NET type **Type**.
```csharp
// Correct:
public class LinkedList<K, T>
{...}
// Avoid:
public class LinkedList<KeyType, DataType>
{...}
```

12\. Use meaningful namespaces such as the product name of the company name.

13\. Avoid fully qualified type names. Use the **using** statement instead.

14\. Group all framework namespaces together and put custom or third party namespaces underneath.
```csharp
using System;
using System.Collections;
using System.ComponentModel;
using System.Data;
using MyCompany;
using MyControls;
```

15\. Use delegate interface instead of explicit delegate instantiation
```csharp
delegate void SomeDelegate();
public void SomeMethod();
{...}
SomeDelegate someDelegate = SomeMethod;
```

16\. Maintain strict indentation
* Use tabs, **not spaces** for indentation
* Set tab size **4** and indent size **4**

17\. Indent comments at the same level of indentation as the code you are documenting.

18\. All comments should pass spell checking and maintain a high standard of grammar.

19\. All member variables should be declared at the top, with one line separating them from the properties or methods.
```csharp
public class MyClass
{
    private int _number;
    private string _name;

    public void SomeMethod1()
    {}

    public void SomeMethod2()
    {}
}
```

20\. Declare a local variable as close as possible to its use.

21\. A file name should reflect the class it contains.

22\. When using partial types and allocating a part per file, 
name each file after the type suffixed with a *p* and an ordinal number:
```csharp
// In MyClassP1.cs
public partial class MyClass
{...}

// In MyClassP2.cs
public partial class MyClass
{...}
```

23\. Always place an open curly brace (**{**) in a new line.

24\. With Lambda expressions, mimic the code layout of a regular method, aligned with 
the delegate declaration. Omit the variable type and rely on type inference yet use parentheses:
```csharp
delegate void SomeDelegate(string someString);

SomeDelegate someDelegate = (name) => 
                            {
                                Trace.WriteLine(name);
                                MessageBox.Show(name);
                            };
```


25\. Only use in-line Lambda expressions when they contain a single simple statement. 
Avoid multiple statements that require a curly brace or a **return** statement with 
inline expressions. Omit parentheses:

```csharp
delegate void SomeDelegate(string someString);

void MyMethod(SomeDelegate someDelegate)
{...}

// Correct:
MyMethod(name => MessageBox.Show(name));

// Avoid:
MyMethod((name) => {Trace.WriteLine(name);MessageBox.Show(name);});
```

26\. Use empty parenthesis on parameter-less anonymous methods

## Coding Practices

1\. Follow the [SOLID principles](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod) as closely as possible
* [SRP - The Single Responsibility Principle](https://docs.google.com/open?id=0ByOwmqah_nuGNHEtcU5OekdDMkk)
    * The class should have one, and only one, reason to change.
* [OCP - The Open Closed Principle](http://docs.google.com/a/cleancoder.com/viewer?a=v&pid=explorer&chrome=true&srcid=0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1&hl=en)
    * You should be able to extend a classes behaviour, without modying it.
* [LSP - The Liskov Substitution Principle](http://docs.google.com/a/cleancoder.com/viewer?a=v&pid=explorer&chrome=true&srcid=0BwhCYaYDn8EgNzAzZjA5ZmItNjU3NS00MzQ5LTkwYjMtMDJhNDU5ZTM0MTlh&hl=en)
    * Derived classes must be substitutable for their base classes.
* [ISP - The Interface Segregation Principle](http://docs.google.com/a/cleancoder.com/viewer?a=v&pid=explorer&chrome=true&srcid=0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi&hl=en)
    * Make fine grained interfaces that are client specific.
* [DIP - The Dependency Inversion Principle](http://docs.google.com/a/cleancoder.com/viewer?a=v&pid=explorer&chrome=true&srcid=0BwhCYaYDn8EgMjdlMWIzNGUtZTQ0NC00ZjQ5LTkwYzQtZjRhMDRlNTQ3ZGMz&hl=en)
    * Depend on abstractions, not on concretions.

2\. A single file should only contribute types to a single namespace. Avoid having multiple namespaces in the same file.

3\. Avoid files with more than 500 lines (excluding machine-generated code).

4\. Avoid methods with more than 25 lines.

5\. Avoid methods with more than 5 arguments. Use structures for passing multiple arguments.

6\.Lines should not exceed 80 characters.

7\. Do not manually edit any machine generated code.
* If modifying machine generated code, modify the format and style to match this coding standard.
* Use partial classes whenever possible to factor out the maintained portions (i.e. Entity Framework generated class files).

8\. Avoid comments that explain the obvious.
* Code should be self explanatory. Good code with readable variable and method names should not require comments.

9\. Document only operational assumptions, algorithm insights and so on.

10\. Avoid method-level documentation, unless developing library methods which will be reused by other developers.

11\. Never hard-code a numeric value, always declare a constant instead.

12\. Avoid using manual string concatenation, instead favour ```string.Format``` or ```string.Concat```:
```csharp
var string1 = "Hello";
var string2 = "World!";

// Avoid:
var myGreeting = string1 + " " + string2;

// Correct:
var myGreeting = string.Format("{0} {1}", string1, string2)

// From C# 6.0 the following is also valid:
var myGreeting = $"{string1} {string2}"
```
13\. Use the **const** directive only on natural constants such as the number of days of the week.

14\. Avoid using const on read-only variables. For that, use the **readonly** directive.
```csharp
public class MyClass
{
    public readonly int Number;
    public MyClass(int someValue)
    {
        Number = someValue;
    }
    public const int DaysInWeek = 7;
}
```
15\. In general, prefer overloading to default parameters:
```csharp
// Avoid:
class MyClass
{
    void MyMethod(int number = 123)
    {...}
}

// Correct:
class MyClass
{
    void MyMethod()
    {
        MyMethod(123);
    }

    void MyMethod(int number)
    {...}
}
```
16\. When using default parameters, restrict them to natural immutable constants such as ```null```, ```false``` or ```0```;
```csharp
void MyMethod(int number = 0)
{...}
void MyMethod(string name = null)
{...}
void MyMethod(bool flag = false)
{...}
```

17\. Only catch exceptions for which you have explicit handling.

18\. In a **catch** statement that throws an exception, always throw the original exception to maintain stack location of original error.
```csharp
catch (Exception ex)
{
    MessageBox.Show(exception.Message)
    throw; // same as throw exception
}
```

19\. Avoid error code as method return values.

20\. When defining custom exceptions:
* Derive the custom exception from **ApplicationException**.
* Provide custom serialization

21\. Make only the most necessary types public, mark others as private, protected or internal.

22\. Avoid code that relies on an assembly running from a particular location.

23\. Minimise code in application assemblies (EXE client assemblies). Use class libraries instead to contain business logic.

24\. Avoid providing explicit values for enums, unless creating a bitwise enumeration.
```csharp
// Correct
public enum Color
{
    Red,
    Green,
    Blue
}

// Avoid
public enum Color
{
    Red = 1,
    Green = 2,
    Blue = 3
}
```

25\. Always use a curly brace scope in an **if** statement, even if conditions a single statement.

26\. Always use zero based arrays

27\. Do not provide public or protected member variables. Use **properties** instead.

28\. Avoid explicit properties that do nothing except access a member variable. Use automatic properties instead:
```csharp
// Avoid:
class MyClass
{
    int _number;

    public int Number
    {
        get { return _number; }
        set { _number = value; }
    }
}

// Correct:
class MyClass
{
    public int Number { get; set; }
}
```

29\. Avoid explicit casting. Use the **as** operator to defensively cast to a type.
```csharp
Dog dog = new GermanShepherd();
GermanShepherd shepherd = dog as GermanShepherd;
if (shepherd != null)
{...}
```

30\. Always use interfaces:
* Avoid having interfaces with one member.
* Strive to have 3-5 members per interface.
* No more than 20 members per interface - 12 is probably a practical limit.

31\. Avoid abstract methods, use interfaces instead

32\. Never assume a type supports an interface. Defensively query for that interface.
```csharp
SomeType obj1;
IMyInterface obj2;

/* Some code to initialize obj1, then: */
obj2 = obj1 as IMyInterface;
if (obj2 != null)
{
    obj2.Method1();
}
else
{
    // Handle error in expected interface
}
```

33\. Never hardcode strings that will be presented to the end users. Use resources instead.

34\. Never hardcode strings that might change based on deployment such as connection strings.

35\. Use ```string.Empty``` instead of "":
```csharp
// Avoid:
string name = "";

// Correct:
string name = string.Emtpy;
```

36\. When building a long string, use ```StringBuilder```, not ```string```.

37\. Use application logging and tracing wherever possible. Third party frameworks such as **log4net** can be used to assist with this.

38\. Do not use the **this** reference unless invoking another constructor from within a constructor.
```csharp
// Example of proper use of 'this'
public class MyClass
{
    public MyClass(string message)
    {}
    public MyClass() 
        : this("hello")
}
```

39\. Do not use the **base** word to access base class members unless you wish to resolve 
a conflict with a subclasses members of the same name or when invoking a base class constructor.
```csharp
// Example of proper use of 'base'
public class Dog
{
    public Dog(string name)
    {}
    virtual public void Bark(int howLong)
    {}
}
public class GermanShepherd : Dog
{
    public GermanShepherd(string name) 
        : base(name)
    {}
    override public void Bark(int howLong)
    {
        base.Bark(howLong);
    }
}
```

40\. Always dispose of unmanaged resources such as database connections by calling the ```Dispose()``` and ```Finalize()``` 
methods or by wrapping the code in a ```using``` statement.
```csharp
using (var db = new DbConnection("connectionString"))
{
    db.GetRecord(1);
}
```

41\. Avoid casting to and from ```System.Object``` in code that uses generics. Use constraints or the **as** operator instead:
```csharp
class SomeClass
{}

// Avoid:
class MyClass<T>
{
    void SomeMethod(T t)
    {
        object temp = t;
        SomeClass obj = (SomeClass) temp;
    }
}

// Correct:
class MyClass<T> where T : SomeClass
{
    void SomeMethod(T t)
    {
        SomeClass obj = t;
    }
}
```

42\. Do not define constraints in generic interfaces. Interface level constracts can often be replaced by strong typing:
```csharp
public class Customer
{...}

// Avoid:
public interface IList<T> where T : Customer
{...}

// Correct:
public interface ICustomerList : IList<Customer>
{...}
```

43\. If a class or a method offers both generic and non generic flavours, always prefer using the generics flavour.

44\. Only use ```var``` when the right side of the assignment clearly indicates the type of the variable:
```csharp
//Avoid:
var myVariable = DoSomething();

// Correct:
var name = EmployeeName;
```

45\. Do not assign method return types or complex expressions int a ```var``` variable, with the exception of LINQ projections that result in anonymous types.

## References
This document cites references from the following source(s):

- Lowy, Juval, (July 2011). "C# Coding Standard: Guidelines and Best Practices." (Version 2.4) www.idesign.net, &copy; 2011 IDesign Inc.
