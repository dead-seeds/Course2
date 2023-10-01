A program that [[fork]]s (which is pretty fast) in an endless loop and eventually [[Kernel]] runs out of space -> computer explodes
```
for (i = 0; i < n; i++)
	fork();
```
#ask Is there a limited amount of space for process structs?