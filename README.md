# Projekte-Statusreport

Statusreport aller laufenden Projekte von INNOTECH Leipzig GmbH (nicht mehr nur Kaufland).

- Ursprüngliche Datenbasis: `Aufstellung Kaufländer.xlsx` (16 Kaufland-Projekte), erweitert um weitere INNOTECH-Projekte (RedBull, AWO, IWB, Mondi u.a.)
- Daten liegen in Supabase (Projekt "Protokoll", Tabelle `kaufland_status` – Name historisch, enthält inzwischen alle Projekte)
- Zusätzlich werden offene Punkte aus der Protokoll-App (Tabellen `protokolle`/`ordner`) je Projekt eingeblendet, sofern der Projektnummer ein Protokoll-Ordner zugeordnet werden kann
- Verknüpfung zur [INNOTECH Protokoll-App](https://innotechleipziggmbh.github.io/innotech-protokoll/) direkt oben im Dashboard (Button „↗ Protokoll-App“)
- „🔒 GF-Anmeldung“-Button oben rechts (kein eigener Tab mehr): nach Login (Supabase-Auth) zeigt das Dashboard direkt in der normalen Projektübersicht zusätzliche, nur für die Geschäftsführung bestimmte Informationen:
  - Je Projekt ein zusätzlicher Block mit Auftragswert, Kosten, Marge und interner Risikobewertung/GF-Notiz (Tabelle `gf_projekt_notizen`, eigene Zugriffsregel nur für angemeldete Nutzer, auch direkt über die Datenbank-API)
  - Ein einklappbarer Themen-Bereich („🔒 Geschäftsführung – Themen“, Titel/Beschreibung/Verantwortlich/Status/Termin) direkt auf der Dashboard-Seite (Tabelle `gf_themen`, gleiche Zugriffsregel)
  - „Nur GF“-Punkte aus der Protokoll-App werden ebenfalls nur bei aktiver Anmeldung in der INNOTECH-ToDo-Übersicht je Projekt gezeigt
- `index.html` ist ein eigenständiges Dashboard (keine Build-Schritte nötig) – kann direkt über GitHub Pages veröffentlicht werden (Settings → Pages → Deploy from branch → main / root)

Hinweis: Repo soll von `Kaufland-Status` auf `Projekt-Status` umbenannt werden (Settings → Repository name) – siehe Hinweise in der Übergabe an Marcus.

Stand: 26.08.2026
