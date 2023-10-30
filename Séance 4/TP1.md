# TP : Exploration des types de données MySQL 🚀

Lors de ce TP, nous allons explorer en profondeur les différents types de données disponibles dans MySQL. Vous aurez l'occasion de mettre en pratique vos connaissances et de renforcer votre compréhension des types de données. Préparez-vous à plonger dans le monde fascinant des bases de données! 😃

## Objectifs 🎯
- Comprendre et différencier les types de données MySQL.
- Savoir quand et comment utiliser chaque type de données.
- Mettre en pratique la création de tables et l'insertion de données.

## Prérequis 📚
- Avoir MySQL installé sur votre machine.
- Être familiarisé avec les commandes de base de MySQL.

## Étapes 🛠️

1. **Démarrage de MySQL** 🚀
   - Ouvrez votre terminal ou votre interface MySQL.
   - Connectez-vous à votre serveur MySQL en utilisant la commande suivante :
     ```sql
     mysql -u votre_nom_utilisateur -p
     ```

2. **Création d'une nouvelle base de données** 📦
   - Pour commencer, créez une nouvelle base de données appelée `exploration_types` :
     ```sql
     CREATE DATABASE exploration_types;
     ```
   - Sélectionnez cette base de données pour la suite du TP :
     ```sql
     USE exploration_types;
     ```

3. **Création de la table `informations`** 🛠️
   - Nous allons créer une table `informations` avec divers types de données. Voici la structure de la table :
     - `id` : Identifiant unique de type `INT` avec auto-increment.
     - `nom` : Nom de la personne de type `VARCHAR(100)`.
     - `age` : Âge de la personne de type `TINYINT`.
     - `email` : Adresse e-mail de type `VARCHAR(255)`.
     - `date_naissance` : Date de naissance de type `DATE`.
     - `salaire` : Salaire mensuel de type `DECIMAL(10,2)`.
   - Exécutez la commande suivante pour créer la table :
     ```sql
     CREATE TABLE informations (
       id INT AUTO_INCREMENT PRIMARY KEY,
       nom VARCHAR(100),
       age TINYINT,
       email VARCHAR(255),
       date_naissance DATE,
       salaire DECIMAL(10,2)
     );
     ```

4. **Insertion de données** 📝
   - Maintenant, insérez quelques données dans la table `informations` pour vous familiariser avec les différents types de données.
     ```sql
     INSERT INTO informations (nom, age, email, date_naissance, salaire)
     VALUES ('Alice', 25, 'alice@email.com', '1998-05-10', 2500.50),
            ('Bob', 30, 'bob@email.com', '1993-03-15', 3200.75),
            ('Charlie', 28, 'charlie@email.com', '1995-07-20', 2900.00);
     ```

5. **Consultation des données** 🧐
   - Utilisez la commande `SELECT` pour afficher les données que vous venez d'insérer :
     ```sql
     SELECT * FROM informations;
     ```

6. **Exercices pratiques** 🏋️‍♂️
   - **Exercice 1** : Créez une nouvelle table `produits` avec les colonnes suivantes :
     - `id` : Identifiant unique de type `INT` avec auto-increment.
     - `nom` : Nom du produit de type `VARCHAR(150)`.
     - `description` : Description du produit de type `TEXT`.
     - `prix` : Prix du produit de type `FLOAT`.
     - `date_ajout` : Date d'ajout du produit de type `DATETIME`.
   - **Exercice 2** : Insérez au moins trois produits dans la table `produits`.
   - **Exercice 3** : Affichez tous les produits dont le prix est supérieur à 50.

---

## Partie 2: Comprendre les types de données MySQL 🧠

Dans cette section, nous allons explorer en détail les différents types de données disponibles dans MySQL. Chaque type de données a ses propres caractéristiques et utilisations. Comprendre ces types est essentiel pour concevoir des bases de données efficaces et précises.

### Types de données numériques 🔢
- **INT**: Pour les entiers. Exemple: 1, 100, -30.
- **FLOAT**: Pour les nombres à virgule flottante. Exemple: 10.5, -3.14.
- **DECIMAL**: Pour les nombres exacts, souvent utilisés pour représenter de l'argent. Exemple: 10.75.
- **TINYINT**: Pour les petits entiers. Exemple: 5, -3.

### Types de données de chaîne de caractères 📜
- **VARCHAR**: Pour les chaînes de caractères de longueur variable. Exemple: "Alice", "Bonjour".
- **TEXT**: Pour les longs textes.
- **CHAR**: Pour les chaînes de caractères de longueur fixe.

### Types de données de date et d'heure 📅
- **DATE**: Pour la date. Exemple: '2023-10-30'.
- **DATETIME**: Pour la date et l'heure. Exemple: '2023-10-30 10:30:00'.
- **TIME**: Pour l'heure. Exemple: '10:30:00'.

### Types de données divers 🎭
- **ENUM**: Pour une liste de valeurs possibles. Exemple: `ENUM('petit', 'moyen', 'grand')`.
- **SET**: Pour une collection de valeurs possibles. Exemple: `SET('rouge', 'bleu', 'vert')`.

### Exercices pratiques 🏋️‍♂️

**Exercice 1**: Création d'une table créative 🎨
- Votre mission est de créer une table `bibliotheque` pour représenter des livres. Soyez créatif et utilisez un maximum de types de données différents pour définir les attributs des livres. Voici quelques idées d'attributs :
  - Titre du livre
  - Auteur
  - Date de publication
  - Genre (utilisez ENUM ou SET)
  - Prix
  - Nombre de pages
  - Évaluation (par exemple, une note sur 5 ou 10)
  - Synopsis (un bref résumé du livre)
  - ... et tout autre attribut que vous jugez pertinent!

**Exercice 2**: Insertion de données 📝
- Une fois votre table créée, insérez au moins trois livres avec des données variées.

**Exercice 3**: Consultation 🕵️‍♂️
- Écrivez des requêtes pour :
  - Trouver tous les livres d'un genre spécifique.
  - Trouver tous les livres publiés après une certaine date.
  - Trouver tous les livres ayant une évaluation supérieure à 4.

---

🌟 **Astuce**: N'hésitez pas à consulter la documentation officielle de MySQL si vous avez des doutes sur un type de données ou si vous souhaitez en savoir plus sur ses caractéristiques.