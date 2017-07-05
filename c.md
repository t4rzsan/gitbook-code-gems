# Coding Standards: Csharp

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

Never use underscore in a name.  As a special case, never prefix fields with an underscore.

Prefix interfaces with an "I": `ICanDo`.

## This

Always use "this" when accessing members.

```C\#
internal class Car
{
    private readonly string vin;

    public Car(string vin)
    {
        this.vin = vin;
        this.DoCarStuff();
    }

    private void DoCarStuff()
    {
        // ...
    }
}
```

## Modifiers

Remember to add modifiers.  Use `readonly` amply.

## Layout

Indentation is 4 spaces.

Code blocks start with a line shift and a curly bracket.  Never use single line blocks without curly brackets.

**Don't:**

```
if (a == 0) {
    this.DoStuff();
}
```

```
if (a == 0)
    this.DoStuff();
```

**Do:**

```
if (a == 0)
{
    this.DoStuff();
}
```

## Files

Create a new file for each type \(class, interface, enum\).  The name of the type much match the name of the file.

Delegates are technically types but there is no need to create a new file for each delegate.

