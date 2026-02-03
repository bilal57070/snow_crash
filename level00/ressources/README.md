## Level 00

### Analyse
Recherche sur le user cible : flag00

```bash
$ find / -user flag00 2> /dev/null
/usr/sbin/john
/rofs/usr/sbin/john
```

### Exploitation
On découvre un fichier nommé john. En affichant son contenu avec cat, on obtient une chaîne de caractères : cdi9604324636.

Cette chaîne est chiffrée via un code de César (ROT). En utilisant un outil de décodage comme dCode, on trouve le mot de passe en clair.
