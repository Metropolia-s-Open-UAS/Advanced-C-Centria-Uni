#### Dictionary Keys Correspond to a Single Value at Most
- [ ] The dictionary has a maximum of one value per key.
- [ ] If a new key-value pair is added to the dictionary.
- [ ]  but the key has already been associated with some other value stored in the dictionary
- [ ]   we will get an `ArgumentException`:
```csharp
Dictionary<string, string> postalCodes = new Dictionary<string, string>();
postalCodes.Add("67100", "Kokkola");
postalCodes.Add("67100", "Karleby");
```
```csharp
Unhandled exception. System.ArgumentException: An item with the same key has already been added. Key: 67100
   at System.Collections.Generic.Dictionary`2.TryInsert(TKey key, TValue value, InsertionBehavior behavior)
   at System.Collections.Generic.Dictionary`2.Add(TKey key, TValue value)
```
- For this, we can prepare ourselves, by checking if a value already exists in the dictionary, and only if it does not, we add the new value:
```csharp
Dictionary<string, string> postalCodes = new Dictionary<string, string>();
postalCodes.Add("00710", "Helsinki");
postalCodes.Add("90014", "Oulu");
postalCodes.Add("33720", "Tampere");
postalCodes.Add("33014", "Tampere");
postalCodes.Add("67100", "Kokkola");
postalCodes.Add("99999", null);

if (!postalCodes.ContainsKey("67100"))
{
  postalCodes.Add("67100", "Karleby");
}
```
- This way our program does not crash, when we try to change the value for "67100". To see what our dictionary contains, we can use a foreach-loop for **KeyValuePair** objects:
```csharp
foreach (KeyValuePair<string, string> kvp in postalCodes)
{
  Console.WriteLine("Key = {0}, Value = {1}",
      kvp.Key, kvp.Value);
}
```
```text
Key = 00710, Value = Helsinki
Key = 90014, Value = Oulu
Key = 33720, Value = Tampere
Key = 33014, Value = Tampere
Key = 67100, Value = Kokkola
Key = 99999, Value =
```
> You might notice a different way of printing the strings. What we did there was **String interpolation**.

> As you can see, we can also give a `null` as a value. We cannot, however, give `null` as a `key`, or we will get `ArgumentNullException`.


