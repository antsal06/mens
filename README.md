# MENS — Motor-cortex · EMG · Neural-coupling · Study

> *"Mein Knie wird nach der Kreuzband-OP wieder stark — aber ich messe, ob mein Kopf dem Bein schon wieder vertraut."*

Ein selbstgebautes EEG-+-EMG-System, das untersucht, wie das Gehirn die Muskelansteuerung nach einer ACL-Rekonstruktion (vorderes Kreuzband) wiedererlernt — gemessen an mir selbst, über die Reha-Wochen hinweg.

*(Arbeitstitel — der Name spielt auf MITs Motto* mens et manus *an: Kopf und Hand. Frei umbenennbar.)*

---

## 1. Worum geht es?

Nach einer Kreuzband-OP gibt es ein gut dokumentiertes Phänomen, die **arthrogene Muskelinhibition (AMI)**: Das Gehirn steuert den Quadrizeps des operierten Beins messbar schwächer an, selbst wenn der Muskel anatomisch intakt ist. In der Praxis heißt das: Die *Kraft* kommt im Reha-Training oft schneller zurück als die *neuronale Kontrolle*. Genau diese Lücke gilt als Mit-Ursache für ein erhöhtes Re-Verletzungsrisiko — und die Standard-Reha misst sie kaum, weil sie auf Kraft und Beweglichkeit schaut, nicht auf das Gehirn.

Dieses Projekt baut ein Werkzeug, das **gleichzeitig** misst:
- **was der Muskel tut** (EMG des Quadrizeps, links und rechts), und
- **wie das Gehirn den Befehl sendet** (EEG über dem Motorkortex, C3 und C4),

und daraus berechnet, **wie gut Gehirn und Muskel zusammenarbeiten** — und ob sich das über meine Reha normalisiert.

## 2. Forschungsfrage & Hypothese

**Forschungsfrage:**
Ist die Kopplung zwischen Motorkortex und Quadrizeps in meinem operierten Bein schwächer oder anders als im gesunden Bein (Stand: 3 Monate post-OP) — und nähert sie sich über die folgenden Reha-Monate der Symmetrie an?

**Hypothese (H1):**
Bei willentlicher isometrischer Quadrizeps-Kontraktion ist auf der operierten Seite mehr kortikaler Aufwand für weniger / gleich viel Muskel-Output nötig (ineffizientere Kopplung). Diese Asymmetrie nimmt über die Reha-Wochen ab.

**Nullhypothese (H0):**
Es gibt keinen messbaren Unterschied der Kopplung zwischen den Seiten, bzw. keine systematische Veränderung über die Zeit.

> **Wichtig:** Auch ein klares H0-Ergebnis ("mit meinem Setup ist kein verlässlicher Unterschied messbar — hier ist warum") ist ein gültiges, ehrliches wissenschaftliches Resultat. Das Projekt scheitert nicht an einem Nullergebnis; es scheitert nur an unehrlicher Auswertung.

## 3. Wissenschaftlicher Hintergrund (Kurzfassung)

- **Kortikomuskuläre Kohärenz (CMC):** etabliertes Maß für die Kopplung zwischen Motorkortex-EEG und Muskel-EMG, typischerweise im **Beta-Band (15–30 Hz)**. Spiegelt, wie synchron Kortex und Muskel "kommunizieren". → der **Nordstern** dieses Projekts.
- **Beta-ERD (event-related desynchronization):** Über dem Motorkortex sinkt die Beta-Aktivität kurz vor und während willentlicher Bewegung. Robust messbar, einfacher als CMC. → die **Mittelstufe**.
- **Lateralität:** Der *linke* Motorkortex (Elektrode **C3**) steuert die *rechte* Körperseite, der *rechte* (**C4**) die linke. Damit lässt sich "rechts vs. links" direkt vergleichen.
- **AMI nach ACL:** Aktivierungsdefizit des Quadrizeps, kann Monate persistieren — 3 Monate post-OP ist ein idealer Startpunkt, um die Erholungskurve einzufangen.

**Suchbegriffe zum Vertiefen:** *corticomuscular coherence*, *arthrogenic muscle inhibition ACL*, *beta-band ERD motor cortex*, *neuroplasticity after ACL reconstruction*, *10–20 EEG system*.

## 4. Design-Entscheidungen (mit Begründung)

