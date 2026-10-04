# Einheit 8

## Iterable\<T>

**tl;dr**\
Iterable = eine Sammlung, über die man Elemente der Reihe nach durchlaufen kann.

Andres ausgedrückt: Ein Objekt, das das Iterable-Interface implementiert, ermöglicht es, seine Elemente nacheinander zu durchlaufen.&#x20;

### **Aufgabenstellung**

#### **Variante 1 - Object Box**

Wir entwickeln eine generische Box, in die wir Elemente eines bestimmten Datentyps hinzufügen können und alle Elemente nacheinander zu durchlaufen - ohne zu wissen wie viele Elemente sich in der box befinden.&#x20;

Wir beginnen mit einer leeren Box. Diese wird mit einem Array von Objekten initialisiert. Das Array hat zu Beginn die Länge null.

{% code lineNumbers="true" %}
```java
public class Box {
  private Object[] values = new Object[0];
}
```
{% endcode %}

Fügen wir nun eine Methode hinzu, um ein Element hinzuzufügen.&#x20;

{% code lineNumbers="true" %}
```java
public class Box {
  private Object[] values = new Object[0];

  public void add(Object element) { 
    // Hier wollen wir ein Element hinzufügen
  }
}
```
{% endcode %}

Da sich ein Array nicht einfach so erweitern lässt, erzeugen wir ein neues Array, das genau ein Element mehr hat, als das bereits existierende.&#x20;

<pre class="language-java" data-line-numbers><code class="lang-java"><strong>public class Box {
</strong>  private Object[] values = new Object[0];

  public void add(Object element) { 
    Object[] newValues = new Object[values.length + 1];
    // Hier wollen wir immer noch ein Element hinzufügen
  }
}
</code></pre>

Nun müssen wir alle Elemente aus dem bereits existierenden Array in das neue Array kopieren. Dies erledigen wir mit einer einfachen _for_-Schleife. Dabei wird jedes Element an Stelle _index_ im bereits existierenden Array an die gleiche Stelle des neuen Arrays kopiert.&#x20;

{% code lineNumbers="true" %}
```java
public class Box {
  private Object[] values = new Object[0];

  public void boolean add(Object element) { 
    Object[] newValues = new Object[values.length + 1];
    for (int index = 0; index < values.length; index++) {
      newValues[index] = values[i];
    }
    // Hier wollen wir immer noch ein Element hinzufügen
  }
}
```
{% endcode %}

Das das neue Array Platz für ein Element mehr hat, können wir an diese Stelle nun das neue Element kopieren.

{% code lineNumbers="true" %}
```java
public class Box {
  private Object[] values = new Object[0];

  public void add(Object element) { 
    Object[] newValues = new Object[values.length + 1];
    for (int index = 0; index < values.length; index++) {
      newValues[index] = values[i];
    }
    newValues[values.length] = element;
  }
}
```
{% endcode %}

Sobald die Methode beendet wurde wird nun das neue Array wieder gelöscht. Da es sich um eine (in der Methode) lokale Variable handelt, kann der Garbage Collector den Speicherbereich nach Beendigung der Methode wieder freigeben. Auf der andern Seite hat das alte Array immer noch nur die Elemente von vorher. Das alte Array wurde von uns nicht verändert.&#x20;

Deswegen setzen wir nun an die Stelle des alten Array das neue. Nach dem Beenden der Methode kann somit auf das neue Array zugegriffen werden. Das alte Array wird vom Garbage Collector gelöscht, da dieses nicht mehr referenziert wird.&#x20;

{% code lineNumbers="true" %}
```java
public class Box {
  private Object[] values = new Object[0];

  public void add(Object element) { 
    Object[] newValues = new Object[values.length + 1];
    for (int index = 0; index < values.length; index++) {
      newValues[index] = values[i];
    }
    newValues[values.length] = element;
    values = newValues;
  }
}
```
{% endcode %}

Bei genauerer Betrachtung hat die Methode noch einen Schwachpunkt - sie erlaubt es uns anstelle eines Objekts einfach _null_ zu übergeben. Das macht kein Probleme biem hinzufügen, aber später, sollten die Werte ausgelesen werden, kann dies zu Problemem führen, wenn der Aufrufer anstelle eines Objekts einfach _null_ erhält.

Um dies zu verhindern können wir z.B. Expections werfen, wenn dies versucht wird - oder die Methode robuster gestalten, indem Sie dies nicht zulässt.

