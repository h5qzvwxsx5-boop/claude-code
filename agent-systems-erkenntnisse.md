# Wie Claude Code Agentensysteme baut: Erkenntnisse aus dem Quellcode

## Das Wichtigste in Kürze

Claude Code verwendet ein modulares System, bei dem spezialisierte KI-Agenten wie Experten in einem Team zusammenarbeiten. Jeder Agent hat eine klar definierte Rolle und Fähigkeiten - genau wie in einem gut organisierten Unternehmen.

---

## Was ist ein Agent?

Ein Agent ist eine spezialisierte KI-Einheit mit einem bestimmten Auftrag. Stell dir vor: Statt eines Alleskönners gibt es Spezialisten für verschiedene Aufgaben.

**Beispiele:**
- Ein **Code-Explorer** analysiert bestehenden Code und versteht, wie alles zusammenhängt
- Ein **Code-Architekt** entwirft neue Funktionen und plant deren Umsetzung
- Ein **Code-Reviewer** prüft die Qualität und findet potenzielle Fehler

---

## Das Geheimnis: Einfache Textdateien

Überraschend: Agenten werden nicht durch komplexen Code definiert, sondern durch einfache Textdateien. Jede Datei enthält:

1. **Name und Beschreibung** - Wer bin ich und wann werde ich gebraucht?
2. **Werkzeuge** - Was darf ich benutzen? (Dateien lesen, schreiben, suchen...)
3. **Persönlichkeit** - Wie soll ich denken und arbeiten?

Das macht das System extrem flexibel: Neue Agenten können in Minuten erstellt werden, ohne eine Zeile Code zu schreiben.

---

## Teamwork: Wie Agenten zusammenarbeiten

Das Besondere an Claude Code ist die Orchestrierung. Mehrere Agenten arbeiten koordiniert an einer Aufgabe:

### Ein Beispiel: Neue Funktion entwickeln

**Phase 1:** Mehrere Explorer-Agenten analysieren parallel den bestehenden Code
↓
**Phase 2:** Ein Architekt-Agent entwirft basierend auf den Erkenntnissen verschiedene Lösungsansätze
↓
**Phase 3:** Nach der Implementierung prüfen Review-Agenten die Qualität

Das Ergebnis: Schnellere, gründlichere Arbeit durch Parallelisierung und Spezialisierung.

---

## Sicherheit durch Einschränkung

Ein kluges Prinzip: Jeder Agent bekommt nur die Werkzeuge, die er wirklich braucht.

- Ein **Analyse-Agent** kann nur lesen - nicht schreiben oder löschen
- Ein **Generator-Agent** kann schreiben, aber keine Systembefehle ausführen
- Kritische Operationen erfordern speziell autorisierte Agenten

Das minimiert Risiken und verhindert unbeabsichtigte Änderungen.

---

## Qualitätskontrolle eingebaut

Besonders clever: Agenten bewerten ihre eigene Sicherheit. Der Code-Reviewer zum Beispiel meldet nur Probleme, bei denen er sich zu mindestens 80% sicher ist.

Das bedeutet:
- Weniger Fehlalarme
- Fokus auf echte Probleme
- Vertrauen in die Ergebnisse

---

## Single-Agent vs. Multi-Agent: Wann was?

Eine wichtige Frage: Braucht man immer mehrere Agenten? Die Antwort ist: Nein.

### Wann ein einzelner Agent besser ist

Nicht jede Aufgabe braucht ein ganzes Team. Ein einzelner Agent ist oft die bessere Wahl bei:

- **Einfachen, klar definierten Aufgaben** - Ein Bugfix in einer Zeile braucht kein Expertenteam
- **Dringenden Änderungen** - Hotfixes profitieren von schneller, direkter Ausführung
- **Trivialen Anpassungen** - Kleine Textänderungen oder Konfigurationsanpassungen

### Die versteckten Kosten von Multi-Agent

Mehrere Agenten bedeuten auch:

