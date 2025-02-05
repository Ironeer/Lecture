---
type: lecture-cg
title: "Suche mit `A*`{=markdown}"
menuTitle: "`A*`{=markdown}"
author: "Carsten Gips (FH Bielefeld)"
weight: 3
readings:
  - key: "Russell2020"
    comment: "`A*`{=markdown}: Abschnitt 3.5.2, Heuristiken: Kapitel 3.6"
quizzes:
  - link: "https://kahoot.it/challenge/07359960?challenge-id=8471c25d-77c6-4c83-b473-6edcacfcb770_1633581428956"
    name: "Selbsttest `A*`{=markdown} (Kahoot)"
assignments:
  - topic: sheet01
youtube:
  - id: eMkEN-HtEs8
fhmedia:
  - link: "https://www.fh-bielefeld.de/medienportal/m/b4967369536da2af1f8b0efc443d7c2275ff292f786144c83524e1eb117dd5fc305993716fe4dc472056114d43360483755c45dd8e5938f635efe4fa0ea02509"
    name: "Direktlink FH-Medienportal: `A*`{=markdown}"
---


## Hole das Buch

:::center
![](images/graph.png){width="60%"}
:::

::: notes
=> [**Problemlösen == Suche im Graphen**]{.alert}
:::

\bigskip
\bigskip

**Informierte Suche: Nutzung der Kostenfunktion**:

**Gesamtkosten**: $f(n) = g(n) + h(n)$

::: notes
*   $n \in S$ auf aktuellem Weg erreichter Knoten
*   $g(n)$ tatsächliche Kosten für Weg vom Start bis Knoten $n$
*   $h(n)$ geschätzte Restkosten für Weg von Knoten $n$ zum Ziel
    => $h(n)$ wird auch "heuristische Funktion" oder "Heuristik" genannt
:::

::: notes
Varianten:
*   `[Branch-and-Bound]({{<ref "/search/informed/branchandbound" >}})`{=markdown}
*   `[Best First]({{<ref "/search/informed/bestfirst" >}})`{=markdown}
*   **A\***
:::

## A\*-Suche

*   Kombination aus Branch-and-Bound und Best-First-Suche

\smallskip

*   Kostenfunktion: $f(n) = g(n) + h(n)$
*   Datenstruktur: **sortierte Queue** (Prioritätsqueue)

\smallskip

*   Voraussetzung:
    1.  Alle Aktionen haben positive Kosten ($g(n) \ge \epsilon$)
    2.  Heuristik $h(n)$ muss *zulässig/konsistent* sein

:::::: notes
:::center
![](images/tafelbeispiel.png){width="90%"}
:::
::::::

[Tafelbeispiel A* (Graph-Search, nur Anfang/Schreibweise)]{.bsp}


::: notes
## Konventionen für diese Lehrveranstaltung

In der Beschreibung der Algorithmen werden häufig nur die letzten Knoten der partiellen Wege
in den Datenstrukturen mitgeführt (das gilt auch für die Beschreibung im [@Russell2020]). Dies
erschwert die Nachvollziehbarkeit, wenn man die Queue oder den Stack schrittweise aufschreibt.
Deshalb wird für diese Veranstaltung die Konvention eingeführt, immer die **partiellen Wege**
aufzuschreiben.

Notieren Sie die Bestandteile der Kosten für jeden partiellen Weg in der Queue einzeln:
"$g(n) + h(n) = f(n)$". Das erleichtert Ihnen die weiteren Schritte, da Sie dort ja nur
mit $g(n)$ weiter rechnen dürfen. Gleichzeitig erleichtert es die Nachvollziehbarkeit.

Auf dem Papier sortiert sich die Queue schlecht, deshalb können Sie darauf verzichten,
wenn Sie den im nächsten Schritt zu expandierenden Weg unterstreichen. Wer nicht mit
Unterstreichen arbeiten will, muss eben dann manuell sortieren ...

Wenn bei der Graph-Search-Variante ein Weg nicht in die Queue aufgenommen wird, weil
bereits ein anderer (günstigerer) Weg zum selben (Zwischen-/End-) Knoten bereits in der
Queue enthalten ist, schreiben Sie dies geeignet auf. Dies gilt auch für den analogen
Fall, wenn ein Weg aus der Queue entfernt wird, weil ein günstigerer Weg zum selben
(Zwischen-/End-) Knoten eingefügt werden soll.
:::


## A\*-Suche -- Anforderungen an Heuristik (Tree-Search)

**Tree-Search-Variante**: Die Heuristik muss [**zulässig**]{.alert} sein:

*   Seien $h^\star(n)$ die tatsächlichen optimalen Restkosten von einem Knoten
    $n$ zum nächsten Ziel.
*   Dann muss für jeden beliebigen Knoten $n$ gelten: $$h(n) \le h^\star(n)$$
*   Außerdem muss gelten:
    *   $h(n) \ge 0$ für jeden Knoten $n$
    *   $h(n) = 0$ für jeden Zielknoten $n$

\medskip
=> Beispiel: Luftlinie als Abschätzung

