#### Example of misusing inheritance
- Let's consider a postal service and some related `classes`.
- **Customer** includes the information related to a customer, and the class **Order** that inherits from the **Customer** class and includes the information about the ordered item.
- The class **Order** also has a method called **PostalAddress** which represents the postal address that the order is shipped to.
```csharp
public class Customer
{
  public string name { get; set; }
  public string address { get; set; }

  public Customer(string name, string address)
  {
    this.name = name;
    this.address = address;
  }
}
```
```csharp
public class Order : Customer
{

  private string product;
  private string count;

  public Order(string product, string count, string name, string address) : base(name, address)
  {
    this.product = product;
    this.count = count;
  }

  public string PostalAddress()
  {
    return this.name + "\n" + this.address;
  }
}
```
- [ ] Above inheritance is not used correctly.
- [ ] When inheriting, the derived class must be a special case of the base class;
- [ ] an order is definitely not a special case of a customer.
> The misuse shows itself in how the code breaks the **single responsibility principle**: the Order class is responsible both for maintaining the customer information and the order information.
- The problem becomes very clear when we think of what a change in a customer's address would cause.
> **In the case that an address changes, we would have to change every order object that relates to that customer. This is hardly ideal. A better solution would be to encapsulate the customer as an object variable of the Order class. Thinking more closely on the semantics of an order, this seems intuitive. An order has a customer.**
- Let's modify the Order class so that it includes a `reference` to a Customer object.
```csharp
public class Order
{

  private Customer customer;
  private string product;
  private string count;

  public Order(Customer customer, string product, string count)
  {
    this.customer = customer;
    this.product = product;
    this.count = count;
  }

  public string PostalAddress()
  {
    return this.customer.name + "\n" + this.customer.address;
  }
}
```
- This version of the **Order** class is better. The method **PostalAddress** uses the customer reference to obtain the postal address instead of inheriting the class Customer. This helps both the maintenance of the program and its concrete functionality.
- Now if we need to change customer information, we don't have to change the order itself.




