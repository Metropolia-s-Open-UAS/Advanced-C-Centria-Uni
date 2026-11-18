#### Dictionaries
- One of the most commonly used data structures among lists is a dictionary. In C#, the `Dictionary<TKey,TValue>` Class is located in the `System.Collections.Generic` Namespace. But what does it do?
> Data in dictionaries is stored as **key-value pairs**, where values can be added, retrieved, and deleted using keys.
- In the example below, a Dictionary object has been created to search for cities by their postal codes,after which four postal code-city pairs have been added to the Dictionary object. At the end of it, the postal code "00710" is retrieved from the dictionary. Both the postal code and the city are represented as strings.
```csharp
using System;
using System.Collections.Generic;

namespace Exercise001
{
  class Program
  {
    static void Main(string[] args)
    {
      Dictionary<string, string> postalCodes = new Dictionary<string, string>();
      postalCodes.Add("00710", "Helsinki");
      postalCodes.Add("90014", "Oulu");
      postalCodes.Add("33720", "Tampere");
      postalCodes.Add("33014", "Tampere");

      Console.WriteLine(postalCodes["33720"]);
    }
  }
}
```
```text
Tampere
```
The internal state of the dictionary created above looks like this. Each key refers to some value.
- If the dictionary does not contain the key used for search, we get a KeyNotFoundException.
```csharp
Dictionary<string, string> postalCodes = new Dictionary<string, string>();
postalCodes.Add("00710", "Helsinki");
postalCodes.Add("90014", "Oulu");
postalCodes.Add("33720", "Tampere");
postalCodes.Add("33014", "Tampere");

Console.WriteLine(postalCodes["67100"]);
```
```csharp
Unhandled exception. System.Collections.Generic.KeyNotFoundException: The given key '67100' was not present in the dictionary.
   at System.Collections.Generic.Dictionary`2.get_Item(TKey key)
   at Exercise001.Program.Main(String[] args) in /mnt/c/Users/HeikkiHei/Documents/coding-exercises/Exercise001/Program.cs:line 17
```
Two type parameters are required when creating a dictionary - the type of the key and the type of the value added. If the keys of the dictionary are of type string, and the values of type integer, the dictionary is created with the following statement
```csharp
Dictionary<string, integer> dict = new Dictionary<string, integer>();
```
- Adding to the dictionary is done through the `Add(key, value)` method that has two parameters, one for the key, the other for the value.
-  Retrieving from a dictionary is done with the familiar dictionary[key] syntax. How ever, this time we are looking for a value with a key, and not with an index.