::: notes
**Hinweis**: Im der englischen Ausgabe des [@Russell2020] wird die
**zulässige Heuristik** auch "**admissible heuristic**" genannt.
:::


## A\* ist optimal

A\* (Tree-Search-Variante) mit zulässiger Heuristik ist optimal.

\bigskip

::: slides
Beweis siehe Übungsblatt "Blatt 01" :-)
:::

::: notes
Beweis siehe Übungsblatt `[Blatt 01]({{<ref "sheet01" >}})`{=markdown} :-)
:::

## Einfache Verbesserungen A\* (Tree-Search)

*   Dynamische Programmierung: Behalte von mehreren Pfaden zum gleichen Knoten
    nur den günstigsten in der Queue

*   Pfade, deren Endknoten bereits früher im Pfad vorkommt (Schleifen), werden
    in Schritt 2 nicht in die Queue aufgenommen

\bigskip

*   Übergang zur Graph-Search-Variante und Markierung von Knoten

    => Achtung: Dann schärfere Anforderungen an Heuristik (Konsistenz)


## A\*-Suche -- Anforderungen an Heuristik (Graph-Search)

**Graph-Search-Variante**: Die Heuristik muss [**konsistent**]{.alert} sein:

Für jeden Knoten $n$ und jeden durch eine Aktion $a$ erreichten Nachfolger $m$
gilt: $$h(n) \le c(n,a,m) + h(m)$$ mit $c(n,a,m)$ Schrittkosten für den Weg von
$n$ nach $m$ mit Aktion $a$.

\medskip
Außerdem muss gelten:

*   $h(n) \ge 0$ für jeden Knoten $n$
*   $h(n) = 0$ für jeden Zielknoten $n$

\medskip
=> Eine konsistente Heuristik ist gleichzeitig zulässig.

::: notes
**Hinweis**: Im der englischen Ausgabe des [@Russell2020] wird die
**konsistente Heuristik** auch "**consistent heuristic**" genannt.
:::


## Eigenschaften Branch-and-Bound, Best-First, A\* {#vergleich-bnb-bf-astar}

<!-- XXX Tabelle doppelt: optimierter Umbruch für Slides -->

::: slides
|                 | **Branch-and-Bound** | **Best-First**    | **A\***              |
|:----------------|:---------------------|:------------------|:---------------------|
| Kosten          | $f(n) = g(n)$        | $f(n) = h(n)$     | $f(n) = g(n) + h(n)$ |
| Vollständigkeit | ja[^4]               | nein[^5]          | ja                   |
| Optimalität     | ja                   | nein              | ja                   |
| Aufwand         | exponentiell         | exponentiell      | exponentiell         |
| Bemerkung       | Probiert erst alle   | Suchverlauf stark | Heuristik: zulässig  |
|                 | "kleinen" Pfade      | abh. v. Heuristik | bzw. konsistent      |
:::

::: notes
|                 | **Branch-and-Bound**               | **Best-First**                      | **A\***                             |
|:----------------|:-----------------------------------|:------------------------------------|:------------------------------------|
| Kosten          | $f(n) = g(n)$                      | $f(n) = h(n)$                       | $f(n) = g(n) + h(n)$                |
| Vollständigkeit | ja[^4]                             | nein[^5]                            | ja                                  |
| Optimalität     | ja                                 | nein                                | ja                                  |
| Aufwand         | exponentiell                       | exponentiell                        | exponentiell                        |
| Bemerkung       | Probiert erst alle "kleinen" Pfade | Suchverlauf stark abh. v. Heuristik | Heuristik: zulässig bzw. konsistent |
:::

[^4]: BnB vollständig: Kosten größer Epsilon (positiv)
[^5]: gilt für Tree-Search-Variante; vollständig bei Graph-Search und endlichen Problemräumen


## Wrap-Up

*   Informierte Suchverfahren
    *   Nutzen reale Pfadkosten und/oder Schätzungen der Restkosten
    *   A*: komplette Kostenfunktion $f(n) = g(n)+h(n)$ \newline
        => besondere Anforderungen an die Heuristik!
        [(Tree-Search: *zulässige* Heuristik; Graph-Search: *konsistente* Heuristik)]{.notes}

\smallskip

::: notes
*   Ausblick auf Verbesserungen der vorgestellten Suchverfahren:
    *   Beschränkung der Suchtiefe ("Depth-Limited-Search")
    *   Iterative Vertiefung der Suchtiefe ("Iterative-Deepening-Search"),
        beispielsweise IDA* ("Iterative-Deepening A*")
    *   Beschränkung des verwendeten Speichers, beispielsweise SMA*
        ("Simplified Memory-Bounded A*")
:::







<!-- DO NOT REMOVE - THIS IS A LAST SLIDE TO INDICATE THE LICENSE AND POSSIBLE EXCEPTIONS (IMAGES, ...). -->
::: slides
## LICENSE
![](https://licensebuttons.net/l/by-sa/4.0/88x31.png)

Unless otherwise noted, this work is licensed under CC BY-SA 4.0.
:::
