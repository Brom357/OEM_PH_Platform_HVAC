# Konfigurationsmanagement-Plan (CM-Plan) nach IEEE 828

**Projekt:** HLK-System für die OEM PH-Plattform  
**Dokumenten-ID:** HVAC-CMP-IEEE-828-V1.0  
**Status:** Freigegeben  

---

## 0. Dokumentenlenkung (Änderungshistorie)

| Version | Datum | Autor | Grund für Änderung | Status |
| :--- | :--- | :--- | :--- | :--- |
| V0.1 | 10.06.2026 | JW    | Erstausstellung (Entwurf) | In Prüfung |
| V1.0 | 24.06.2026 | JW    | Freigabe nach Concept Freeze Audit | Freigegeben |

---

## 1. Einleitung (Introduction)

### 1.1 Zweck und Geltungsbereich (Purpose & Scope)
Dieser CM-Plan regelt alle Aktivitäten zur Identifikation, Steuerung, Statusberichterstattung und Auditierung des HLK-Systems (Heizung, Lüftung, Klima) für die Modellplattform des OEMs. Der Plan ist für alle Projektbeteiligten der HVACMASTER sowie für Zulieferer verbindlich. Er umfasst die drei Fahrzeugvarianten:
* **BE1** (Full Electric Limousine, SOP Herbst 2027)
* **PH1** (Plug-in Hybrid Limousine, SOP Frühling 2028)
* **BC1** (Sportive Electric Coupé, SOP Frühling 2029)

### 1.2 Referenzen und mitgeltende Dokumente (References)
* *IEEE 828-2012 Standard for Configuration Management in Systems and Software Engineering*
* *Lastenheft des OEMs für die PH-Plattform (HLK-Spezifikation)*
* *ISO 26262 (Funktionale Sicherheit im Automotive-Bereich)*

---

## 2. KM-Organisation und Verantwortlichkeiten (Management)

### 2.1 Organisationsstruktur & Rollen
* **Configuration Manager (KM-Verantwortlicher):** Verantwortlich für die Einhaltung dieses Plans, das Einrichten des Git-Repositories, die Vergabe von Zugriffsrechten, die Durchführung von Audits und das Setzen von Meilenstein-Tags.
* **Configuration Control Board (CCB / Änderungskomitee):** Das Gremium besteht aus dem HVACMASTER-Chefingenieur, dem Produktmanager und dem OEM-Projektleiter. Es besitzt die alleinige Entscheidungsbefugnis über die Genehmigung von Änderungsanträgen (Change Requests), die Auswirkung auf Projektmeilensteine oder variantenübergreifende Baselines haben.
* **Entwickler (Hardware/Software):** Verantwortlich für die Erstellung und Modifikation von CIs innerhalb der zugewiesenen Branches sowie die Durchführung von Code-Reviews via Pull Requests.

---

## 3. Konfigurationsidentifikation (Configuration Identification)

### 3.1 Identifikation der Konfigurationseinheiten (CIs)
Das System wird in logische Einheiten zerlegt, die unter strikter Versionskontrolle im Git-Repository `oem-ph-platform-hvac` verwaltet werden:

* **Management & Prozesse:** `CM/CM-Plan.md`, `CM/audit.md`, `CM/error_list.md`
* **Anforderungen:** `requirements/legal_requirements.md`, `requirements/core_spec.md`
* **Hardware (Mechanik):** `hardware/geometry/luftkanaele.step`, `hardware/specs/klimaduesen.pdf`, `hardware/specs/reinluftfilter.json`
* **Elektrik/Elektronik (E/E):** `ee/communication/can_matrix.dbc`, `ee/schemas/pinout_base.pdf`
* **Software-Core:** `software/core/climatronic_regler.c`, `software/core/sensor_fusion.c`
* **Variantensteuerung:** `config/system_architecture.json` (Fahrzeugspezifische Parameter)

### 3.2 Benennungs- und Versionierungskonventionen
* **Repository-Name:** `oem-ph-platform-hvac`
* **Commits:** Verpflichtende Nutzung von *Conventional Commits* (z. B. `feat(hvac-core): ...`, `fix(hvac-be1): ...`).
* **Baselines:** Werden über Git Tags nach dem Schema `v[Major].[Minor].[Patch]-[Meilenstein]-[Variante]` (z. B. `v1.0.0-SOP-BE1`) fixiert.

---

## 4. Konfigurationssteuerung (Configuration Control)

### 4.1 Branching-Strategie (Workflow)
* **`main`-Branch:** Repräsentiert die geprüfte und stabile Plattform-Basis (Common Core). Direkte Commits sind per Branch-Protection-Rule gesperrt.
* **`variant/*`-Branches:** Langlebige, isolierte Entwicklungsbranches für die Fahrzeugvarianten:
  * `variant/BE1-limousine`
  * `variant/PH1-hybrid`
  * `variant/BC1-coupe`

### 4.2 Änderungsmanagement-Prozess (Change Management)
1. **Antrag:** Einreichung eines Change Requests (CR) bei technischen Abweichungen (z. B. Erhöhung der Wärmepumpenleistung von 1,5 kW auf 2,0 kW).
2. **Auswirkungsanalyse:** Der Configuration Manager prüft die Seiteneffekte auf andere Branches/Fahrzeuge.
3. **Entscheidung:** Das CCB gibt die Änderung frei oder lehnt sie ab.
4. **Integration:** Die Umsetzung erfolgt im spezifischen Varianten-Branch. Der Commit-Kommentar muss die CCB-Freigabe referenzieren.

---

## 5. Konfigurationsstatusbericht (Configuration Status Accounting)

Der Status aller CIs und Branches wird kontinuierlich überwacht:
* **Nachverfolgbarkeit (Traceability):** Jede Änderung an einer Datei muss über die Git-Historie (`git log`, `git blame`) eindeutig einem Entwickler, einem Datum und einer CCB-Ticketnummer zugeordnet werden können.
* **Berichterstattung:** Wöchentlicher automatisierter Export des Git-Graphen sowie des Status offener Pull Requests an die Projektleitung.

---

## 6. Konfigurationsaudits und Reviews (Configuration Audits)

Vor dem Einfrieren einer neuen Baseline oder einem Produktions-Release (SOP) führt der Configuration Manager Audits durch:

* **Functional Configuration Audit (FCA):** Überprüfung, ob das System die funktionalen Anforderungen erfüllt. Die Testergebnisse aus `testing/test_cases_core.py` sowie thermische Simulationsberichte müssen zu 100% erfolgreich vorliegen.
* **Physical Configuration Audit (PCA):** Abgleich der im Git-Branch eingecheckten CIs (Dokumente, Software, CAD) mit der realen, freizugebenden Stückliste. 
* **Dokumentation:** Die Ergebnisse des Audits und verbleibende Restrisiken werden in den Dateien `CM/audit.md` und `CM/error_list.md` im jeweiligen Branch revisionssicher dokumentiert.

---

## 7. Werkzeuge, Infrastruktur und Datenerhalt (Tools & Backups)

* **Versionsverwaltung:** Git (gehostet auf dediziertem, ausfallsicherem Server).
* **Entwicklungsumgebung:** Visual Studio Code (vorgeschriebene KM-Erweiterung: GitLens).
* **Datensicherung (Backup):** Tägliche, inkrementelle automatisierte Backups des Git-Servers auf ein geografisch getrenntes Speichermedium.
* **Archivierung (Retention):** Release-relevante Meilenstein-Tags unterliegen einer gesetzlichen Aufbewahrungspflicht von 15 Jahren nach Produktionsende (SOP) zur Absicherung gegen Produkthaftungsrisiken.