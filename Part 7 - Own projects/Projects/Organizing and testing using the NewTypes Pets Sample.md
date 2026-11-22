#### Organizing and testing using the NewTypes Pets Sample
##### Using folders to organize code
-  If you want to introduce new types into a console app, you can do so by adding files containing the types to the app. For example, if you add files containing `AccountInformation` and `MonthlyReportRecords` types to your project, the project file structure is flat and easy to navigate:
```text
/MyProject
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```
> However, this flat structure only works well when the size of your project is relatively small. Can you imagine what happens if you add 20 types to the project? The project definitely wouldn't be easy to navigate and maintain with that many files littering the project's root directory.

- To organize the project, create a new folder and name it **Models** to hold the type files. Place the **type** files into the **Models** folder:
```text
/MyProject
|__/Models
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```
- Projects that logically group files into folders are easy to navigate and maintain.
##### Projects that logically group files into folders are easy to navigate and maintain.
###### Building the sample
- The sample contains two types, `Dog` and `Cat`, and has them implement a common interface, `IPet`. For the NewTypes project, your goal is to organize the pet-related types into a Pets folder.
- If another set of types is added later, WildAnimals for example, they're placed in the NewTypes folder alongside the Pets folder.
- The WildAnimals folder may contain types for animals that aren't pets, such as `Squirrel` and `Rabbit` types. In this way as types are added, the project remains well organized.
```text
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
```
IPet.cs:
```csharp
using System;

namespace Pets
{
    public interface IPet
    {
        string TalkToOwner();
    }
}
```
Dog.cs:
```csharp
using System;

namespace Pets
{
    public class Dog : IPet
    {
        public string TalkToOwner() => "Woof!";
    }
}
```
Cat.cs:
```csharp
using System;

namespace Pets
{
    public class Cat : IPet
    {
        public string TalkToOwner() => "Meow!";
    }
}
```
Program.cs:
```csharp
using System;
using Pets;
using System.Collections.Generic;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            List<IPet> pets = new List<IPet>
            {
                new Dog(),
                new Cat()
            };

            foreach (var pet in pets)
            {
                Console.WriteLine(pet.TalkToOwner());
            }
        }
    }
}
```
NewTypes.csproj:
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net11.0</TargetFramework>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```
> Optional exercise: You can add a `new pet type`, such as a `Bird`, by extending this project. Make the bird's `TalkToOwner` method give a Tweet! to the owner. Run the app again. The output will include Tweet!
























