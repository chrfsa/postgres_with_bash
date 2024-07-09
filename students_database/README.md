# Gestion de Base de Données avec PostgreSQL et Bash

## Description
Ce projet contient des scripts Bash pour insérer des données à partir de fichiers CSV dans une base de données PostgreSQL et pour récupérer des informations à partir de cette base de données. Il inclut également des instructions pour créer la base de données et les tables nécessaires, ainsi que pour exporter la base de données dans un fichier `.sql`.

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
    ```

2. Créez la base de données et les tables nécessaires :
    ```sql
    -- Connectez-vous à PostgreSQL
    psql -U postgres

    -- Créez la base de données
    CREATE DATABASE students;

    -- Connectez-vous à la base de données
    \c students

    -- Créez les tables
    CREATE TABLE majors (
      major_id SERIAL PRIMARY KEY,
      major VARCHAR(255) UNIQUE NOT NULL
    );

    CREATE TABLE courses (
      course_id SERIAL PRIMARY KEY,
      course VARCHAR(255) UNIQUE NOT NULL
    );

    CREATE TABLE students (
      student_id SERIAL PRIMARY KEY,
      first_name VARCHAR(255) NOT NULL,
      last_name VARCHAR(255) NOT NULL,
      major_id INT REFERENCES majors(major_id),
      gpa NUMERIC(3, 2) NOT NULL
    );

    CREATE TABLE majors_courses (
      major_id INT REFERENCES majors(major_id),
      course_id INT REFERENCES courses(course_id),
      PRIMARY KEY (major_id, course_id)
    );
    ```

3. Assurez-vous que les scripts Bash ont les permissions d'exécution :
    ```bash
    chmod +x insert_data.sh
    chmod +x retrieve_data.sh
    ```

## Utilisation

### Insertion de Données
Pour insérer des données à partir de fichiers CSV (`courses.csv` et `students.csv`) dans la base de données `students`, exécutez le script `insert_data.sh` :
```bash
./insert_data.sh
```
### Récupération de Données
Pour récupérer des informations de la base de données students, exécutez le script retrieve_data.sh :
```bash
./retrieve_data.sh
```
4. Exporter la Base de Données

Pour exporter la base de données dans un `fichier .sql`, utilisez la commande suivante :
```bash
pg_dump --clean --create --inserts --username=<username> students > students.sql
```

