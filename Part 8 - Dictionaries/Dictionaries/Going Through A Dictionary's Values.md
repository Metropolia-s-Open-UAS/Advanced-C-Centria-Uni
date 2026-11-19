#### Going Through A Dictionary's Values
- The preceding functionality could also be implemented by going through the dictionary's values. The set of values can be retrieved with the `dictionary's Values​​()` property. This set of values can also be iterated ober ​​with a for-each loop.
```csharp
public List<Book> GetBooksByPart(string titlePart)
{
  List<Book> books = new List<Book>();
  titlePart = SanitizedString(titlePart);
  Dictionary<string, Book>.ValueCollection values = this.directory.Values;

  foreach (Book book in values)
  {
    if (book.name.Contains(titlePart))
    {
      books.Add(book);
    }
  }
  return books;
}
```
> As with the previous example, the speed advantage that comes with the dictionary is lost.

