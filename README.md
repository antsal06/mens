# MENS — Motor-cortex · EMG · Neural-coupling · Study

> *"Mein Knie wird nach der Kreuzband-OP wieder stark — aber ich messe, ob mein Kopf dem Bein schon wieder vertraut."*

Ein selbstgebautes EEG-+-EMG-System, das untersucht, wie das Gehirn die Muskelansteuerung nach einer ACL-Rekonstruktion (vorderes Kreuzband, **STG-Technik**) wiedererlernt — gemessen an mir selbst, über die Reha-Wochen hinweg.

*(Arbeitstitel — der Name spielt auf MITs Motto* mens et manus *an: Kopf und Hand. Frei umbenennbar.)*

---

## 1. Worum geht es?

Nach einer Kreuzband-OP gibt es ein gut dokumentiertes Phänomen, die **arthrogene Muskelinhibition (AMI)**: Das Gehirn steuert die Beinmuskulatur des operierten Beins messbar schwächer an, selbst wenn der Muskel anatomisch intakt ist. Die *Kraft* kommt im Reha-Training oft schneller zurück als die *neuronale Kontrolle* — und genau diese Lücke gilt als Mit-Ursache für erhöhtes Re-Verletzungsrisiko. Die Standard-Reha misst sie kaum.

**Besonderheit meines Falls (STG-Rekonstruktion):** Bei mir wurden Semitendinosus- und Gracilissehne als Transplantat entnommen. Meine **Hamstrings** haben also nicht nur eine Inhibition, sondern eine *chirurgisch reale* Veränderung (Donor-Site-Morbidität) — der Semitendinosus regeneriert oft nur teilweise und mit veränderter Architektur. Deshalb sind die Hamstrings hier das **primäre Ziel**: funktionell kritisch, weil sie als ACL-Schützer wirken (sie ziehen die Tibia nach hinten und entlasten das Transplantat). Der Quadrizeps-Ansatz ist 1:1 übertragbar und dient als Vergleich.

Dieses Projekt baut ein Werkzeug, das **gleichzeitig** misst:
- **was der Muskel tut** (EMG, operiertes vs. gesundes Bein), und
- **wie das Gehirn den Befehl sendet** (EEG über dem Motorkortex, C3 und C4),

und daraus berechnet, **wie gut Gehirn und Muskel zusammenarbeiten** — und ob sich das über meine Reha normalisiert.

## 2. Forschungsfrage & Hypothese

**Primäre Forschungsfrage:**
Ist die Kopplung zwischen Motorkortex und **Hamstrings** im operierten (STG-)Bein schwächer oder anders als im gesunden Bein (Stand: 3 Monate post-OP) — und nähert sie sich über die folgenden Reha-Monate der Symmetrie an?

**Zweite Analyse-Achse (Ko-Kontraktion):**
Wie verhält sich die **Quadrizeps-Hamstring-Ko-Aktivierung** (beide EMG gleichzeitig) auf dem operierten Bein? Nach STG-Entnahme ist Timing/Verhältnis oft verändert — und das ist direkt ACL-Schutz-relevant.

**Hypothese (H1):**
Bei willentlicher isometrischer Kontraktion ist auf der operierten Seite mehr kortikaler Aufwand für gleich viel / weniger Muskel-Output nötig (ineffizientere Kopplung). Diese Asymmetrie nimmt über die Reha-Wochen ab.

**Nullhypothese (H0):**
Kein messbarer Kopplungsunterschied zwischen den Seiten bzw. keine systematische Veränderung über die Zeit.

> **Wichtig:** Auch ein klares H0-Ergebnis ("mit meinem Setup ist kein verlässlicher Unterschied messbar — hier ist warum") ist ein gültiges, ehrliches wissenschaftliches Resultat. Das Projekt scheitert nicht an einem Nullergebnis, sondern nur an unehrlicher Auswertung.

## 3. Wissenschaftlicher Hintergrund (Kurzfassung)

