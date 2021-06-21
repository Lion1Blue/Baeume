# Bäume

>Bäume sind verallgemeinerte Listenstrukturen. Ein Element - überlicherweise spricht man von *Knoten* - hat nicht wie im Falle linearer Listen, nur einen Nachfolger, sondern eine endlich, begrenzte Anzahl von so genannten *Söhnen*. In der Regel ist einer der Knoten als *Wurzel* des Baumes ausgezeichnet. Das ist zugleich der einzige Knoten ohne *Vorgänger*. Jeder andere Knoten hat einen unmittelbaren Vorgänger, der auch *Vater* des Knotens genannt wird.
>Da die Menge der Knoten eines Baumes stets als endlich vorausgesetzt wird, muss es Knoten geben, die keine Söhne haben. Diese Knoten werden üblicherweise als *Blätter* bezeichnet; alle anderen Knoten nennt man *innere Knoten*.


[Baumstruktur]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Baum_Beispiel.jpg  "Baumstruktur"
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

[Binärbaum]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaum.png  "Binärbaum"
![Alt-Text][Binärbaum]

***

### Suchen

>Wir beginnen bei der Wurzel p und vergleichen x mit dem bei p gespeicherten Schlüssel; ist x kleiner als der Schlüssel von p, setzten wir die Suche beim linken Sohn von p fort. Ist x größer als der Schlüssel von p, setzen wir die Suche beim rechten  Sohn von p fort. So lange bis der gesuchte Schlüssel gefunden ist.

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


### Einfügen

>Wir beginnen bei der Wurzel p und vergleichen x mit dem bei p gespeicherten Schlüssel; ist x kleiner als der Schlüssel von p, setzten wir die Suche beim linken Sohn von p fort. Ist x größer als der Schlüssel von p, setzen wir die Suche beim rechten  Sohn von p fort. So lange bis der Sohn nil - also nicht vorhanden - ist, dort wird dann der neue Knoten eingefügt.

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

[BinärbaumEinfügen]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumEinf%C3%BCgen.png  "1 eingefügt"
![Alt-Text][BinärbaumEinfügen]

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

[BinärbaumEntfernen15]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumEntfernen15.png  "15 entfernt"
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

[BinärbaumEntfernen7]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumEntfernen7.png  "7 entfernt"
![Alt-Text][BinärbaumEntfernen7]

***

Neues Beispiel:  
  
[BinärbaumGroß]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumGroß.png  "Binärbaum"
![Alt-Text][BinärbaumGroß]
  
Schlüssel **65**

**65** wird mit 41 (Wurzel) verglichen  
-> **65** ist größer -> es wird im rechten Sohn weitergesucht  
**65** wird mit 65 verglichen  
-> Knoten zum Entfernen gefunden  
Es wird im rechten Sohn das kleinste Element (symmetrischer Nachfolger) gesucht  
-> symmetrischer Nachfolger ist 66  
66 kommt an die Stelle der **65**  

Binärbaum nach dem Entfernen:  
  
[BinärbaumGroßEntfernen65]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumGroßEntfernen65.png  "65 entfernt"
![Alt-Text][BinärbaumGroßEntfernen65]

***

### Nachteil von Binärbäumen

>Das Suchen, Einfügen und Entfernen eines Schlüssels in einem zufällig erzeugten binären Suchbaum mit N Schlüsseln ist zwar im Mittel in O(log n) Schritten ausführbar. Im schlechtesten Fall kann jedoch ein Aufwand von der Ordnung O(N) zur Ausführung dieser Operationen erforderlich sein, weil der gegebene Baum mit N Schlüsseln zu einer lineraren Liste degeneriert ist.

Beispiel:
  
[BinärbaumRechtsschief]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/Bin%C3%A4rbaumRechtsschief.png  "rechtsschiefer Binärbaum"
![Alt-Text][BinärbaumRechtsschief]
  
Deshalb wird im folgenden Abschnitt auf balancierte Bäume eingegangen.

## Balancierte Bäume

Aufgrund dieses Nachteils gibt es Balancierte Bäume. Diese verhindern durch zusätzliche Bedingungen ein Degenerieren der Baumstruktur. Im folgenden wird der AVL-Baum behandelt.

## AVL-Bäume

>Ein binärer Suchbaum ist *AVL-ausgeglichen* oder *höhenbalanciert*, kurz; Ein AVL-Baum, wenn für jeden Knoten p des Baumes gilt, dass sich die Höhe des linken Teilbaums von der Höhe des rechten Teilbaums von p höchstens um 1 unterscheidet.

