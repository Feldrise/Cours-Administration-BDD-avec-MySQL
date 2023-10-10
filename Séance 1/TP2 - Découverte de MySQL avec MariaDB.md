# Travaux Pratiques : Découverte de MySQL avec MariaDB

---

## Partie 1 : Configuration initiale, création et exploration de la base de données
**Durée estimée : 20 minutes**

### Objectifs
- Vérifier et comprendre la bonne installation de MariaDB.
- Explorer l'interface en ligne de commande de MySQL.
- Créer une première base de données et explorer ses propriétés.
- Apprendre à lister les bases de données existantes.

### Étapes
1. **Vérification de l'installation**
    - Ouvrez le terminal ou l'invite de commandes.
    - Connectez-vous à MariaDB avec l'utilisateur `root` :
      ```bash
      mysql -u root -p
      ```
      Entrez le mot de passe défini lors de l'installation de MariaDB. Si vous vous connectez avec succès, vous êtes prêt à continuer! 🎉
      
2. **Exploration de l'interface CLI**
    - Pour obtenir une liste des commandes disponibles, tapez :
      ```sql
      HELP;
      ```
      Prenez un moment pour explorer quelques commandes. Ne vous inquiétez pas, vous n'avez pas besoin de tout mémoriser maintenant. C'est juste pour vous donner une idée de ce qui est possible! 🧐
      
3. **Création et exploration de la base de données**
    - Créez une nouvelle base de données appelée `maPremiereBDD` :
      ```sql
      CREATE DATABASE maPremiereBDD;
      ```
    - Vérifiez que votre base de données a été créée en listant toutes les bases de données :
      ```sql
      SHOW DATABASES;
      ```
      Vous devriez voir `maPremiereBDD` dans la liste! 📘
      
    - Sélectionnez et explorez la base de données `maPremiereBDD` :
      ```sql
      USE maPremiereBDD;
      ```
    - Vérifiez les tables existantes (il ne devrait y en avoir aucune pour le moment) :
      ```sql
      SHOW TABLES;
      ```
      C'est normal que rien ne s'affiche, nous n'avons pas encore créé de table! 🚧

---

# Travaux Pratiques : Découverte de MySQL avec MariaDB

---

## Partie 2 : Création de tables et modélisation basique
**Durée estimée : 20 minutes**

### Objectifs
- Maîtriser la création de tables.
- Comprendre la définition des types de données dans MySQL.
- Explorer la mise en place de relations entre les tables.

### Étapes

