---
title: "CA1401: P-Invokes should not be visible"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "PInvokesShouldNotBeVisible"
  - "CA1401"
helpviewer_keywords:
  - "CA1401"
  - "PInvokesShouldNotBeVisible"
ms.assetid: 0f4d96c1-f9de-414e-b223-4dc7f691bee3
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1401: P/Invokes should not be visible

|||
|-|-|
|TypeName|PInvokesShouldNotBeVisible|
|CheckId|CA1401|
|Category|Microsoft.Interoperability|
|Breaking change|Breaking|

## Cause
A public or protected method in a public type has the <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> attribute (also implemented by the `Declare` keyword in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]).

## Rule description
Methods that are marked with the <xref:System.Runtime.InteropServices.DllImportAttribute> attribute (or methods that are defined by using the `Declare` keyword in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) use Platform Invocation Services to access unmanaged code. Such methods should not be exposed. By keeping these methods private or internal, you make sure that your library cannot be used to breach security by allowing callers access to unmanaged APIs that they could not call otherwise.

## How to fix violations
To fix a violation of this rule, change the access level of the method.

## When to suppress warnings
Do not suppress a warning from this rule.

## Example
The following example declares a method that violates this rule.

[!code-vb[FxCop.Interoperability.DllImports#1](../code-quality/codesnippet/VisualBasic/ca1401-p-invokes-should-not-be-visible_1.vb)]
[!code-csharp[FxCop.Interoperability.DllImports#1](../code-quality/codesnippet/CSharp/ca1401-p-invokes-should-not-be-visible_1.cs)]