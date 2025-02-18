---
title: "CA1810: Initialize reference type static fields inline"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "InitializeReferenceTypeStaticFieldsInline"
  - "CA1810"
helpviewer_keywords:
  - "InitializeReferenceTypeStaticFieldsInline"
  - "CA1810"
ms.assetid: e9693118-a914-4efb-9550-ec659d8d97d2
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1810: Initialize reference type static fields inline

|||
|-|-|
|TypeName|InitializeReferenceTypeStaticFieldsInline|
|CheckId|CA1810|
|Category|Microsoft.Performance|
|Breaking change|Non-breaking|

## Cause
A reference type declares an explicit static constructor.

## Rule description
When a type declares an explicit static constructor, the just-in-time (JIT) compiler adds a check to each static method and instance constructor of the type to make sure that the static constructor was previously called. Static initialization is triggered when any static member is accessed or when an instance of the type is created. However, static initialization is not triggered if you declare a variable of the type but do not use it, which can be important if the initialization changes global state.

When all static data is initialized inline and an explicit static constructor is not declared, Microsoft intermediate language (MSIL) compilers add the `beforefieldinit` flag and an implicit static constructor, which initializes the static data, to the MSIL type definition. When the JIT compiler encounters the `beforefieldinit` flag, most of the time the static constructor checks are not added. Static initialization is guaranteed to occur at some time before any static fields are accessed but not before a static method or instance constructor is invoked. Note that static initialization can occur at any time after a variable of the type is declared.

Static constructor checks can decrease performance. Often a static constructor is used only to initialize static fields, in which case you must only make sure that static initialization occurs before the first access of a static field. The `beforefieldinit` behavior is appropriate for these and most other types. It is only inappropriate when static initialization affects global state and one of the following is true:

- The effect on global state is expensive and is not required if the type is not used.

- The global state effects can be accessed without accessing any static fields of the type.

## How to fix violations
To fix a violation of this rule, initialize all static data when it is declared and remove the static constructor.

## When to suppress warnings
It is safe to suppress a warning from this rule if performance is not a concern; or if global state changes that are caused by static initialization are expensive or must be guaranteed to occur before a static method of the type is called or an instance of the type is created.

## Example

The following example shows a type, `StaticConstructor`, that violates the rule and a type, `NoStaticConstructor`, that replaces the static constructor with inline initialization to satisfy the rule.

[!code-csharp[FxCop.Performance.RefTypeStaticCtor#1](../code-quality/codesnippet/CSharp/ca1810-initialize-reference-type-static-fields-inline_1.cs)]
[!code-vb[FxCop.Performance.RefTypeStaticCtor#1](../code-quality/codesnippet/VisualBasic/ca1810-initialize-reference-type-static-fields-inline_1.vb)]

Note the addition of the `beforefieldinit` flag on the MSIL definition for the `NoStaticConstructor` class.

```
.class public auto ansi StaticConstructor
extends [mscorlib]System.Object
{
} // end of class StaticConstructor

.class public auto ansi beforefieldinit NoStaticConstructor
extends [mscorlib]System.Object
{
} // end of class NoStaticConstructor
```

## Related rules

- [CA2207: Initialize value type static fields inline](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)