| Aspekt | Nachteil bei Multi-Agent |
|--------|--------------------------|
| **Koordination** | Agenten müssen synchronisiert werden |
| **Latenz** | Orchestrierung kostet Zeit |
| **Komplexität** | Mehr Fehlerquellen beim Zusammenspiel |
| **Kontextverlust** | Informationen können zwischen Agenten verloren gehen |
| **Debugging** | Schwerer nachzuvollziehen, was schief ging |

### Die Faustregel aus der Praxis

Claude Code empfiehlt diese Staffelung:

| Projektgröße | Empfohlene Agentenzahl |
|--------------|------------------------|
| Einfach | 2 Agenten |
| Mittel | 3 Agenten |
| Standard | 4 Agenten |
| Groß | 6 Agenten |
| Komplex | 8 Agenten |

### Wann Multi-Agent sich lohnt

Multi-Agent macht Sinn, wenn:
- **Mehrere Dateien** betroffen sind
- **Architekturentscheidungen** getroffen werden müssen
- **Anforderungen unklar** sind und verschiedene Perspektiven helfen
- **Unabhängige Prüfungen** gewünscht sind (Qualitätssicherung durch Redundanz)
- **Parallelisierung** die Geschwindigkeit erhöht

### Das Fazit zur Agent-Anzahl

Die richtige Anzahl von Agenten ist wie bei einem Projektteam: So wenig wie möglich, so viele wie nötig. Ein Alleskönner für einfache Aufgaben, ein Spezialistenteam für komplexe Herausforderungen.

---

## Wie baut man einen optimalen Agenten?

Ob einzeln oder im Team - jeder Agent folgt dem gleichen Bauplan. Das Geheimnis liegt in der klaren Struktur.

### Die Anatomie eines Agenten

Ein Agent besteht aus vier Elementen:

1. **Identität** - Name und wann er zum Einsatz kommt
2. **Werkzeuge** - Was darf er benutzen?
3. **Fähigkeiten** - Welches Modell steckt dahinter?
4. **Persönlichkeit** - Der System-Prompt, das Herzstück

### Der System-Prompt: Das Herzstück

Der System-Prompt ist wie eine Stellenbeschreibung für den Agenten. Die optimale Struktur:

**1. Rolle definieren**
> "Du bist ein Experte für [Fachgebiet] mit Spezialisierung auf [Kernkompetenz]."

**2. Aufgaben auflisten**
- Hauptaufgabe klar benennen
- Nebenaufgaben priorisieren
- Grenzen setzen (was gehört NICHT dazu)

**3. Prozess beschreiben**
Schritt für Schritt, wie der Agent vorgehen soll:
1. Erst X tun
2. Dann Y prüfen
3. Schließlich Z liefern

**4. Qualitätsstandards festlegen**
- Was ist ein gutes Ergebnis?
- Welche Kriterien müssen erfüllt sein?

**5. Ausgabeformat vorgeben**
- Wie soll das Ergebnis aussehen?
- Welche Struktur wird erwartet?

**6. Sonderfälle behandeln**
- Was tun bei Unklarheiten?
- Wie mit Fehlern umgehen?

### Die vier Agent-Typen

| Typ | Aufgabe | Beispiel-Einsatz |
|-----|---------|------------------|
| **Analyse** | Untersuchen & Verstehen | Code-Review, Datenanalyse |
| **Generierung** | Erstellen & Produzieren | Texte schreiben, Code generieren |
| **Validierung** | Prüfen & Bewerten | Qualitätskontrolle, Compliance-Check |
| **Orchestrierung** | Koordinieren & Steuern | Workflow-Management |

### Die goldenen Regeln

**Machen:**
- Spezifisch sein statt vage
- Klare Schritte vorgeben
- Ausgabeformat definieren
- Sonderfälle bedenken

**Vermeiden:**
- "Sei hilfreich" (zu vage)
- Zu viele Werkzeuge geben
- Prozessschritte weglassen
- Ausgabeformat offen lassen

### Das Prinzip der minimalen Rechte

Jeder Agent bekommt nur die Werkzeuge, die er wirklich braucht:

| Agent-Typ | Empfohlene Werkzeuge |
|-----------|---------------------|
| Analyse | Nur Lesen und Suchen |
| Generierung | Lesen und Schreiben |
| Testing | Lesen und Ausführen |

