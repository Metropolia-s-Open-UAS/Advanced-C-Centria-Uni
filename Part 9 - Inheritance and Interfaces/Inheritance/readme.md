#### Inheritance
- [ ]  `Classes` are used to clarify the concepts of the problem domain in object-oriented programming.
- [ ]  Every class we create adds functionality to the programming language.
- [ ]  This functionality is needed to solve the problems that we encounter.
> An essential idea behind object-oriented programming is that **solutions rise from the interactions between objects which are created from classes.**
- [ ] An object in object-oriented programming is an independent unit that has a state, which can be modified by using the methods that the object provides.
- [ ]  Objects are used in cooperation; each has its own area of responsibility.
- Every C# class extends the class **Object**, which means that every class we create has at their disposal all the methods defined in the Object class.
-  If we want to change how these methods defined in Object function, they must be overriden by defining a new implementation for them in the newly created class.
> The **objects** we create receive methods **Equals** and **GetHashCode**, among others, from the **Object** class.
- Ever class derives from Object, but it's also possible to defire from other classes than that.If we examine the API (Application Programming Interface) of C#'s Int32 (or integer, as we know it), we notice that Int32 has base class called ValueType. ValueType, in turn, has the class Object as its base class.
```text
Inheritance
Object --> ValueType --> Int32
```
   1. Each class can directly extend only one class.
   2. However, a class indirectly inherits all the properties of the class it extends.
   3. So the `Int32` class derives from the class `ValueType`, and indirectly derives from the class `Object`.
   4. So `Int32` has at its disposal variables and methods of the classes `ValueType` and `Object`.
> We use the `:` (or colon) notation to inherit a class The class that receives the properties is called the **derived class**, and the class whole properties are inherited is called the **base class**.
- Let's take a look at a car manufacturing system that manages car parts. A basic component of part management is the class Part, which defines the identifier, the manufacturer, and the description.
```csharp
namespace Exercise001
{
  public class Part
  {

    public string identifier { get; }
    public string manufacturer { get; }
    public string description { get; }

    public Part(string identifier, string manufacturer, string description)
    {
      this.identifier = identifier;
      this.manufacturer = manufacturer;
      this.description = description;
    }
  }
}
```
- One part of the car is the engine. As is the case with all parts, the engine, too, has a manufacturer, an identifier, and a description. In addition each engine has a type: for instance, an internal combustion engine, an electric motor, or a hybrid engine.
- The traditional way to implement the class Engine,**without using inheritance**, would be this.
```csharp
namespace Exercise001
{
  public class Engine
  {
    public string engineType { get; }
    public string identifier { get; }
    public string manufacturer { get; }
    public string description { get; }

    public Engine(string engineType, string identifier, string manufacturer, string description)
    {
      this.engineType = engineType;
      this.identifier = identifier;
      this.manufacturer = manufacturer;
      this.description = description;
    }
  }
}
```
- [ ] We notice a significant amount of overlap between the contents of Engine and Part.
- [ ] It can confidently be said the `Engine` is a special case of `Part`.
- [ ] `Engine` is `Part`, but it also has properties that a Part does not have, which in this case means the engine type.
> Let's recreate the class Engine, and this time use inheritance in our implementation. We'll create the class Engine which inherits the class Part: an engine is a special case of a part.
```csharp
namespace Exercise001
{
  public class Engine : Part
  {
    public string engineType { get; }

    public Engine(string engineType, string identifier, string manufacturer, string description) : 
      base(identifier, manufacturer, description)
    {
      this.engineType = engineType;
    }
  }
}
```
- The class definition `public class Engine : Part` indicates that the class `Engine` inherits the functionality of the class `Part`. We also define an object variable engineType in the class Engine.
- The constructor of the Engine class is worth some interest. On its declaration line we use the keyword base to call the constructor of the baseclass.
>  The call `base(identifier, manufacturer, description)` calls the constructor `public Part(string identifier, string manufacturer, string description)` which is defined in the class Part. Through this process the object variables defined in the base class are initiated with their initial values. After calling the base call's constuctor, in the code block of the Engine constructor we set the proper value for the object variable engineType.
#### Note
- The base call bears some resemblance to the this call in a constructor (i.e. when overloading a constructor); this is used to call a constructor of this class, while base is used to call a constructor of the base class. If a constructor uses the constructor of the base class, so base is called in it, the base call must be on the definition line of the constructor. This is similar to the case with calling this (must also be the definition line of the constructor).
- Since the class Engine extends the class Part, it has at its disposal all the methods that the class Part offers. You can create instances of the class Engine the same way you can of any other class.
```csharp
static void Main(string[] args)
{
  Engine engine = new Engine("combustion", "hz", "volkswagen", "VW GOLF 1L 86-91");
  Console.WriteLine(engine.engineType);
  Console.WriteLine(engine.identifier);
  Console.WriteLine(engine.manufacturer);
  Console.WriteLine(engine.description);
}
```
```text
combustion
hz
volkswagen
VW GOLF 1L 86-91
```
- As you can see, the class `Engine` has all the methods that are defined in the class `Part`.

