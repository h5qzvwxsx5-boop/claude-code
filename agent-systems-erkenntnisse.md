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
