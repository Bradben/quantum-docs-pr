---
uid: Microsoft.Quantum.Diagnostics.DumpRegister
title: DumpRegister function
ms.date: 11/25/2020 12:00:00 AM
ms.topic: article
qsharp.kind: function
qsharp.namespace: Microsoft.Quantum.Diagnostics
qsharp.name: DumpRegister
qsharp.summary: Dumps the current target machine's status associated with the given qubits.
---

# DumpRegister function

Namespace: [Microsoft.Quantum.Diagnostics](xref:Microsoft.Quantum.Diagnostics)

Package: [Microsoft.Quantum.QSharp.Core](https://nuget.org/packages/Microsoft.Quantum.QSharp.Core)


Dumps the current target machine's status associated with the given qubits.

```qsharp
function DumpRegister<'T> (location : 'T, qubits : Qubit[]) : Unit
```


## Input

### location : 'T

Provides information on where to generate the state's dump.


### qubits : [Qubit](xref:microsoft.quantum.lang-ref.qubit)[]

The list of qubits to report.



## Output : [Unit](xref:microsoft.quantum.lang-ref.unit)

None.

## Type Parameters

### 'T



## Remarks

This method allows you to dump the information associated with the state of the