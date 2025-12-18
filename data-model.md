# Datenmodell (Current Version)

Hier ist geplante Datenmodell der Web-App TaskScore aufgezeigt.
Es zeigt die UI-Screens und Flask-Routes. Eine Datenbank ist aktuell nicht implementiert

---

## Überblick

- Pro Woche steht ein festes Punktekonto (z. B. 100 Punkte) zur Verfügung
- Aufgaben werden einem Wochentag zugeordnet
- Punkte repräsentieren Zeitaufwand und Priorität
- Fortschritt ergibt sich aus erledigten Punkten

---

## Entitäten

### USER
| Feld | Typ | Beschreibung |
|-----|-----|-------------|
| id | integer (PK) | eindeutige Nutzer-ID |
| name | string | Anzeigename |
| email | string | optional |

---

### WEEK_PLAN
| Feld | Typ | Beschreibung |
|-----|-----|-------------|
| id | integer (PK) | eindeutige Wochen-ID |
| user_id | integer (FK) | Referenz auf USER |
| week_start | date | Startdatum der Woche (Montag) |
| total_points | integer | Wochenbudget (z. B. 100) |

---

### DAY_PLAN
| Feld | Typ | Beschreibung |
|-----|-----|-------------|
| id | integer (PK) | eindeutige Tages-ID |
| week_plan_id | integer (FK) | Referenz auf WEEK_PLAN |
| weekday | string | Montag – Sonntag |
| planned_points | integer | geplante Punkte pro Tag |

---

### TASK
| Feld | Typ | Beschreibung |
|-----|-----|-------------|
| id | integer (PK) | eindeutige Aufgaben-ID |
| week_plan_id | integer (FK) | Referenz auf WEEK_PLAN |
| title | string | Titel der Aufgabe |
| description | string | optionale Beschreibung |
| weekday | string | zugeordneter Wochentag |
| points_total | integer | geplante Punkte |
| points_done | integer | erledigte Punkte |
| status | string | OPEN / IN_PROGRESS / DONE |

---

## Entity-Relationship-Diagramm (ER)

```mermaid
erDiagram
    USER ||--o{ WEEK_PLAN : has
    WEEK_PLAN ||--o{ DAY_PLAN : contains
    WEEK_PLAN ||--o{ TASK : includes

    USER {
        int id PK
        string name
        string email
    }

    WEEK_PLAN {
        int id PK
        int user_id FK
        date week_start
        int total_points
    }

    DAY_PLAN {
        int id PK
        int week_plan_id FK
        string weekday
        int planned_points
    }

    TASK {
        int id PK
        int week_plan_id FK
        string title
        string description
        string weekday
        int points_total
        int points_done
        string status
    }