- **Kortikomuskuläre Kohärenz (CMC):** etabliertes Maß für die Kopplung zwischen Motorkortex-EEG und Muskel-EMG, typischerweise im **Beta-Band (15–30 Hz)**. → der **Nordstern** dieses Projekts.
- **Beta-ERD (event-related desynchronization):** Über dem Motorkortex sinkt die Beta-Aktivität kurz vor/während willentlicher Bewegung. Robust, einfacher als CMC. → die **Mittelstufe**.
- **Lateralität:** Linker Motorkortex (**C3**) → rechte Körperseite; rechter (**C4**) → linke. Damit lässt sich "rechts vs. links" direkt vergleichen.
- **AMI nach ACL** kann Monate persistieren — 3 Monate post-OP ist ein idealer Startpunkt für die Erholungskurve.
- **STG-Donor-Site:** Entnahme von Semitendinosus/Gracilis führt zu messbarem Hamstring-Defizit (v.a. bei tiefer Kniebeugung) und veränderter Aktivierung. Die Hamstrings sind ACL-Agonisten (Transplantat-Schutz).

**Suchbegriffe zum Vertiefen:** *corticomuscular coherence*, *arthrogenic muscle inhibition ACL*, *hamstring graft donor site morbidity*, *beta-band ERD motor cortex*, *neuroplasticity after ACL reconstruction*, *SENIAM surface EMG placement*, *10–20 EEG system*, *NMES quadriceps activation*.

## 4. Design-Entscheidungen (mit Begründung)

| # | Entscheidung | Begründung |
|---|--------------|------------|
| D1 | **EMG + EEG kombiniert**, nicht nur eins | Die Kopplung *zwischen* beiden Signalen ist der Kern. |
| D2 | **Kraftmaschine, isometrisch & submaximal** — nicht beim Laufen | EEG (µV) wird bei Bewegung von 10–100× größeren Artefakten in denselben Bändern überdeckt. Maschine + ruhige isometrische Halte minimiert das. **Bewusst kein 1RM** (Kieferpressen/Pressatmung zerschießen das EEG). |
| D3 | **Primär Hamstrings** (STG-Donor-Site), Quad als übertragbarer Vergleich | Die Hamstrings sind chirurgisch real verändert (Sehnenentnahme), funktionell ACL-schützend → klinisch spannender als reine Quad-Inhibition. |
| D4 | **Elektroden bei C3 / C4** | Minimal-Setup für die "rechts vs. links"-Frage (kontralaterale Steuerung). |
| D5 | **Ein synchroner Mehrkanal-Frontend (ADS1299)** | Für CMC müssen EEG und EMG auf *demselben Takt* abgetastet werden — technisch zwingend. |
| D6 | **Drei-Stufen-Architektur** (§7) | Graceful degradation: scheitert die CMC-Stufe an Rauschen, bleibt ein vollwertiges Projekt. |
| D7 | **Drahtlos (BLE)** als Standard-Transport | Galvanische Trennung by design → Sicherheit + weniger Netzbrumm. |
| D8 | **Erst kaufen/lernen, dann selbst layouten** | Rauschen löst man durch bewährtes Frontend + saubere Elektroden, nicht primär durch eigene Platine. Eigene PCB = dokumentierter Stretch. |
| D9 | **Reproduzierbare Positionierung per 3D-Rahmen** | Längsschnitt erfordert identische Elektrodenposition jede Session. |
| D10 | **Gold-Cup-Elektroden für EEG *und* EMG** (statt Einweg-Pads) | Voll wiederverwendbar (wichtig für Längsschnitt), ein Elektrodentyp = konsistente Eigenschaften. TENS-Pads nur fürs frühe Rumprobieren. |
| D11 | **Mess-Arm zuerst, Interventions-Arm (NMES) danach** (§15) | Erst sauber beobachten können, dann eingreifen und die Wirkung messen → von *beobachten* zu *intervenieren*. |
| D12 | **tDCS bleibt offene, unentschiedene Option** (§16) | Hirnstimulation hat eine viel höhere Sicherheits-Hürde als Muskelstimulation → bewusst nicht im Haupt-Plan. |

## 5. Systemarchitektur (Signalkette)

