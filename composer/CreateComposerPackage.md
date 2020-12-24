# Erstellen einer Composer-Paketbibliothek

> In diesem Beitrag erfährst du, wie du eine PHP-Bibliothek erstellen, die über Composer problemlos in jede PHP-Anwendung integriert werden kann.

Roland Kruggel, Dezember 2020

copy and translation from [here](http://www.darwinbiler.com/creating-composer-package-library/)


Einer der Hauptgründe für alte PHP-Anwendungen ist, dass PHP-Entwickler dazu neigen, Ausschnitte von Code aus dem Internet überall, ohne jede Art von Struktur, Testprozess und Abhängigkeitsmanagement, zu kopieren und einzufügen. Dies macht jede PHP-Anwendung zu einem großen Schlammball, der immer mehr Schlamm ansammelt, wenn er auf einem anderen monkey-coder vorbeirollt, der versucht, Änderungen wie möglich durch Schneiden von Ecken und Anwenden schneller Patches umzusetzen.

> Sei nicht Teil dieses Problems. Kapsel deinen code in eine wiederverwendbare Bibliothek!

Dieser Beitrag soll dir das Leben als Bibliotheksautor so einfach wie möglich machen, indem er dir zeigt, wie du eine neue Bibliothek mit möglichst wenigen Schritten implementieren kannst.

### Erstelle die Projektordnerstruktur

Führe folgendes in deiner Konsole aus (Du musst natürlich zuerst Composer installiert haben). Die **Mylibrary** im Befehl ist der Name deiner Bibliothek. Ersetze sie daher durch den tatsächlichen Namen.

    composer create-project buonzz/composer-library-template mylibrary

was ist passiert?

Nicht viel, es wird nur eine neue Bibliothek unter dem Ordner *mylibrary* erstellt. Schauen wir uns die generierten Dateien an.

* **src** enthält Ihren Code. Jede Klasse muss sich in einer eigenen Datei in diesem Ordner befinden.
* **tests** jede Klasse, die du in dem src-Ordner schreibst, muss/sollte getestet werden bevor sie überhaupt an einer anderen Stelle benutzt werden kann. Grundsätzlich haben wir dort Testklassen, um andere Klassen zu testen.
* **.gitignore** Es gibt bestimmte Dateien, die wir nicht in Git veröffentlichen möchten. Deshalb fügen wir sie einfach zu dieser Datei hinzu, damit sie "von Git ignoriert werden".
* **LICENSE** Bedingungen, wie viel Freiheit andere Programmierer diese Bibliothek nutzen dürfen.
* **README.md** ist eine Mini-Dokumentation der Bibliothek. Dies ist normalerweise die "Homepage" Ihres Repos, wenn du es in GitHub und Packagist veröffentlicht hast.
* **composer.json**  werden die Informationen zu Ihrer Bibliothek gespeichert, z. B. Paketname, Autor und Abhängigkeiten.
* **phpunit.xml** Es ist eine Konfigurationsdatei von PHPUnit, damit Testklassen die von dir geschriebenen Klassen testen kannst.

Dies ist die grundlegende Struktur, mit der du beginnen kannst.

### Passe die generierten Dateien an

Du sehst eine Beispielklasse, die unter **src/YourClass.php** generiert wurde. Du musst dies mit dem tatsächlichen Klassennamen umbenennen. Denke daran, dass du nicht mehrere Klassen in der selben PHP-Datei einfügen sollst. Daher sollte der Klassenname, den du für diese Datei auswählst, auch mit dem Dateinamen übereinstimmen. Wenn du eine weitere Klasse schreiben musst, erstelle eine neue Datei.

#### Namensraum

Es wird empfohlen, jede Ihrer Klassen mit einem Namespace zu versehen, damit deine Klassen nicht mit einem anderen Klassennamen kollidieren, wenn sie von einer Anwendung verwendet werden. Normalerweise ist der gute Namespace Ihr GitHub-Benutzername. In meinem Fall ist mein GH-Benutzername beispielsweise ???Buonzz. Daher ist es sinnvoll, einen Namespace wie **???Buonzz\MyLibrary zu haben**

Im Allgemeinen sollte jede Klasse, die du **erstellst**, unter der Syntax **VendorName\PackageName** leben. Dies sollte die erste Zeile jeder Klasse in Ihrer Bibliothek sein.

    <?php 
    namespace ???Buonzz\Template;

Im obigen Beispiel lautet der VendorName Buonzz und der Paketname Template. Du musst eine eigene auswählen und sicherstellen, dass diese konsistent in allen PHP-Dateien in dieser Bibliothek abgelegt ist.

Du musst auch die Datei **composer.json** bearbeiten, um diese Änderungen dort widerzuspiegeln.

    "name": "vendorname/packagename"

Dann

    "psr-4": { "VendorName\\PackageName\\": "src/" }

Die obigen Informationen werden von packagist.org verwendet, um den Namen deines Pakets zu identifizieren, und das zweite Snippet ermöglicht es dem Autoloader, genau zu wissen, in welchem Namespace Ihre Klassen gefunden werden sollen.

#### Passe das Branding an

Als Nächstes musst du eine kleine Beschreibung des Verwendungszwecks dieser Bibliothek sowie Schlüsselwörter hinzufügen, um dieses Paket auf packagist.org leicht zu finden. Du gibst auch die Autoreninformationen mit deinem Namen an. Dies alles kann auch in composer.json angepasst werden

    "description": "this is my very own php package.",    "keywords": ["mypackage", "composer", "package"], 
    "license": "DBAD", 
    "authors": [ { "name": "Your Name", "email": "your email" } ]

Überprüfe anschließend deine Datei composer.json, um sicherzustellen, dass du beim Ausführen der Anpassungen keinen Tippfehler gemacht hast.

    composer validate

Danach musst du die enthaltene Datei README.md anpassen. Es handelt sich im Grunde genommen um eine kurze Dokumentation zu dem Zweck, den Anforderungen und der Verwendung dieser Bibliothek. Eine ausführlichere Dokumentation zum Erstellen einer README-Datei findest du [hier](http://www.darwinbiler.com/designing-and-making-the-readme-file-for-your-github-repository/).

#### Schreibe die Testklasse

Im Testordner befindet sich eine Anbietertestklasse. Dies wird als "YourClassTest.php" bezeichnet. Der bereitgestellte Code überprüft einfach die entsprechende Klasse, wenn ein Syntaxfehler vorliegt. Denke daran, dass jeder Klasse im Ordner src eine Testklasse zugeordnet sein sollte. Der Name der Testklasse sollte mit der Klasse übereinstimmen, die getestet wird, plus "Test" -String am Ende. Wenn du also eine **src/Utils.php** Klasse haben, benötigst du auch **test/UtilsTest.php**

Wir verwenden eine Bibliothek namens PHPUnit, um diesen Testprozess zu vereinfachen. Um PHPUnit zu installieren, musst du es zuerst installieren.

    composer install

Dadurch wird phpunit in **vendor/bin/phpunit** installiert

Bearbeite nun die **Testklasse** mit Ihrem eigenen Namespace, indem du die **???Buonzz\Template** Namespaces durch deinne eigenenersetzen. Führe danach die PHPUnit aus, indem du sie in der Konsole ausführst.

    vendor/bin/phpunit

Es sollte Erfolg haben, und du kannst diesen Entwicklungszyklus fortsetzen, bis du alle deine Klassen und die entsprechenden Testklassen geschrieben hast. Das Testen von Einheiten ist ein sehr komplexes Thema. Wenn du also mehr über die Idee erfahren möchtest, helfen dir die folgenden Links weiter.

* [TDD](https://en.wikipedia.org/wiki/Test-driven_development)
* [PHPUnit](https://phpunit.de/getting-started.html)

> Du solltest deine Bibliothek so gestalten, dass sie selbst getestet werden kann, ohne externe Abhängigkeiten (Datenbanken, API, Klassen / Funktionen in einem anderen CMS oder einer anderen Bibliothek) so weit wie möglich zu berücksichtigen.

### Veröffentliche deine Arbeit

> Stelle vor dem veröffentlichen deines Pakets sicher, dass du das Feld "Typ" in der Datei composer.json in "Library" geändert hast. Auf diese Weise erkennt packagist.org Ihr Paket als Bibliothek.

Sobald du mit dem Schreiben deiner Klassen fertig bist und diese vollständig getestet hast, ist es zeit deine Arbeit zu veröffentlichen. Du musst über ein Konto bei den folgenden Websites verfügen, bevor du deine Arbeit veröffentlichen kannst:

* GitHub.com
* Packagist.org

Melde dich an, wenn du noch kein Konto hast. Sobald du fertig bist, erstelle ein neues Repo in deinem Github-Konto. Das Repo sollte den gleichen Namen haben wie deine Bibliothek. Schiebe danach die Bibliothek zu diesem Repo.

Führe in der Konsole folgende Befehle, in dem Root-Direktory deiner Entwicklung, aus.

    git init
    git remote add origin git@github.com:yourusername/yourlibraryname.git
    git add --all
    git commit -m "initial files"
    git tag -a v1.0.0 -m "initial release"
    git push -u origin master
    git push --tags

??? Klicke anschließend im Repo auf die Registerkarte **Einstellungen**. Klicke **in** der linken Seitenleiste auf **Webhooks & Services**. Klicke auf der Registerkarte **Dienste auf** **Dienst** **hinzufügen.** Wählen Sie **Packagist**.

Dazu müssst du einen Benutzernamen in packagist zusammen mit dem Token eingeben.

Um das Token zu erhalten, gehe zu deiner [Profilseite](https://packagist.org/profile/) und klicke auf die Schaltfläche **Token** anzeigen, um das Token zu kopieren. Fügen Sie dieses Token in GitHub ein.

Jetzt können Sie Ihr Paket an packagist senden!

Gehen Sie zu [https://packagist.org/packages/submit](https://packagist.org/packages/submit) und fügen Sie die URL Ihres Github-Repos ein. Es kann eine Weile dauern, bis packagist Ihren Paketnamen und Ihre Bibliothek überprüft. Sobald dies erledigt ist, ist Ihr Paket jetzt in packagist verfügbar!

Um deine Bibliothek einfach zu nutzen

    composer init
    composer require yourusername/yourpackagename

Erstelle dann eine index.php-Datei, die den Autoloader lädt

    require 'vendor/autoload.php';

Alle Klassen in deiner Bibliothek sind jetzt einsatzbereit.

---

### Fanden Sie das nützlich?

Ich helfe immer gerne! Du kannst deine Unterstützung und Wertschätzung zeigen, indem du [mir einen Kaffee kaufst](https://www.buymeacoffee.com/rkruggel) .