| # | Entscheidung | Begründung |
|---|--------------|------------|
| D1 | **EMG + EEG kombiniert**, nicht nur eins | Die Kopplung *zwischen* beiden Signalen ist der Kern. EMG allein misst nur den Muskel, EEG allein nur das Gehirn. |
| D2 | **Messung in der Kraftmaschine, isometrisch & submaximal** — nicht beim Laufen | EEG (µV-Bereich) wird bei Bewegung von Artefakten überdeckt, die 10–100× größer sind und in denselben Frequenzbändern liegen. Eine stabilisierende Maschine + ruhige isometrische Halte minimiert Kopf-/Nackenartefakte. **Bewusst kein 1RM** — maximales Grinden erzeugt Kieferpressen + Pressatmung, was das EEG zerschießt. |
| D3 | **Elektroden bei C3 / C4** | Minimal-Setup, das die "rechts vs. links"-Frage direkt adressiert (kontralaterale Steuerung). |
| D4 | **Ein synchroner Mehrkanal-Frontend (ADS1299)** statt mehrerer Einzelmodule | Für die Kohärenz-Berechnung müssen EEG und EMG auf *demselben Takt* abgetastet werden. Das ist technisch zwingend, kein Show-off. |
| D5 | **Drei-Stufen-Architektur** (siehe §7) | Graceful degradation: Wenn die ambitionierte CMC-Stufe zu verrauscht ist, bleibt aus den unteren Stufen ein vollwertiges Projekt. |
| D6 | **Drahtlose Datenübertragung (BLE)** | Galvanische Trennung "by design" → Sicherheit (siehe §11) und weniger Netzbrumm-Artefakte. |
| D7 | **Erst kaufen / lernen, dann selbst layouten** | Das Rauschproblem löst man durch ein bewährtes Frontend-Design, gute Elektroden und saubere Referenz/Masse — nicht primär durch eine selbstgefertigte Platine. Eigene PCB = dokumentierter Stretch (Phase-Upgrade), nicht Startpunkt. |
| D8 | **Reproduzierbare Elektrodenpositionierung per 3D-Rahmen** | Für einen *Längsschnitt* muss C3/C4 jede Session am gleichen Punkt sitzen, sonst vergleicht man Äpfel mit Birnen. |
| D9 | **Längsschnitt ab Monat 3** | Fängt die Erholungskurve ein, statt sie zu verpassen. |

## 5. Systemarchitektur (Signalkette)

```
[Gold-Cup-Elektroden C3/C4]  ──┐
[EMG-Elektroden Quad L/R]    ──┤
                               ▼
                  [Analog-Frontend: ADS1299]   ← Verstärkung, 24-bit ADC, alle Kanäle synchron
                               │  (SPI)
                               ▼
                  [Mikrocontroller: ESP32]     ← Sampling, Pufferung, BLE-Stream
                               │  (BLE, drahtlos = isoliert)
                               ▼
                  [Software-Frontend (Claude-built)]
                     ├─ Live-Signalqualität / Impedanz-Check
                     ├─ Filter (Bandpass, Notch 50 Hz)
                     ├─ Beta-ERD & CMC-Berechnung
                     ├─ Dashboard (Next.js): C3/C4, EMG-Hüllkurven, Kopplungs-Metrik
                     └─ Session-Logging  ──►  [Längsschnitt-Datensatz]  ──►  [ML-Pipeline]
```

## 6. Einkaufsliste (Bill of Materials)

> **Preise sind grobe Richtwerte (Stand 2026) und schwanken** — Bezugsquellen vor dem Kauf prüfen. Ich kann dir aktuelle Quellen/Preise gezielt raussuchen.

### 6.1 Elektroden & Verbrauchsmaterial
| Teil | Zweck | Richtpreis |
|------|-------|-----------|
| Gold-Cup-Elektroden-Set (10–20 Stk.) | EEG an C3/C4 + Referenz + Masse; Reserve | ~35 € |
| Leitfähige Paste (z.B. Ten20) | Ankopplung Gold-Cups an Kopfhaut | ~15 € |
| Peeling-/Prep-Gel (z.B. NuPrep) | senkt Hautwiderstand (Impedanz) | ~10 € |
| Einweg-Klebeelektroden (Ag/AgCl, Pack) | EMG auf Quadrizeps L/R (einfacher als Cups) | ~10 € |

### 6.2 Elektronik
| Teil | Zweck | Richtpreis |
|------|-------|-----------|
| **ADS1299**-Board (8 Kanäle, 24 bit) | Biopotential-Frontend für EEG **und** EMG, synchron | ~40–120 € (stark variabel) |
| *Alternative für v1:* BioAmp EXG Pill (Upside Down Labs) | Open-Hardware-Einstieg, 1 Kanal EEG/EMG zum Lernen | ~25–30 € / Stück |
| ESP32 Dev-Board | Sampling über SPI, BLE-Stream | ~8–12 € |
| LiPo-Akku + Lade-/Schutzmodul | **batteriebetrieben = isoliert** (Pflicht, siehe §11) | ~12 € |
| Touchproof-Steckverbinder (DIN 1,5 mm) | Standard-Anschluss für Biopotential-Elektroden | ~10 € |
| Kabel, Header, Lochrasterplatine, Widerstände, Kleinteile | Aufbau/Verdrahtung | ~20 € |