```
[Gold-Cup-Elektroden C3/C4]      ──┐
[Gold-Cup-EMG Hamstring L/R]     ──┤   (+ optional Quadrizeps für Ko-Kontraktion)
                                   ▼
                  [Analog-Frontend: ADS1299]   ← Verstärkung, 24-bit ADC, alle Kanäle synchron
                                   │  (SPI)
                                   ▼
                  [Mikrocontroller: ESP32]     ← Sampling, Pufferung, BLE-Stream
                                   │  (BLE, drahtlos = isoliert)
                                   ▼
                  [Laptop-Software (Open Source + Claude-built)]
                     ├─ BrainFlow  → Datenstrom in Python
                     ├─ Live-Signalqualität / Impedanz-Check
                     ├─ Filter (Bandpass, 50-Hz-Notch)
                     ├─ MNE-Python → Beta-ERD & Kohärenz
                     ├─ Dashboard (Next.js): C3/C4, EMG-Hüllkurven, Kopplungs-Metrik
                     └─ Session-Logging  ──►  [Längsschnitt-Datensatz]  ──►  [ML-Pipeline]
```

## 6. Einkaufsliste (Bill of Materials)

> **Preise sind grobe Richtwerte (Stand 2026) und schwanken** — Quellen vor dem Kauf prüfen. Ich kann dir aktuelle Bezugsquellen/Preise gezielt raussuchen.

### 6.1 Elektroden & Verbrauchsmaterial
| Teil | Zweck | Richtpreis |
|------|-------|-----------|
| Gold-Cup-Elektroden-Set (10–20 Stk.) | EEG (C3/C4 + Ref + Masse) **und** EMG — wiederverwendbar | ~35 € |
| Leitfähige Paste (z.B. Ten20) | Ankopplung der Gold-Cups | ~15 € |
| Peeling-/Prep-Gel (z.B. NuPrep) | senkt Hautwiderstand (Impedanz) | ~10 € |
| *(vorhanden)* TENS-Pads | nur für frühe Tests/Lernen — fürs Logging nicht ideal | 0 € |

### 6.2 Elektronik
| Teil | Zweck | Richtpreis |
|------|-------|-----------|
| **ADS1299**-Board (8 Kanäle, 24 bit) | Biopotential-Frontend für EEG **und** EMG, synchron | ~40–120 € (stark variabel) |
| *Alternative für v1:* BioAmp EXG Pill | Open-Hardware-Einstieg, 1 Kanal zum Lernen | ~25–30 €/Stk. |
| ESP32 Dev-Board | Sampling über SPI, BLE-Stream | ~8–12 € |
| LiPo-Akku + Lade-/Schutzmodul | **batteriebetrieben = isoliert** (Pflicht, §11) | ~12 € |
| Touchproof-Steckverbinder (DIN 1,5 mm) | Standard-Biopotential-Anschluss | ~10 € |
| Kabel, Header, Lochrasterplatine, Kleinteile | Aufbau/Verdrahtung | ~20 € |

### 6.3 Optional / Stretch
| Teil | Zweck | Richtpreis |
|------|-------|-----------|
| USB-Isolator | falls *kabelgebunden* an PC statt BLE (§14) | ~15–25 € |
| Eigene PCB (z.B. JLCPCB, 5 Stk.) | Phase-Upgrade: eigenes ADS1299-Layout | ~25–30 € inkl. Versand |
| *(vorhanden)* TENS/EMS-Gerät | Interventions-Arm NMES (§15) | 0 € |

### 6.4 Budget-Einordnung (ehrlich)
- **v1-Einstieg** (BioAmp-Lernpfad, EMG + 1 EEG-Kanal): ~120–150 € → oberer Bereich deines Budgets (100 € ± 50).
- **Vollsystem** (ADS1299, EEG + EMG synchron): eher **150–250 €** → leicht über Budget. Phasenweise aufbauen: erst Günstiges zum Lernen, dann ADS1299 als gezielte Investition.

## 7. Drei-Stufen-Architektur (Risikoabsicherung)