[AVL-Baum-Kein-AVL]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL_Baum_und_kein_AVL_Baum.jpg  "AVL-Baum"
![Alt-Text][AVL-Baum-Kein-AVL]
  
Dadurch ist die Höhe des Suchbaums O(log n), womit alle weiteren Grundoperationen in O(log n) ausführbar sind.

### Suchen

> Da AVL-Bäume insbesondere binäre Suchbäume sind, kann man in ihnen nach einem Schlüssel geanuse suchen wie in einem natürlichen Baum. Dazu folgt man im schlechtesten Fall einem Pfad von der Wurzel zu einem Blatt. Weil die Höhe logarithmisch beschränkt bleibt, ist klar, dass man in einem AVL-Baum mit N Schlüsseln in höhstens O(log n) Schritten einen Schlüssel wieder finden kann bzw. feststellen kann, dass ein Schlüssel im Baum nicht vorkommt.

#### Beispiel
  
siehe Beispiel natürlicher Baum.
  
***


### Einfügen
>Um einen Schlüssel in einen AVL-Baum *einzufügen* sucht man zunächst nach dem Schlüssel noch nicht im Baum vorkommt, endet die Suche in einem Baltt, das die erwartete Position des Schlüssels repräsentiert. Man fügt den Schlüssel dort, wie im Falle natürlicher Bäume ein. Im Unterschied zu natürlichen Bäumen kann aber nunmehr ein Suchbaum vorliegen, der kein AVL-Baum mehr ist.
>Deshalb muss jeder Knoten einen Balance-Grad mitführen um die AVL-Bedingungen bei Operationen zu garantieren
>bal(p) = Höhe des rechten Teilbaumes von p - Höhe des linken Teilbaumes von p


[avlbaum]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/avlbaum.png  "AVL-Baum"
![Alt-Text][avlbaum]

AVL-Bäume sind daruch charakteriesiert, dass für jeden inneren Knoten p gilt bal(p) ∈ {-1, 0, +1}.

Wird der Schlüssel x in einen leeren Baum einfügt, wird x die Wurzel des Baumes.

[AVL-Baum-Einfügen-Wurzel]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-WurzelX.png  "AVL-Baum-Einfügen-Wurzel"
![Alt-Text][AVL-Baum-Einfügen-Wurzel]

Sonst sei p der Vater von einem Blatt und hat bal(p) ∈ {-1, 0, +1}  

Fallunterscheidung beim Einfügen:

**Fall 1 [bal(p) = +1]**

[AVL-Baum-Einfügen-Fall1]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-Fall1.png  "AVL-Baum-Einfügen-Fall 1"
![Alt-Text][AVL-Baum-Einfügen-Fall1]

**Fall 2 [bal(p) = -1]**

[AVL-Baum-Einfügen-Fall2]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-Fall2.png  "AVL-Baum-Einfügen-Fall 2"
![Alt-Text][AVL-Baum-Einfügen-Fall2]

**Fall 3 [bal(p) = 0]**

[AVL-Baum-Einfügen-Fall3]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-Fall3.png  "AVL-Baum-Einfügen-Fall 3"
![Alt-Text][AVL-Baum-Einfügen-Fall3]


>Durch Einfügen eines neuen Knotens als rechten oder linken Sohn von p wird p ein Knoten mit Balancefaktor -1 oder +1 und die Höhe des Teilbaumes mit Wurzel p wächst um 1. Wir rufen daher eine Prozedur *upin(p)* für den Knoten p auf, die den Suchpfad zurückläuft, die Balandefaktoren prüft, gegebenenfalls adjustiert und UMstrukturierungen (so genannte Rotationen oder Doppelrotationen) vornimmt, die sicherstellen, dass für alle Knoten die Höhendifferenten der jeweils zugehörigen Teilbäume wieder höchstens 1 sind. Also

**Fall 3.1 [bal(p) = 0 und einzufügender Schlüssel x > Schlüssel k von p]**

[AVL-Baum-Einfügen-Fall3.1]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-Fall3.1.png  "AVL-Baum-Einfügen-Fall 3.1"
![Alt-Text][AVL-Baum-Einfügen-Fall3.1]

**Fall 3.2 [bal(p) = 0 und einzufügender Schlüssel x < Schlüssel k von p]**

[AVL-Baum-Einfügen-Fall3.2]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-Fall3.2.png  "AVL-Baum-Einfügen-Fall 3.2"
![Alt-Text][AVL-Baum-Einfügen-Fall3.2]

