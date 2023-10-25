A state of a [[Process]] when it _spins_ in an empty loop until the resource becomes available. Typically done using [[Compare and set]]:
```
while (CAS(flag, 1)) {}
```