Hierfür ändern wir die Signatur der Methode und liefern einen boolschen Wert zurück, ob das Hinzufügen funktioniert hat.&#x20;

{% code lineNumbers="true" %}
```java
public class Box {

  private Object[] values = new Object[0];

  /**
   * Adds a non-null element to the end of this box.
   * 
   * @param element the element to add
   * @return true if the element was added; false if element is null
   */
  public boolean add(Object element) {

    if (element == null) {
      return false;
    }

    Object[] newValues = new Object[values.length + 1];

    for (int i = 0; i < values.length; i++) {
      newValues[i] = values[i];
    }

    newValues[values.length] = element;
    return true;
  }

}
```
{% endcode %}

Sollte der Aufrufer versuchen den Wert _null_ hinzuzufügen kehren wir aus der Methode zurück und liefern den Wert _false_ an den Aufrufer.&#x20;

Nach dem erfolgreichen Hinzufügen des neuen Wertes[^1] liefert die Methode _true_ zurück.

Nun wollen wir erreichen, dass wir alle Elemente in der Box durchlaufen können. Da wir nicht wissen wie viele Elemente sich gerade in der Box befinden, muss die Box hierfür Buch führen. Hierzu führen wir einen Zähler ein, der die Position angibt, in dem wir uns gerade befinden.&#x20;

{% code lineNumbers="true" %}
```java
public class Box {

  private Object[] values = new Object[0];
  int position = 0;
  
  // vorheriger Code... 
  
}
```
{% endcode %}

Die Idee dahinter ist nun, dass wir ein Element nach dem anderen aus der Box holen und dabei die Position hoch zählen. Hierfür implementieren wir eine Methode die uns das nächste Element aus der Box gibt.&#x20;

{% code lineNumbers="true" %}
```java
public class Box {

  private Object[] values = new Object[0];
  int position = 0;

  public Object next() {
      return values[position++];
  }
  
  // vorheriger Code...
  
}
```
{% endcode %}

Wir liefern hierzu das Element aus dem Array an der Stelle position und erhöhen diese direkt danach um 1. Die Positfix-Notation ist hier notwenidg, da wir nach dem _return_ den Wert nicht mehr erhöhen könnne. In dieser Schreibweise lesen wir den Wert aus _position,_ greifen auf das entsprechende Element zu, erhöhen dann den Wert, der in _position_ steht um 1 und geben das zuvor ausgelesene Element zurück.&#x20;

Im vorliegenden Fall würde nach dem ersten Aufruf _position_ nun auf 1 stehen und beim nächsten Zugriff ein Fehler auftreten. Konkret wird beim nächsten Aufruf von _next_ eine _IndexOutOfBoundsException_ auftreten.&#x20;

Damit der Aufrufer dies vermeiden kann, bieten wir eine Möglichkeit an abzufragen, ob es überhaupt noch ein Element in der box gibt.&#x20;

{% code lineNumbers="true" %}
```java
  public class Box {

  private Object[] values = new Object[0];
  int position = 0;

  public Object next() {
      return values[position++];
  }
  
  public boolean hasNext() {
    return (position < values.length);
  }
  
  // vorheriger Code
  
}
```
{% endcode %}

Die Methode _hasNext_ in Zeile 10 macht genau das. Sie prüft ob die aktuelle Position kleiner der Anzahl der Elemente im Array ist. Bei 0 Elementen liefert der Wert 0 in position _false_.&#x20;

Ein Aufrufer kann nun durch die Liste gehen indem er die beiden Methoden hasNext und next wie in den Zeilen 9 bis 11 nutzt.

{% code lineNumbers="true" %}
```java
 public class BoxTest {
  public static void main(String[] args) {

    Box box = new Box();
    box.add("Hallo");
    box.add("Welt");
    box.add(42);

    while (box.hasNext()) {
      System.out.println(box.next());
    }
  }
}
```
{% endcode %}

Der Beispielcode funktioniert und liefert&#x20;

```
Hallo                                                                                            
Welt                                                                                             
42 
```

Allerdings sind die beide ersten Werte Strings und der dritte Wert ein Integer. Problematisch könnte dies werden, wenn wir uns als Aufrufer darauf verlässt, dass sich in der Box nur Objkekte eines bestimmten Typs befinden (z.B. Integer).