1. **Table `etudiants`**
   
    Créez une table `etudiants` avec les champs suivants :
    - `id` (numéro d'identification unique, auto-incrémenté)
    - `nom` (chaîne de caractères de 50 caractères maximum)
    - `prenom` (chaîne de caractères de 50 caractères maximum)
    - `email` (chaîne de caractères de 100 caractères maximum)
    - `date_naissance` (date)

    Exemple de code:
    ```sql
    CREATE TABLE etudiants (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nom VARCHAR(50),
        prenom VARCHAR(50),
        email VARCHAR(100) UNIQUE,
        date_naissance DATE
    );
    ```
    Vous avez maintenant une table pour stocker les informations des étudiants. 🎉

2. **Table `cours`**

    Créez une autre table `cours` pour stocker les informations sur différents cours offerts :
    - `id` (identifiant unique, auto-incrémenté)
    - `nom` (chaîne de caractères de 100 caractères maximum)
    - `description` (texte)

    ```sql
    CREATE TABLE cours (
        id INT AUTO_INCREMENT PRIMARY KEY,
        nom VARCHAR(100),
        description TEXT
    );
    ```

    Bravo ! Vous venez d'ajouter une autre table. 📚

3. **Table `inscription`**

    Cette table servira à relier les étudiants aux cours auxquels ils sont inscrits :
    - `id` (identifiant unique, auto-incrémenté)
    - `id_etudiant` (référence à la table `etudiants`)
    - `id_cours` (référence à la table `cours`)
    - `date_inscription` (date et heure)

    ```sql
    CREATE TABLE inscription (
        id INT AUTO_INCREMENT PRIMARY KEY,
        id_etudiant INT,
        id_cours INT,
        date_inscription DATETIME DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (id_etudiant) REFERENCES etudiants(id),
        FOREIGN KEY (id_cours) REFERENCES cours(id)
    );
    ```

    Avec cette table, vous avez mis en place des relations entre les tables ! 🌐

4. **Exercice pratique**

    Essayez de créer une nouvelle table `professeurs` avec des champs que vous jugez pertinents (comme `id`, `nom`, `prenom`, `email`, `matiere`, etc.). C'est l'occasion d'appliquer ce que vous avez appris. 😊

**Temps d'échange**

Discutez avec vos camarades des choix que vous avez faits pour la table `professeurs`. Quels champs avez-vous ajoutés? Pourquoi? Partagez vos raisons et comparez avec les choix des autres.

J'espère que cette partie a éclairci le processus de création de tables et la mise en place de relations entre elles dans MySQL. À la prochaine étape ! 🚀👩‍💻👨‍💻

---

# Partie 3 : Insertion et manipulation de données
**Durée estimée : 20 minutes**

### Objectifs
- Insérer des données dans différentes tables.
- Comprendre les relations entre différentes tables.
- Apprendre à mettre à jour et supprimer des enregistrements.

### Étapes

1. **Insertion d'étudiants**

    Vous allez d'abord ajouter plus d'étudiants dans la table `etudiants`. Utilisez la commande `INSERT`.

    Exemple :
    ```sql
    INSERT INTO etudiants (nom, prenom, email)
    VALUES ('Lefevre', 'Emilie', 'emilie.lefevre@email.com'),
           ('Bernard', 'Nicolas', 'nicolas.bernard@email.com'),
           ('Leroy', 'Alice', 'alice.leroy@email.com');
    ```

    👩‍💻 Votre exercice : Ajoutez encore 5 étudiants de votre choix.

2. **Insertion de professeurs**

    Maintenant, ajoutons des professeurs à la table `professeurs`. Supposons que cette table ait des champs tels que `id`, `nom`, `prenom`, `annees_experience` et `matiere`.

    Exemple :
    ```sql
    INSERT INTO professeurs (nom, prenom, matiere)
    VALUES ('Blanchard', 'Christophe', 'Informatique'),
           ('Morel', 'Sophie', 'Mathématiques');
    ```

    👨‍🏫 Votre exercice : Ajoutez encore 3 professeurs avec leurs spécialités respectives.

3. **Insertion de cours**
    Exemple :
    ```sql
    INSERT INTO cours (nom_cours, id_professeur)
    VALUES ('Programmation en C', 'Un super cours sur un des plus ancien langage encore actif'),
           ('Analyse mathématique', 'Des maths, on vous vois les dev qui veulent juste fuires 😉');
    ```

    📚 Votre exercice : Ajoutez 2 cours supplémentaires.

4. **Insertion d'inscriptions**

    On sait que la table `inscription` a les champs `id_etudiant`, `id_cours`, et `date_inscription`.

    Exemple :
    ```sql
    INSERT INTO inscription (id_etudiant, id_cours, date_inscription)
    VALUES (1, 1, '2023-10-09'),   -- Supposons que l'étudiant 1 s'inscrive au cours 1 aujourd'hui
           (2, 2, '2023-10-09');   -- Et que l'étudiant 2 s'inscrive au cours 2 aujourd'hui
    ```

    📅 Votre exercice : Inscrivez 3 autres étudiants à des cours variés. Vous pouvez même inscrire un étudiant à plusieurs cours!

5. **Mise à jour d'enregistrements**

    Parfois, nous devons corriger ou mettre à jour des informations. Utilisez la commande `UPDATE`.

    Exemple : Mettons à jour l'email d'Emilie Lefevre :
    ```sql
    UPDATE etudiants
    SET email = 'emilie.updated@email.com'
    WHERE nom = 'Lefevre' AND prenom = 'Emilie';
    ```

    🔄 Votre exercice : Changez la matière choisi par un des étudiants que vous avez ajoutés.

6. **Suppression d'enregistrements**

    Si vous souhaitez supprimer un enregistrement, utilisez la commande `DELETE`. Attention, faites cela avec prudence !

    Exemple : Supprimer un étudiant par son email :
    ```sql
    DELETE FROM etudiants WHERE email = 'emilie.updated@email.com';
    ```

    ❌ Votre exercice : Supprimez l'un des cours que vous avez ajoutés (et assurez-vous de bien supprimer les inscriptions associées).


---

# Partie 4 : Consultation et Manipulation des Enregistrements

**Durée estimée : 30 minutes**

### Objectifs

- Maîtriser les requêtes SQL basiques pour la consultation des données.
- Explorer les méthodes pour filtrer, trier et joindre les tables.
- Utiliser des fonctions d'agrégation pour résumer des données.

### Étapes

1. **Affichage Basique**
   
   Commencez par afficher tous les étudiants de la table `etudiants` :
    ```sql
    SELECT * FROM etudiants;
    ```

2. **Filtrage des Résultats**

   Utilisez la clause `WHERE` pour filtrer les étudiants ayant le nom 'Doe' :
    <!-- ```sql
    SELECT * FROM etudiants WHERE nom = 'Doe';
    ``` -->
   
   Essayez de filtrer les professeurs ayant plus de 10 ans d'expérience :
   <!-- ```sql
   SELECT * FROM professeurs WHERE annees_experience > 10;
   ``` -->

3. **Trier les Résultats**

   Triez tous les cours par leur nom de manière ascendante :
   <!-- ```sql
   SELECT * FROM cours ORDER BY nom ASC;
   ``` -->

4. **Jointures entre les Tables**

   Utilisez une jointure `INNER JOIN` pour récupérer la liste des étudiants inscrits à un cours
    <!-- ```sql
    SELECT etudiants.nom, etudiants.prenom, cours.nom
    FROM inscription
    INNER JOIN etudiants ON inscription.etudiant_id = etudiants.id
    INNER JOIN cours ON inscription.cours_id = cours.id;
    ``` -->

5. **Fonctions d'Agrégation**

   Comptez le nombre total d'étudiants inscrits à chaque cours
    <!-- ```sql
    SELECT cours.nom_cours, COUNT(etudiants.id) AS nombre_etudiants
    FROM inscription
    INNER JOIN cours ON inscription.cours_id = cours.id
    INNER JOIN etudiants ON inscription.etudiant_id = etudiants.id
    GROUP BY cours.nom_cours;
    ``` -->

<!-- 6. **Requêtes Combinées**

   Essayez d'obtenir la liste des professeurs qui n'ont pas de cours assignés. Pour cela, utilisez une combinaison de `LEFT JOIN` et `WHERE` :
   ```sql
   SELECT professeurs.nom, professeurs.prenom
   FROM professeurs
   LEFT JOIN cours ON professeurs.id = cours.professeur_id
   WHERE cours.id IS NULL;
   ``` -->

6. **Bonus: Sous-requêtes**

   Trouvez le nom du cours ayant le plus d'étudiants inscrits. Pour cela, utilisez une sous-requête
    <!-- ```sql
    SELECT nom_cours, COUNT(etudiant_id) AS nombre_etudiants
    FROM inscription
    INNER JOIN cours ON inscription.cours_id = cours.id
    GROUP BY nom_cours
    HAVING nombre_etudiants = (SELECT MAX(count_etudiant) FROM (SELECT COUNT(etudiant_id) AS count_etudiant FROM inscription GROUP BY cours_id) AS sub);
    ``` -->

---

**Temps d'échange tout au long du TP**

Prenez un moment pour discuter avec vos camarades des différentes méthodes que vous avez utilisées et de leurs avantages. Posez des questions à votre professeur si vous avez des doutes ou si vous souhaitez des clarifications. 

Continuez à explorer et à poser des questions ! 🧠🚀