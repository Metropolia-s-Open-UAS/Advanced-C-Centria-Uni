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
    return this.name == comparedBook.name && this.published == comparedBook.published && this.content == comparedBook.content;
  }
}
```