1. **Rückgrat (funktioniert immer):** EMG-Asymmetrie (Hamstrings operiert vs. gesund) bei isometrischer Kontraktion. Schon allein ein vollständiges Mini-Projekt.
2. **Mittelstufe:** EEG-Beta-ERD-Lateralität C3 vs. C4 während der Kontraktion.
3. **Nordstern:** Kortikomuskuläre Kohärenz (EEG↔EMG-Kopplung im Beta-Band).

## 8. Phasen / Roadmap

| Phase | Ziel | Erfolgskriterium |
|-------|------|------------------|
| **0 — Setup & Sicherheit** | Biopotential-Sicherheit, Dev-Umgebung, Löt-Basics mit Papa, Einlesen (10–20, CMC, SENIAM) | Sicheres, batteriebetriebenes Testsetup |
| **1 — EMG Proof of Concept** | Sauberes Einkanal-EMG, Erfassung + Visualisierung | Muskel anspannen → klares Signal |
| **2 — Dual-EMG** | Beide Hamstrings gleichzeitig, isometrisch | Erste Links/Rechts-Asymmetrie |
| **3 — EEG hinzufügen** | Sauberes C3/C4-Signal, Beta-ERD beobachten | ERD reproduzierbar erkennbar |
| **4 — Synchrones Mehrkanalsystem** | ADS1299: EEG+EMG auf einem Takt, CMC berechnen | Kohärenz-Wert pro Session |
| **5 — Längsschnitt** | Sessions über Wochen/Monate loggen | Datensatz mit ≥ X Sessions/Bein |
| **6 — Interventions-Arm (NMES)** | NMES anwenden, akute + längsschnittliche Wirkung messen (§15) | Vorher/Nachher-Effekt quantifizierbar |
| **7 — ML & Analyse** | Klassifikation operiert/gesund, Erholungskurve, Abgleich mit Reha-Tests | Belastbare Auswertung + Visualisierung |
| **8 — Dokumentation** | Ergebnisse ehrlich aufschreiben (inkl. Nullresultate), Portfolio/MIT | README + Bericht + öffentliches Repo |

*(tDCS, §16, ist bewusst **nicht** Teil dieser Roadmap — offene Option, später zu entscheiden.)*

## 9. Messprotokoll (Kern, wird in Phase 0–2 finalisiert)

- **EEG-Elektroden:** C3, C4; Referenz an Ohrläppchen/Mastoid; Masse separat.
- **EMG-Platzierung (nach SENIAM):** Hamstrings — **Biceps femoris lateral** als verlässlicher Abgriff; **medial** (Semitendinosus/-membranosus) als der "interessant-veränderte" Punkt nach ST-Entnahme. Optional Quadrizeps (Rectus femoris/Vastus medialis) für die Ko-Kontraktion.
- **Aufgabe:** standardisierte isometrische **Knie-Beugung** (Leg Curl, prone) für die Hamstrings; *übertragbar:* Knie-Streckung (Leg Extension) für den Quad. Submaximal, definierte Last/Winkel, **entspannter Kiefer**, ruhige Atmung, Kopf still.
- **Ablauf pro Trial:** Ruhe-Baseline → Kontraktion (definierte Dauer) → Ruhe. Mehrere Trials/Bein, randomisierte Reihenfolge.
- **Reproduzierbarkeit:** gleicher 3D-Positionierungsrahmen, gleiche Tageszeit, gleiches Aufwärmen.
- **Aufgezeichnet:** Roh-EEG (C3/C4) + Roh-EMG (Hamstrings L/R, optional Quad), Zeitstempel, Last/Winkel, subjektive Anstrengung (RPE).

## 10. 3D-Druck-Teile & Material

| Teil | Material | Begründung |
|------|----------|-----------|
| Kopf-/Positionierungsrahmen für C3/C4 | **TPU** (ggf. PLA-Gerüst + TPU-Pads) | flexibel, hautfreundlich, reproduzierbare Position |
| EMG-Halter/Gurt für Hamstrings (& Quad) | **TPU** | biegt sich mit, sitzt fest, drückt nicht |
| Gehäuse für Elektronik (ADS1299 + ESP32 + Akku) | **PLA** | starr, schützend, schnell & billig |
| Zugentlastungen / Kabelclips | **TPU** | schützt Lötstellen vor Kabelzug |

