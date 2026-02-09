---
source_url: https://google.github.io/styleguide/csharp-style.html
fetched_at: 2026-02-09T09:31:51.636662
---

# styleguide

This style guide is for C# code developed internally at Google, and is the default style for C# code at Google. It makes stylistic choices that conform to other languages at Google, such as Google C++ style and Google Java style.

Naming rules follow
[Microsoft’s C# naming guidelines](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/naming-guidelines).
Where Microsoft’s naming guidelines are unspecified (e.g. private and local
variables), rules are taken from the
[CoreFX C# coding guidelines](https://github.com/dotnet/runtime/blob/HEAD/docs/coding-guidelines/coding-style.md)

Rule summary:

`PascalCase`

.`camelCase`

.`_camelCase`

.`MyRpc`

instead of `MyRPC`

`I`

, e.g. `IInterface`

.`PascalCase`

, e.g. `MyFile.cs`

.`MyClass.cs`

.```
public protected internal private
new abstract virtual override sealed static readonly extern unsafe volatile
async
```

.`using`

declarations go at the top, before any namespaces. `using`

import order is alphabetical, apart from `System`

imports which always go
first.Developed from Google Java style.

`else`

.`if`

/`for`

/`while`

etc., and after commas.```
using System; // `using` goes at the top, outside the
// namespace.
namespace MyNamespace { // Namespaces are PascalCase.
// Indent after namespace.
public interface IMyInterface { // Interfaces start with 'I'
public int Calculate(float value, float exp); // Methods are PascalCase
// ...and space after comma.
}
public enum MyEnum { // Enumerations are PascalCase.
Yes, // Enumerators are PascalCase.
No,
}
public class MyClass { // Classes are PascalCase.
public int Foo = 0; // Public member variables are
// PascalCase.
public bool NoCounting = false; // Field initializers are encouraged.
private class Results {
public int NumNegativeResults = 0;
public int NumPositiveResults = 0;
}
private Results _results; // Private member variables are
// _camelCase.
public static int NumTimesCalled = 0;
private const int _bar = 100; // const does not affect naming
// convention.
private int[] _someTable = { // Container initializers use a 2
2, 3, 4, // space indent.
}
public MyClass() {
_results = new Results {
NumNegativeResults = 1, // Object initializers use a 2 space
NumPositiveResults = 1, // indent.
};
}
public int CalculateValue(int mulNumber) { // No line break before opening brace.
var resultValue = Foo * mulNumber; // Local variables are camelCase.
NumTimesCalled++;
Foo += _bar;
if (!NoCounting) { // No space after unary operator and
// space after 'if'.
if (resultValue < 0) { // Braces used even when optional and
// spaces around comparison operator.
_results.NumNegativeResults++;
} else if (resultValue > 0) { // No newline between brace and else.
_results.NumPositiveResults++;
}
}
return resultValue;
}
public void ExpressionBodies() {
// For simple lambdas, fit on one line if possible, no brackets or braces required.
Func<int, int> increment = x => x + 1;
// Closing brace aligns with first character on line that includes the opening brace.
Func<int, int, long> difference1 = (x, y) => {
long diff = (long)x - y;
return diff >= 0 ? diff : -diff;
};
// If defining after a continuation line break, indent the whole body.
Func<int, int, long> difference2 =
(x, y) => {
long diff = (long)x - y;
return diff >= 0 ? diff : -diff;
};
// Inline lambda arguments also follow these rules. Prefer a leading newline before
// groups of arguments if they include lambdas.
CallWithDelegate(
(x, y) => {
long diff = (long)x - y;
return diff >= 0 ? diff : -diff;
});
}
void DoNothing() {} // Empty blocks may be concise.
// If possible, wrap arguments by aligning newlines with the first argument.
void AVeryLongFunctionNameThatCausesLineWrappingProblems(int longArgumentName,
int p1, int p2) {}
// If aligning argument lines with the first argument doesn't fit, or is difficult to
// read, wrap all arguments on new lines with a 4 space indent.
void AnotherLongFunctionNameThatCausesLineWrappingProblems(
int longArgumentName, int longArgumentName2, int longArgumentName3) {}
void CallingLongFunctionName() {
int veryLongArgumentName = 1234;
int shortArg = 1;
// If possible, wrap arguments by aligning newlines with the first argument.
AnotherLongFunctionNameThatCausesLineWrappingProblems(shortArg, shortArg,
veryLongArgumentName);
// If aligning argument lines with the first argument doesn't fit, or is difficult to
// read, wrap all arguments on new lines with a 4 space indent.
AnotherLongFunctionNameThatCausesLineWrappingProblems(
veryLongArgumentName, veryLongArgumentName, veryLongArgumentName);
}
}
}
```


`const`

should always be made `const`

.`const`

isn’t possible, `readonly`

can be a suitable alternative.`IReadOnlyCollection`

/ `IReadOnlyList`

/ `IEnumerable`

as inputs to methods
when the inputs should be immutable.`IList`

over `IEnumerable`

. If not transferring ownership, prefer the
most restrictive option.`ToList()`

will be less performant than filling in a container directly.`=>`

) when possible.`{ get; set; }`

syntax.For example:

```
int SomeProperty => _someProperty
```


Structs are very different from classes:

`transform.position.x = 10`

doesn’t set the transform’s
position.x to 10; `position`

here is a property that returns a `Vector3`

by value, so this just sets the x parameter of a copy of the original.Almost always use a class.

Consider struct when the type can be treated like other value types - for example, if instances of the type are small and commonly short-lived or are commonly embedded in other objects. Good examples include Vector3, Quaternion and Bounds.

Note that this guidance may vary from team to team where, for example, performance issues might force the use of structs.

`out`

for returns that are not also inputs.`out`

parameters after all other parameters in the method definition.`ref`

should be used rarely, when mutating an input is necessary.`ref`

as an optimisation for passing structs.`ref`

to pass a modifiable container into a method. `ref`

is only
required when the supplied container needs be replaced with an entirely
different container instance.`myList.Where(x)`

to `myList where x`

.`Container.ForEach(...)`

for anything longer than a single statement.`List<>`

over arrays for public variables, properties,
and return types (keeping in mind the guidance on `IList`

/ `IEnumerable`

/
`IReadOnlyList`

above).`List<>`

when the size of the container can change.`List<>`

both represent linear, contiguous containers.`std::vector`

, arrays are of fixed capacity,
whereas `List<>`

can be added to.`List<>`

is
more flexible.`Tuple<>`

, particularly when
returning complex types.`String.Format()`

vs `String.Concat`

vs `operator+`

`operator+`

concatenations will be slower and cause
significant memory churn.`StringBuilder`

will be faster for multiple
string concatenations.`using`

`using`

. Often this is a sign
that a `Tuple<>`

needs to be turned into a class.
`using RecordList = List<Tuple<int, float>>`

should probably be a
named class instead.`using`

statements are only file scoped and so of limited use.
Type aliases will not be available for external users.For example:

```
var x = new SomeClass {
Property1 = value1,
Property2 = value2,
};
```


`unity_app`

, namespaces are not necessary.`out`

value.Notes:

`StatusOr`

equivalent in the future, if there is enough demand.C# (like many other languages) does not provide an obvious mechanism for removing items from containers while iterating. There are a couple of options:

`someList.RemoveAll(somePredicate)`

is recommended.`RemoveAll`

may not be
sufficient. A common alternative pattern is to create a new container
outside of the loop, insert items to keep in the new container, and swap the
original container with the new one at the end of iteration.`Invoke()`

and use the null conditional
operator - e.g. `SomeDelegate?.Invoke()`

. This clearly marks the call at the
callsite as ‘a delegate that is being called’. The null check is concise and
robust against threading race conditions.`var`

keyword`var`

is encouraged if it aids readability by avoiding type names
that are noisy, obvious, or unimportant.Encouraged:

`var apple = new Apple();`

, or ```
var
request = Factory.Create<HttpRequest>();
```

`var item = GetItem(); ProcessItem(item);`

Discouraged:

`var success = true;`

```
var
number = 12 * ReturnsFloat();
```

```
var
listOfItems = GetList();
```

Derived from the Google C++ style guide.

When the meaning of a function argument is nonobvious, consider one of the following remedies:

`bool`

argument with
an `enum`

argument. This will make the argument values self-describing.Consider the following example:

```
// Bad - what are these arguments?
DecimalNumber product = CalculateProduct(values, 7, false, null);
```


versus:

```
// Good
ProductOptions options = new ProductOptions();
options.PrecisionDecimals = 7;
options.UseCache = CacheUsage.DontUseCache;
DecimalNumber product = CalculateProduct(values, options, completionDelegate: null);
```