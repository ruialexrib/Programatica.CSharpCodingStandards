# Programatica.CSharpCodingStandards
C# Coding Standards

## Original credits to
http://jesseliberty.com/2020/01/29/c-coding-standards/

### Use PascalCasing for class names and method names
```csharp
public class ClientActivity 
{ 
    public void ClearStatistics() 
    { 
        //... 
    } 

    public void CalculateStatistics() 
    { 
        //... 
    } 
} 
```
Why: consistent with the Microsoft’s .NET Framework and easy to read.

### Use camelCasing for method arguments and local variables
```csharp
public class UserLog 
{ 
   public void Add(LogEvent logEvent) 
   { 
    var itemCount = logEvent.Items.Count; 

    // ... 
   } 
} 
```
Why: consistent with the Microsoft’s .NET Framework and easy to read.

### Do not use Hungarian notation or any other type identification in identifiers (except interfaces)
```csharp
// Correct 
int counter; 
string name; 

// Avoid 
int iCounter; 
string strName; 
```
Why: The Visual Studio IDE makes determining types very easy (via tooltips). In general you want to avoid type indicators in any identifier. Exception: begin interface names with a capital I followed by Pascal case. Example IFoo.

### Do not use SCREAMING CAPS for constants or read-only variables
```csharp
// Correct 
public static const string ShippingType = "DropShip"; 

// Avoid 
public static const string SHIPPINGTYPE = "DropShip";
```
Why: consistent with the Microsoft’s .NET Framework. Caps grab too much attention.

### Avoid using Abbreviations. Exceptions: abbreviations commonly used as names, such as Id, Xml, Ftp, Uri
```csharp
// Correct 
UserGroup userGroup; 
Assignment employeeAssignment; 
 
// Avoid 
UserGroup usrGrp; 
Assignment empAssignment; 

// Exceptions 
CustomerId customerId; 
XmlDocument xmlDocument; 
FtpHelper ftpHelper; 
UriPart uriPart; 
```
Why: consistent with the Microsoft’s .NET Framework and prevents inconsistent abbreviations.

### Use PascalCasing for abbreviations 3 characters or more (2 chars are both uppercase)
```csharp
HtmlHelper htmlHelper; 
FtpTransfer ftpTransfer; 
UIControl uiControl; 

The type here is Pascal, but the field is camelNotation.
```
Why: consistent with the Microsoft’s .NET Framework. Caps would grab visually too much attention.

### Do not use Underscores in identifiers. Prefix private member variables with an underscore
```csharp
// Correct 
public DateTime clientAppointment; 
public TimeSpan timeLeft; 

// Avoid 
public DateTime client_Appointment; 
public TimeSpan time_Left; 

// Exception 
private DateTime _registrationDate; 
```
Why: consistent with the Microsoft’s .NET Framework and makes code more natural to read. Also avoids underline stress (inability to see underline). Note, using an underscore for member names is still controversial.

### Use predefined type names instead of system type names like Int16, Single, UInt64, etc.
```csharp
// Correct 
string firstName; 
int lastIndex; 
bool isSaved; 
 
// Avoid 
String firstName; 
Int32 lastIndex; 
Boolean isSaved; 
```
Why: consistent with the Microsoft’s .NET Framework and makes code more natural to read.

### Use implicit type var for local variable declarations.
```csharp
var stream = File.Create(path); 
var customers = new Dictionary(); 
var index = 100; 
var greeting = "hello"; 
var isCompleted = true;
```
Why: removes clutter, particularly with complex generic types. Type is easily detected with Visual Studio tooltips. Facilitates programming in that you don’t necessarily need to know the type (e.g., of method calls)

### prefix interfaces with the letter I. Interface names are noun (phrases) or adjectives
```csharp
public interface IShape 
{ 

} 

public interface IShapeCollection 
{ 

} 

public interface IGroupable 
{ 

} 
```
Why: consistent with the Microsoft’s .NET Framework.

