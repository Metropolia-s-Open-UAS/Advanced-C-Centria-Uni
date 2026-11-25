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
- The Location method is not meant for external use, which is why it is defined as protected. Derived classes will still be able to access the method.
- Manhattan distance means the distance between two points if you can only travel in the direction of the coordinate axes. It is used in many navigation algorithms, for example.
> A colored point is otherwise identical to a point, but it contains also a color that expressed as a string. Due to the similarity, we can create a new class by extending the class Point.
```csharp
namespace Exercise001
{
  public class ColorPoint : Point
  {

    private string color;

    public ColorPoint(int x, int y, string color) : base(x, y)
    {
      this.color = color;
    }

    public override string ToString()
    {
      return base.ToString() + " color: " + color;
    }
  }
}
```
- The `class` defines an object variable in which we store the color. The coordinates are already defined in the base class. We want the string representation to be the same as with points, but to also include information about the color. The overriden ToString method calls the ToString method of the base class, and adds to it the color of the point.
- Next we'll add a few points to a list. Some of them are "normal" while others are color points. At the end of the example we'll print the points on the list. For each point, the ToString to be executed is determined by the actual type of the point, even though the list knows all the points by the Point type.
```csharp
static void Main(string[] args)
{
  List<Point> points = new List<Point>();
  points.Add(new Point(4, 8));
  points.Add(new ColorPoint(1, 1, "green"));
  points.Add(new ColorPoint(2, 5, "blue"));
  points.Add(new Point(0, 0));

  foreach (Point p in points)
  {
    Console.WriteLine(p);
  }
}
```
```text
(4, 8) distance 12
(1, 1) distance 2 color: green
(2, 5) distance 7 color: blue
(0, 0) distance 0
```
- We also want to include a three-dimensional point in our program. Since it has no color information, let's derive it from the class **Point**.
```csharp
namespace Exercise001
{
  using System;
  public class Point3D : Point
  {

    private int z;

    public Point3D(int x, int y, int z) : base(x, y)
    {
      this.z = z;
    }
    new protected string Location()
    {
      return base.Location() + ", " + z;    // the resulting string has the form "x, y, z"
    }
    new public int ManhattanDistanceFromOrigin()
    {
      // first ask the base for the distance based on x and y
      // and add the effect of the z coordinate to that result
      return base.ManhattanDistanceFromOrigin() + Math.Abs(z);
    }

    public override string ToString()
    {
      return "(" + this.Location() + ") distance " + this.ManhattanDistanceFromOrigin();
    }
  }
}
```
> In our methods Location and ManhattanDistanceFromOrigin we use the keyword **new**, because we are overriding the methods from the **base** class. Without the keyword, we would get a warning.
```csharp
static void Main(string[] args)
{
  List<Point> points = new List<Point>();
  points.Add(new Point(4, 8));
  points.Add(new ColorPoint(1, 1, "green"));
  points.Add(new ColorPoint(2, 5, "blue"));
  points.Add(new Point3D(5, 2, 8));
  points.Add(new Point(0, 0));

  foreach (Point p in points)
  {
    Console.WriteLine(p);
  }
}
```
```text
(4, 8) distance 12
(1, 1) distance 2 color: green
(2, 5) distance 7 color: blue
(5, 2, 8) distance 15
(0, 0) distance 0
```
- We notice that the `ToString` method in **Point3D** is exactly the same as the **ToString** of **Point**. Could we save some effort and not override ToString? The answer happens to be yes! The Point3D class is refined into this:
```csharp
namespace Exercise001
{
  using System;
  public class Point3D : Point
  {

    private int z;

    public Point3D(int x, int y, int z) : base(x, y)
    {
      this.z = z;
    }
    new protected string Location()
    {
      return base.Location() + ", " + z;    // the resulting string has the form "x, y, z"
    }
    new public int ManhattanDistanceFromOrigin()
    {
      return base.ManhattanDistanceFromOrigin() + Math.Abs(z);
    }
  }
}
```
- What happens in detail when we call the `ToString` method of a **three-dimensional point**? The execution advances in the following manner.
  1. Look for a definition of `ToString` in the class **Point3D**. It does not exist, so the base class is next to be examined.
  2. Look for a definition of `ToString` in the base class **point**. It can be found, so the code inside the implementation of the method is executed
    - so the exact code to be executed is return `"("+this.Location()+") distance " + this.ManhattanDistanceFromOrigin();`
    - the method Location is executed first
    - look for a definition of Location in the class `Point3D`. It can be found, so its code is executed.
    - This location calls the Location of the base class to calculate the result
    - next we look for a definition of **ManhattanDistanceFromOrigin** in the **Point3D** class. It's found and its code is then executed
    - Again, the method calls the similarly named method of the base class during its execution
> As we can see, the sequence of events caused by the method call has multiple steps. The principle, however, is clear: The definition for the method is first searched for in the class definition of the actual type of the object. If it is not found, we next examine the base class. If the definition cannot be found there, either, we move on to the base class of this base class, etc...






