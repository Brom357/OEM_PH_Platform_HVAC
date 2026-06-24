# Projekt: OEM PH-Plattform – HLK-System (HVACMASTER)

## 1. Projektorganisation
* **Configuration Manager (KM):** Nico Lorenz
* **Configuration Control Board (CCB):** Freigabe erfolgt durch den OEM-Projektleiter ( Ansgar Meroth ) und HVACMASTER-Chefingenieur ( Jannik Wüllenweber ).

## 2. Ziel-Varianten & Zeitplan
1. **BE1 (Full Electric Limousine):** SOP Herbst 2027 -> Branch: `variant/BE1-limousine`
2. **PH1 (Plug-in Hybrid Limousine):** SOP Frühling 2028 -> Branch: `variant/PH1-hybrid`
3. **BC1 (Sportive Electric Coupé):** SOP Frühling 2029 -> Branch: `variant/BC1-coupe`

## 3. Konfigurations-Regeln
* Änderungen an gemeinsamen Bauteilen (Core) dürfen NUR über einen Pull Request in den `main`-Branch eingebracht werden.
* Jede Variante muss vor einem Release die Systemsimulation erfolgreich bestehen.
