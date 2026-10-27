---
title: Was ist ein LLM
tags:
  - ki-grundlagen
  - llm
created: 2026-10-27
updated: 2026-10-27
status: active
---

# Was ist ein LLM
## Was macht ein LLM?

- Ein LLM (Large Language Model) **setzt Text fort**: Aus der bisherigen Eingabe (dem Kontext) berechnet es Wahrscheinlichkeiten für das nächste Token (Wortteil), wählt eines aus und wiederholt das, bis die Antwort fertig ist.
- Es schlägt nichts in einer Datenbank nach. Es nutzt **gelernte statistische Muster** aus Sprache, Fakten und typischen Denkwegen. Deshalb wirkt es kompetent, kann aber auch plausibel klingenden Unsinn erzeugen (Halluzination).
- Es hat **kein Gedächtnis** zwischen zwei Anfragen. Alles, was es berücksichtigen soll, muss im Kontextfenster stehen.

## Was bedeutet „trainiert"?

- **Vortraining:** Das Modell bekommt riesige Textmengen und soll immer wieder das nächste Token vorhersagen. Bei jedem Fehler werden seine Milliarden Parameter (Gewichte) ein kleines Stück korrigiert. So entstehen die Muster.
- **Nachtraining:** Mit Beispielen und menschlichem Feedback lernt das Modell, sich wie ein Assistent zu verhalten. Es folgt Anweisungen, lehnt Unpassendes ab und ruft Werkzeuge im richtigen Format auf.
- Nach dem Training sind die Gewichte **eingefroren**. Das Wissen hat deshalb einen Stichtag (Knowledge Cutoff). Im Gespräch lernt das Modell nicht dazu, es verarbeitet nur den aktuellen Kontext.

## Zusammenhang mit KI-Agent vs. Chat

- In beiden Fällen arbeitet **dasselbe LLM**. Der Unterschied liegt in der Umgebung:
  - Im **Chat** liefert das Modell Text als Antwort.
  - Im **Agenten** erzeugt es zusätzlich Werkzeugaufrufe. Die Umgebung führt diese aus und gibt die Ergebnisse in einer Schleife an das Modell zurück.
- Dass das Modell Werkzeuge sinnvoll einsetzen kann, ist kein Zusatzprogramm. Auch das ist **antrainiert** (siehe Nachtraining).
- → Ausführlich: [[KI-Agent-vs-Chat]] · Wie daraus der konkrete Agenten-Workflow wird: [[Agenten-Workflow]]

## Verwandt

- [[Agenten-Workflow]] – wie aus dem LLM ein Agent wird: Ziel → Plan → Tool-Use → Iteration
- [[90-Index/Wissensindex]]
