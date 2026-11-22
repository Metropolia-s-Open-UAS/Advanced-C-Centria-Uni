#### Method to Test For Equality - "Equals"
- [ ] The Equals method checks by default whether the object given as a parameter has the same reference as the object its being compared to.
- [ ]  In other words, the default behaviour checks whether the two objects are the same.
- [ ]  If the reference is the same, the method returns true, and false otherwise.
> This can be illustrated with the following example. The Book class does not have its own implementation of the Equals method, so it falls back on the default implementation provided by C#.
```csharp
Book bookObject = new Book("Book object", 2000, "...");
Book anotherBookObject = bookObject;

if (bookObject.Equals(anotherBookObject))
{
  Console.WriteLine("The books were the same");
}
else
{
  Console.WriteLine("The books weren't the same");
}

// we now create an object with the same content that's nonetheless its own object
anotherBookObject = new Book("Book object", 2000, "...");

if (bookObject.Equals(anotherBookObject))
{
  Console.WriteLine("The books were the same");
}
else
{
  Console.WriteLine("The books weren't the same");
}
```
```text
The books were the same
The books weren't the same
```
- [ ] The internal structure of the book objects (i.e., the values of their instance variables ) in the previous example is the same
- [ ] but only the first comparison prints "The books were the same".
- [ ] This is because the references are the same in the first case
- [ ] i.e., the object is compared to itself. The second comparison is about two different entities, even though the variables have the same values.

- [ ] If we want to compare our own classes using the Equals method, then it must be defined inside the class.
- [ ] The method created accepts an Object-type reference as a parameter, which can be any object.
  1. The comparison first looks at the references.
  2. This is followed by checking the parameter object's type with the instanceof operation
  3. if the object type does not match the type of our class
  4. **the object cannot be the same.**
> **We then create a version of the object that is of the same type as our class, after which the object variables are compared against each other.**
```csharp
public override bool Equals(object compared)
{
  // if the variables are located in the same position, they are equal
  if (this == compared)
  {
    return true;
  }

  // if the compared object is null or not of type Book, the objects are not equal
  if ((compared == null) || !this.GetType().Equals(compared.GetType()))
  {
    return false;
  }
  else
  {
    // convert the object to a Book object
    Book comparedBook = (Book)compared;

    // if the values of the object variables are equal, the objects are, too
    return this.name == comparedBook.name && this.published == comparedBook.published
    && this.content == comparedBook.content;
  }
}
```
The Book-class in it's entirety.
```csharp
namespace Exercise001
{
  public class Book
  {
    public string name { get; set; }
    public string content { get; set; }
    public int published { get; set; }

    public Book(string name, int published, string content)
    {
      this.name = name;
      this.published = published;
      this.content = content;
    }

    public override string Tostring()
    {
      return "Name: " + this.name + " (" + this.published + ")\n"
          + "Content: " + this.content;
    }

    public override bool Equals(object compared)
    {
      // if the variables are located in the same position, they are equal
      if (this == compared)
      {
        return true;
      }

      // if the compared object is null or not of type Book, the objects are not equal
      if ((compared == null) || !this.GetType().Equals(compared.GetType()))
      {
        return false;
      }
      else
      {
        // convert the object to a Book object
        Book comparedBook = (Book)compared;

        // if the values of the object variables are equal, the objects are, too
        return this.name == comparedBook.name && this.published == comparedBook.published
        && this.content == comparedBook.content;
      }
    }
  }
}
```
Now the book comparison returns true if the instance variables of the books are the same.
```csharp
Book bookObject = new Book("Book object", 2000, "...");
Book anotherBookObject = new Book("Book object", 2000, "...");

if (bookObject.Equals(anotherBookObject))
{
  Console.WriteLine("The books were the same");
}
else
{
  Console.WriteLine("The books weren't the same");
}
```
```cmd
Book.cs(3,16): warning CS0659: 'Book' overrides Object.Equals(object o) but does not override Object.GetHashCode() [/mnt/c/Users/HeikkiHei/Documents/coding-exercises/Exercise001/Exercise001.csproj
The books were the same
```
- We also get the very familiar warning. Finally in this section, we will do something about it.
> The List also uses the Equals method in its internal implementation. If we don't define the Equals method in our objects, the contains method of the List does not work properly. If you try out the code below with two Book classes, one with the Equals method defined, and another without it, you'll see the difference.
```csharp
List<Book> books = new List<Book>();
Book bookObject = new Book("Book Object", 2000, "...");
books.Add(bookObject);

if (books.Contains(bookObject))
{
  Console.WriteLine("Book Object was found.");
}

bookObject = new Book("Book Object", 2000, "...");

if (!books.Contains(bookObject))
{
  Console.WriteLine("Book Object was not found.");
}
```
> This reliance on default methods such as Equals is actually the reason why C# demands that variables added to List and Dictionary are of reference type. Each reference type variable comes with default methods, such as Equals, which means that you don't need to change the internal implementation of the List class when adding variables of different types.











