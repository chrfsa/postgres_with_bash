# Gestion de la Base de Données de la Coupe du Monde avec PostgreSQL et Bash

## Description
Ce projet contient des scripts Bash pour insérer des données à partir d'un fichier CSV dans une base de données PostgreSQL, ainsi que pour récupérer des informations à partir de cette base de données. Il inclut également des instructions pour créer la base de données et les tables nécessaires, ainsi que pour exporter la base de données dans un fichier `.sql`.

## Table des Matières
1. [Prérequis](#prérequis)
2. [Installation](#installation)
3. [Utilisation](#utilisation)
   - [Insertion de Données](#insertion-de-données)
   - [Récupération de Données](#récupération-de-données)
4. [Exporter la Base de Données](#exporter-la-base-de-données)

## Prérequis
- PostgreSQL installé et configuré
- Accès à un utilisateur PostgreSQL avec les permissions nécessaires
- Bash shell

## Installation
1. Clonez le dépôt :
    ```bash
    git clone https://github.com/chrfsa/postgres_with_bash.git
    cd postgres_with_bash
    cd game_database
    ```

2. Créez la base de données et les tables nécessaires :
    ```sql
    -- Connectez-vous à PostgreSQL
    psql -U postgres

    -- Créez la base de données
    CREATE DATABASE worldcup;

    -- Connectez-vous à la base de données
    \c worldcup

    -- Créez les tables
    CREATE TABLE teams (
      team_id SERIAL PRIMARY KEY,
      name VARCHAR(255) UNIQUE NOT NULL
    );

    CREATE TABLE games (
      game_id SERIAL PRIMARY KEY,
      year INT NOT NULL,
      round VARCHAR(255) NOT NULL,
      winner_id INT REFERENCES teams(team_id),
      opponent_id INT REFERENCES teams(team_id),
      winner_goals INT NOT NULL,
      opponent_goals INT NOT NULL
    );
    ```

3. Assurez-vous que les scripts Bash ont les permissions d'exécution :
    ```bash
    chmod +x insert_data.sh
    chmod +x retrieve_data.sh
    ```

## Utilisation

### Insertion de Données
Pour insérer des données à partir du fichier CSV (`games.csv`) dans la base de données `worldcup`, exécutez le script `insert_data.sh` :
```bash
./insert_data.sh
```
### Récupération de Données
Pour récupérer des informations de la base de données students, exécutez le script quereis.sh :
```bash
./queries.sh
```
## Exporter la Base de Données
Pour exporter la base de données dans un `fichier .sql`, utilisez la commande suivante :
```bash
pg_dump --clean --create --inserts --username=<username> worldcup > worldcup.sql
```