#### Variante 2 - Generische Box&#x20;

Um dem Aufrufer mehr Sicherheit zu geben überführen wir die Box nun in eine generische Box.&#x20;

Wir wollen nun das interne Object Array beibehalten. Da wir in Java kein generisches Array erzeugen können, ist es notwendig in Zeile 8 einen Cast auf den Typ T durchzuführen. Java sieht diesen Cast allerdings als unischer an, weswegen der Compiler eine Fehlermeldung bzw. ein Warning liefern wird.&#x20;

Um diese Warnung zu ignorieren nutzen wir die Annotation `@SuppressWarnings("unchecked")` . Wir können es diesem Fall mit gutem Gewissen tun, da wir beim Hinzufügen in der _add_-Methode nur Elemente des Typs T zulassen.&#x20;

Da das Array _values_ als _privat_ gekennzeichnet ist, ist es nicht möglich, dass auf anderem Weg etwas anderes als ein Element vom Typ T hinzugefügt wird.&#x20;

{% code lineNumbers="true" %}
```java
public class Box<T> {

  private Object[] values = new Object[0];
  int position = 0;

  @SuppressWarnings("unchecked")
  public T next() {
    return (T) values[position++];
  }

  public boolean hasNext() {
    return position < values.length;
  }

  /**
   * Adds a non-null element to the end of this box.
   * 
   * @param element the element to add
   * @return true if the element was added; false if element is null
   */
  public boolean add(T element) {

    if (element == null) {
      return false;
    }

    Object[] newValues = new Object[values.length + 1];

    for (int i = 0; i < values.length; i++) {
      newValues[i] = values[i];
    }

    newValues[values.length] = element;
    values = newValues;
    return true;
  }

}
```
{% endcode %}

Wir können nun dei generische Box wie zuvor testen. Da die konkrete Box nun eine "Box of String" ist, können nur Strings hinzugefügt werden - und die next-Methode liefert immer einen String zurück.&#x20;

```java
public class BoxTest {
  public static void main(String[] args) {

    Box<String> box = new Box<String>();
    box.add("Hallo");
    box.add("Welt");
    box.add("42");

    while (box.hasNext()) {
      System.out.println(box.next());
    }
  }
}
```

#### Idee wiederverwenden

Wir verwenden diese Idee so gut, dass wir dies nicht nur für die Klasse Box, sondern für so ziemlich alles verwenden möchten, in dem wir Elemente abspeichern können. z.B. Box, ReverseList, Tree etc.&#x20;

**Übung:** Kopiere die Datei Box.java in Tree.java und ReverseList.java und passe die Klassennamen entsprechend an, so dass wir drei Klassen Box, Tree und ReverseList haben.

Möchten wir nun Code schreiben, der auf diese Funktionalität zurückgreift, ist es erforderlich, dass wir alle diese Klassen kennen, in denen wir dies aufrufen möchten.&#x20;

Schreiben wir also eine kleine Klasse die uns die unterschiedlichen Datenstrukturen auf der Konsole ausgibt:&#x20;

{% code lineNumbers="true" %}
```java
public class ConsoleUtils {

  public static <T> void print(Box<T> box) {
    while (box.hasNext()) {
      System.out.println(box.next());
    }
  }

  public static <T> void print(Tree<T> tree) {
    while (tree.hasNext()) {
      System.out.println(tree.next());
    }
  }

  public static <T> void print(ReverseList<T> reverseList) {
    while (reverseList.hasNext()) {
      System.out.println(reverseList.next());
    }
  }
}
```
{% endcode %}

Wir finden die Idee so gut, dass wir nun auch die Klassen Queue und Graph auf die gleiche Art und Weise implementieren wollen. Nun müssen wir auch die ConsoleUtils Klasse erweitern.&#x20;

Wir erzeugen hiermit sehr viel identischen Code. Bei Änderungen müssen wir alles anpassen, und je mehr print Methoden wir haben, desto leichter schleichen sich Fehler ein, wenn diese Methoden angepasst werden müssen.&#x20;

#### Interface extrahieren

Bei genauer Betrachtung benötigen alle _print_ Methoden lediglich die Methoden _next_ und _hasNext_. Dabei ist uns gleichgültig um welche Art der Datenstruktur es sich handelt.&#x20;

