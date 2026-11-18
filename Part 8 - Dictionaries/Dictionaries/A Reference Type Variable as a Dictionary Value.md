#### A Reference Type Variable as a Dictionary Value
- [ ] Let's take a look at how a spreadsheet works using a library example.
- [ ] You can search for books by book title. If a book is found with the given search term, the library returns a **reference** to the book.
- [ ] Let's begin by creating an example class Book that has its name, content and the year of publication as instance variables.
```csharp
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

  public override string ToString()
  {
    return "Name: " + this.name + " (" + this.published + ")\n"
        + "Content: " + this.content;
  }
}
```
Let's create a dictionary that uses the book's name as a key, i.e., a string-type object, and the book we've just created as the value.
```csharp
Dictionary<string, Book> directory = new Dictionary<string, Book>();
```
The dictionary above uses string as a key. Let's expand the example so that two books are added to the dictionary, "Sense and Sensibility" and "Pride and Predujice".
```csharp
Book senseAndSensibility = new Book("Sense and Sensibility", 1811, "...");
Book prideAndPredujice = new Book("Pride and Prejudice", 1813, "....");

Dictionary<string, Book> directory = new Dictionary<string, Book>();
directory.Add(senseAndSensibility.name, senseAndSensibility);
directory.Add(prideAndPredujice.name, prideAndPredujice);
```
Books can be retrieved from the directory by book name. A search for "Persuasion" will not produce any results, in which case the dictionary gives an error. The book "Pride and Prejudice" is found, however. Let's play it safe, and put both inside an if:
```csharp
if (directory.ContainsKey("Persuation"))
{
  Console.WriteLine(directory["Persuasion"]);
}
else
{
  Console.WriteLine("Book not found!");
}

Console.WriteLine();
if (directory.ContainsKey("Pride and Prejudice"))
{
  Console.WriteLine(directory["Pride and Prejudice"]);
}
```
```text
Book not found!

Name: Pride and Prejudice (1813)
Content: ....
```