**Faustregel:** alles, was **Haut berührt oder sich biegt → TPU**; alles, was **starr schützen/tragen** soll → **PLA**.

## 11. ⚠️ Elektrische Sicherheit (nicht verhandelbar)

Du verbindest Elektroden mit deinem Körper. Mit Vorsicht völlig handhabbar, aber diese Regeln gelten **immer**:

1. **Nur Batteriebetrieb, solange Elektroden am Körper sind.** Niemals an Netzstrom oder an ein netzgespeistes/ladendes (geerdetes) Laptop angeschlossen messen.
2. **Drahtlos (BLE) übertragen** → galvanische Trennung by design. Falls kabelgebunden zum PC: **USB-Isolator** Pflicht (siehe §14).
3. Der ADS1299 ist ein hochohmiges Messfrontend — keine Ströme in den Körper einspeisen.
4. **Papa (Physiklehrer) reviewt den elektrischen Aufbau**, bevor erstmals Elektroden an den Körper kommen.
5. **NMES (§15):** nur mit dem dafür gebauten TENS/EMS-Gerät und nach dessen Anleitung; nicht über Herz/Hals/Karotis; **nicht gleichzeitig auf denselben Elektroden messen und stimulieren** (Stim-Artefakt überlagert/beschädigt das Recording — Standard: stimulieren *und dann* messen, oder getrennte Elektroden).
6. **Nicht an Personen mit Herzproblemen/Herzschrittmacher.** Gesunde Selbst-Experimentation.

## 12. Ethik & Geltungsbereich

- **Kein Medizinprodukt, keine Diagnose.** n = 1 Selbstexperiment.
- Einsichten für die Reha-Trainerin sind **explorativ** — medizinische/therapeutische Entscheidungen bleiben bei den Fachleuten.
- Ergebnisse werden **ehrlich** dokumentiert, inkl. Nullresultaten und Limitierungen.

## 13. Ehrliche Limitierungen (= wissenschaftliche Reife)

- **Wenige Kanäle:** "welche Hirnregionen aktiv sind" ist *nicht* drin. Möglich ist C3/C4-Lateralität, keine Source-Localization.
- **Bein-Motorkortex liegt medial/tief** (anders als die seitlich gut messbare Hand) → Bein-Laterität ist schwerer abzugreifen.
- **Quad vs. Hamstring kortikal nicht trennbar:** Beide liegen im selben medialen Bein-Areal. C3/C4 misst "Bein-Lateralität bei der jeweiligen Aufgabe", keinen muskel-spezifischen "Spot". Die muskel-spezifische Auflösung liegt auf der **EMG**-Seite.
- **Signalqualität** mit Hobby-Equipment + Cup-Elektroden im Haar bleibt grenzwertig; viel Aufwand fließt in saubere Ankopplung.
- **n = 1:** keine Verallgemeinerung, nur eine Einzelfall-Erholungskurve.
- **CMC ist analytisch anspruchsvoll** und rauschempfindlich → daher die Drei-Stufen-Absicherung.

## 14. Software-Stack & Laptop-Anbindung

**Mentales Modell (korrekt):** Das *Board* macht die Hardware (Verstärkung, ADC, Sampling), der *Laptop* die Auswertung.

**Transport — zwei saubere Wege:**
- **(a) Drahtlos (Standard):** ESP32 streamt per **BLE** an den Laptop. Inhärent isoliert, weniger Netzbrumm.
- **(b) Kabelgebunden:** nur mit **USB-Isolator** dazwischen *und/oder* Laptop im Akkubetrieb (Ladegerät raus) — sonst Fehlerstrompfad über den Körper.