### 6.3 Optional / Stretch
| Teil | Zweck | Richtpreis |
|------|-------|-----------|
| USB-Isolator | falls *kabelgebunden* an PC statt BLE | ~15–25 € |
| Eigene PCB (z.B. JLCPCB, 5 Stk.) | Phase-Upgrade: eigenes ADS1299-Layout | ~25–30 € inkl. Versand |

### 6.4 Budget-Einordnung (ehrlich)
- **v1-Einstieg** (BioAmp-Lernpfad, EMG + 1 EEG-Kanal): ~120–150 € → im oberen Bereich deines Budgets (100 € ± 50).
- **Vollsystem** (ADS1299, 2× EEG + 2× EMG synchron): eher **150–250 €** → leicht über Budget. Bewusst phasen-weise aufbauen: erst das Günstige zum Lernen, dann das ADS1299-Board als gezielte Investition.

## 7. Drei-Stufen-Architektur (Risikoabsicherung)

1. **Rückgrat (funktioniert immer):** EMG-Asymmetrie beider Quadrizeps bei isometrischer Kontraktion. → Schon das allein ist ein vollständiges Mini-Projekt.
2. **Mittelstufe:** EEG-Beta-ERD-Lateralität C3 vs. C4 während der Kontraktion.
3. **Nordstern:** Kortikomuskuläre Kohärenz (EEG↔EMG-Kopplung im Beta-Band).

## 8. Phasen / Roadmap

| Phase | Ziel | Erfolgskriterium |
|-------|------|------------------|
| **0 — Setup & Sicherheit** | Biopotential-Sicherheit verstehen, Dev-Umgebung, Löt-Basics mit Papa (Physiklehrer), 10–20-System & CMC einlesen | Sicheres, batteriebetriebenes Testsetup steht |
| **1 — EMG Proof of Concept** | Sauberes Einkanal-EMG, Erfassung + Visualisierung | Muskel anspannen → klares Signal sichtbar |
| **2 — Dual-EMG** | Beide Quadrizeps gleichzeitig, isometrisch | Erste echte Links/Rechts-Asymmetrie-Daten |
| **3 — EEG hinzufügen** | Sauberes C3/C4-Signal bei Kontraktion, Beta-ERD beobachten | ERD reproduzierbar erkennbar |
| **4 — Synchrones Mehrkanalsystem** | ADS1299: EEG+EMG auf einem Takt, CMC berechnen | Kohärenz-Wert pro Session berechenbar |
| **5 — Längsschnitt** | Sessions über Wochen/Monate loggen | Datensatz mit ≥ X Sessions pro Bein |
| **6 — ML & Analyse** | Klassifikation operiert/gesund, Erholungskurve modellieren, mit Reha-Tests abgleichen | Belastbare Auswertung + Visualisierung |
| **7 — Dokumentation** | Ergebnisse ehrlich aufschreiben (inkl. Nullresultate), Portfolio/MIT | README + Bericht + Repo öffentlich |

## 9. Messprotokoll (Kern, wird in Phase 0–2 finalisiert)

- **Elektroden:** C3, C4 (EEG); Referenz an Ohrläppchen/Mastoid; Masse separat; EMG bipolar über jedem Vastus medialis/Rectus femoris.
- **Aufgabe:** standardisierte isometrische Quadrizeps-Kontraktion in der Maschine, submaximal (z.B. fester %-Anteil oder definierter Winkel/Last), **entspannter Kiefer**, ruhige Atmung, Kopf still.
- **Ablauf pro Trial:** Ruhe-Baseline → Kontraktion (definierte Dauer) → Ruhe. Mehrere Trials pro Bein, randomisierte Reihenfolge.
- **Reproduzierbarkeit:** gleicher 3D-Positionierungsrahmen, gleiche Tageszeit, gleiche Aufwärm-Routine jede Session.
- **Aufgezeichnet:** Rohsignale EEG (C3/C4) + EMG (L/R), Zeitstempel, Last/Winkel, subjektive Anstrengung (RPE).

## 10. 3D-Druck-Teile & Material

