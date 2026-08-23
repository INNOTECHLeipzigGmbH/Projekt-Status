# Projekte-Statusreport

Statusreport aller laufenden Projekte von INNOTECH Leipzig GmbH (nicht mehr nur Kaufland).

- Ursprüngliche Datenbasis: `Aufstellung Kaufländer.xlsx` (16 Kaufland-Projekte), erweitert um weitere INNOTECH-Projekte (RedBull, AWO, IWB, Mondi u.a.)
- Daten liegen in Supabase (Projekt "Protokoll", Tabelle `kaufland_status` – Name historisch, enthält inzwischen alle Projekte)
- Zusätzlich werden offene Punkte aus der Protokoll-App (Tabellen `protokolle`/`ordner`) je Projekt eingeblendet, sofern der Projektnummer ein Protokoll-Ordner zugeordnet werden kann
- Verknüpfung zur [INNOTECH Protokoll-App](https://innotechleipziggmbh.github.io/innotech-protokoll/) direkt oben im Dashboard (Button „↗ Protokoll-App“)
- Eigener Tab „🔒 Geschäftsführung“: Themen mit Titel, Beschreibung, Verantwortlich, Status und Termin – nur nach Anmeldung sichtbar (Supabase-Auth), Daten liegen in einer eigenen Tabelle `gf_themen` mit eigener Zugriffsregel (nur für angemeldete Nutzer, auch direkt über die Datenbank-API)
- `index.html` ist ein eigenständiges Dashboard (keine Build-Schritte nötig) – kann direkt über GitHub Pages veröffentlicht werden (Settings → Pages → Deploy from branch → main / root)

Hinweis: Repo soll von `Kaufland-Status` auf `Projekt-Status` umbenannt werden (Settings → Repository name) – siehe Hinweise in der Übergabe an Marcus.

Stand: 21.08.2026
