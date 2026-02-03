## Level 01

### Analyse
On inspecte le fichier /etc/passwd qui liste tous les utilisateurs du système. Le mot de passe de l'utilisateur flag01 y est directement stocké sous forme de hash.

```bash
$ cat /etc/passwd | grep flag01
flag01:42hDRu9IW9p6:1001:1001:flag01:/home/flag/flag01:/bin/bash
```
On identifie le hash suivant : 42hDRu9IW9p6.

### Exploitation
Pour cracker ce mot de passe, on utilise le programme John the Ripper. On isole le hash dans un fichier local, puis on lance l'outil pour effectuer une attaque par dictionnaire ou par force brute.

```bash
$ echo "flag01:42hDRu9IW9p6" > /tmp/password.txt
$ john /tmp/password.txt
...
abcdefg          (flag01)
```