| Teil | Material | Begründung |
|------|----------|-----------|
| Kopf-/Positionierungsrahmen für C3/C4 | **TPU** (ggf. PLA-Gerüst + TPU-Pads) | flexibel, hautfreundlich, hält Elektroden reproduzierbar an Position |
| EMG-Halter/Gurt für Quadrizeps | **TPU** | biegt sich mit dem Bein mit, sitzt fest, drückt nicht |
| Gehäuse für Elektronik (ADS1299 + ESP32 + Akku) | **PLA** | starr, schützend, schnell & billig zu drucken |
| Zugentlastungen / Kabelclips | **TPU** | flexibel, schützt Lötstellen vor Kabelzug |

**Faustregel:** alles, was **Haut berührt oder sich biegt → TPU**; alles, was **starr schützen/tragen** soll → **PLA**.

## 11. ⚠️ Elektrische Sicherheit (nicht verhandelbar)

Du verbindest Elektroden mit deinem Körper. Das ist mit Vorsicht völlig handhabbar, aber diese Regeln gelten **immer**:

1. **Nur Batteriebetrieb, solange Elektroden am Körper sind.** Niemals an Netzstrom oder an ein netzgespeistes/ladendes (geerdetes) Laptop angeschlossen messen.
2. **Drahtlos (BLE) übertragen** → galvanische Trennung by design. Falls doch kabelgebunden zum PC: **USB-Isolator** dazwischen, Pflicht.
3. Der ADS1299 ist ein hochohmiges Messfrontend, ausgelegt für Biopotentiale — keine Ströme in den Körper einspeisen.
4. **Papa (Physiklehrer) reviewt den elektrischen Aufbau**, bevor zum ersten Mal Elektroden an den Körper kommen.
5. **Nicht an Personen mit Herzproblemen/Herzschrittmacher.** Dieses Projekt ist gesunde Selbst-Experimentation.

## 12. Ethik & Geltungsbereich

- **Kein Medizinprodukt, keine Diagnose.** n = 1 Selbstexperiment.
- Einsichten für die Reha-Trainerin sind **explorativ** — medizinische/therapeutische Entscheidungen bleiben bei den Fachleuten.
- Ergebnisse werden **ehrlich** dokumentiert, inklusive Nullresultaten und Limitierungen.

## 13. Ehrliche Limitierungen (= wissenschaftliche Reife)

- **Wenige Kanäle:** "welche Hirnregionen aktiv sind" ist *nicht* drin. Möglich ist C3/C4-Lateralität, nicht Source-Localization.
- **Bein-Motorkortex liegt medial/tief** (anders als die seitlich gut messbare Hand) → Bein-Laterität ist schwerer abzugreifen als Hand-Laterität.
- **Signalqualität** mit Hobby-Equipment und Cup-Elektroden im Haar bleibt grenzwertig; viel Aufwand fließt in saubere Ankopplung.
- **n = 1:** keine Verallgemeinerung, nur eine Einzelfall-Erholungskurve.
- **CMC ist analytisch anspruchsvoll** und empfindlich gegenüber Rauschen → deshalb die Drei-Stufen-Absicherung.

## 14. Software-Stack (mit Claude gebaut)

- **Firmware (ESP32):** SPI-Treiber für ADS1299, Sampling, BLE-Stream.
- **Erfassung & DSP (Python):** Bandpass + 50-Hz-Notch, Artefakt-Erkennung, Beta-ERD, Kohärenz.
- **Frontend (Next.js):** Live-Dashboard (C3/C4, EMG-Hüllkurven, Kopplungs-Metrik, Signalqualität), Session-Steuerung.
- **Datenhaltung:** strukturiertes Logging jeder Session → Längsschnitt-Datensatz.
- **ML-Pipeline:** Feature-Extraktion (Beta-Power, ERD-Tiefe, CMC, EMG-RMS/Median-Frequenz), Klassifikation operiert/gesund, Modellierung der Erholungskurve, Abgleich mit funktionellen Reha-Tests.

## 15. Was ich am Ende wissen will

- Wie groß ist meine Links/Rechts-Asymmetrie — und wie schrumpft sie über die Reha?
- Sendet mein Gehirn auf der operierten Seite "mehr Aufwand für weniger Output"?
- Normalisiert sich die Gehirn-Muskel-Kopplung über die Zeit?
- Hält meine **neuronale** Erholung mit meiner **Kraft**-Erholung Schritt — oder hinkt sie nach? *(Die eigentlich spannende, in der ACL-Forschung offene Frage.)*

---

*Projekt von Anton — Selbstexperiment zur neuromuskulären Erholung nach ACL-Rekonstruktion. Mens et manus.*