---
title: "CA1023: Indexers should not be multidimensional"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "IndexersShouldNotBeMultidimensional"
  - "CA1023"
helpviewer_keywords:
  - "CA1023"
  - "IndexersShouldNotBeMultidimensional"
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CPP
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1023: Indexers should not be multidimensional

|||
|-|-|
|TypeName|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Category|Microsoft.Design|
|Breaking change|Breaking|

## Cause
A public or protected type contains a public or protected indexer that uses more than one index.

## Rule description
Indexers, that is, indexed properties, should use a single index. Multi-dimensional indexers can significantly reduce the usability of the library. If the design requires multiple indexes, reconsider whether the type represents a logical data store. If not, use a method.

## How to fix violations
To fix a violation of this rule, change the design to use a lone integer or string index, or use a method instead of the indexer.

## When to suppress warnings
Suppress a warning from this rule only after carefully considering the need for the nonstandard indexer.

## Example
The following example shows a type, `DayOfWeek03`, with a multi-dimensional indexer that violates the rule. The indexer can be seen as a type of conversion and therefore is more appropriately exposed as a method. The type is redesigned in `RedesignedDayOfWeek03` to satisfy the rule.

[!code-vb[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/VisualBasic/ca1023-indexers-should-not-be-multidimensional_1.vb)]
[!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CPP/ca1023-indexers-should-not-be-multidimensional_1.cpp)]
[!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CSharp/ca1023-indexers-should-not-be-multidimensional_1.cs)]

## Related rules
[CA1043: Use integral or string argument for indexers](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

[CA1024: Use properties where appropriate](../code-quality/ca1024-use-properties-where-appropriate.md)