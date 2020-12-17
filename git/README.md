# Git
Alles zum Git und Github. Es wird von der Konsole / Linux aufgerufen.



### git clone

Ein Repository von Github clonen. Das Verzeichniss `docs` wird im aktuellen Verzeichnis erstellt

    git clone https://github.com/rkruggel/docs.git

### git commit

Wenn Änderungen gemacht wurden muss commitet werden

    git add --all
    git commit -m "First commit"

Es erscheint so etwas:

    [main a8e0fde] First commit
     6 files changed, 22 insertions(+), 2 deletions(-)
     create mode 100644 .ztr-directory
     create mode 100644 git/.ztr-directory
     create mode 100644 git/README.md
     create mode 100644 php/.ztr-directory
     create mode 100644 php/README.md


### git push
schreibt alle commits in das Repository.

    ~/Develop/docs$ git push -u origin
    
Es erscheit so etwas

    Username for 'https://github.com': rkruggel
    Password for 'https://rkruggel@github.com': 
    Objekte aufzählen: 10, Fertig.
    Zähle Objekte: 100% (10/10), Fertig.
    Delta-Kompression verwendet bis zu 8 Threads.
    Komprimiere Objekte: 100% (6/6), Fertig.
    Schreibe Objekte: 100% (8/8), 905 Bytes | 905.00 KiB/s, Fertig.
    Gesamt 8 (Delta 0), Wiederverwendet 0 (Delta 0)
    To https://github.com/rkruggel/docs.git
       3594b25..a8e0fde  main -> main
    Branch 'main' folgt nun Remote-Branch 'main' von 'origin'.
    roland@roland-desktop:~/Develop/docs$ 



