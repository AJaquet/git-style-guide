# Git Stilrichtlinien

Dies sind Git Stilrichtlinien, inspiriert von
[*How to Get Your Change Into the Linux Kernel*](https://www.kernel.org/doc/Documentation/SubmittingPatches),
den [git man pages](http://git-scm.com/doc)
sowie unterschiedlichen anderen, populären Vorgehensweisen.

Übersetzungen sind für folgende Sprachen verfügbar:

* [Chinesisch (vereinfacht)](https://github.com/aseaday/git-style-guide)
* [Chinesisch (traditionell)](https://github.com/JuanitoFatas/git-style-guide)
* [Französisch](https://github.com/pierreroth64/git-style-guide)
* [Griechisch](https://github.com/grigoria/git-style-guide)
* [Japanisch](https://github.com/objectx/git-style-guide)
* [Koreanisch](https://github.com/ikaruce/git-style-guide)
* [Portugisisch](https://github.com/guylhermetabosa/git-style-guide)
* [Spanisch](https://github.com/alexsimo/git-style-guide)
* [Thailändisch](https://github.com/zondezatera/git-style-guide)
* [Türkisch](https://github.com/CnytSntrk/git-style-guide)
* [Ukrainisch](https://github.com/denysdovhan/git-style-guide)

Wenn du zu diesem Projekt beitragen willst fühle dich willkommen!
Erstelle einen Fork des Projekts und öffne einen Pull Request.

# Inhaltsverzeichnis

1. [Branches](#branches)
2. [Commits](#commits)
  1. [Nachrichten](#nachrichten)
3. [Merging](#merging)
4. [Weiteres](#weiteres)

## Branches

* Wähle *kurze* und *beschreibende* Namen:

  ```shell
  # gut
  $ git checkout -b oauth-migration

  # schlecht - zu ungenau
  $ git checkout -b login_fix
  ```

* Identifikatoren von korrespondierenden Tickets in externen Services
 (z.B. GitHub Issues) sind auch gute Kandidaten für Branchnamen.
 Zum Beispiel:

  ```shell
  # GitHub Issue #15
  $ git checkout -b issue-15
  ```

* Nutze *Bindestriche* um Wörter zu trennen.

* Wenn mehrere Leute am *selben* Feature arbeiten, kann es hilfreich sein,
  *persönliche* Featurebranches sowie einen *teamweiten* Featurebranch zu haben.
  Befolge folgende Namenskonvention:

  ```shell
  $ git checkout -b feature-a/master # Teamweiter Branch
  $ git checkout -b feature-a/maria  # Marias persönlicher Branch
  $ git checkout -b feature-a/nick   # Nicks persönlicher Branch
  ```

  Mergen der persönlichen Branches mit dem teamweiten Branch
  erfolgt hier nach belieben (vergleiche ["Merging"](#merging)).
  Beizeiten wird der teamweite Branch dann in den "master" Branch gemerged.

* Lösche deinen Branch nach dem mergen aus dem Upstream Repository,
  sofern dem nichts entgegen steht.

  Tipp: Benutze den folgenden Befehl vom "master" Branch aus,
  um gemergede Branches anzuzeigen:

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

## Commits

* Jedes Commit sollte eine einzelne, *zusammenhängende Änderung* repräsentieren.
  Fasse nicht mehrere *unabhängige Änderungen* in einem Commit zusammen.
  Wenn beispielsweise eine Änderung einen Bug behebt
  und Performanceverbesserungen vornimmt,
  sollte sie auf zwei separate Commits aufgeteilt werden.

  *Tipp: Nutze `git add -p` um interaktiv einzelne Abschnitte
  modifizierter Dateien zu stagen.

* Spalte nicht eine einzelne, *zusammenhängende Änderung* in mehrere Commits auf.
  So sollten beispielsweise die Implementation eines Features
  und die korrespondierenden Tests in einem Commit zusammengefasst sein.

* Committe *früh* und *oft*.
  Kleine, abgeschlossene Commits sind einfacher zu verstehen
  und leichter rückgängig zu machen, falls etwas schief geht.

* Commits sollten *logisch* geordnet sein.
  Wenn beispielsweise *Commit X* von Änderungen aus *Commit Y* abhängt,
  dann sollte *Commit Y* vor *Commit X* kommen.

Notiz: Beim unabhängigen Arbeiten an einem lokalen Branch,
der *noch nicht gepusht* wurde, ist es unproblematisch,
Commits als temporäre Schnappschüsse der eigenen Arbeit zu benutzen.
Hier gilt es jedoch, die Commits vor dem Pushen entsprechend zu pflegen,
sodass sie den Regeln entsprechen.

### Nachrichten

* Benutze den Editor, nicht das Terminal, um Commitnachrichten zu schreiben:

  ```shell
  # gut
  $ git commit

  # schlecht
  $ git commit -m "Quick fix"
  ```

  Commits vom Terminal zu erstellen befürwortet die Einstellung,
  die ganze Commitnachricht in eine einzelne Zeile zu bekommen.
  Dies führt typischerweise zu uninformativen, mehrdeutigen Commitnachrichten.

* Die Zusammenfassung (erste Zeile der Nachricht) sollte
  *beschreibend* aber *knapp* sein.
  Idealer Weise sollte sie nicht länger als *50 Zeichen* sein.
  Sie sollte sich an Groß- und Kleinschreibung halten,
  und im Imperativ, Präsens geschrieben sein.
  Sie sollte nicht mit einem Satzzeichen enden,
  weil sie effektiv der *Titel* der Commitnachricht ist:

  ```shell
  # gut - Imperativ, Präsens, großer Anfang, weniger als 50 Zeichen
  Mark huge records as obsolete when clearing hinting faults

  # schlecht
  fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
  ```

* Nach der Zusammenfassung sollte eine Leerzeile kommen,
  der eine detailliertere Beschreibung folgt.
  Diese Beschreibung sollte bei *72 Zeichen* umgebrochen werden,
  und erklären, *warum* die Änderung notwendig war,
  *wie* das Problem gehandhabt wird,
  und welche *Nebeneffekte* auftreten könnten.

  Die Beschreibung sollte auch auf weitere Ressourcen hinweisen
  (z.B. durch einen Link zum Issue im Bugtracker.):

  ```text
  Kurze (50 Zeichen max.) Zusammenfassung

  Detaillierterer Text, wenn notwendig. Umgebrochen bei spätestens 72
  Zeichen. In manchen Zusammenhängen wird die erste Zeile
  als Betreff einer Email und die genauere Beschreibung als Inhalt
  benutzt. Hier ist die Leerzeile häufig besonders wichtig,
  solange nicht der Inhalt weg fällt.
  Programme wie rebase können fehlerhaft reagieren,
  wenn die Leerzeile fehlt.

  Weitere Paragraphen werden durch Leerzeilen getrennt.

  - Stichpunkte sind auch in Ordnung

  - Es werden Bindestriche oder Sternchen,
    durch ein Leerzeichen separiert, benutzt.
    Zwischen einzelnen Stichpunkten folgt eine Leerzeile.

  Quelle http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  Denke beim Schreiben einer Commitnachricht vor allem an die Frage,
  was du wissen wollen würdest, wenn du die Nachricht in einem Jahr lesen würdest.

* Wenn ein *Commit A* von einem *Commit B* abhängt,
  sollte diese Abhängigkeit in der Commitnachricht
  von *Commit A* festgehalten werden.
  Benutze die SHA1 hashes, um Commits zu referenzieren.

  Wenn *Commit A* entsprechend einen Bug behebt,
  der durch *Commit B* hervorgerufen wurde,
  sollte dies genauso festgehalten werden.

* Wenn ein Commit mit einem Anderem gesquashed werden soll
  benutze `--squash` und `--fixup` entsprechend,
  um die Intention offenzulegen:

  ```shell
  $ git commit --squash f387cab2
  ```

  *(Tipp: Nutze `--autosquash` beim rebasen.
    Die markierten Commits werden dann automatisch gesquashed.)*

## Merging

* **Schreibe nicht veröffentlichte Geschichte um.**
  Die Geschichte eines Repositories ist für sich genommen wertvoll,
  und es ist wichtig, feststellen zu können *was tatsächlich passierte*.
  Veränderungen der veröffentlichten Geschichte
  sind eine typische Problemquelle,
  und störend für alle Beteiligten an einem Projekt.

* Es gibt trotzdem Ausnahmen, bei denen es legitim ist,
  die Geschichte zu ändern:

  * Du arbeitest alleine an einem Branch, und dieser wird nicht reviewed.

  * Du möchtest deinen Branch aufräumen (z.B: Commits squashen)
    und/oder zum "master" Branch rebasen um später zu mergen.

  Ansonsten gilt *ändere niemals die Geschichte des "master" Branches*
  oder irgend eines speziellen Branches (z.B. von CI Servern genutzt).

* Halte die Geschichte *sauber* und *einfach*.
  *Direkt vor dem Mergen* deines Branches:

    1. Stelle sicher, dass dein Branch den Stilrichtlinien entspricht,
       und räume gegebenenfalls entsprechend auf, wenn dies nicht der Fall ist
       (squashen/umsortieren von Commits, umschreiben von Commitnachrichten, …)

    2. Rebase deinen Branch auf den Branch, mit dem er gemerged werden soll:

      ```shell
      [my-branch] $ git fetch
      [my-branch] $ git rebase origin/master
      # then merge
      ```

      Dies führt zu einem Branch, der direkt ans Ende des "master"
      Branches passt, und damit zu einer sehr einfachen Geschichte.

      *(Notiz: Diese Strategie passt besser zu Projekten
        mit kurzzeitigen Branches. Ansonsten kann es besser sein,
        den "master" Branch gelegentlich zu mergen anstatt darauf zu rebasen.)*

* Wenn dein Branch mehr als ein Commit enthält,
  merge nicht mit fast-forward:

  ```shell
  # gut - stellt sicher, dass ein merge commit erstellt wird
  $ git merge --no-ff my-branch

  # schlecht
  $ git merge my-branch
  ```

## Weiteres

* Es gibt eine Reihe von Workflows mit jeweils
  unterschiedlichen Stärken und Schwächen.
  Ob ein Workflow eine gute Wahl ist hängt ab vom Team,
  dem Projekt und eurem Vorgehen beim Entwickeln.

  Trotzdem ist es wichtig, sich wirklich auf einen Workflow festzulegen
  und diesem zu folgen.

* *Sei konsistent.*
  Dies betrifft den Workflow aber gilt auch für Commitnachrichten,
  Branch Namen und Tags.
  Ein konsistenter Stil im Repository sorgt dafür, dass es einfach ist,
  durch lesen des Logs und von Commitnachrichten herauszufinden,
  was vor sich geht.

* *Teste vor dem Pushen.* Veröffentliche keine halbfertige Arbeit.

* Benutze [annotierte Tags](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Annotated-Tags)
  um wichtige Releases oder wichtige Geschichtspunkte zu markieren.
  Bevorzuge [leichtgewichtige Tags](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Lightweight-Tags)
  zum persönlichen Gebrauch, z.B. als Lesezeichen oder zukünftige Referenzen.

* Halte dein Repository sauber,
  durch gelegentliches Ausführen von Wartungsarbeiten:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

# Lizenz

![CC license](http://i.creativecommons.org/l/by/4.0/88x31.png)

Diese Arbeit ist lizenziert unter der [Creative Commons Attribution 4.0
International lizens](https://creativecommons.org/licenses/by/4.0/).

# Mitwirkende

Agis Anastasopoulos / [@agisanast](https://twitter.com/agisanast) / http://agis.io
... und [Kontributoren](https://github.com/agis-/git-style-guide/graphs/contributors)!
