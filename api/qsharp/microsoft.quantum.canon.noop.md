---
uid: Microsoft.Quantum.Canon.NoOp
title: NoOp operation
ms.date: 11/25/2020 12:00:00 AM
ms.topic: article
qsharp.kind: operation
qsharp.namespace: Microsoft.Quantum.Canon
qsharp.name: NoOp
qsharp.summary: Performs the identity operation (no-op) on an argument.
---

# NoOp operation

Namespace: [Microsoft.Quantum.Canon](xref:Microsoft.Quantum.Canon)

Package: [Microsoft.Quantum.QSharp.Core](https://nuget.org/packages/Microsoft.Quantum.QSharp.Core)


Performs the identity operation (no-op) on an argument.

```qsharp
operation NoOp<'T> (input : 'T) : Unit is Adj + Ctl
```


## Description

This operation takes a value of any type and does nothing to it.

## Input

### input : 'T

A value to be ignored.



## Output : [Unit](xref:microsoft.quantum.lang-ref.unit)



## Type Parameters

### 'T



## Remarks

In almost all cases, the type parameter for `NoOp` needs to be specified

## See Also

- [Microsoft.Quantum.Intrinsic.I](xref:Microsoft.Quantum.Intrinsic.I)