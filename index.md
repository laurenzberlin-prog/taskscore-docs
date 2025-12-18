# TaskScore – Documentation Website

Diese Seite dokumentiert den aktuellen Stand der Web-App **TaskScore**
(Work in Progress).

---

## UI Screens

### Startseite
![Startseite](screens/home.png)

Die Startseite gibt einen Überblick über das Konzept von TaskScore und
dient als zentraler Einstiegspunkt zur Anwendung.

---

### Aufgabenverwaltung
![Aufgaben](screens/tasks.png)

In dieser Ansicht können Aufgaben angelegt werden.  
Jede Aufgabe besitzt:
- Titel
- Beschreibung
- Wochentag
- Punktwert (Zeitaufwand / Priorität)

---

### Wochenplan
![Wochenplan](screens/plan.png)

Der Wochenplan visualisiert die Punkteverteilung pro Wochentag
auf Basis eines festen Wochenbudgets (100 Punkte).

---

### Fortschritt
![Fortschritt](screens/progress.png)

Diese Ansicht zeigt den Fortschritt der Woche:
- Gesamtpunkte
- Erledigte Punkte
- Prozentualer Fortschritt (visuelle Anzeige)

---

## Zusammenhang UI & Backend

Die dargestellten Screens werden durch eine Flask-Anwendung realisiert.
Jede UI-Seite entspricht einer eigenen URL-Route:

| UI Screen        | Route       |
|------------------|-------------|
| Startseite       | `/`         |
| Aufgaben         | `/tasks`    |
| Wochenplan       | `/plan`     |
| Fortschritt      | `/progress` |

---

## Datenmodell (aktueller Stand)

Das Datenmodell befindet sich aktuell in einer einfachen, nicht-persistenten
Form (In-Memory-Strukturen).  
Eine spätere Version wird eine Datenbank-Anbindung enthalten.
