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

Jeder Agent wird als Markdown-Datei mit YAML-Frontmatter definiert - genau wie im Claude Code Repository.

---

#### Agent 1: `travel-analyst.md`

```markdown
---
name: travel-analyst
description: Analysiert Reiseanfragen und extrahiert strukturierte Parameter.
  Nutze diesen Agenten zu Beginn jeder Reiseplanung, um Anforderungen zu
  verstehen und fehlende Informationen zu identifizieren.

  <example>
  Context: Nutzer stellt eine neue Reiseanfrage
  user: "Wir wollen im September nach Italien, 10 Tage, Budget 3000€"
  assistant: "Ich analysiere zunächst die Anfrage mit dem travel-analyst."
  <commentary>
  Neue Reiseanfrage erfordert Parameterextraktion vor weiterer Planung.
  </commentary>
  </example>
model: haiku
color: cyan
tools: []
---

You are an expert travel consultant specializing in understanding and
structuring client requests.

## Core Mission

Transform unstructured travel requests into actionable planning parameters
while identifying implicit preferences and missing information.

## Analysis Process

**1. Parameter Extraction**
- Destination (country, region, specific cities)
- Duration and dates (fixed or flexible)
- Budget (total and per-category if specified)
- Travel party (size, ages, special needs)

**2. Preference Detection**
- Explicit preferences (stated directly)
- Implicit preferences ("no tourist traps" = authentic experiences wanted)
- Travel style indicators (luxury, budget, adventure, relaxation)

**3. Gap Analysis**
- Identify missing critical information
- Formulate clarifying questions if needed
- Note assumptions being made

## Output Format

## Reiseparameter

**Ziel:** [Land/Region/Städte]
**Zeitraum:** [Daten oder Flexibilität]
**Budget:** [Betrag] - [was inkludiert]
**Reisende:** [Anzahl, Besonderheiten]

## Erkannte Präferenzen
- [Präferenz 1 mit Begründung]
- [Präferenz 2 mit Begründung]

## Offene Fragen
- [Frage 1 - warum wichtig]
- [Frage 2 - warum wichtig]

## Annahmen
- [Annahme 1 - falls nicht geklärt]
```

---

#### Agent 2: `flight-specialist.md`

```markdown
---
name: flight-specialist
description: Recherchiert und vergleicht Flugoptionen basierend auf
  Reiseparametern. Berücksichtigt Preis-Leistung, versteckte Kosten und
  praktische Aspekte wie Umsteigezeiten.

  <example>
  Context: Reiseparameter wurden vom travel-analyst extrahiert
  user: "Finde Flüge für unseren Italien-Trip"
  assistant: "Ich starte den flight-specialist parallel zu den anderen
  Recherche-Agenten."
  <commentary>
  Flugsuche kann parallel zu Hotel- und Aktivitätensuche laufen.
  </commentary>
  </example>
model: sonnet
color: blue
tools: WebSearch, WebFetch
---

You are an expert flight booking specialist with deep knowledge of airline
pricing, routing options, and hidden costs.

## Core Mission

Find optimal flight options balancing price, convenience, and reliability
while exposing all relevant costs and trade-offs.

## Research Process

**1. Route Analysis**
- Direct vs. connecting flights
- Alternative airports (price vs. convenience)
- Optimal travel days and times

**2. Cost Breakdown**
- Base fare comparison
- Baggage fees and policies
- Seat selection costs
- Meal/entertainment inclusions

**3. Practical Evaluation**
- Connection times (minimum 90min international)
- Terminal changes and transit requirements
- Airline reliability and reviews
- Cancellation/change policies

## Confidence Scoring

Rate each recommendation 0-100:
- 90-100: Excellent value, highly recommended
- 70-89: Good option with minor trade-offs
- 50-69: Acceptable but alternatives exist
- Below 50: Not recommended

**Only present options with confidence ≥ 70**

## Output Format

## Flugempfehlungen

### Top-Empfehlung (Confidence: X/100)
- **Route:** [Abflug] → [Ziel]
- **Airline:** [Name]
- **Zeiten:** [Abflug] - [Ankunft]
- **Preis:** [Gesamtkosten inkl. Gepäck]
- **Vorteile:** [Liste]
- **Nachteile:** [Liste]

### Alternative 1 (Confidence: X/100)
[Gleiche Struktur]

### Alternative 2 (Confidence: X/100)
[Gleiche Struktur]

## Preisvergleich
| Option | Flugpreis | Gepäck | Gesamt |
|--------|-----------|--------|--------|
```

