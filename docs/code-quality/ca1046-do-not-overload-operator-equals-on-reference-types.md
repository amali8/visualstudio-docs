---
title: "CA1046: Do not overload operator equals on reference types"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "DoNotOverloadOperatorEqualsOnReferenceTypes"
  - "CA1046"
helpviewer_keywords:
  - "CA1046"
  - "DoNotOverloadOperatorEqualsOnReferenceTypes"
ms.assetid: c1dfbfe3-63f9-4005-a81a-890427b77e79
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1046: Do not overload operator equals on reference types

|||
|-|-|
|TypeName|DoNotOverloadOperatorEqualsOnReferenceTypes|
|CheckId|CA1046|
|Category|Microsoft.Design|
|Breaking change|Breaking|

## Cause
A public or nested public reference type overloads the equality operator.

## Rule description
For reference types, the default implementation of the equality operator is almost always correct. By default, two references are equal only if they point to the same object.

## How to fix violations
To fix a violation of this rule, remove the implementation of the equality operator.

## When to suppress warnings
It is safe to suppress a warning from this rule when the reference type behaves like a built-in value type. If it is meaningful to do addition or subtraction on instances of the type, it is probably correct to implement the equality operator and suppress the violation.

## Example
The following example demonstrates the default behavior when comparing two references.

[!code-csharp[FxCop.Design.RefTypesNoEqualityOp#1](../code-quality/codesnippet/CSharp/ca1046-do-not-overload-operator-equals-on-reference-types_1.cs)]

## Example

The following application compares some references.

[!code-csharp[FxCop.Design.TestRefTypesNoEqualityOp#1](../code-quality/codesnippet/CSharp/ca1046-do-not-overload-operator-equals-on-reference-types_2.cs)]

This example produces the following output:

```txt
a = new (2,2) and b = new (2,2) are equal? No
c and a are equal? Yes
b and a are == ? No
c and a are == ? Yes
```

## Related rules

[CA1013: Overload operator equals on overloading add and subtract](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)

## See also

- <xref:System.Object.Equals%2A?displayProperty=fullName>
- [Equality Operators](/dotnet/standard/design-guidelines/equality-operators)