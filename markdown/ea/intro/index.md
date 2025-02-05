---
type: lecture-cg
title: "Einführung Evolutionäre Algorithmen"
menuTitle: "Intro EA/GA"
author: "Carsten Gips (FH Bielefeld)"
weight: 1
readings:
  - key: "Russell2020"
    comment: "GA: Abschnitt 4.1.4"
  - key: "Schwefel1995"
    comment: "Originalarbeit zu Evolutionsstrategien"
  - key: "Michalewicz1996"
  - key: "Baeck1996"
  - key: "Nissen1997"
assignments:
  - topic: sheet02
youtube:
  - id: pKdKcPLI7V4
fhmedia:
  - link: "https://www.fh-bielefeld.de/medienportal/m/7804b1839761e3ca43478cbd5eea342fc6f61539fe481d34efe0d3d64747ef4fe2a6de4c9f079ce806f6ac7194b48b0c4324bd17c3483dd318d027d94242d8f9"
    name: "Direktlink FH-Medienportal: KI Einführung Evolutionäre Algorithmen"
---


## Evolution sehr erfolgreich bei Anpassung

::: center
![](https://images.unsplash.com/flagged/photo-1552863473-6e5ffe5e052f?fm=png&crop=entropy&cs=tinysrgb){width="60%"}

[Quelle: [Photo](https://unsplash.com/photos/aWDgqexSxA0) by [Johannes Plenio](https://unsplash.com/@jplenio) on [Unsplash](https://unsplash.com/) ([Unsplash License](https://unsplash.com/license))]{.origin}
:::

\bigskip
\bigskip

::: cbox
[**Wie funktioniert's?**]{.alert}
:::

[kurze Diskussion]{.bsp}


## EA -- Zutaten und Mechanismen

*   Zutaten:
    *   **Individuen**: Kodierung möglicher Lösungen
    *   **Population** von Individuen
    *   **Fitnessfunktion**: Bewertung der Angepasstheit

\bigskip

*   Mechanismen ("Operatoren"):
    *   Selektion
    *   Rekombination (Crossover)
    *   Mutation


## EA -- Allgemeiner Ablauf

::: center
![](images/ea_prinz.png){width="80%"}
:::


## EA -- Beispiel

::: center
![](images/4-queens-example.png){width="40%"}
:::

::: notes
Jedes Individuum kodiert ein Spielfeld mit einer konkreten Anordnung **aller**
Königinnen => **Vollständige Zustandsbeschreibung**.

Dabei korrespondiert der Index in das Array des Individuums mit der jeweiligen
Spalte des Spielfelds. Die Zahl an einer Arrayposition gibt dann an, in welcher
Zeile in dieser Spalte eine Königin ist.

Crossover: Die ausgewählten Individuen werden an der selben Stelle aufgetrennt
und die Hälften verkreuzt zu zwei neuen Individuen zusammengesetzt. Es entstehen
zwei neue Anordnungen der Königinnen (zwei neue Spielfelder).
:::

[Beispiel mit 4-Queens-Puzzle]{.bsp}


## EA -- Strömungen

1.  **Genetische Algorithmen** (GA)
    *   Holland und Goldberg (ab 1960)
    *   Binäre Lösungsrepräsentation (Bitstring): $\mathbf{g} = (g_1, \dots, g_m)\in \{ 0,1\}^m$
    *   Fitnessbasierte stochastische Selektion
    *   $\mu$ Eltern erzeugen $\mu$ Kinder

\smallskip

2.  **Evolutionsstrategien** (ES)
    *   Rechenberg und Schwefel (ab 1960)
    *   Kodierung reellwertiger Parameter: $\mathbf{g} = (\mathbf{x}, \mathbf{\sigma})$
        mit $\mathbf{x} = (x_1, \dots, x_n) \in \mathbb{R}^n$
    *   $\mu$ Eltern erzeugen $\lambda$ Kinder mit $\mu \le \lambda$

\smallskip

3.  **Evolutionäre Programmierung** (EP)

::: notes
*Hinweis*: Häufig finden sich Mischformen, beispielsweise GA mit reellwertigen Parametern

*Hinweis*: Im Folgenden werden **Genetische Algorithmen** (GA) betrachtet. Sie
finden jeweils Hinweise auf die Gestaltung der Operatoren bei ES.
:::


## Anwendungsbeispiele für Evolutionäre Algorithmen

*   Berechnung und Konstruktion komplexer Bauteile: beispielsweise
    Tragflächenprofile (Flugzeuge), Brücken oder Fahrzeugteile unter
    Berücksichtigung bestimmter Nebenbedingungen
*   Scheduling-Probleme: Erstellung von Stunden- und Raumplänen oder Fahrplänen
*   Berechnung verteilter Netzwerktopologien: Wasserversorgung, Stromversorgung,
    Mobilfunk
*   Layout elektronischer Schaltkreise


## Wrap-Up

Lokale Suchverfahren: Nur das Ergebnis zählt!

\bigskip

*   Evolutionäre Algorithmen: Unterschied GA und ES (grober Überblick)







<!-- DO NOT REMOVE - THIS IS A LAST SLIDE TO INDICATE THE LICENSE AND POSSIBLE EXCEPTIONS (IMAGES, ...). -->
::: slides
## LICENSE
![](https://licensebuttons.net/l/by-sa/4.0/88x31.png)

Unless otherwise noted, this work is licensed under CC BY-SA 4.0.

### Exceptions
*   [Photo "Evolution Walk"](https://unsplash.com/photos/aWDgqexSxA0) by [Johannes Plenio](https://unsplash.com/@jplenio) on [Unsplash](https://unsplash.com/), licensed under [Unsplash License](https://unsplash.com/license)
:::
