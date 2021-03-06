# C\#

Standards for coding C\# in random order.

## Naming

You can use Danish and English, and you are free to mix them.

Start metod names with a verb in imperative mode \(bydeform\).

```csharp
public string GetPolicenummer()
{
    // ...
}
```

There may be exceptions, for example `ToString()`.

Use camel notation and use a capital letter for each new word: `GetPolicenummer`, `Skadeforsikring`.

All names start with a capital letter, except for private instance member fields.

```csharp
public const int MyConstant = 42;
private int myInstanceField;
```

Never use underscores in a name. As a special case, never prefix fields with an underscore.

Prefix interfaces with an "I": `ICanDo`.

## This

Always use "this" when accessing members.

```csharp
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

Remember to add modifiers. Use `readonly` amply.

Alway make instance fields private. Expose internal state only through properties and add property setters only if absolutely necessary.

Constants may be non-private.

**Do:**

```csharp
public class Car
{
    public const int NumberOfWheels = 4;
    private readonly string vin;

    public Car(string vin)
    {
        this.vin = vin;
    }

    public int Vin
    {
        get
        {
            return this.vin;
        }
    }
}
```

## Layout

### Indentation

Indentation is 4 spaces which is the default in Visual Studio.

### Blocks

Code blocks start with a line shift and a curly bracket. Never use single line blocks without curly brackets.

**Do:**

```csharp
if (a == 0)
{
    this.DoStuff();
}
```

**Don't:**

```csharp
if (a == 0) {
    this.DoStuff();
}
```

```csharp
if (a == 0)
    this.DoStuff();
```

### Whitespace

#### Operators

Use spaces before and after operators.

**Do:**

```csharp
int a = (b + c) * 10;
```

**Don't:**

```csharp
int a=(b+c)*10;
```

#### Parentheses

Avoid spaces before and after parentheses in parameter lists.

**Do:**

```csharp
public void DoStuff(int parameter1)
{
    // ...
}
```

**Don't:**

```csharp
public void DoStuff ( int parameter1 )
{
    // ...
}
```

Put a space in front of a parenthesis in formulaes.

**Do:**

```csharp
int a = 10 * (b + c) + 11;
```

**Don't:**

```csharp
int a = 10 *( b + c )+ 11;
```

#### Casts

Do not leave a blank after a cast.

**Do:**

```csharp
int a = (int)b;
```

**Don't:**

```csharp
int a = (int) b;
```

## Files

Create a new file for each type \(class, interface, enum\). The name of the type much match the name of the file.

Delegates are technically types but there is no need to create a new file for each delegate.

## StyleCop

Do use StyleCop to enforce conventions and standards.

Check out the [GitHub StyleCop](https://github.com/DotNetAnalyzers/StyleCopAnalyzers) repository on how to install StyleCop into your project.

After installation, you need to add a ruleset fil to your project. The official AT StyleCop ruleset file is located in TFS on this path: $/AT/Udvikling/Core/Main/AT.ruleset. Copy the file and add it to your solution in Visual Studio.

To add the ruleset file to a project, right-click the project in Visual Studio and click "Properties". On the left, choose "Code Analysis". In the dropdown click "Browse" and choose the AT.ruleset file.

StyleCop will now warn when you break the rules in your project.

