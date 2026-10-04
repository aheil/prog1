# Versionsverwaltungssystem

Es gibt alternative Bezeichnungen:

* Version Control Systems (VCS)
* Source Control Management (SCM)
* Revision Control Systems (RCS)

Herausforderung bei der Verwaltung von Quell-Code:

1. Software-Projekte können schnell sehr groß und unübersichtlich werden und **hunderte bzw. tausende von Code-Dateien enthalten.**
2. **Sehr viele** **Entwickler** (2, 10, hundert, oder sogar tausend) können an einem Projekt beteiligt sein.

Versionsverwaltungen können helfen diese Komplexität in den Griff zu bekommen, indem die **Änderungen an den Dateien über die Zeit hinweg protokolliert** werden.

Versionsverwaltungen lassen pro Datei die Änderungen nachvollziehen.\
Das heißt: **wer** hat **was wann geändert**.

So eine Historie ist auch **für einzelner Entwickler sinnvoll**:

* **Änderungen über die Zeit** nachvollziehen
* "**Zurückrollen**" zu einem bestimmten Zeitpunkt
* **Löschen** ohne Reue

Was wäre bei einem Entwickler die Alternative?

Viele (sehr viele) Kopien einer Datei anfertigen: jeden Tag, nach jeder Änderung. Wie werden die Änderungen protokolliert? Wie kann man das bei sehr vielen Dateien praktikabel gestalten.

Bei mehreren Entwicklern kommen weitere Herausforderungen hinzu:

* Wie kommen die anderen -Entwickler&#x20;
* Wie kann man sehen, we**r welche Änderungen** gemacht hat
* Wie lassen sich Konflikte auflösen, **wenn mehrere Entwickler Änderungen an der gleichen Datei** (insb. der gleichen Zeile) durchgeführt haben?

Was wäre die Alternative? Code-Dateien per E-Mail verschicken?  Es scheint also keinen guten Weg zu geben, Änderungen möglichst geschickt und zeitsparend zu verwalten.

**Versionierung** von Quell-Code erlaubt all die zuvor genannten Probleme zu lösen, außerdem lässt sich der

* **Zustand eines Projekts wiederherstellen**: zum **Testen**, für ein **Release** oder um die Einführung eines Fehlers zu finden bzw. den Bug zu beheben.
