#### Testing the sample
- [ ] The NewTypes project is in place, and you've organized it by keeping the pets-related types in a folder.
- [ ] Next, create your test project and start writing tests with the **xUnit** test framework.
- [ ] `Unit testing` allows you to automatically check the behavior of your pet types to confirm that they're operating properly.

- Navigate back to the src folder and create a test folder with a NewTypesTests folder within it. At a command prompt from the NewTypesTests folder, execute dotnet new xunit. This command produces two files: `NewTypesTests.csproj` and `UnitTest1.cs`.
- The test project can't currently test the types in NewTypes and requires a project reference to the NewTypes project. To add a project reference, use the dotnet reference add command:
```.NET CLI
dotnet reference add ../../src/NewTypes/NewTypes.csproj
```
Or, you also have the option of manually adding the project reference by adding an `<ItemGroup>` node to the NewTypesTests.csproj file:
```xml
<ItemGroup>
  <ProjectReference Include="../../src/NewTypes/NewTypes.csproj" />
</ItemGroup>
```
NewTypesTests.csproj:
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net11.0</TargetFramework>
    <Nullable>enable</Nullable>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="18.11.0" />
    <PackageReference Include="xunit" Version="2.9.3" />
    <PackageReference Include="xunit.runner.visualstudio" Version="4.0.1" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="../../src/NewTypes/NewTypes.csproj"/>
  </ItemGroup>

</Project>
```
The `NewTypesTests.csproj` file contains the following package references:

   1. `Microsoft.NET.Test.Sdk`, the .NET testing infrastructure
   2. `xunit`, the xUnit testing framework
   3. `xunit.runner.visualstudio`, the test runner
   4. `NewTypes`, the code to test
Change the name of `UnitTest1.cs` to `PetTests.cs` and replace the code in the file with the following code:
```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }

    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }
}
```
> Although you expect that the `expected` and `actual` values are equal, an initial assertion with the Assert.NotEqual check specifies that these values are not equal. **Always initially create a test to fail** in order to check the logic of the test. After you confirm that the test fails, adjust the assertion to allow the test to pass.
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
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```
> Change the assertions of your tests from `Assert.NotEqual` to `Assert.Equal`:
```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();

        Assert.Equal(expected, actual);
    }

    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();

        Assert.Equal(expected, actual);
    }
}
```