### Name source files according to their main classes
```csharp
// Located in Task.cs 
public partial class Task 
{ 
   //... 
} 
```
Why: consistent with the Microsoft practices. Files are alphabetically sorted and partial classes remain adjacent.

### organize namespaces with a clearly defined structure. Generally namespaces should reflect the folder hierarchy within a project
```csharp
// Examples 
namespace foo.CloudServices.OccupantMobileApp
namespace foo.CloudServices.OccupantMobileApp.iOS
namespace foo.CloudServices.OccupantMobileApp.Android
namespace foo.CloudServices.Xamarin.Core
namespace foo.CloudServices.Core
```
Why: consistent with the Microsoft’s .NET Framework. Maintains good organization of your code base.

### Vertically align curly braces.
```csharp
// Correct 
class Program 
{ 
   static void Main(string[] args) 
   { 

   } 
} 
```
Why: Microsoft has a different standard, but developers have overwhelmingly preferred vertically aligned brackets.

### Declare all member variables at the top of a class, with static variables at the very top. Exception, keep backing variables with their property
```csharp
// Correct 
public class Account 
{ 
   private static string _bankName; 
   private static decimal _reserves; 
   private int myAge;
   private string myName;

   public string Number {get; set;} 

   // Constructor 
   public Account() 
   { 
       // ... 
   } 
} 
```
Why: generally accepted practice that prevents the need to hunt for variable declarations.

### Use singular names for enums. Exception: bit field enums
```csharp
// Correct 
public enum Color 
{ 
   Red, 
   Green, 
   Blue, 
   Yellow, 
   Magenta, 
   Cyan 
} 

// Exception 
[Flags] 
public enum Dockings 
{ 
   None = 0, 
   Top = 1,  
   Right = 2,  
   Bottom = 4, 
   Left = 8 
} 
```
Why: consistent with the Microsoft’s .NET Framework and makes the code more natural to read. Plural flags because enum can hold multiple values (using bitwise ‘OR’).

### Do not explicitly specify a type of an enum or values of enums (except bit fields and where the value is required)
```csharp
// Don't 
public enum Direction : long 
{ 
   North = 1, 
   East = 2, 
   South = 3, 
   West = 4 
} 

// Correct 
public enum Direction 
{ 
   North, 
   East, 
   South, 
   West 
} 

// Correct
public enum Temperatures
{
   Freezing = 32,
   Boiling = 212
}

// Exception
[Flags]
enum Days
{
    None      = 0b_0000_0000, // 0
    Sunday    = 0b_0000_0001, // 1
    Monday    = 0b_0000_0010, // 2
    Tuesday   = 0b_0000_0100, // 4
    Wednesday = 0b_0000_1000, // 8
    Thursday  = 0b_0001_0000, // 16
    Friday    = 0b_0010_0000, // 32
    Saturday  = 0b_0100_0000  // 64 
}
class MyClass
{
    Days meetingDays = Days.Tuesday | Days.Thursday;
}
```
Why: can create confusion when relying on actual types and values. Exception is when enums are used (foolishly) in bitwise operations.

### Do not suffix enum names with Enum
```csharp
// Don't 
public enum CoinEnum 
{ 
   Penny, 
   Nickel, 
   Dime, 
   Quarter, 
   Dollar 
} 

// Correct 
public enum Coin 
{ 
   Penny, 
   Nickel, 
   Dime, 
   Quarter, 
   Dollar 
} 
```
Why: consistent with the Microsoft’s .NET Framework and consistent with prior rule of no type indicators in identifiers.

### Do name global styles and static resources with their functional purpose instead of (for example) a color name
```xml
// Don't
    <Application.Resources>
        <ResourceDictionary>
           <Color x:Key="Red">#FFDC0A0A</Color>
        </ResourceDictionary>
    </Application.Resources>

//Correct
    <Application.Resources>
        <ResourceDictionary>
           <Color x:Key="Error">#FFDC0A0A</Color>
        </ResourceDictionary>
    </Application.Resources>
```
Why: It will be easier to maintain a static resource when you know when to use it and it’s functional purpose. For example, if your company changes the color for errors, then it will be easy to know what to update and you will only have to update it in one place.. It is a clean coding practice and is self documenting.