**Software-Kette (Open Source + eigenes):**
- **BrainFlow** — holt den Datenstrom vom Board in Python (abstrahiert viele ADS1299-/OpenBCI-Boards).
- **MNE-Python** — Analyse: Filter, Beta-ERD, Kohärenz (CMC).
- **LSL (Lab Streaming Layer)** — optionaler Streaming-Standard, von vielen Tools gesprochen.
- **OpenBCI GUI** — schnelles Visualisieren, falls ein OpenBCI-kompatibles Board verwendet wird.
- **Eigenes (mit Claude):** Firmware (ESP32/SPI/BLE), DSP, **Next.js-Dashboard** (Live C3/C4, EMG-Hüllkurven, Kopplungs-Metrik, Signalqualität), Session-Logging, **ML-Pipeline** (Features: Beta-Power, ERD-Tiefe, CMC, EMG-RMS/Median-Frequenz; Klassifikation operiert/gesund; Modellierung der Erholungskurve; Abgleich mit funktionellen Reha-Tests).

## 15. Interventions-Arm: NMES (die Schleife schließen)

Vom *Beobachten* zum *Eingreifen* — und das macht das Projekt für MIT deutlich stärker.

- **Was:** **NMES/EMS** (neuromuskuläre Elektrostimulation) löst über das (vorhandene) TENS/EMS-Gerät echte Muskelkontraktionen aus. NMES des Quadrizeps ist **evidenzbasierter Standard** gegen genau die AMI, die hier untersucht wird — analog auf die Hamstrings anwendbar.
- **Unterschied zu reinem TENS:** TENS-Modus = sensorisch (Schmerz); **EMS-Modus = motorisch** (echte Kontraktion). Für die Aktivierung den EMS-Modus.
- **Experiment:** Baseline messen (EMG/EEG) → NMES-Protokoll anwenden → Wirkung **akut** (gleiche Session) und **längsschnittlich** (über Wochen) messen. Operiert vs. gesund vergleichen.
- **Forschungsfrage:** Verbessert NMES die willentliche Aktivierung / die kortikomuskuläre Kopplung der operierten Seite — und hält der Effekt an?
- **Sicherheit:** siehe §11 Punkt 5.

## 16. Optionale Erweiterung: tDCS — **noch nicht entschieden**

> Hier dokumentiert, weil es eine reale, zu deinem Problem passende Forschungsrichtung ist — **aber bewusst nicht im Haupt-Plan und nicht ohne fachliche Begleitung.**

- **Was:** **tDCS** (transkranielle Gleichstromstimulation) — schwacher Strom durch die Kopfhaut moduliert die kortikale Erregbarkeit. Wird tatsächlich für **AMI / kortikospinale Erregbarkeit nach Knieverletzung** beforscht.
- **Warum interessant:** Es zielt auf die *Gehirn*-Seite des Defizits, nicht nur den Muskel — der logische Gegenpol zu NMES.
- **Warum (noch) nicht im Plan — ehrlich:** Hirnstimulation hat eine **viel höhere Sicherheits-Hürde** als Muskelstimulation. DIY-tDCS trägt reale Risiken (Hautverbrennungen, Montage-Fehler, unklare Langzeiteffekte), und man kann kaum verifizieren, dass man es korrekt macht. **Empfehlung:** die Forschung lesen, und *falls* überhaupt, nur unter qualifizierter Begleitung — nicht solo am eigenen Gehirn. Bewusst als offene Option dokumentiert, Entscheidung später.

## 17. Was ich am Ende wissen will

- Wie groß ist meine Links/Rechts-Asymmetrie (Hamstrings) — und wie schrumpft sie über die Reha?
- Sendet mein Gehirn auf der operierten Seite "mehr Aufwand für weniger Output"?
- Normalisiert sich die Gehirn-Muskel-Kopplung über die Zeit?
- Ist die Quad-Hamstring-Ko-Aktivierung verändert (ACL-Schutz)?
- Verbessert NMES die Aktivierung — akut und dauerhaft?
- Hält meine **neuronale** Erholung mit meiner **Kraft**-Erholung Schritt — oder hinkt sie nach? *(Die in der ACL-Forschung offene Frage.)*

---

*Projekt von Anton — Selbstexperiment zur neuromuskulären Erholung nach ACL-Rekonstruktion (STG). Mens et manus.*