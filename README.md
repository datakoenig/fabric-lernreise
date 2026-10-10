# Fabric Einsteiger-Lernreise – Testdaten

Synthetische Testdaten für den Beispielfall „Anlagenbau Muster GmbH" der Fabric Einsteiger-Lernreise von platformimpulse. Alle Werte, Firmennamen, Adressen und E-Mail-Adressen sind erfunden. Zeitraum 01.2024 bis 09.2026.

## Ordner = Quelle

Alle Dateien liegen in `Testdaten/`. Der Unterordner sagt, wo die Datei im Kurs liegt. Jede Quelle kommt einmal vor, mit dem Ladewerkzeug, das zu ihr passt.

| Ordner | Quelle im Kurs | Inhalt | Werkzeug | Video |
|---|---|---|---|---|
| `fabric_sql/` | Fabric SQL Database `SQLDB_SAP_Stammdaten`, Schema `sap` | `SQLDB_SAP_Stammdaten.sql` legt `sap.LFA1` (80 Lieferanten) und `sap.MARA` (420 Materialien) an und befüllt sie. `csv_fallback/` nur, falls die Datenbank nicht verfügbar ist. | Dataflow Gen2 | 1.2 |
| `azure_sap-export/` | ADLS Gen2, Container `sap-export` | `stammdaten/Kunden.csv` (SE16-Download eines Kollegen, deutsches Format) · `stammdaten/DD03T_Feldtexte.csv` · `schnittstelle/2026-09/`: Projekte, Kundenauftraege, Bestellungen, Wareneingaenge · `schnittstelle/2026-10_nachtrag/` (ab Woche 3) · `schnittstelle/2026-11_v2/` (ab Woche 4) | Dataflow Gen2 (Kunden) · Pipeline Copy Data (Schnittstelle) · Shortcut | 1.2 · 1.3 · 1.4 · 3.2 · 4.4 |
| `sharepoint_vertrieb/` | SharePoint-Bibliothek „Lernreise Fabric/Vertrieb" | `Forecast_Vertrieb.xlsx` (Vertriebs-Pipeline, 3 Blätter) · `Kunden_Mapping.csv` (ab Woche 2) | Dataflow Gen2 | 2.4 |
| `manueller_upload/` | Du lädst selbst hoch | `Regionen_Berechtigungen.csv` | Upload + „Als Tabelle laden" | 2.2 / 4.3 |
| `trainer_referenz/` | Trainer-Lakehouse `LH_Referenz` | `Wechselkurse.csv` — Fallback, falls `api.frankfurter.app` nicht erreichbar ist; normal entsteht die Tabelle live per Web-Connector | Dataflow Gen2 → Shortcut | 1.1 / 1.4 |

## Zwei Dateiformate, mit Absicht

Schnittstellen-Exporte (`schnittstelle/`, `DD03T`) sind maschinell: Trennzeichen `,`, UTF-8 ohne BOM, Punkt als Dezimaltrenner, ISO-Datum `JJJJ-MM-TT`, alle Texte in Anführungszeichen.

Von Menschen erzeugte Dateien (`Kunden.csv`, SharePoint, Upload, Wechselkurse-Fallback) sind deutsch: Trennzeichen `;`, UTF-8 mit BOM, `1.234,56`, `TT.MM.JJJJ`, SAP-Nummern mit führenden Nullen als Text.

`Projekte.csv` enthält Projekt-Kopfzeilen (z. B. `P-2025-027`) und darunter je fünf PSP-Elemente (`P-2025-027.1` … `.5`). Aufträge und Bestellungen verweisen auf PSP-Elemente, der Auftragswert steht nur auf dem Kopf.

## Fabric SQL Database befüllen

Im Workspace eine Fabric SQL Database `SQLDB_SAP_Stammdaten` anlegen, den Query-Editor öffnen, `Testdaten/fabric_sql/SQLDB_SAP_Stammdaten.sql` komplett einfügen und ausführen (ca. 2 Minuten). Die Abschlussabfrage zeigt 80 / 420 Zeilen. Das Skript lässt sich beliebig oft wiederholen.

## Hinweis

Die Daten sind wie im echten Leben nicht ganz sauber. Schau genau hin, bevor du ihnen traust.

## Download

Ganzes Paket: grüner Button **Code → Download ZIP**. Die Dateien bitte nicht in Excel öffnen und wieder speichern — Trennzeichen, BOM und Zahlenformate sind Teil der Übung.