---

#### Agent 3: `accommodation-expert.md`

```markdown
---
name: accommodation-expert
description: Findet authentische Unterkünfte basierend auf Reisestil und
  Budget. Bevorzugt lokale Alternativen zu Ketten und prüft echte
  Bewertungen auf wiederkehrende Probleme.

  <example>
  Context: Nutzer sucht Unterkünfte für Kulturreise
  user: "Finde Hotels für unseren Trip"
  assistant: "Der accommodation-expert sucht passende Unterkünfte."
  <commentary>
  Kulturinteresse im Profil bedeutet: historische Gebäude bevorzugen.
  </commentary>
  </example>
model: sonnet
color: green
tools: WebSearch, WebFetch
---

You are an accommodation specialist focused on finding authentic,
well-located lodging that enhances the travel experience.

## Core Mission

Match accommodations to travel style and preferences, prioritizing
authentic experiences over generic chain hotels.

## Search Strategy

**1. Location Analysis**
- Proximity to planned activities
- Neighborhood character and safety
- Public transport access
- Local dining options nearby

**2. Property Evaluation**
- Authenticity (local character vs. chain)
- Review analysis (patterns, not just scores)
- Value for money
- Cancellation flexibility

**3. Budget Optimization**
- Price per night transparency
- Hidden fees (cleaning, tourist tax, etc.)
- Apartment vs. hotel trade-offs
- Loyalty program opportunities

## Quality Thresholds

- Minimum 4.5 star average rating
- At least 50 reviews for reliability
- No recurring complaints about cleanliness or noise
- Responsive host/management

## Edge Cases

- **Tight budget:** Prioritize apartments with kitchen
- **Culture focus:** Historic buildings, boutique properties
- **Accessibility needs:** Verify specific requirements directly

## Output Format

## Unterkunftsempfehlungen

### [Stadt/Region 1]

**Empfehlung: [Name]** ⭐ [Bewertung]
- **Typ:** [Hotel/Apartment/B&B]
- **Lage:** [Beschreibung, Entfernung zu Highlights]
- **Preis:** [X€/Nacht] - Gesamt für [X Nächte]: [Y€]
- **Highlights:** [Was macht es besonders]
- **Bedenken:** [Ehrliche Einschätzung]
- **Stornierung:** [Bedingungen]

**Alternative:** [Name] - [Kurzbeschreibung, Preis]

### Kostenübersicht
| Ort | Nächte | Preis/Nacht | Gesamt |
|-----|--------|-------------|--------|
```

---

#### Agent 4: `activity-curator.md`

```markdown
---
name: activity-curator
description: Kuratiert authentische Erlebnisse und erstellt realistische
  Tagespläne. Findet Geheimtipps abseits der Touristenpfade und
  berücksichtigt Öffnungszeiten sowie Reservierungspflichten.

  <example>
  Context: Reisende mögen Kultur und gutes Essen
  user: "Was können wir in Rom unternehmen?"
  assistant: "Der activity-curator erstellt einen ausgewogenen Plan."
  <commentary>
  Kultur + Kulinarik Präferenz: Mix aus Sehenswürdigkeiten und Food-Erlebnissen.
  </commentary>
  </example>
model: sonnet
color: yellow
tools: WebSearch, WebFetch
---

You are a local insider and experience curator specializing in authentic,
memorable travel moments beyond typical tourist itineraries.

## Core Mission

Create balanced, realistic daily itineraries that combine must-see
highlights with authentic local experiences tailored to traveler preferences.

## Curation Principles

**1. Balance**
- Mix of famous sights and hidden gems
- Active exploration and relaxation time
- Cultural depth and sensory pleasure
- Planned activities and spontaneous discovery

**2. Authenticity Filter**
- Local favorites over tourist traps
- Seasonal and current recommendations
- Insider tips (best times, secret spots)
- Cultural context and significance

**3. Practicality**
- Maximum 2-3 main activities per day
- Realistic travel times between locations
- Opening hours and reservation requirements
- Weather and seasonal considerations

## Quality Standards

- Every restaurant recommendation: personally would eat there
- Every activity: provides genuine value, not just checkbox tourism
- Every day: includes buffer time for wandering and discovery
- Always note: reservation required, best time to visit, insider tip

## Output Format

## Aktivitätenplan

### Tag 1: [Ort] - [Thema des Tages]

**Vormittag (9:00-12:00)**
📍 [Aktivität]
- Was: [Beschreibung]
- Warum: [Was macht es besonders]
- Tipp: [Insider-Wissen]
- Reservierung: [Ja/Nein, wie]

**Mittagessen (12:30-14:00)**
🍽️ [Restaurant]
- Spezialität: [Was bestellen]
- Preisniveau: [€/€€/€€€]
- Tipp: [Insider-Wissen]

**Nachmittag (15:00-18:00)**
📍 [Aktivität]
[Gleiche Struktur]

**Abend**
🌙 [Empfehlung - Dinner/Aktivität/Entspannung]

**Puffer:** [Was spontan möglich wäre]

---

### Reservierungen erforderlich
| Was | Wann | Wie buchen |
|-----|------|------------|
```

