## Level 13

### Analyse
Le binaire affiche :

```text
UID 2013 started us but we we expect 4242
```
le programme vérifie l’UID avec getuid() avant d’exécuter getflag

### Exploitation
On utilise gdb pour modifier la valeur de retour de getuid()

```bash
break getuid
run
finish
set $eax = 4242
continue
```
