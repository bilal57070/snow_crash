## Level 09

### Analyse
on trouve un fichier nommé level02.pcap. Un fichier PCAP est une capture de trafic réseau contenant l'intégralité des paquets ayant circulé sur une interface donnée. Pour analyser ces données, on peut utiliser des outils comme Wireshark (interface graphique) ou tcpdump (ligne de commande).

```bash
$ tcpdump -A -r level02.pcap
```

### Exploitation
En examinant les paquets de la session Telnet (un protocole non sécurisé où les données circulent en clair), on peut isoler la saisie du mot de passe.

Point crucial : L'analyse doit se faire caractère par caractère. Certains octets particuliers apparaissent, représentés par un . dans le terminal. Ces caractères correspondent en réalité à la touche "Retour arrière" (Backspace) du clavier (code ASCII 127).

Si on voit ft_p.a.ssword, cela signifie :

1. ft_p 
2. Effacer le p
3. a
4. Effacer le a
5. ssword

Le mot de passe final doit donc être reconstruit en appliquant manuellement ces suppressions.

Mot de passe final : "ft_waNDReL0L"
