#### Abstract classes
- Sometimes, when planning a hierarchy of inheritance, there are cases when there exists a clear concept, but that concept is not a good candidate for an object in itself.
- he concept would be beneficial from the point of view of inheritance, since it includes variables and functionality that are shared by all the classes that would inherit it.
- **On the other hand, you should not be able to create instances of the concept itself.**
> An **abstract class** combines **interfaces** and **inheritance**. You cannot create instances of them -- you can only create instances of derived classes of an abstract class.
- They can include normal methods which have a method body, but it's also possible to define **abstract** methods that only contain the method definition. Implementing the abstract methods is the responsibility of derived classes.
- Generally, **abstract classes** are used in situations where the concept that the class represents is **not a clear independent concept**. In such a case you **shouldn't be able to create instances of it**.
- [ ] To define an `abstract class` or an abstract method the keyword abstract is used.
- [ ] An **`abstract` class** is defined with the phrase `public abstract class NameOfClass`;
- [ ] an **`abstract` method** is defined by `public abstract returnType NameOfMethod`.
>  Let's take a look at the following **abstract** class called **Operation**, which offers a **structure for operations and executing them**.
```csharp
namespace Exercise001
{
  public abstract class Operation
  {

    public string name { get; }

    public Operation(string name)
    {
      this.name = name;
    }

    public abstract void Execute();
  }
}
```
- The **abstract** class Operation works as a basis for implementing different actions. For instance, you can implement the plus operation by extending the **Operation** class in the following manner.
```csharp
namespace Exercise001
{
  using System;
  public class PlusOperation : Operation
  {
    public PlusOperation() : base("PlusOperation")
    {
    }

    public override void Execute()
    {
      Console.Write("First number: ");
      int first = Convert.ToInt32(Console.ReadLine());
      Console.Write("Second number: ");
      int second = Convert.ToInt32(Console.ReadLine());

      Console.WriteLine("The sum of the numbers is " + (first + second));
    }
  }
}
```
- [ ] Since all the classes that inherit from Operation have also the type Operation
- [ ] we can create a user `interface` by using Operation type `variables`
- [ ]  Next we'll show the class **UserInterface** that contains a list of operations. It's possible to add operations to the **UI** dynamically.
```csharp
namespace Exercise001
{
  using System;
  using System.Collections.Generic;
  public class UserInterface
  {

    private List<Operation> operations;

    public UserInterface()
    {
      this.operations = new List<Operation>();
    }

    public void AddOperation(Operation operation)
    {
      this.operations.Add(operation);
    }

    public void Start()
    {
      while (true)
      {
        PrintOperations();
        Console.WriteLine("Choice: ");

        string choice = Console.ReadLine();
        if (choice == "0")
        {
          break;
        }

        ExecuteOperation(choice);
        Console.WriteLine();
      }
    }

    private void PrintOperations()
    {
      Console.WriteLine("\t0: Stop");
      int i = 0;
      while (i < this.operations.Count)
      {
        string operationName = this.operations[i].name;
        Console.WriteLine("\t" + (i + 1) + ": " + operationName);
        i = i + 1;
      }
    }

    private void ExecuteOperation(string choice)
    {
      int operation = Convert.ToInt32(choice);

      Operation chosen = this.operations[operation -1];
      chosen.Execute();
    }
  }
}
```
```csharp
UserInterface userInterface = new UserInterface();
userInterface.AddOperation(new PlusOperation());

userInterface.Start();
```
```cmd
0: Stop
        1: PlusOperation
Choice:
> 1
First number: 4
Second number: 5
The sum of the numbers is 9

        0: Stop
        1: PlusOperation
Choice:
> 0
```
> The greatest difference between `interfaces` and `abstract` classes is that `abstract` classes can contain object variables and constructors in addition to methods. Since you can also define functionality in abstract classes, you can use them to define e.g. default behavior. In the user interface above storing the name of the operation used the functionality defined in the abstract Operation class.