Weniger ist mehr: Ein Agent mit eingeschränkten Rechten kann weniger Schaden anrichten.

---

## Praktische Anwendungsfälle

### Für Unternehmen

**Software-Entwicklung:**
- Code-Review mit parallelen Prüfern (Bugs, Sicherheit, Stil)
- Feature-Entwicklung: Explorer → Architekt → Implementierer → Reviewer

**Kundenservice:**
- Agent 1 kategorisiert die Anfrage
- Agent 2 durchsucht die Wissensdatenbank
- Agent 3 formuliert die Antwort
- Agent 4 prüft auf Compliance

**Recruiting:**
- Lebenslauf-Analyse parallel zur Stellenprofil-Prüfung
- Ranking mit Begründung als Ergebnis

**Content-Erstellung:**
- Recherche → Entwurf → Korrektur → Faktencheck
- Jeder Schritt von einem Spezialisten

**Compliance & Audit:**
- Mehrere unabhängige Prüfungen
- Nur Findings mit hoher Confidence melden
- Dokumentation automatisch erstellen

### Für Privatpersonen

Auch im privaten Bereich kann Multi-Agent sinnvoll sein - bei wichtigen Entscheidungen:

| Anwendung | Agent-Setup |
|-----------|-------------|
| **Reiseplanung** | Flug + Hotel + Aktivitäten parallel recherchieren |
| **Hauskauf** | Markt + Finanzierung + Rechtliches prüfen |
| **Lernen** | Erklärer + Übungsleiter + Prüfungssimulator |
| **Große Käufe** | Recherche + Preisvergleich + Bewertungsanalyse |

**Aber Vorsicht:** Für alltägliche Fragen reicht ein einzelner Agent völlig aus. Multi-Agent lohnt sich erst bei komplexen, wichtigen Entscheidungen.

### Die Entscheidungshilfe

```
Einzelne Perspektive reicht?     → Single-Agent
Mehrere unabhängige Prüfungen?   → Multi-Agent
Aufgabe parallelisierbar?        → Multi-Agent (schneller)
Hohe Fehlerkosten?               → Multi-Agent (Redundanz)
Einfache Routineaufgabe?         → Single-Agent
```

---

## Beispiel: Multi-Agent-System für Reiseplanung

Um die Konzepte greifbar zu machen, hier ein vollständiges Beispiel - ein Agentensystem, das eine Reise plant.

### Die Ausgangssituation

**Anfrage:** "Plane einen 10-tägigen Italien-Urlaub für 2 Personen im September. Budget: 3.000€. Wir mögen Kultur, gutes Essen und wollen nicht nur Touristenfallen sehen."

### Das Team: 5 spezialisierte Agenten

#### Agent 1: Der Reise-Analyst

**Rolle:** Versteht die Anfrage und extrahiert die wichtigen Parameter.

**System-Prompt (vereinfacht):**
> Du bist ein erfahrener Reiseberater, der Kundenanfragen analysiert.
>
> **Deine Aufgaben:**
> 1. Extrahiere alle relevanten Parameter (Ziel, Dauer, Budget, Präferenzen)
> 2. Identifiziere implizite Wünsche ("nicht nur Touristenfallen" = Geheimtipps gewünscht)
> 3. Erkenne fehlende Informationen und formuliere Rückfragen
>
> **Ausgabeformat:**
> - Reiseziel: [Land/Region]
> - Zeitraum: [Daten]
> - Budget: [Betrag] für [was alles]
> - Prioritäten: [Liste]
> - Offene Fragen: [Falls vorhanden]

**Werkzeuge:** Keine (reiner Analyse-Agent)

---

#### Agent 2: Der Flug-Spezialist

**Rolle:** Findet die besten Flugverbindungen.

