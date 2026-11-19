#### Dictionary as an Instance Variable
- [ ] The example considered above on storing books is problematic in that the book's spelling format must be remembered accurately.
- [ ]  Someone may search for a book with a lowercase letter, another may, for example, enter a space to begin typing a name.
- [ ]  Let's take a look at a slightly more forgiving search by book title.
- We make use of the tools provided by the string-class to handle strings. The `ToLower()` method creates a new string with all letters converted to lowercase.
- The `Trim()` method, on the other hand, creates a new string where empty characters such as spaces at the beginning and end have been removed.
```csharp
string text = "Pride and Prejudice     ";
text = text.ToLower(); // text currently "pride and prejudice     "
text = text.Trim(); // text now "pride and prejudice"
```
- The conversion of the string described above will result in the book being found, even if the user happens to type the title of the book with lower-case letters.
- Let's create a Library class that encapsulates a dictionary containing books, and enables you to case-independent search for books.
- We'll add methods for adding, retrieving and deleting to the Library class. Each of these is based on a sanitized name - this involves converting the name to lowercase and removing extrenous spaces from the beginning and end.
> Let's first outline the method for adding. The book is added to the dictionary with the book name as the key and the book itself as the value. Since we want to allow for minor misspellings, such as capitalized or lower-cased strings, or ones with spaces at the beginning and/or end, the key - the title of the book - is converted to lowercase, and spaces at the beginning and end are removed.
```csharp
public class Library
{
  private Dictionary<string, Book> directory;

  public Library()
  {
    this.directory = new Dictionary<string, Book>();
  }

  public void AddBook(Book book)
  {
    string name = book.name;
    if (name == null)
    {
      name = "";
    }

    name = name.ToLower();
    name = name.Trim();

    if (this.directory.ContainsKey(name))
    {
      Console.WriteLine("Book is already in the library!");
    }
    else
    {
      directory.Add(name, book);
    }
  }
}
```
- The **ContainsKey** method of the directory is being used above to check for the existence of a key. The method returns true if any value has been added to the directory with the given key. Otherwise, the method returns false.
- We can already see that code dealing with string sanitizion is needed in every method that handles a book, which makes it a good candiate for a separate helper method. The method is implemented as a class method since it doesn't handle object variables.
```csharp
public static string SanitizedString(string input)
{
  if (input == null)
  {
    return "";
  }

  input = input.ToLower();
  return input.Trim();
}
```
- The implementation is much neater when the helper method is used.
```csharp
using System;
using System.Collections.Generic;

namespace Exercise001
{
  public class Library
  {
    private Dictionary<string, Book> directory;

    public Library()
    {
      this.directory = new Dictionary<string, Book>();
    }

    public void AddBook(Book book)
    {
      string name = SanitizedString(book.name);

      if (this.directory.ContainsKey(name))
      {
        Console.WriteLine("Book is already in the library!");
      }
      else
      {
        directory.Add(name, book);
      }
    }

    public Book GetBook(string bookTitle)
    {
      bookTitle = SanitizedString(bookTitle);
      if (this.directory.ContainsKey(bookTitle))
      {
        return this.directory[bookTitle];
      }
      else
      {
        return null;
      }
    }

    public void RemoveBook(string bookTitle)
    {
      bookTitle = SanitizedString(bookTitle);

      if (this.directory.ContainsKey(bookTitle))
      {
        this.directory.Remove(bookTitle);
      }
      else
      {
        Console.WriteLine("Book was not found, cannot be removed!");
      }
    }


    public static string SanitizedString(string input)
    {
      if (input == null)
      {
        return "";
      }

      input = input.ToLower();
      return input.Trim();
    }
  }
}
```
- Let's see this in action
```csharp
Book senseAndSensibility = new Book("Sense and Sensibility", 1811, "...");
Book prideAndPredujice = new Book("Pride and Prejudice", 1813, "....");

Library library = new Library();
library.AddBook(senseAndSensibility);
library.AddBook(prideAndPredujice);

Console.WriteLine(library.GetBook("pride and prejudice"));
Console.WriteLine();

Console.WriteLine(library.GetBook("PRIDE AND PREJUDICE"));
Console.WriteLine();

Console.WriteLine(library.GetBook("SENSE"));
```
```text
Name: Pride and Prejudice (1813)
Content: ....

Name: Pride and Prejudice (1813)
Content: ....
```
> In the above example, we adhered to the **DRY (Don't Repeat Yourself)** principle according to which code duplication should be avoided. **Sanitizing a string**, i.e., changing it to lowercase, and trimming, i.e., removing empty characters from the beginning and end, would have been repeated many times in our library class without the SanitizedString method. Repetitive code is often not noticed until it has already been written, which means that it almost always makes it's way into the code. There's nothing wrong with that - the important thing is that the code is cleaned up so that places that require tidying up are noticed.



