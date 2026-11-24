#### Access modifiers private, protected, and public
- **Private members** are visible only in derived classes that are nested in their base class.
> Otherwise, they are not visible in derived classes. So, from the Engine class there would be no way to directly access the variables identifier, manufacturer, and description,if they were defined private in the base class Part. Now they are public, and as such usable from the derived class.
#### Note!
- We have not defined set for our variables in Part. This means, that the derived class Engine cannot set the values for the variables, only get them.
- A derived class sees everything that is defined with the **public** modifier in the base class.
-  IF we want to define some variables or methods that are visible to the derived classes but invisible to everything else, we can use the access modifier **protected** to achieve this.