**System-Prompt (vereinfacht):**
> Du bist ein Experte für Flugbuchungen mit Fokus auf Preis-Leistung.
>
> **Deine Aufgaben:**
> 1. Recherchiere Flugoptionen für die gegebenen Parameter
> 2. Vergleiche Direktflüge vs. Umsteigeverbindungen
> 3. Berücksichtige Gepäckregeln und versteckte Kosten
> 4. Empfehle die beste Option mit Begründung
>
> **Qualitätsstandards:**
> - Mindestens 3 Optionen vergleichen
> - Gesamtkosten inkl. aller Gebühren angeben
> - Flugzeiten und Umsteigezeiten berücksichtigen
>
> **Ausgabeformat:**
> Top-Empfehlung: [Airline, Preis, Zeiten]
> Alternative 1: [...]
> Alternative 2: [...]
> Begründung: [Warum die Top-Empfehlung]

**Werkzeuge:** Web-Suche, Preisvergleich-APIs

---

#### Agent 3: Der Unterkunfts-Experte

**Rolle:** Findet passende Hotels und Unterkünfte.

**System-Prompt (vereinfacht):**
> Du bist ein Unterkunfts-Spezialist mit Fokus auf authentische Erlebnisse.
>
> **Deine Aufgaben:**
> 1. Finde Unterkünfte, die zum Reisestil passen
> 2. Bevorzuge lokale Alternativen zu großen Ketten
> 3. Achte auf Lage (Nähe zu Sehenswürdigkeiten, aber ruhig)
> 4. Prüfe echte Bewertungen auf wiederkehrende Probleme
>
> **Qualitätsstandards:**
> - Mindestens 4,5 Sterne Durchschnittsbewertung
> - Preis pro Nacht transparent angeben
> - Stornierungsbedingungen prüfen
>
> **Sonderfälle:**
> - Bei knappem Budget: Apartments statt Hotels vorschlagen
> - Bei Kulturinteresse: Unterkünfte in historischen Gebäuden bevorzugen

**Werkzeuge:** Web-Suche, Booking-Plattformen

---

#### Agent 4: Der Aktivitäten-Kurator

**Rolle:** Stellt das Erlebnisprogramm zusammen.

**System-Prompt (vereinfacht):**
> Du bist ein lokaler Insider, der authentische Erlebnisse kuratiert.
>
> **Deine Aufgaben:**
> 1. Erstelle einen ausgewogenen Mix aus Kultur, Kulinarik und Erholung
> 2. Finde Geheimtipps abseits der Touristenpfade
> 3. Plane realistische Tagesabläufe (nicht überladen)
> 4. Berücksichtige Öffnungszeiten und Reservierungspflichten
>
> **Qualitätsstandards:**
> - Maximal 2-3 Aktivitäten pro Tag
> - Pufferzeit für spontane Entdeckungen einplanen
> - Lokale Restaurants statt Touristenfallen
>
> **Ausgabeformat:**
> Tag 1: [Ort]
> - Vormittag: [Aktivität] - [Warum empfohlen]
> - Mittag: [Restaurant-Tipp] - [Spezialität]
> - Nachmittag: [Aktivität]
> - Abend: [Empfehlung]

**Werkzeuge:** Web-Suche, Reiseführer-Datenbanken

---

#### Agent 5: Der Reise-Koordinator (Orchestrator)

**Rolle:** Führt alles zusammen und erstellt den finalen Plan.

**System-Prompt (vereinfacht):**
> Du bist ein erfahrener Reiseplaner, der alle Teilpläne zu einem stimmigen Ganzen verbindet.
>
> **Deine Aufgaben:**
> 1. Prüfe die Ergebnisse der anderen Agenten auf Konsistenz
> 2. Stelle sicher, dass das Budget eingehalten wird
> 3. Optimiere die Reihenfolge (logische Reiseroute)
> 4. Identifiziere Konflikte (z.B. Hotel zu weit von Aktivitäten)
> 5. Erstelle den finalen, buchbaren Reiseplan
>
> **Qualitätsstandards:**
> - Gesamtbudget darf nicht überschritten werden
> - Keine unrealistischen Transfers zwischen Orten
> - Alle Buchungen müssen zum Zeitpunkt passen
>
> **Ausgabeformat:**
> ## Reiseübersicht
> [Zusammenfassung]
>
> ## Budget-Aufstellung
> - Flüge: X€
> - Unterkünfte: X€
> - Aktivitäten: X€
> - Puffer: X€
> - **Gesamt: X€**
>
> ## Detailplan
> [Tag-für-Tag-Plan]
>
> ## Buchungsschritte
> [Was zuerst buchen, Links]

