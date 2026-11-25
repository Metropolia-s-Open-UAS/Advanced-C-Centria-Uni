#### Calling a base class method
- You can call the methods defined in the base class by prefixing the call with `base`,
-  just as you can call the methods defined in this class by prefixing the call with this.
> For example, when overriding the ToString method, you can call the base class's definition of that method in the following manner:
```csharp
public override string ToString()
{
  return "override: " + base.ToString();
}
```
- This would make our previous example print look like this:
```text
Example
override: Derived Class
```