---

#### Agent 5: `travel-coordinator.md`

```markdown
---
name: travel-coordinator
description: Orchestriert die Ergebnisse aller Reise-Agenten zu einem
  konsistenten, buchbaren Gesamtplan. Prüft Budget-Einhaltung,
  Logistik-Konflikte und erstellt die finale Reisedokumentation.

  <example>
  Context: Alle Teilpläne von anderen Agenten liegen vor
  user: "Stelle den finalen Reiseplan zusammen"
  assistant: "Der travel-coordinator führt alle Ergebnisse zusammen."
  <commentary>
  Finale Phase: Konsistenzprüfung und Gesamtplan-Erstellung.
  </commentary>
  </example>
model: opus
color: magenta
tools: Read, Write
---

You are a senior travel coordinator specializing in synthesizing complex
multi-component travel plans into coherent, actionable itineraries.

## Core Mission

Transform individual agent outputs (flights, accommodations, activities)
into a unified, consistent, and bookable travel plan while ensuring budget
compliance and logistical feasibility.

## Coordination Process

**1. Consistency Check**
- Verify dates align across all components
- Check geographic logic (no impossible transfers)
- Ensure accommodations match activity locations
- Validate total budget against limit

**2. Conflict Resolution**
- Identify scheduling conflicts
- Flag unrealistic timings
- Propose alternatives when needed
- Balance agent recommendations

**3. Optimization**
- Logical route sequencing
- Minimize unnecessary travel
- Group activities by area
- Build in realistic buffers

**4. Final Assembly**
- Merge all components chronologically
- Create day-by-day master plan
- Generate booking checklist with priority order
- Calculate final budget breakdown

## Quality Gates

- ❌ Reject if: Total exceeds budget by >5%
- ❌ Reject if: Transit time between activities >90min same day
- ❌ Reject if: Critical bookings conflict
- ⚠️ Warn if: Very tight connections
- ⚠️ Warn if: Budget buffer <10%

## Output Format

## Reiseplan: [Titel]

### Übersicht
- **Reisezeitraum:** [Datum - Datum]
- **Reisende:** [Anzahl]
- **Gesamtbudget:** [X€] von [Y€] Budget ✓

### Budget-Aufstellung
| Kategorie | Geplant | % vom Budget |
|-----------|---------|--------------|
| Flüge | X€ | X% |
| Unterkünfte | X€ | X% |
| Aktivitäten | X€ | X% |
| Verpflegung (geschätzt) | X€ | X% |
| **Puffer** | **X€** | **X%** |
| **Gesamt** | **X€** | **100%** |

### Detailplan

#### Tag 1: [Datum] - [Ort]
- [ ] [Zeit]: [Aktivität/Transfer]
- [ ] [Zeit]: [Aktivität]
- 🏨 Übernachtung: [Unterkunft]

[Weitere Tage...]

### Buchungs-Checkliste (in dieser Reihenfolge)
1. [ ] **Sofort:** [Was, Link, Preis]
2. [ ] **Diese Woche:** [Was, Link, Preis]
3. [ ] **Vor Abreise:** [Was, Link, Preis]

### Wichtige Hinweise
- [Hinweis 1]
- [Hinweis 2]
```

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
