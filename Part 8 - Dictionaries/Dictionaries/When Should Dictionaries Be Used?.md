#### When Should Dictionaries Be Used?
- The dictionary is implemented in such a way that searching by a key is very fast.
- The dictionary generates a `"hash value"` from the key, i.e., a piece of code, which is used to store the value a specific location.
- When a key is used to retrieve information from a dictionary, this particular code identifies the location where the `value` associated with the `key` is.
- In practice, it's not necessary to go through all the key-value pairs in the dictionary when searching for a key; the set that's checked is significantly smaller.
> Consider the library example that was introduced above. The whole program could just as well have been implemented using a list. In that case, the books would be placed on the list instead of the directory, and the book search would happen by iterating over the list.

> In the example below, the books have been stored in a list and searching for them is done by going through the list.
```csharp
List<Book> books = new List<Book>();
Book senseAndSensibility = new Book("Sense and Sensibility", 1811, "...");
Book prideAndPrejudice = new Book("Pride and Prejudice", 1813, "....");
books.Add(senseAndSensibility);
books.Add(prideAndPrejudice);

// searching for a book named Persuasion
foreach (Book book in books)
{
  if (book.name == "Persuation")
  {
    Console.WriteLine(book);
    break;
  }
}

Console.WriteLine();
// searching for a book named Sense and Sensibility
foreach (Book book in books)
{
  if (book.name == "Sense and Sensibility")
  {
    Console.WriteLine(book);
    break;
  }
}
``` 
```text
Name: Sense and Sensibility (1811)
Content: ...
```
- Now the program works quite the same as our Dictionary version, right?
- Functionally, yes. Let's however, consider the performance of the program. C#'s DateTime() has property Ticks, which represents the given date and time of a DateTime instance. A Tick is one hundred nanoseconds.



