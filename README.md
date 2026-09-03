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
  - Jede Karte hat einen Betreff, einen Link (Cloud-URL oder Windows-Explorer-Pfad, mit eigenem Chip-Symbol 🔗/📁), wer sie erfasst hat („Ihr Name/Kürzel” – feste Mehrfachauswahl aus allen INNOTECH-Mitarbeitern außer Britta Riedel, alphabetisch sortiert, kein Freitext), und eine frei editierbare Notiz
  - Jeder Mitarbeiter kann eine neue Karte anlegen (Button „+ Eingang erfassen”); der Status wird per Drag & Drop zwischen den Spalten gesetzt
  - Karten lassen sich jederzeit über „✎ Bearbeiten” nachträglich anpassen (Betreff, Link, Name/Kürzel) – die Änderungen werden direkt in der Karte gespeichert, ohne den Status/die Spalte zu verändern
  - Karten lassen sich per „✕” wieder entfernen (mit Rückfrage)
  - Daten liegen in der Tabelle `projekt_eingang` (gleiche offene Zugriffsregel wie die übrigen Projektfelder)
- **Ansprechpartner** je Projekt/Gewerk – auch für Kolleg:innen sichtbar, die nicht am Projekt arbeiten, damit sofort klar ist, wer für welches Gewerk zuständig ist:
  - Kompakte Avatar-Vorschau als eigene Spalte „Ansprechpartner” direkt in der Projektübersicht (auch ohne Aufklappen sichtbar), voller Block „🧑‍🤝‍🧑 Ansprechpartner” mit Kontaktkarten in der aufgeklappten Projektzeile
  - Gewerk wird aus einer festen Liste gewählt (PL INNOTECH, PL Kunde, Bauleitung, Architektur, Statik, Elektro, TGA/HLS, Sanitär, Brandschutz, Fassade, Sonstiges) – jeweils farblich codiert; ein Kontakt kann mehrere Gewerke haben (auf einer Karte gebündelt)
  - Zentrale Kontaktliste (Tabelle `kontakte`): derselbe Kontakt kann mehreren Projekten zugeordnet werden, ohne Kontaktdaten mehrfach zu pflegen (Abgleich aktuell über den Namen)
  - Kontakt aus Outlook per Drag & Drop auf das Formular ziehen – sowohl als **vCard (.vcf)** als auch direkt als **Outlook-Kontaktelement (.msg)** (je nach Outlook-/Browser-Version zieht Outlook manchmal eine .msg- statt eine .vcf-Datei): Name, Firma, Telefon und Mail werden automatisch übernommen, Gewerk wird danach ausgewählt; alternativ komplett manuelle Eingabe. Falls Outlook beim Ziehen gar keine lesbare Datei mitgibt, erscheint eine klare Meldung mit Anleitung statt stiller Untätigkeit; die Ablagefläche lässt sich außerdem anklicken, um eine Datei ganz normal per Dateiauswahl zu laden. *Hinweis zur .msg-Unterstützung:* der .msg-Parser ist direkt in `index.html` eingebettet (keine externe Bibliothek/CDN mehr, kein Internetzugriff im Browser nötig) und wird nur bei Bedarf (erster .msg-Drop) einmalig aktiviert; dadurch ist `index.html` als Datei spürbar größer geworden (ca. 730 KB statt vorher ca. 115 KB)
  - Zuordnungen liegen in der Tabelle `projekt_ansprechpartner` (Projekt × Kontakt × Gewerk, gleiche offene Zugriffsregel wie die übrigen Projektfelder)
- Bei den folgenden Feldern ist die Auswahl bewusst auf eine **feste, alphabetisch sortierte Personenliste mit Mehrfachauswahl** eingeschränkt (kein Freitext mehr, um Tippfehler/Varianten zu vermeiden):
  - „PL Innotech” im Bearbeiten-Formular: Marcus Riedel, Stefan Riedel, Maximilian Fehst, Henryk Fehst
  - „Ihr Name/Kürzel” bei der Eingangskontrolle und „Verantwortlich” bei eigenen ToDos: alle INNOTECH-Mitarbeiter außer Britta Riedel (Marcus Riedel, Stefan Riedel, Maximilian Fehst, Henryk Fehst, Julia Albert, Maximilian Roth, Anh Nguyen, Daniel Hentschel, Michael Bonitz)
  - Bei eigenen ToDos gibt es zusätzlich ein **Termin-Feld** (Datum), das zusammen mit dem Verantwortlichen in der ToDo-Übersicht angezeigt wird
