#### The actual type of an object dictates which method is executed
- An `object's` type decides what the `methods` provided by the `object` are. Let's create a couple of examples for this.
```csharp
namespace Exercise001
{
  public class Person
  {
    public string name { get; set; }
    public string address { get; set; }

    public Person(string name, string address)
    {
      this.name = name;
      this.address = address;
    }

    public override string ToString()
    {
      return this.name + ", " + this.address;
    }
  }
}
```
```csharp
namespace Exercise001
{
  public class Student : Person
  {
    public int credits { get; set; }
    public Student(string name, string address) : base(name, address)
    {
      this.credits = 0;
    }

    public void Study()
    {
      this.credits++;
    }
  }
}
```
- If a `reference` to a Student type object is stored in a Person type variable, only the methods defined in the Person class (and its base class and interfaces) are available:
```csharp
Person ollie = new Student("Ollie", "6381 Hollywood Blvd. Los Angeles 90028");

Console.WriteLine(ollie.credits);       // DOESN'T WORK!
ollie.Study();              // DOESN'T WORK!
Console.WriteLine(ollie);   // ollie.ToString() WORKS
```
- [ ] We get an error for the first two calls to **ollie**.
- [ ] So an object has at its disposal the methods that relate to its type, and also to its base `classes` and `interfaces`.
- [ ] The Student object above offers the methods defined in the the classes Person and Object.
```csharp
public override string ToString()
{
  return base.ToString() + " credits: " + this.credits;
}
```
- The class Person had already overriden the ToString method it inherited from the class Object, and now we override the ToString from the Person class. If we handle an object by some other type than its actual type, which version of the object's method is called?
- In the following example, we'll have students that we refer to by variables of different types. Which version of the ToString method will be executed: the one defined in Objecct, Person, or Student?
```csharp
Student ollie = new Student("Ollie", "6381 Hollywood Blvd. Los Angeles 90028");
Console.WriteLine(ollie);
Person olliePerson = new Student("Ollie", "6381 Hollywood Blvd. Los Angeles 90028");
Console.WriteLine(olliePerson);
Object ollieObject = new Student("Ollie", "6381 Hollywood Blvd. Los Angeles 90028");
Console.WriteLine(ollieObject);

Object alice = new Student("Alice", "177 Stewart Ave. Farmington, ME 04938");
Console.WriteLine(alice);
```
```text
Ollie, 6381 Hollywood Blvd. Los Angeles 90028 credits: 0
Ollie, 6381 Hollywood Blvd. Los Angeles 90028 credits: 0
Ollie, 6381 Hollywood Blvd. Los Angeles 90028 credits: 0
Alice, 177 Stewart Ave. Farmington, ME 04938 credits: 0
```
> The `method` to be executed is chosen based on the actual type of the `object`, which means the class whose **constructor** is called when the object is created. If the method has no definition in that class, the version of the method is chosen from the class that is closest to the actual type in the inheritance hierarchy.

- Regardless of the type of the variable, the method that is executed is always chosen based on the actual type of the object. Objects are polymorphic, which means that they can be used via many different variable types. **The executed method always relates to the actual type of the object**. This phenomenon is called **polymorphism**.

1. Let's examine polymorphism with another example.
2. You could represent a point in two-dimensional coordinate system with the following class:
```csharp
namespace Exercise001
{
  using System;
  public class Point
  {

    private int x;
    private int y;

    public Point(int x, int y)
    {
      this.x = x;
      this.y = y;
    }

    public int ManhattanDistanceFromOrigin()
    {
      return Math.Abs(x) + Math.Abs(y);
    }

    protected string Location()
    {
      return x + ", " + y;
    }

    public override string ToString()
    {
      return "(" + this.Location() + ") distance " + this.ManhattanDistanceFromOrigin();
    }
  }
}
```


