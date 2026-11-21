#### Creating our first program
- We have tried our hands with the very basic `dotnet` command, mainly the `dotnet run` to try how our exercises work locally.
- The command in question is part of the `dotnet` program we installed as a prerequisite for the basic course.
- The program has, of course, other commands available. We are going to use `dotnet new` to create our own program at this point.
> Note!
The instructions are written with Visual Studio Code in mind, as we use that for our exercises.

  1. Start Visual Studio Code
  2. Select File > Open Folder from the main menu
  3. In the Open Folder dialog, create a HelloWorld folder and select it
- The folder name becomes the project name and the namespace name by default. You'll add code later in the tutorial that assumes the project namespace is HelloWorld.

  4. Open the Terminal in Visual Studio Code, and make sure you are in the correct folder (the one just created).
  5. In the terminal, enter the following command:
```cmd
dotnet new console
```
- When using dotnet 6.0 the template is quite simple, only containing the Console.WriteLine(String) method to display "Hello World!" in the console window.
```cmd
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```
- [ ] In practice (and in older versions of dotnet), the template is something like the following:
- [ ] The template creates a simple "Hello World" application. It calls the `Console.WriteLine(String)` method to display "Hello World!" in the console window.
- [ ] The template code defines a class, Program, with a single method, Main, that takes a String array as an argument:
```csharp
namespace HelloWorld
{
    using System;

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
- Main is the application entry point, the method that's called automatically by the runtime when it launches the application.
- Any command-line arguments supplied when the application is launched are available in the args array.
- To run the application, use the familiar `dotnet` run command.





