# Ein bestehendes Projekt weiterentwickeln

## Ausgangssituation

Es besteht ein Composer Projekt welches in den Ansätzen sehr gut ist, jedoch so einige Dinge nicht kann die ich gerne haben möchte. Da seit fast einem Jahr keine Pullrequests mehr eingefügt worden sind und es im allgemeinen so aussieht als ob das Projekt verwaist ist möchte ich aus diesem Projekt einen Entwicklungszweig abspalten. Man muss ja nicht jedes Rad neu erfinden. Von der Lizens her gesehen ist das auch möglich. Das Projekt steht unter der MIT-Lizenz. 

Das konkrete Projekt sind hier [laravel-livewire-forms](https://github.com/kdion4891/laravel-livewire-forms) und [laravel-livewire-tables](https://github.com/kdion4891/laravel-livewire-tables) von dem User [kdion4891](https://github.com/kdion4891). Als Beschreibungsbeispiel werde ich hier  [laravel-livewire-forms](https://github.com/kdion4891/laravel-livewire-forms) nehmen.

## Schritt 1
Von dem original Projekt erstelle ich einen clone. Ich nehme dazu die Konsole.

> git clone https://github.com/kdion4891/laravel-livewire-forms.git

Dieses erzeugt das Directory *laravel-livewire-forms*. Dann lösche ich die Verbindung zum Git repositore von Kdion4891 weil ich ja nicht sein Projekt weiter führen will sonder ein eigenes machen will.

> cd laravel-livewire-forms
> rm -rf .git

Jetzt habe ich das rohe Original.

## Schritt 2
Ein lokales Git Repository erstellen und alle Daten bereit stellen.
Dieses führe ich alles auf der Konsole aus.

> git init

Das Repository ist jetzt da. Um nich allen Blödsinn zu 
veröffentlichen muss eine *.gitignore* her. 

    vendor/
    node_modules/

    public/storage
    public/hot
    public/css/tmpcompile
    public/ace/
    public/jqwidgets/

    storage/*.key
    .env
    Homestead.yaml
    Homestead.json
    .phpunit.result.cache
    .ztr-directory
    *.log

Nun alle files dem Repository hinzufügen und committen

> git add *   
> git commit -m 'Initial commit'

sdfgsdgfsd sdf













## Schritt 3
Erste Veröffentlichung auf Github. Ab jetzt sind schon mal alle
Daten save.