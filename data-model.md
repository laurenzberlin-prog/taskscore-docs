# Datenmodell (Current Version)

Dieses Datenmodell bildet das Konzept von **TaskScore** ab:
- pro Woche steht ein Punktekonto (z. B. 100 Punkte) zur Verfügung
- Aufgaben werden einem Wochentag zugeordnet und mit Punkten bewertet
- Fortschritt ergibt sich aus erledigten Punkten

> Hinweis: Aktueller Stand ist ein UI-/Routing-Prototyp ohne Datenbank.
> Das Modell beschreibt die geplante persistente Struktur (z. B. SQLite).

---

## Entitäten

### USER
| Feld | Typ | Beschreibung |
|------|-----|--------------|
| id | integer (PK) | eindeutige Nutzer-ID |
| name | string | Anzeigename |
| email | string | optional |

---

### WEEK_PLAN
| Feld | Typ | Beschreibung |
|------|-----|--------------|
| id | integer (PK) | eindeutige Wochenplan-ID |
| user_id | integer (FK) | gehört zu USER |
| week_start | date | Startdatum der Woche (Montag) |
| total_points | integer | Wochenbudget (z. B. 100) |

---

### DAY_PLAN
| Feld | Typ | Beschreibung |
|------|-----|--------------|
| id | integer (PK) | eindeutige Tagesplan-ID |
| week_plan_id | integer (FK) | gehört zu WEEK_PLAN |
| weekday | string | Montag … Sonntag |
| planned_points | integer | geplante Punkte für den Tag |

---

### TASK
| Feld | Typ | Beschreibung |
|------|-----|--------------|
| id | integer (PK) | eindeutige Aufgaben-ID |
| week_plan_id | integer (FK) | gehört zu WEEK_PLAN |
| title | string | Titel der Aufgabe |
| description | string | Beschreibung |
| weekday | string | zugeordneter Wochentag |
| points_total | integer | Punktwert der Aufgabe (Aufwand/Priorität) |
| points_done | integer | bereits erledigte Punkte |
| status | string | z. B. OPEN / IN_PROGRESS / DONE |

---

## Beziehungen (ER)

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