>Die Prozedur *upin*: Wenn *upin* aufgerufen wird, so ist bal(p) ∈ {-1, +1} und die Höhe des Teilbaumes mit Wurzel p ist um 1 gewachsen. Wir müssen darauf achten, dass diese Invariante vor jedem rekursien Aufruf von *upin* gilt; *upin(p)* bricht ab, falls p keinen Vater hat, d.h. wenn p die Wurzel des Baumes ist. Wir unter scheiden zwei Fälle, je nachdem ob p linker oder rechter Sohn seines Vaters φp.

**Fall 1 [p ist linker Sohn seines Vaters φp]**

**Fall 1.1 [bal(φp) = +1]**

[AVL-Baum-Einfügen-upin1.1]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-upin1.1.png  "AVL-Baum-Einfügen-upin 1.1"
![Alt-Text][AVL-Baum-Einfügen-upin1.1]

**Fall 1.2 [bal(φp) = 0]**

[AVL-Baum-Einfügen-upin1.2]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-upin1.2.png  "AVL-Baum-Einfügen-upin 1.2"
![Alt-Text][AVL-Baum-Einfügen-upin1.2]

Man beachte, dass vor dem rekursiven Aufruf von *upin* die Invariante gilt.

**Fall 1.3 [bal(φp) = -1]**

[AVL-Baum-Einfügen-upin1.3]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-upin1.3.png  "AVL-Baum-Einfügen-upin 1.3"
![Alt-Text][AVL-Baum-Einfügen-upin1.3]


>Die Invariante sagt, dass der Teilbaum mit Wurzel p in der Höhe um 1 gewachsen ist. Aus der Voraussettzung *bal(φp)* = -1 kann man in diesem Fall schließen, dass bereits vor dem Einfügen des neuen Schlüssels in den linken Teilbaum von φp mit Wurzel p dieser Teilbaum eine um 1 größere Höhe hatte als der rechte Teilbaum von φp. Da der Teilbaum mit Wurzel p in der Höhe noch um 1 gewachsen ist, ist die AVL-Ausgeglichenheit bei φp verletzt. Wir müssen also umstrukturieren und unterscheiden dazu zwei Fälle, je nachdem, ob *bal(p)* = +1 oder *bal(p)* = -1 ist. (Wegen der Invariante ist *bal(p)* = 0 nicht möglich !)

**Fall 1.3.1 [bal(p) = -1]**

[AVL-Baum-Einfügen-upin1.3.1]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-upin1.3.1.png  "AVL-Baum-Einfügen-upin 1.3.1"
![Alt-Text][AVL-Baum-Einfügen-upin1.3.1]


**Fall 1.3.2 [bal(p) = +1]**

[AVL-Baum-Einfügen-upin1.3.2]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Einf%C3%BCgen-upin1.3.2.png  "AVL-Baum-Einfügen-upin 1.3.2"
![Alt-Text][AVL-Baum-Einfügen-upin1.3.2]


**Fall 2 [p ist rechter Sohn seines Vaters φp]**
>In diesem Fall geht man völlig analog vor und gleicht den Baum, wenn nötig durch eine Rotation nach links. bzw. Doppelrotation rachts-links bei φp wieder aus.
  
>Ein Aufruf der Prozedur *upin* kannn schlimmstenfalls für alle Knoten auf dem Sichpfad von der Einfügestelle zurück zur Wurzel erforderlich sein. In jedem Fall wird von der Einfügestelle zurück zur Wurzel erforderlich sein. In jedem Fall wird aber höchstens eine Rotation oder Doppelrotation durchgeführt.

#### Beispiel

***

### Entfernen
>Zunächst geht man genau so vor wie bei natürlichen Suchbäumen. Man sucht nach dem zu entfernenden Schlüssel. Findet man ihn nicht, ist das Entfernen bereits beendet. Sonst liegt einer der folgenden drei Fälle vor:

**Fall 1**

>Der zu entfernende Schlüssel ist der Schlüssel eines Knotens, dessen beide Söhne Blätter sind. Dann entfernt man den Knoten und ersetzt ihn durch ein Blatt. Falls der Baum nunmehr nicht der leere Baum geworden ist, bezeichne p den Vater des neuen Blattes. Weil der Teilbaum von p, mit Wurzel q die Höhe 0, 1 oder 2 haben. Hat er die Höhe 1 so ändert man einfach die Balance von p von 0 auf +1 oder -1 und ist fertig. Hat der Teilbaum mit Wurzel q die Höhe 0, so ändert man die Balance p von +1 oder -1 auf 0. In diesem Fall ist die Höhe des Teilbaums  mit Wurzel p um 1 gefallen. Damit können sich auch für alle Knoten auf dem Scuhpfad nach p die Balancefaktoren und die Höhen der Teilbäume verändert haben. Wir rufen daher eine Prozedur upout(p) auf, die die AVL-Ausgeglichenheit wieder herstellt

