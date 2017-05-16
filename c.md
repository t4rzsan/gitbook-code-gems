# Coding Standards: C\#

Standards for coding C\# in random order.

## Naming

You can use Danish and English, and you are free to mix them.

Start metod names with a verb.  

```
public string GetPolicenummer()
{
    // ...
}
```

There may be exceptions, for example `ToString()`.

Use camel notation and use a capital letter for each new word: `GetPolicenummer`, `Skadeforsikring`.

All names start with a capital letter, except for private instance member fields.  

Never use underscore underscore in a name.  Specifically, never prefix fields with an underscore.

## This

Always use "this" when accessing members.

```
internal class Car
{
    private readonly string vin;
    
    public Car(string vin)
    {
        this.vin = vin;
        this.DoCarStuff();
    }
}
```

## Modifiers

Remember to add modifiers.  Use `readonly` amply.



