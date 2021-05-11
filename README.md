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
  
Eine Zeigerrealisierung der Knoten sieht wie folgt aus:  
````
type
  Knotenzeiger = ↑Knoten;
  Knoten = record
              leftson, rigthson : Knotenzeiger;
              key : integer;
           end
````
  
Da die Blätter eines Suchbaumes keine Schlüssel speichern, müssen sie auch nicht explizit als Knoten des oben angegebenen Typs repräsentiert werden. Mankann sie vielmehr einfach durch **nil**-Zeiger in den jeweiligen Vätern repräsentieren.

Ein Baum ist dann gegeben durch einen Zeiger auf die Wurzel:  
````
var root : Knotenzeiger
````

Die folgenden Methoden zum Einfügen, Suchen und Entfernen werden nur für den *Suchbaum* beschrieben.  
Es wird dieser Binärbaum als Ausgangssituation verwendet:

[Binärbaum]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaum.png  "Optionaler Titel"
![Alt-Text][Binärbaum]

***

### Einfügen

````
procedure Einfügen(p : Knotenzeiger; x : integer);
{sucht im Baum mit Wurzel p nach Schlüssel x}

begin
  if p = nil
    then {neuen Knoten mit Schlüssel x einfügen}
      begin
        new(p);
        p↑.leftson := nil;;
        p↑.leftson := nil
        p↑.key := x
        end
  else
    if x < p↑.key
      then Einfügen(p↑.leftson,x)
    else
      if y > p↑.key
        then Einfügen(p↑.rightson, x)
      else
        write('Knoten mit Schlüssel x gefunden')
        
end {Einfügen}
````

#### Beispiel

***

Schlüssel **7**

**7** wird mit 15 (Wurzel) verglichen  
-> **7** ist kleiner -> es wird im liken Sohn weitergesucht  
**7** wird mit 6 verglichen  
-> **7** ist größer -> es wird im rechten Sohn weitergesucht  
**7** wird mit 7 verglichen  
-> **7** ist im Baum schon vorhanden, es wird **kein** Knoten eingefügt  

***

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
procedure Suche(p : Knotenzeiger; x : integer);
{sucht im Baum mit Wurzel p nach Schlüssel x}

begin
  if p = nil
    then write('Es gibt keinen Knotern im Baum mit Schlüssel x)
  else
    if x < p↑.key
      then Suchen(p↑.leftson,x)
    else
      if y > p↑.key
        then Suchen(p↑.rightson, x)
      else
        write('Knoten mit Schlüssel x gefunden')
        
end {Suchen}
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

***

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

>Um einen Knoten zu entfernen, sucht man zunächst nach dem zu entfernenden Schlüssel x. Kommt x im Baum nicht vor, ist nichts zu tun. Ist x der Schlüssel eines Knotens, der keinen oder nur einen inneren Knoten als Sohn hat, ist das Entfernen einfach. Man entfernt den Knoten mit Schlüssel x und ersetzt ihn gegebenenfalls durch seinen einzigen Sohn. Schwieriger ist das Entfernen von x, wenn x Schlüssel eines Knotens ist, dessen beide Söhne innere Knoten sind, die Schlüssel gespeichert haben. Sei x der Schlüssel des Knotens p. Dann suchen wir im rechten Teilbaum von p den Knoten q mit dem kleinsten Schlüssel y, der größer als x ist. Der Knoten q heist ***symmetrische Nachfolger*** von p. Man ersetzt nun den Schlüssel x swa Knotens p durch den Schlüssel y und entfernt den Knoten q.

````
function vatersymnach (p : Knotenzeiger) : Knotenzeiger;
{liefert für einen Knotenzeiger p mit p↑.rightson ≠ nil einen Zeiger
auf den Vater des symmetrischen Nachfolgers von p↑}

begin
  if p↑.rigthson↑.leftson ≠ nil
    then  {sonst ist p das Ergebnis}
      begin
        p := p↑.rightson;
        while p↑.leftson.↑leftson ≠ nil do
          p := p↑.leftson
      end;
   vatersymnach := p
end {vatersymnach}
````

````
procedure Entfernen(p : Knotenzeiger; x : integer)
{ entfernt einen Knoten mit Schlüssel x aus dem Baum mit Wurzel p }

q : Knotenzeiger;

begin
  if p = nil
    then {Schlüssel k nicht im Baum}
  else
    if k < p↑.key
      then Entfernen(p↑.leftson, x)
    else
      if k > p↑.key
        then Entfernen(p↑.rightson, x)
      else {p↑.key = k}
        if p↑.leftson = nil
          then p := p↑.rigthson
        else
          if p↑.rigthson = nil
            then p := p↑.leftson
          else {p↑.lleftson != nil and p↑.rigthson != nil}
            begin
              q := vatersymnaach(p);
              if q = p
                then {rechter Sohn von q ist symmetrischer Nachfolger}
                begin
                  p↑.key := q↑.rigthson↑.key;
                  q↑.rightson := q↑.rigthson↑.rightson
                end
              else {liker Sohn von q ist symmetrischer Nachfolger}
                begin
                  p↑.key = q↑.leftson↑.key;
                  q↑.leftson := q↑.leftson↑.rightson
            end
end {Entfernen}
````

Ausgangssituation Binärbaum:  
  
![Alt-Text][Binärbaum]


#### Beispiel

Schlüssel **10**

**10** wird mit  15 (Wurzel) verglichen  
-> **10** ist kleiner -> es wird im linken Sohn weitergesucht  
**10** wird mit 6 verglichen  
-> **10** ist größer -> es wird im rechten Sohn weitergesucht  
**10** wird mit 7 verglichen  
-> **10** ist größer -> es wird im rechten Sohn weitergesucht  
rechter Sohn ist ein Blatt -> der Knoten mit dem Schlüssel 10 kann **nicht** entfernt werden da er nicht existiert  

***

Schlüssel **15**

**15** wird mit 15 (Wurzel) vergleichen  
-> Knoten wurde gefunden  
rechter Sohn des Knotens hat nur einen Sohn (23)  
-> 15 wird 23 ersetzt  

Binärbaum nach dem Entfernen:  

[BinärbaumEntfernen15]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumEntfernen15.png  "Optionaler Titel"
![Alt-Text][BinärbaumEntfernen15]

***

Schlüssel **7**

**7** wird mit 15 (Wurzel) verglichen  
-> **7** ist kleiner -> es wird im linken Sohn weitergesucht  
**7** wird mit 6 verglichen  
-> **7** ist größer -> es wird im rechten Sohn weitergesucht  
**7** wird mit 7 verglichen  
Knoten wurde gefunden  
Knoten ist ein Blatt  
-> Knoten mit dem Schlüssel 7 wird entfernt  

Binärbaum nach dem Entfernen:  

[BinärbaumEntfernen7]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumEntfernen7.png  "Optionaler Titel"
![Alt-Text][BinärbaumEntfernen7]

***

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