**Fall 2**
>Der zu entfernende Schlüssel ist der Schlüssel eines Knotens p, der nur einen inneren Knoten q als Sohn hat. Dann müssen beide Söhne von q Blätter sein. Man ersetzt also den Schlüssel von p durch den Schlüssel von q und ersetzt q durch ein Blatt. Damit ist nunmehr p ein Knoten mit *bal(p)* = 0 und die Höhe des Teilbaums mit Wurzel p um 1 gesunken (von 2 auf 1). Auch in diesem Fall rufen wir *upout(p)* auf um die AVL-Ausgeglichenheit wieder herzustellen.

**Fall 3**

>Der zu entfernende Schlüssel ist der Schlüssel eines Knotens p, dessen beide Söhne innere Knoten sind. Dann geht man wie im Falle natürlicher Suchbäume vor und ersetzt den Schlüssel durch den Schlüssel des symmetrischen Nachfolgers und entfernt den symmetrischen Nachfolger. Dass muss dann ein Knoten sein, dessen Schlüssel wie im Fall 1 und 2 beschrieben entfernt wird. In jedem Fall haben wir das Entfernen reduziert auf die Ausführung der Prozedur *upout(p)* für einen Knoten p mit *bal(p)* = 0, dessen Teilbaum in der Höhe um 1 gefallen ist.

Die Prozedur *upout*: Sie kann längs des Suchpfades rekursiv aufgerufen werden, adjustiert die Höhenbalance und führt gegebenenfalls Rotationen oder Doppelrotationen durch  um den Baum wieder auszugleichen. Wenn *opout(p)* aufgerufen wird, gilt: *bal(p)* = 0 und der Teilbaum mit Wurzel p ist in der Höhe um 1 gefallen. Wir müssen darauf achten, dass diese Invariante vor jedem rekursiven Aufruf von *upout* gilt. Wir unterscheiden wieder zwei Fälle, je nachdem ob p linker oder rechter Sohn seines Vaters φp ist.

**Fall 1 [p ist linker Sohn seines Vaters φp]**

**Fall 1.1 [bal(φp) = -1]

[AVL-Baum-Entfernen-upout1.1]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Entfernen-upout1.1.png  "AVL-Baum-Entfernen-upout 1.1"
![Alt-Text][AVL-Baum-Entfernen-upout1.1]

Man beachte, dass vor dem rekursiven Aufruf von *upout* die Invariante für φp gilt.

**Fall 1.2 [bal(φp) = 0]**

[AVL-Baum-Entfernen-upout1.2]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Entfernen-upout1.2.png  "AVL-Baum-Entfernen-upout 1.2"
![Alt-Text][AVL-Baum-Entfernen-upout1.2]

**Fall 1.3 [bal(φp) = +1]**

[AVL-Baum-Entfernen-upout1.3]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Entfernen-upout1.3.png  "AVL-Baum-Entfernen-upout 1.3"
![Alt-Text][AVL-Baum-Entfernen-upout1.3]

>Der rechte Teilbaum von φp mit der Wurzel q ist also höher als der linke mit Wurzel p, der darüber hinaus noch in der Höhe um 1 gefallen ist. Wir machen eine Fallunterscheidung nach dem Balancefaktor von q.

**Fall 1.3.1 [bal(q) = 0]**

[AVL-Baum-Entfernen-upout1.3.1]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Entfernen-upout1.3.1.png  "AVL-Baum-Entfernen-upout 1.3.1"
![Alt-Text][AVL-Baum-Entfernen-upout1.3.1]

**Fall 1.3.2 [bal(q) = +1]**

[AVL-Baum-Entfernen-upout1.3.3]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Entfernen-upout1.3.3.png  "AVL-Baum-Entfernen-upout 1.3.3"
![Alt-Text][AVL-Baum-Entfernen-upout1.3.3]

Man beachte, dass vor dem rekursiven Aufruf von upout die Invariante für r gilt!

**Fall 1.3.3 [bal(q) = -1]**

[AVL-Baum-Entfernen-upout1.3.3]: https://github.com/Lion1Blue/Baeume/blob/main/BilderB%C3%A4ume/AVL-Baum-Entfernen-upout1.3.3.png  "AVL-Baum-Entfernen-upout 1.3.3"
![Alt-Text][AVL-Baum-Entfernen-upout1.3.3] 

**Fall 2 [p ist rechter Sohn seines Vaters φp]**

In diesem Fall geht man völlig analog vor und gleicht den Baum, wenn nötig, durch eine Rotation nach links bzw. eine Doppelrotation rechts-links bei φp wieder aus.


#### Beispiel


## B-Bäume