Wenn alle Klassen (_Box_, _ReverseList_, _Tree_, _Queue_ und _Graph_) die gleichen Methoden anbieten, die wir nutzen möchten, könnten diese Methoden in einem Interface zusammenfassen. Alle Klassen bieten diese Methoden and um über den Inhalt zu iterieren. Daher ist es naheliegend das Interface Iterator zu nennen. Die jede Klasse bereits generisch ist, ist auch ein generisches Interface erforderlich.&#x20;

{% code lineNumbers="true" %}
```java
public interface Iterator<T> {
  public boolean hasNext();
  public T next();  
}
```
{% endcode %}

Examplarisch passen wir nun die Klasse Box an und lassen&#x20;

{% code lineNumbers="true" %}
```java
public class Box<T> implements Iterator<T> {

  private Object[] values = new Object[0];
  int position = 0;

  @SuppressWarnings("unchecked")
  @Override
  public T next() {
    return (T) values[position++];
  }
  
  @Override
  public boolean hasNext() {
    return position < values.length;
  }

  /**
   * Adds a non-null element to the end of this box.
   * 
   * @param element the element to add
   * @return true if the element was added; false if element is null
   */
  public boolean add(T element) {

    if (element == null) {
      return false;
    }

    Object[] newValues = new Object[values.length + 1];

    for (int i = 0; i < values.length; i++) {
      newValues[i] = values[i];
    }

    newValues[values.length] = element;
    values = newValues;
    return true;
  }

}
```
{% endcode %}

Die einzigen Änderungen sind in Zeile 1, 7 und 12. Wir haben die Methoden als überschreiben gekennzeichnet und das Interface somit implementiert. Der Aufrufer kann sich nun darauf verlassen, dass jeder Klasse die Iterator\<T> implementiert über die beiden Methoden verfügt.

{% hint style="info" %}
Es geht bei der Verwendung von Schnittstellen somit nicht darum, was ein Objekt ist, sondern was es kann.&#x20;
{% endhint %}

Wir können nun unserer Helferklasse vereinfachen. Anstelle eine konkrete Implementierung pro Klasse, arbeiten wir nun nur noch mit dem Interface.

{% code lineNumbers="true" %}
```java
public class ConsoleUtils {

  public static <T> void print(Iterator<T> iterator) {
    while (iterator.hasNext()) {
      System.out.println(iterator.next());
    }
  }
}
```
{% endcode %}

Jedes Objekt einer Klasse, die unser _Iterator\<T>_ implementiert, kann nun dieser _print_-Methode übergeben werden. Auch wenn dies Klasse noch nicht existiert und erst in Zukunft geschreiben wird - sofern diese zukünftige Klasse das Interface implementiert, kann Sie in der _print-_&#x4D;ethode genutzt werden.&#x20;

Genau diesen Iterator gibt es bereits im Package java.util. Für nun in alle Klassen als erstes folgende Zeile hinzu, danach lösche die Iterator.java und _Iterator.class_ Datei. Ab nun nutzen sowohl die Box (und ggf. andere Klassen) als auch die _ConsoleUtils_ den Iterator aus der Java Klassenbibliothek.

{% code lineNumbers="true" %}
```java
import java.util.Iterator;
```
{% endcode %}

{% hint style="warning" %}
Stelle sicher, dass die _Iterator.java_ und ggf. die _Iterator.class_ Datei gelöscht sind.
{% endhint %}

{% code lineNumbers="true" %}
```java
import java.util.Iterator;

public class ConsoleUtils {

  public static <T> void print(Iterator<T> iterator) {
    while (iterator.hasNext()) {
      System.out.println(iterator.next());
    }
  }
}
```
{% endcode %}

und&#x20;

{% code lineNumbers="true" %}
```java
import java.util.Iterator;

public class Box<T> implements Iterator<T> { 
  // hier der restliche Code... 
} 
```
{% endcode %}

### Separation of Concerns&#x20;

Bei genauer Betrachtung führen nun unserer Behältnisse Aktionen aus, die eigentlich nicht in deren Zuständigkeit liegen. So kann man eine Box nicht wirklich fragen ob noch ein weiteres Element enthalten ist, oder die Box um das nächste Element bitten.&#x20;

Daher lagern wir diese gesamte Funktionalität nun in eine weitere Klasse aus und erstellen einen _BoxIterator._

