## Level 14

### Analyse
Il n’y a aucun binaire exploitable directement.  
La seule chose accessible est `getflag`.

On doit comprendre comment `getflag` décide quel flag afficher.

En analysant le binaire (strings, ltrace, gdb), on remarque une série de comparaisons sur l’UID.  
Le dernier flag est retourné uniquement si l’UID correspond à celui du level14.

### Exploitation
On attache `getflag` avec gdb et on force la valeur de retour de `getuid()`.

```bash
$ gdb /bin/getflag

(gdb) catch syscall ptrace
(gdb) commands 1
> set ($eax) = 0
> continue
> end

break getuid
run
finish
set $eax = 3014
continue
```

Le programme croit être exécuté par le bon utilisateur et affiche le dernier flag.
