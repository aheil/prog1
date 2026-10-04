# Übungen Einheit 1

## Aufgabe 1.1

Erstelle eine neue Java‑Datei mit dem Namen **`Student.java`**.

1. Implementiere eine Klasse **`Student`** mit folgenden Feldern:

```java
String name;
String firstName;
int studentId;
int age;
String address;
String phoneNumber;
String email;
```

2. Kompiliere die Datei (`javac Student.java`) und führe die Klasse Student aus (`java Student`).
3. Was passiert, wenn du die Klasse ausführst?
4. Was könnte man tun, damit sich die Klasse ausführen lässt?

**Zur Erinnerung**: Wenn eine Klasse ein "Bauplan" für ein Objekt ist, dann sind Felder (engl. fields) die Eigenschaften, die dieses Objekt haben wird.&#x20;

Wichtige Merkmal von Feldern:&#x20;

* Sie werden **innerhalb** einer Klasse, aber **außerhalb** von Methoden definiert.
* Sie speichern den **Zustand** eines Objekts.
* Sie können verschiedene Sichtbarkeiten haben (`public`, `private`, …).
* Jedes Objekt erhält **seine eigene Kopie** dieser Felder.

## Aufgabe 1.2

Während der Vorlesung hast du bereits den Modifie&#x72;**`public`** kennengelernt, der für Klassen und Methoden verwendet wurde.

Wende nun den Modifier **`private`** auf jedes Feld in deinem Code an, z. B. `private String name`.

1. Was könnte es bedeuten, wenn du diesen Modifierauf ein Feld anwendest?\
   Lies dazu bitte die entsprechende Java‑Dokumentation unter:\
   https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html
2. **Kompiliere** die Datei `Student.java` (`javac Student.java`) und stelle sicher, dass keine Fehler auftreten.

## Aufgabe 1.3

1. Schreibe für jedes Feld eine sogenannte **Setter‑Methode**, die es dir ermöglicht, auf das entsprechende Feld zuzugreifen, auch wenn es `private` ist.\
   \
   Benenne die Methoden passend zu dem Feld, das du setzen möchtest, z. B.\
   `setName()`, `setAge()` usw.

Beispiel:

```java
public void setName(String name) {
  this.name = name;
}
```

**Hinweis**: Im Gegensatz zu einem Konstruktor erlaubt dir eine Setter‑Methode, den Wert jedes Feldes **einzeln** zu setzen. Außerdem kann die Setter-Methode auch aufgerufen werden, nachdem das Objekt einmal erzeugt wurde.&#x20;

2. Für das Feld `name` kopiere folgende Methode in deine Klasse:

```java
public void getName() {
  return this.name; 
} 
```

3. Kompiliere die Datei. Was passiert, wenn Du versuchst die Datei zu kompilieren?
4. Ändere deinen Code und ersetze das Schlüsselwort **`void`** im obigen Code durch **`String`**.
5. Kompiliere die Datei **`Student.java`** erneut.
6. Implementiere ähnliche **Getter‑Methoden** für jedes Feld in der Klasse.\
   Benutze die jeweils passenden **Rückgabetypen** und wähle passende Methodennamen.

**Hinweis**: Getter Methoden ermöglichen es, private Felder einer eines Objektes auszulesen.