{% code lineNumbers="true" %}
```java
import java.util.Iterator;

public class BoxIterator<T> implements Iterator<T> {

  private Box<T> box;
  int position;
  
  public BoxIterator(Box<T> box) {
    this.box = box;
    int position = 0;  
  }

  @Override
  public boolean hasNext() {
    return position < box.values.length;
  }

  @SuppressWarnings("unchecked")
  @Override
  public T next() {
    return (T) box.values[position++];
  }
}
```
{% endcode %}

Damit der BoxIterator auf die Felder der Box zugreifen kann, übergeben wir dem Iterator eine Box - und zwar genau die, über die er iterieren soll. Gleichzeitig setzen wir die Position im Iterator auf 0. Die Box muss sich nun nicht mehr merken, an welcher Stelle der Iterator steht.&#x20;

Der Code der Box hat sich dementsprechend vereinfacht.&#x20;

```java
public class Box<T> {

  public Object[] values = new Object[0];

  /**
   * Adds a non-null element to the end of this box.
   * 
   * @param element the element to add
   * @return true if the element was added; false if element is null
   */
  public boolean add(T element) {

    if (element == null) {
      return false;
    }

    Object[] newValues = new Object[values.length + 1];

    for (int i = 0; i < values.length; i++) {
      newValues[i] = values[i];
    }

    newValues[values.length] = element;
    values = newValues;
    return true;
  }
```

Da die Box selbst nun kein Iterator mehr ist, ist es erforderlich eine Methode zu implementieren, die einen BoxIterator zurückliefert.&#x20;

Wir fügen daher der Box folgende Methode hinzu:&#x20;

```java
  public Iterator<T> iterator() {
    return new BoxIterator<T>(this);
  }
```

Um neben der Box auch andere Behältnisse nach Iteratoren zu fragen, greifen wir wieder auf den Trick zurück und deklarieren diese Methode in einem eigenen Interface Iterable\<T> um die Box zu kennzeichnen, dass man durch ihren Inhalt durchiterieren kann, in dem man einen Iterator anfordert.

{% code lineNumbers="true" %}
```java
public interface Iterable<T> {
  public Iterator<T> iterator();
}
```
{% endcode %}

Danach lassen wir die Klasse Box (und alle andere Behältnisse) dieses Interface implementieren:&#x20;

{% code lineNumbers="true" %}
```java
public class Box<T> implements Iterable<T> {
  // vorheriger Code
}
```
{% endcode %}

Somit haben wir das Prinzip "Seperation of Concerns" umgesetzt. Unserer Box liefert uns einene Iterator, der Iterator führt die eigentliche Iteration, also das Durchlaufen der Elemente in der Box durch.&#x20;

Das Interface gibt es ebenfalls in der Java-Klassenbibliothek im Package `java.lang.Iterable;`

Nachem wir das eigene Iterable Interface wieder glöscht haben passen wir die Box entsprechend an, so dass der Code nun folgendermaßen aussieht. Der BoxIterator kann unverändert bleiben.

```java
import java.lang.Iterable;
import java.util.Iterator;

public class Box<T> implements Iterable<T> {

  public Object[] values = new Object[0];

  /**
   * Adds a non-null element to the end of this box.
   * 
   * @param element the element to add
   * @return true if the element was added; false if element is null
   */
  public boolean add(T element) {

    if (element == null) {
      return false;
    }

    Object[] newValues = new Object[values.length + 1];

    for (int i = 0; i < values.length; i++) {
      newValues[i] = values[i];
    }

    newValues[values.length] = element;
    values = newValues;
    return true;
  }

  /**
   * Returns an iterator for this box.
   * 
   * @return an iterator for this box.
   */
  @Override
  public Iterator<T> iterator() {
    return new BoxIterator<T>(this);
  }
}
```

### Overhead reduzieren

#### Ausgangspunkt

Für jeden weiteren Typen eines Behältnisses wäre es nun erforderlich einen eigenen Iterator analog zum Box Iterator zu implementieren.&#x20;

Weiterhin ist das Feld _values_ in der Box noch immer public. Um den Code robuster zu gestalte, sollte dies als private gekennzeichnet werden und der Zugriff über über eine Methode gekapslet werden.&#x20;

Allerdings führt auch dies wieder zu zusätzlichem Code.&#x20;

#### Inner Classes

