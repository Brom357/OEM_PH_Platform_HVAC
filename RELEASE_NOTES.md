# Release Notes - HLK-System BE1 Limousine

**Release-Version:** v1.0.0-SOP-BE1  
**Datum:** 15.10.2027  
**Basiert auf Plattform-Baseline:** v0.2.0-Base-Freeze  

## Übersicht
Dieses Release beinhaltet die finale, serienreife Konfiguration des Heiz-, Lüftungs- und Klimasystems (HLK) für die Full Electric Limousine (BE1).

## Wichtigste Änderungen gegenüber der Plattform-Basis:
* **Hardware:** Upgrade des Kompressors auf eine **2,0 kW bidirektionale Wärmepumpe** (COP 3.0) zur Sicherung der Batteriekühlung beim Schnellladen (genehmigt via Ticket #HLK-402).
* **Software:** Integration der automatisierten **Preconditioning-Logik** zur Innenraum-Vorkonditionierung.
* **Bugfixes:** Behebung des Anlaufproblems des Kompressors bei Temperaturen um den Gefrierpunkt (#BUG-BE1-08).

## Bekannte Einschränkungen (Restrisiken)
* Übersetzungs-Strings für den asiatischen Markt in `klimaduesen.pdf` sind noch im Entwurfsstatus. Ein Delta-Release erfolgt zu Meilenstein *Design Freeze Asien*.