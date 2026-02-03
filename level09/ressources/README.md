## Level 09

### Analyse
Le fichier token contient des données chiffrées. Le binaire level09 semble appliquer un décalage progressif : le caractère à la position $i$ subit un décalage ASCII de $+i$.

```bash
$ ./level09 aaaa
abcd
$ .level09 bbbb
bcde
```

### Exploitation
Pour retrouver le mot de passe original, il faut inverser l'algorithme ($char[i] - i$). On utilise un programme C dédié :

```c
#include <unistd.h>
int main(int ac, char **av) {
    int i = 0;
    char c;
    while (av[1][i]) {
        c = av[1][i] - i;
        write(1, &c, 1);
        i++;
    }
    write(1, "\n", 1);
}
```
