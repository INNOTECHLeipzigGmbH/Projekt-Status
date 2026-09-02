# Projekte-Statusreport

Statusreport aller laufenden Projekte von INNOTECH Leipzig GmbH (nicht mehr nur Kaufland).

- Ursprüngliche Datenbasis: `Aufstellung Kaufländer.xlsx` (16 Kaufland-Projekte), erweitert um weitere INNOTECH-Projekte (RedBull, AWO, IWB, Mondi u.a.)
- Daten liegen in Supabase (Projekt "Protokoll", Tabelle `kaufland_status` – Name historisch, enthält inzwischen alle Projekte)
- Zusätzlich werden offene Punkte aus der Protokoll-App (Tabellen `protokolle`/`ordner`) je Projekt eingeblendet, sofern der Projektnummer ein Protokoll-Ordner zugeordnet werden kann
- Verknüpfung zur [INNOTECH Protokoll-App](https://innotechleipziggmbh.github.io/innotech-protokoll/) direkt oben im Dashboard (Button „↗ Protokoll-App“)
- „🔒 GF-Anmeldung“-Button oben rechts (kein eigener Tab mehr): nach Login (Supabase-Auth) zeigt das Dashboard direkt in der normalen Projektübersicht zusätzliche, nur für die Geschäftsführung bestimmte Informationen:
  - Je Projekt ein zusätzlicher Block mit Auftragswert, Kosten, Marge und interner Risikobewertung/GF-Notiz (Tabelle `gf_projekt_notizen`, eigene Zugriffsregel nur für angemeldete Nutzer, auch direkt über die Datenbank-API)
  - Ein einklappbarer Themen-Bereich („🔒 Geschäftsführung – Themen“, Titel/Beschreibung/Verantwortlich/Status/Termin) direkt auf der Dashboard-Seite (Tabelle `gf_themen`, gleiche Zugriffsregel)
  - „Nur GF”-Punkte aus der Protokoll-App werden ebenfalls nur bei aktiver Anmeldung in der INNOTECH-ToDo-Übersicht je Projekt gezeigt
- Je Projekt kann ein **Terminplan** hinterlegt werden (Block „📅 Terminplan” in der aufgeklappten Projektzeile, für alle sichtbar): Export aus MS Project als **XML** (Datei → Speichern unter → Dateityp „XML”, NICHT .mpp/PDF/Bild) hochladen – die App zeichnet daraus direkt einen Gantt-Zeitstrahl (Vorgänge, Gliederungsebenen, Meilensteine als Rauten, Fortschrittsbalken). Ein erneuter Upload ersetzt den bisherigen Terminplan vollständig (Tabelle `projekt_terminplan`, gleiche Zugriffsregel wie die übrigen Projektfelder)
- Je Projekt gibt es einen Block „📥 Eingangskontrolle” (aufgeklappte Projektzeile, für alle sichtbar): ein Kanban-Board mit 4 Spalten (Ampel) für alle eingehenden Dateien/Anhänge zu diesem Projekt:
  - **Grau** „Neu / ungeprüft” → **Rot** „Dringend” → **Gelb** „Geprüft – Aufgabe offen” → **Grün** „Geprüft – erledigt”
  - Jede Karte hat einen Betreff, einen Link (Cloud-URL oder Windows-Explorer-Pfad, mit eigenem Chip-Symbol 🔗/📁), wer sie erfasst hat, und eine frei editierbare Notiz
  - Jeder Mitarbeiter kann eine neue Karte anlegen (Button „+ Eingang erfassen”); der Status wird per Drag & Drop zwischen den Spalten gesetzt
  - Karten lassen sich per „✕” wieder entfernen (mit Rückfrage)
  - Daten liegen in der Tabelle `projekt_eingang` (gleiche offene Zugriffsregel wie die übrigen Projektfelder)
- **Ansprechpartner** je Projekt/Gewerk – auch für Kolleg:innen sichtbar, die nicht am Projekt arbeiten, damit sofort klar ist, wer für welches Gewerk zuständig ist:
  - Kompakte Avatar-Vorschau als eigene Spalte „Ansprechpartner” direkt in der Projektübersicht (auch ohne Aufklappen sichtbar), voller Block „🧑‍🤝‍🧑 Ansprechpartner” mit Kontaktkarten in der aufgeklappten Projektzeile
  - Gewerk wird aus einer festen Liste gewählt (PL INNOTECH, PL Kunde, Bauleitung, Architektur, Statik, Elektro, TGA/HLS, Sanitär, Brandschutz, Fassade, Sonstiges) – jeweils farblich codiert; ein Kontakt kann mehrere Gewerke haben (auf einer Karte gebündelt)
  - Zentrale Kontaktliste (Tabelle `kontakte`): derselbe Kontakt kann mehreren Projekten zugeordnet werden, ohne Kontaktdaten mehrfach zu pflegen (Abgleich aktuell über den Namen)
  - Kontakt aus Outlook als **vCard (.vcf) per Drag & Drop** auf das Formular ziehen – Name, Firma, Telefon und Mail werden automatisch übernommen, Gewerk wird danach ausgewählt; alternativ komplett manuelle Eingabe
  - Zuordnungen liegen in der Tabelle `projekt_ansprechpartner` (Projekt × Kontakt × Gewerk, gleiche offene Zugriffsregel wie die übrigen Projektfelder)
- `index.html` ist ein eigenständiges Dashboard (keine Build-Schritte nötig) – kann direkt über GitHub Pages veröffentlicht werden (Settings → Pages → Deploy from branch → main / root)

Hinweis: Repo soll von `Kaufland-Status` auf `Projekt-Status` umbenannt werden (Settings → Repository name) – siehe Hinweise in der Übergabe an Marcus.

Stand: 02.09.2026