Beide Punkte können wir in Java durch eine sog. Inner Class lösen. Hierbei wird eine Klasse nicht in einer eigenen Datei definiert - sondern direkt in einer anderen Klasse. Solche Inner Classes werden im Code einer anderen Klasse definiert. Sie sind nach außen nicht sichtbar, haben aber Zugriff auf die (privaten) Felder der äußeren Klasse.&#x20;

Mit kleinen Änderungen können wir somit den Code des BoxIterators direkt in die Box kopieren.&#x20;

{% code lineNumbers="true" %}
```java
import java.lang.Iterable;
import java.util.Iterator;

public class Box<T> implements Iterable<T> {

  public Object[] values = new Object[0];

  /**
   * Inner class providing an iterator for a box
   */
  class BoxIterator implements Iterator<T> {

    int position = 0;

    @Override
    public boolean hasNext() {
      return position < values.length;
    }

    @SuppressWarnings("unchecked")
    @Override
    public T next() {
      return (T) values[position++];
    }
  }

  /**
   * Adds a non-null element to the end of this box.
   * 
   * @param element the element to add
   * @return true if the element was added; false if element is null
   */
  public boolean add(T element) {

    if (element == null) {
      return false;
    }

    Object[] newValues = new Object[values.length + 1];

    for (int i = 0; i < values.length; i++) {
      newValues[i] = values[i];
    }

    newValues[values.length] = element;
    values = newValues;
    return true;
  }

  /**
   * Returns an iterator for this box.
   * 
   * @return an iterator for this box.
   */
  @Override
  public Iterator<T> iterator() {
    return new BoxIterator();
  }
}
```
{% endcode %}

Der Code für den Iterator findet sich in Zeile 11 bis 25. Da die Innere Klasse auf die Felder der aüßeren Klasse zugreifen kann, ist es nicht mehr notwendig die Instanz der Box an den Iterator zu übergeben. Die Position des Iterators lassen wir bei 0 beginnen, indem die Variable für einen neuen Iterator in Zeile 13 immer mit 0 initialisiert wird.&#x20;

In Zeile 57 erzeugen wir einen neuen BoxIterator und geben diesen zurück. Da die iterator Methode jedoch nur das Interface an den Aufrufer liefert, ist für den Aufrufer nicht ersichtlich ob es sich um ein BoxIterator, einen QueueIterator oder einen GraphIterator etc. handelt. Für den Aufrufer zählt lediglich, dass der die im Iterator spezifiziert Methoden aufrufen kann - und dies wird über das Interface sichergestellt.&#x20;

### Finale

Die for-each Schleife in Java nutzt genau diese Interfaces um über entsprechende Konstrukte (oder Behältnisse) für Objekte zu iterieren und die einzelnen Elemente zurückzuliefern.&#x20;

{% code lineNumbers="true" %}
```java
public class Main {
    public static void main(String[] args) {

        // 1. Eine Box für Integer erstellen
        Box<Integer> box = new Box<>();

        // 2. Elemente hinzufügen
        box.add(10);
        box.add(20);
        box.add(30);

        // 3. for-each Schleife verwenden
        // -> funktioniert, weil Box<T> Iterable<T> implementiert
        System.out.println("Inhalt der Box:");

        for (Integer value : box) {
            System.out.println(value);
        }

        /*
         * Was passiert im Hintergrund?
         * 
         * Der for-each wird vom Compiler ungefähr so übersetzt:
         * 
         * Iterator<Integer> it = box.iterator();
         * while (it.hasNext()) {
         *     Integer value = it.next();
         *     System.out.println(value);
         * }
         * 
         * -> dabei wird unsere innere Klasse BoxIterator verwendet!
         */
    }
}
```
{% endcode %}

### Ein paar abschließende Bemerkungen

Ein Iterator ist somit ein "Wegwerfprodukt", da er nach einmaligem Gebrauch nicht mehr verwendet werden kann - er steht dann immer auf der letzten Position und lässt sich nicht reseten.&#x20;

Ein Iterator kann uns nicht die aktuelle Anzahl oder die maximale Anzahl an Elementen liefern - und wire können in einem Iterator nicht rückwärts laufen oder diesen zurücksetzen.&#x20;

Bertrachten wir unsere eigene implemntieren, sehen wir auch, dass wie die Behältnisse, die einen Iterator zurückliefern in der Zeit, in der wir darüber iterieren nicht verändern sollten, würde man Elemente entfernen - oder hinzufügen würden sich Position und geamtzahl der Elemente verändern.



[^1]: 
