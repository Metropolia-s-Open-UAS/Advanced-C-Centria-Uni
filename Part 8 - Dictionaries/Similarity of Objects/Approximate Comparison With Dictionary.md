#### Approximate Comparison With Dictionary
- In addition to `Equals`, the `GetHashCode` method can also be used for approximate comparison of **objects**. The method creates from the object a `"hash code"`, i.e, a number, that tells a bit about the object's content. If two `objects` have the same `hash value`, they may be `equal`. On the other hand, if two objects have different hash values, they are certainly unequal.
- `Hash codes` are used in `Dictionaries`, for instance. Dictionary's internal behavior is based on the fact that `key-value` pairs are stored in an array of lists based on the key's hash value. Each array index points to a list. The hash value identifies the array index, whereby the list located at the array index is traversed. The value associated with the key will be returned if, and only if, the exact same value is found in the list (equality comparison is done using the Equals method). This way, the search only needs to consider a fraction of the keys stored in the hash map.
- So far, we've only used `string` objects as `Dictionary` keys, which have conveniently had ready-made `GetHashCode` methods implemented. Let's create an example where this is not the case: we'll continue with the books and keep track of the books that are on loan. We'll implement the book keeping with a Dictionary. The key is the book and the value attached to the book is a string that tells the borrower's name:
```csharp
Dictionary<Book, string> borrowers = new Dictionary<Book, string>();

Book bookObject = new Book("Book Object", 2000, "...");
borrowers.Add(bookObject, "Pekka");
borrowers.Add(new Book("Test Driven Development", 1999, "..."), "Arto");

Console.WriteLine(borrowers[bookObject]);
Console.WriteLine(borrowers[new Book("Book Object", 2000, "...")]);
Console.WriteLine(borrowers[new Book("Test Driven Development", 1999, "...")]);
```
```cmd
Pekka
Unhandled exception. System.Collections.Generic.KeyNotFoundException: The given key 'Name: Book Object (2000) 
[. . .]
```
- We get an error, as the `object` created in the second `Console.WriteLine` does not match any key (neither does the third one, but the program quits on the first error).
> We find the `borrower` when searching for the same `object` that was given as a key to the dictionarys's Add method.
- [ ]  However, when searching by the exact same book but with a different object,a `borrower` isn't found, and we get the error instead.
- [ ]  The reason lies in the default implementation of the `GetHashCode` method in the Object class.
- [ ]  The default `implementation` creates a `HashCode` value based on the `object's reference`, which means that books having the same content that are nonetheless different objects get different results from the `GetHashCode` method.
- [ ]  As such, the `object` is not being searched for in the right place.
> For the Dictionary to work in the way we want it to, that is, to return the borrower when given an object with the correct content (not necessarily the same object as the original key), the class that's the key must overwrite the GetHashCode method in addition to the Equals method.
- The method must be overwritten so that it gives the same numerical result for all objects with the same content. Also, some objects with different contents may get the same result from the GetHashCode method. However, with the Dictionary's performance in mind, it is essential that objects with different contents get the same hash value as rarely as possible.
- We've previously used `string objects` as `Dictionary keys`, so we can deduce that the string class has a well-functioning `GetHashCode` implementation of its own. We'll `Delegate`, i.e., transfer the computational responsibility to the string object.
```csharp
public override int GetHashCode()
{
  return this.name.GetHashCode();
}
```
- The above solution is quite good. However, if name is `null`, we see a `NullReferenceException error`. Let'fix this by defining a condition: if the value of the name variable is null, we'll return the year of publication as the hash value.
```csharp
public override int GetHashCode()
{
  if (this.name == null)
  {
    return this.published;
  }
  return this.name.GetHashCode();
}
```
- Now, all of the books that share a name are bundleded into one group. Let's improve it further so that the year of publiciation is also taken into account in the hash value calculation that's based on the book title.
```csharp
public override int GetHashCode()
{
  if (this.name == null)
  {
    return this.published;
  }
  return this.published + this.name.GetHashCode();
}
```
- It's now possible to use the book as the hash map's key. This way the problem we faced earlier gets solved and the book borrowers are found:
```csharp
Dictionary<Book, string> borrowers = new Dictionary<Book, string>();

Book bookObject = new Book("Book Object", 2000, "...");
borrowers.Add(bookObject, "Pekka");
borrowers.Add(new Book("Test Driven Development", 1999, "..."), "Arto");

Console.WriteLine(borrowers[bookObject]);
Console.WriteLine(borrowers[new Book("Book Object", 2000, "...")]);
Console.WriteLine(borrowers[new Book("Test Driven Development", 1999, "...")]);
```
```cmd
Pekka
Pekka
Arto
```
> Let's revise the ideas once more: for a class to be used as a Dictionary's key, we need to define for it:
    1. method `Equals` , so that all equal or apporiximately `equal` objects cause the comparison to return true and all false for all the rest 
    2. method `GetHashCode` , so that as few `objects` as possible end up with the same hash value