- Feste **INNOTECH-Mitarbeiterliste** (Britta Riedel, Marcus Riedel, Stefan Riedel, Maximilian Fehst, Henryk Fehst, Daniel Hentschel, Michael Bonitz, Julia Albert, Maximilian Roth, Anh Nguyen) erscheint weiterhin als Auswahlvorschlag (Autovervollständigung, mit weiterhin möglicher freier Eingabe z.B. für externe Personen) im Namensfeld bei Ansprechpartnern und bei „Verantwortlich” bei GF-Themen; die Liste ist im Code als `INNOTECH_MITARBEITER`-Konstante gepflegt
- **„🔒 Angebote”-Tab** (neu, oben in den Reitern neben „Dashboard”/„Tabellenansicht”): eine eigenständige, zweite Liste – **nicht** nur eine gefilterte Ansicht der Projekte – für die Angebotsphase, ausschließlich für die Geschäftsführung sichtbar (derselbe Login wie bei „🔒 GF-Anmeldung” oben rechts; ohne Anmeldung erscheint dort nur eine Anmelde-Aufforderung, auch über die Datenbank-API nicht einsehbar):
  - Eigene Tabelle `angebote_status` (gleicher Aufbau wie `kaufland_status`, aber eigene Datensätze) mit den Spalten Angebot, Auftraggeber, PL Innotech, PL Kunde, Status, Angebotsdatum, Frist, Angebotswert, Ansprechpartner
  - Statt der Projekt-Leistungsphasen-Checkliste gibt es einen einfachen **Angebotsstatus**: In Arbeit → Versendet → Rückmeldung ausstehend → Gewonnen/Verloren
  - „+ Angebot anlegen” öffnet direkt das Bearbeiten-Formular für ein neues Angebot; „✎ Bearbeiten” passt ein bestehendes Angebot jederzeit an (Name, Auftraggeber, PL Innotech, PL Kunde, Partner, Status, Angebotsdatum, Frist, Angebotswert, eigene ToDos)
  - In der aufgeklappten Zeile stehen dieselben vier Bausteine wie bei Projekten zur Verfügung, mit eigenen Datentabellen (`angebot_terminplan`, `angebot_eingang`, `angebot_ansprechpartner`) statt der Projekt-Tabellen, aber identischer Bedienung:
    - 📅 **Terminplan** (Gantt aus MS-Project-XML-Export, wie bei Projekten)
    - 📥 **Eingangskontrolle** (Kanban mit denselben 4 Ampel-Spalten, inkl. nachträglichem Bearbeiten)
    - 🧑‍🤝‍🧑 **Ansprechpartner** (inkl. Drag&Drop aus Outlook, zentrale Kontaktliste `kontakte` wird mit den Projekten geteilt)
    - **Eigene ToDos** (inkl. Verantwortlich-Mehrfachauswahl und Termin-Feld)
  - Alle vier Angebote-Tabellen sind wie `gf_themen`/`gf_projekt_notizen` per Datenbankregel (RLS) ausschließlich für angemeldete Nutzer zugänglich – auch direkt über die Datenbank-API
- `index.html` ist ein eigenständiges Dashboard (keine Build-Schritte nötig) – kann direkt über GitHub Pages veröffentlicht werden (Settings → Pages → Deploy from branch → main / root)

Hinweis: Repo soll von `Kaufland-Status` auf `Projekt-Status` umbenannt werden (Settings → Repository name) – siehe Hinweise in der Übergabe an Marcus.

Stand: 03.09.2026 (neuer „🔒 Angebote”-Tab für die Geschäftsführung mit eigener Angebotsliste, Angebotsstatus und denselben Bausteinen wie bei Projekten – Terminplan, Eingangskontrolle, Ansprechpartner, eigene ToDos; feste Personenauswahl bei PL Innotech/Eingangskontrolle/eigenen ToDos, Eingangskontrolle nachträglich bearbeitbar, Outlook-.msg-Unterstützung bei Ansprechpartnern)