**Werkzeuge:** Lesen (Ergebnisse der anderen Agenten), Schreiben (finaler Plan)

---

### Der Ablauf: So arbeiten die Agenten zusammen

```
Anfrage: "Plane Italien-Urlaub..."
           │
           ▼
    ┌──────────────┐
    │ Reise-Analyst │ ──→ Parameter & Prioritäten
    └──────────────┘
           │
           ▼
    ┌──────────────────────────────────────┐
    │         PARALLEL AUSFÜHRUNG           │
    │                                        │
    │  ┌─────────────┐  ┌─────────────────┐ │
    │  │Flug-Spezialist│  │Unterkunfts-Experte│ │
    │  └─────────────┘  └─────────────────┘ │
    │         │                  │          │
    │  ┌─────────────────────────┐          │
    │  │  Aktivitäten-Kurator    │          │
    │  └─────────────────────────┘          │
    └──────────────────────────────────────┘
           │
           ▼
    ┌──────────────────┐
    │ Reise-Koordinator │ ──→ Finaler Plan
    └──────────────────┘
           │
           ▼
    Fertiger Reiseplan mit Budget
```

### Warum funktioniert das?

| Prinzip | Umsetzung im Beispiel |
|---------|----------------------|
| **Spezialisierung** | Jeder Agent ist Experte für einen Bereich |
| **Parallelisierung** | Flug, Hotel und Aktivitäten werden gleichzeitig recherchiert |
| **Minimale Rechte** | Analyse-Agent hat keine Schreibrechte |
| **Qualitätskontrolle** | Koordinator prüft auf Konsistenz und Budget |
| **Klare Ausgabeformate** | Jeder Agent liefert strukturierte Ergebnisse |

### Das Ergebnis

Statt eines generischen Reiseplans erhält man:
- **Durchdachte Flugauswahl** mit Preisvergleich
- **Authentische Unterkünfte** statt Kettenhotels
- **Lokale Geheimtipps** statt Touristenfallen
- **Realistischer Tagesablauf** ohne Überforderung
- **Budget-Transparenz** mit Puffer für Spontanes

### Zum Nachbauen

Dieses System lässt sich mit aktuellen KI-Tools umsetzen:
- Jeder Agent = ein separater Chat mit spezifischem System-Prompt
- Orchestrierung = manuell oder per Automatisierung (z.B. mit n8n, Make)
- Parallel-Ausführung = mehrere API-Calls gleichzeitig

Der Aufwand lohnt sich besonders bei:
- Wichtigen Reisen (Hochzeitsreise, Jubiläum)
- Komplexen Routen (mehrere Länder/Städte)
- Speziellen Anforderungen (Barrierefreiheit, Ernährung)

---

## Was können wir daraus lernen?

### Für Unternehmen:
- **Spezialisierung schlägt Generalismus** - Definierte Rollen führen zu besseren Ergebnissen
- **Einfachheit gewinnt** - Textbasierte Konfiguration statt komplexer Programmierung
- **Sicherheit durch Design** - Berechtigungen von Anfang an einschränken

### Für die KI-Entwicklung:
- **Modulare Architekturen** ermöglichen schnelle Anpassungen
- **Orchestrierung** ist der Schlüssel zu komplexen Aufgaben
- **Selbstbewertung** erhöht die Zuverlässigkeit

---

## Fazit

Claude Code zeigt, wie moderne KI-Systeme gebaut werden können: Nicht als monolithische Superintelligenz, sondern als Team spezialisierter Agenten, die koordiniert zusammenarbeiten.

Das Prinzip ist übertragbar auf viele Bereiche - von der Softwareentwicklung bis zum Projektmanagement. Die Zukunft gehört nicht dem einen Alleskönner, sondern dem gut orchestrierten Team von Spezialisten.

---

*Basierend auf der Analyse des Claude Code Repositories von Anthropic.*
