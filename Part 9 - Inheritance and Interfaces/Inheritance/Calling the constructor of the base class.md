#### Calling the constructor of the base class
- You use the keyword `base` to call the constructor of the base class. The call receives as parameters the types of values that the base class constructor requires. If there are multiple constructors in the base class, the parameters of the base call dictate which of them is used.
- When the `constructor` (of the derived class) is called, the variables defined in the base class are initialized. The events that occur during the constructor call are practically identical to what happens with a normal constructor call. If the base class doesn't provide a non-parameterized constructor, there must always be an explicit call to the constructor of the base class in the constructors of the derived class.
- We demonstrate in the example below how to call this and base. The class **Baseclass** includes an object variable and two constructors. One of them calls the other constructor with the `this` keyword. The class **DerivedClass** includes a parameterized constructor, but it has no object variables. The constructor of DerivedClass calls the parameterized constructor of the base class.
```csharp
namespace Exercise001
{
  public class BaseClass
  {
    private string objectVariable;

    public BaseClass() : this("Example")
    {
    }

    public BaseClass(string value)
    {
      this.objectVariable = value;
    }

    public override string ToString()
    {
      return this.objectVariable;
    }
  }
}
```
```csharp
namespace Exercise001
{
  public class DerivedClass : BaseClass
  {
    public DerivedClass() : base("Derived Class")
    {
    }
  }
}
```
```csharp
BaseClass bas = new BaseClass();
DerivedClass der = new DerivedClass();

Console.WriteLine(bas);
Console.WriteLine(der);
```
```text
Example
Derived Class
```










