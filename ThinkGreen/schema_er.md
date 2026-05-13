# Schéma Entité-Relation (ER) - ThinkGreen

Ce document présente le schéma conceptuel de la base de données pour l'application **ThinkGreen**.

## Diagramme ER

```mermaid
erDiagram
    USERS ||--o{ PLANTS : "gère"
    PLANTS ||--o{ WATERING_SCHEDULE : "planifie"
    
    USERS {
        int id PK
        string username "Unique"
        string email "Unique"
        string password
        enum role "admin, user"
        timestamp created_at
    }

    PLANTS {
        int id PK
        string name
        string species
        string location
        date planted_date
        enum status "healthy, needs_water, sick, harvested"
        int user_id FK
        timestamp created_at
    }

    WATERING_SCHEDULE {
        int id PK
        int plant_id FK
        enum action "water, fertilize, prune"
        date scheduled_date
        boolean completed
        text notes
        timestamp created_at
    }

    WEATHER_ALERTS {
        int id PK
        enum alert_type "frost, heatwave, storm, drought"
        enum severity "low, medium, high, critical"
        text message
        date alert_date
        string region
        timestamp created_at
    }
```

## Description des Tables

### 1. USERS
Stocke les informations sur les utilisateurs de l'application.
- **id**: Identifiant unique.
- **username/email**: Informations de connexion uniques.
- **role**: Définit les permissions (Administrateur ou Utilisateur standard).

### 2. PLANTS
Contient les données relatives aux plantes ajoutées par les utilisateurs.
- **user_id**: Clé étrangère reliant la plante à son propriétaire.
- **status**: État actuel de la plante pour le suivi visuel.

### 3. WATERING_SCHEDULE
Gère les tâches d'entretien (arrosage, fertilisation, taille).
- **plant_id**: Clé étrangère reliant l'action à une plante spécifique.
- **completed**: État de réalisation de la tâche.

### 4. WEATHER_ALERTS
Table indépendante stockant les alertes météorologiques régionales pour informer les utilisateurs des risques potentiels.
