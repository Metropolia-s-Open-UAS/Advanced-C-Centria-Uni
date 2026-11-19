#### Going Through A Dictionary's Keys
- We may sometimes want to search for a book by a part of it's title. The `get method (dictionary[key])` in the dictionary is not applicable in this case as it's used to search by a specific key. Searching by a part of a book title is not possible with it.
- We can go through the values ​​of a dictionary by using a `for-each` loop on the `KeyCollection` returned by the Keys property of the dictionary.
- Below, a search is performed for all the books whose names contain the given string.
```csharp
public List<Book> GetBooksByPart(string titlePart)
{
  List<Book> books = new List<Book>();
  titlePart = SanitizedString(titlePart);
  Dictionary<string, Book>.KeyCollection keys = this.directory.Keys;

  foreach (string bookTitle in keys)
  {
    if (bookTitle.Contains(titlePart))
    {
      books.Add(this.directory[bookTitle]);
    }
  }
  return books;
}
```
- This way, however, we lose the speed advantage that comes with the dictionary. The dictionary is implemented in such a way that searching by a single key is extremely fast. The example above goes through all the book titles when looking for the existence of a single book using a particular key.



