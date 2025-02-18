---
title: "CA1410: COM registration methods should be matched"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA1410"
  - "ComRegistrationMethodsShouldBeMatched"
helpviewer_keywords:
  - "CA1410"
  - "ComRegistrationMethodsShouldBeMatched"
ms.assetid: f3b2e62d-fd66-4093-9f0c-dba01ad995fd
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1410: COM registration methods should be matched

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|Category|Microsoft.Interoperability|
|Breaking change|Non-breaking|

## Cause

A type declares a method that is marked with the <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> attribute but does not declare a method that is marked with the <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> attribute, or vice versa.

## Rule description

For Component Object Model (COM) clients to create a .NET type, the type must first be registered. If it is available, a method that is marked with the <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> attribute is called during the registration process to run user-specified code. A corresponding method that is marked with the <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> attribute is called during the unregistration process to reverse the operations of the registration method.

## How to fix violations

To fix a violation of this rule, add the corresponding registration or unregistration method.

## When to suppress warnings

Do not suppress a warning from this rule.

## Example

The following example shows a type that violates the rule. The commented code shows the fix for the violation.

[!code-csharp[FxCop.Interoperability.ComRegistration#1](../code-quality/codesnippet/CSharp/ca1410-com-registration-methods-should-be-matched_1.cs)]
[!code-vb[FxCop.Interoperability.ComRegistration#1](../code-quality/codesnippet/VisualBasic/ca1410-com-registration-methods-should-be-matched_1.vb)]

## Related rules

[CA1411: COM registration methods should not be visible](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## See also

- <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>
- [Register Assemblies with COM](/dotnet/framework/interop/registering-assemblies-with-com)
- [Regasm.exe (Assembly Registration Tool)](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)