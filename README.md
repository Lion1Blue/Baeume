# Bäume

>Bäume sind verallgemeinerte Listenstrukturen. Ein Element - überlicherweise spricht man von *Knoten* - hat nicht wie im Falle linearer Listen, nur einen Nachfolger, sondern eine endlich, begrenzte Anzahl von so genannten *Söhnen*. In der Regel ist einer der Knoten als *Wurzel* des Baumes ausgezeichnet. Das ist zugleich der einzige Knoten ohne *Vorgänger*. Jeder andere Knoten hat einen unmittelbaren Vorgänger, der auch *Vater* des Knotens genannt wird.
>Da die Menge der Knoten eines Baumes stets als endlich vorausgesetzt wird, muss es Knoten geben, die keine Söhne haben. Diese Knoten werden üblicherweise als *Blätter* bezeichnet; alle anderen Knoten nennt man *innere Knoten*.


[Baumstruktur]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Baum_Beispiel.jpg  "Optionaler Titel"
![Alt-Text][Baumstruktur]
  
  
  
Ein Baum ist in der Informatik eine Datenstruktur, mit der sich hierarchische Strukturen abbilden lassen, deshalb gehören sie zu den wichtigsten in der Informatik auftretenden Datenstrukturen.  
Da sie zu den meist verwendeten Datenstrukturen in der Informatik gehören, gibt es viele Spezialisierungen.


## Binärbaum
>Binärbäume sind in der Informatik die am häufigsten verwendete Unterart der Bäume. Im Gegensatz zu anderen Arten von Bäumen können die Knoten eines Binärbaumes nur höchstens zwei direkte Nachkommen haben.
>Meist wird verlangt, dass sich die Kindknoten eindeutig in linken und rechten *Sohn* einteilen lassen. 
>Ein Binärbaum ist entweder leer, oder er besteht aus einer Wurzel mit einem linken und rechten Teilbaum, die wiederum Binärbäume sind.


## Natürliche Bäume

Natürliche Bäume sind Binärbäume die zur Speicherung von Schlüsseln eingesetzt werden. Es wird angenommen, dass sämtliche Schlüssel paarweise verschieden und ganzzahlig sind.
Prinzipiell wird zwischen zwei verschiedenen Speicherungsformen unterschieden.  
Sind die Schlüssel nur in den inneren Knoten gespeichert und haben die Blätter keine Schlüssel, so spricht man von *Suchbäumen*. Sind die Schlüssel in den Blättern gespeichert, Spricht man von *Blattsuchbäumen*.

Suchbäume lassen sich folgendermaßen charakterisieren. Für jeden Knoten *p* gilt:  
Die Schlüssel im linken Teilbaum von *p* sind sämtlich kleiner als der Schlüssel von *p*, und dieser ist wiederum kleiner als sämtliche Schlüssel im rechten Teilbaum von *p*.

Die folgenden Methoden zum Einfügen, Suchen und Entfernen werden nur für den *Suchbaum* beschrieben.  
Es wird dieser Binärbaum als Ausgangssituation verwendet:

[Binärbaum]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaum.png  "Optionaler Titel"
![Alt-Text][Binärbaum]

### Einfügen

````
Einfügen(p, x)
{ fügt in den Baum mit Wurzel p einen Knoten mit Schlüssel x ein }

Fall 1 [p ist inner Knoten mit linkem Sohn p1 und rechtem Sohn p2]
  if x < Schlüssel(p)
    then Einfügen(p1, x)
  else
    if x > Schlüssel(p)
      then Einfügen(p2, x)
    else
      write("Schlüssel kam schon vor")
  
Fall 2 [p ist Blatt]
  then { neuen Knoten mit Schlüssel x einfügen }

````

#### Beispiel

Schlüssel **7**

**7** wird mit 15 (Wurzel) verglichen  
-> **7** ist kleiner -> es wird im liken Sohn weitergesucht  
**7** wird mit 6 verglichen  
-> **7** ist größer -> es wird im rechten Sohn weitergesucht  
**7** wird mit 7 verglichen  
-> **7** ist im Baum schon vorhanden, es wird **kein** Knoten eingefügt  

Schlüssel **1**

**1** wird mit 15 (Wurzel) verglichen  
-> **1** ist kleiner -> es wird im linken Sohn weitergesucht  
**1** wird mit 6 verglichen  
-> **1** ist kleiner -> es wird im linken Sohn weitergesucht  
**1** wird mit 4 verglichen  
-> **1** ist kleiner -> es wird im linken Sohn weitergesucht  
linker Sohn ist ein Blatt  
-> ein neuer Knoten mit dem Schlüssel **1** wird eingefügt  

Baum nach dem Einfügen der **1**  

[BinärbaumEinfügen]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumEinf%C3%BCgen.png  "Optionaler Titel"
![Alt-Text][BinärbaumEinfügen]

***

### Suchen
  
````
Suche(p, x);
{ sucht im Baum mit Wurzel p nach einem Schlüssel x }

Fall 1 [p ist innerer Knoten mit linkem Sohn p1 und rechtem Sohn p2]
   if x < Schlüssel(p)
      then Suche(p1, x)
   else
      if x > Schlüssel(p)
         then Suche(p2, x)
      else { x = Schlüssel(p), d.h. gesuchter Schlüssel p gefunden }
      
Fall 2 [p ist Blatt]
   { gesuchter Schlüssel kommt im Baum nicht vor }
````

#### Beispiel:

Schlüssel **50**

**50** wird 15 (Wurzel) verglichen  
-> **50** ist größer -> es wird im rechten Sohn weitergesucht  
**50** wird mit 23 verglichen  
-> **50** ist größer -> es wird im rechten Sohn weitergesucht  
**50** wird mit 71 verglichen  
-> **50** ist kleiner -> es wird im linken Sohn weitergesucht  
**50** wird mit **50** verglichen  
-> Knoten mit dem Schlüssel **50** wurde gefunden  

Schlüssel **1**  

**1** wird mit 15 (Wurzel) verglichen
-> **1** ist kleiner -> es wird im linken Sohn weitergesucht  
**1** wird mit 6 verglichen  
-> **1** ist kleiner -> es wird im linken Sohn weitergesucht  
**1** wird mit 4 verglichen  
-> **1** ist kleiner -> es wird im linken Sohn wietergesucht  
linker Sohn ist ein Blatt
-> Knoten mit dem Schlüssel **1** wurde **nicht** gefunden  

***

### Entfernen

````
Entfernen(p, x)
{ entfernt einen Knoten mit Schlüssel x aus dem Baum mit Wurzel p }

Fall 1 [p ist Blatt]
  then { Schlüssel
````


#### Beispiel

## Balancierte Bäume

### Einfügen

#### Beispiel

***

### Suchen

#### Beispiel

***

### Entfernen

#### Beispiel

## Randomisierte Bäum

## Selbstanordnende Binärbäume

## B-Bäume