### If your line of code is greater than 80, chop it to two or more lines (ReSharper can help) except where essential

Why: Programmers set their fonts differently and we want to avoid horizontal scrolling. A consistent width across the project will make the code easier to read.

### Do prefer Switch statements to multiple nested if statements
```csharp
// Don't
if (...)
{
    if (...)
    {
    ...
    }
}
else if(...)
{
    ...
}

// Correct
switch(...)
case 1:
  ...
  break;
case 2:
   ...
   Break;
```
Why – makes the code easier to understand and maintain. Nested if statements are error prone.

### Do always use braces with conditionals, for loops, etc.
```csharp
// Correct
   if (condition)
   {
       action;
   }
   
// Don't
   if(conditioin) 
      action;
```
why – without the braces it is too easy to accidentally add a second line thinking it is included in the if, when it isn’t.

### Where possible prefer switch expressions over switch statements . (new in C# 8)
```csharp
// wrong
switch(foo)
{
    case 1:
      x = 50;
      break;
    case 2:
      x = 100
      break;
     default:
       x = 0;
       break
}

// Correct

foo switch
{
    1 => 50;
    2 => 100;
    _ => 0;
}
```
Why easier to read, easier to understand and maintain, more concise. (Note, only available as of C# 8)

### Do enable nullable references and treat these warnings as errors
```csharp
#nullable enable
Person? person;  //etc.
```
Why? Significantly cuts down on null reference exceptions.

### Do use null conditional (?.) operator rather than if statements for null
```csharp
// wrong
if (a != null)
{
    if (b != null)
    {
        return c.name;
    }
}

// right
return a?.b?.c.name;
```
why – Recommended by Microsoft. Easier to read and understand and thus to maintain. More concise.

### Do use null coalescing (??) operator rather than if statements for null
```csharp
// wrong
if (a != null)
{
    if (b != null)
    {
        return c.name;
    }
    {
        else return string.empty;
    }
}
else
{
    return string.empty;
}

// right
return a?.b?.c.name ?? string.empty;
```
why – Recommended by Microsoft. Easier to read and understand and thus to maintain. More concise.

### Prefer SetValue & Lambda expressions for properties (inherit from BaseViewModel)
```csharp
// wrong
private string _property;
public string Property
{
    get { return _property; }
    set
    {
        _property = value;
        OnPropertyChanged;
    }
}

// right
private string _property;
public string Property
{
  get => _property;
  set => SetValue(ref _property, value);
}

// SetValue is created in the base class and handles checking for changed values and calls to INotifyPropertyChanged.
```
Why: code is more concise, easier to understand and maintain and allows the base view to consolidate the handling of property changed.

### Declare and define commands in one statement in the ViewModel
```csharp
public ICommand MyCommand =>
    new Command( async ( ) => await OnMyCommand( ) )
```
Why: Easier to read and maintain, everything is in one place.

### Do not place all backing variables together — put them with their properties
```csharp
// Wrong
private string _prop1;
private int _prop2;
private int _prop3;

public string Prop1
{ ... }
public int Prop2
{...}
public int Prop3
{...}

// Correct
private string _prop1;
public string Prop1
{ ... }

private int _prop2;
public int Prop2
{...}

private int _prop3;
public int Prop3
{...}
```
Why: It makes it far easier to debug issues with getters and setters if the backing variable is with the property — and it cuts down on aggravating scrolling back and forth.

### Treat Warnings As Errors

Why: It is all too easy to ignore warnings, and they pile up. Especially with the advent of nullable types, those warnings can save you from the infamous null object reference exception. If you can’t get rid of a warning, consider using a pragma, and failing that, add a comment.

### Use “TODO” sparingly, and check the TODO list often

Why: It is easy for the TODO list to grow so large that it is meaningless, it also represents code which isn’t complete.
There should be no TODO tasks or blocks of commented code as part of ANY pull request.
