# Offene und behobene Fehlerliste (Abweichungsbericht)

**Baseline-Zuordnung:** v0.2.0 (Base Freeze)  
**Letzte Aktualisierung:** 24.06.2026  

---

## 1. Behobene Fehler (Resolved Issues)

### ID: BUG-001
*   **Komponente:** `software/core/sensor_fusion.c`
*   **Beschreibung:** Der Sensor-Fusion-Algorithmus lieferte sporadisch fehlerhafte Temperatur-Mittelwerte bei extremen Minusgraden (Simulation bei -20°C).
*   **Lösung:** Filter-Logik (Plausibilitätsprüfung der Sensorrohdaten) überarbeitet. Der anschließende Testlauf verlief erfolgreich.
*   **Status:** **BEHOBEN**

---

## 2. Offene Fehler / Abweichungen (Open Deviations)

### ID: BUG-002
*   **Komponente:** `hardware/specs/klimaduesen.pdf`
*   **Beschreibung:** In den Spezifikationen der Klimadüsen fehlen noch die finalen Übersetzungs-Strings für den asiatischen Markt (Metadaten).
*   **KM-Bewertung:** Unkritisch für den rein technischen Plattform-Freeze im aktuellen Meilenstein.
*   **CCB-Entscheidung:** Die Abweichung wird für den *Concept Freeze* akzeptiert. Der Fehler muss zwingend bis zum *Design Freeze* der jeweiligen Fahrzeugvarianten (`variant/*`) behoben sein.
*   **Status:** **OFFEN (AKZEPTIERT)**