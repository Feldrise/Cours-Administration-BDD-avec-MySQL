# TP : Jeux de caractères et collations dans MySQL 🌐

Lorsque nous travaillons avec des bases de données, il est crucial de comprendre comment les données textuelles sont stockées et interprétées. Dans ce TP, nous allons explorer en profondeur les concepts des jeux de caractères et des collations dans MySQL. Préparez-vous à découvrir et à mettre en pratique ces concepts essentiels! 😊

## Introduction 📚

**Jeux de caractères** : Un jeu de caractères est un ensemble de symboles et d'encodages. Dans MySQL, par exemple, `utf8` est un jeu de caractères qui peut représenter n'importe quel caractère universel.

**Collation** : Une collation est un ensemble de règles qui détermine comment les données du jeu de caractères sont comparées et triées. Par exemple, `utf8_general_ci` est une collation insensible à la casse pour le jeu de caractères `utf8`.

## Objectifs 🎯
- Comprendre l'importance et l'utilisation des jeux de caractères et des collations dans MySQL.
- Savoir comment définir, modifier et interroger les jeux de caractères et les collations pour une base de données, une table ou une colonne.

## Exercice 1: Exploration des jeux de caractères et des collations 🕵️‍♂️

### Étapes:

1. **Consultation des jeux de caractères et des collations par défaut** 🧐
   - Affichez le jeu de caractères et la collation par défaut de votre serveur MySQL :
     ```sql
     SHOW VARIABLES LIKE 'character_set_server';
     SHOW VARIABLES LIKE 'collation_server';
     ```

2. **Modification du jeu de caractères et de la collation de la base de données** 🔄
   - Modifiez le jeu de caractères de votre base de données `exploration_types` en `utf8mb4` et la collation en `utf8mb4_unicode_ci` :
     ```sql
     ALTER DATABASE exploration_types CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
     ```

3. **Création d'une table avec un jeu de caractères spécifique** 🛠️
   - Créez une table `messages` avec une colonne `texte` de type `TEXT` et un jeu de caractères `utf8mb4` :
     ```sql
     CREATE TABLE messages (
       id INT AUTO_INCREMENT PRIMARY KEY,
       texte TEXT CHARACTER SET utf8mb4
     );
     ```

4. **Insertion de données avec différents caractères** 🌍
   - Insérez quelques messages contenant des emojis, des caractères spéciaux et des textes dans différentes langues pour tester le jeu de caractères :
     ```sql
     INSERT INTO messages (texte) VALUES ('Bonjour tout le monde! 😃🌍');
     INSERT INTO messages (texte) VALUES ('Hola Mundo! 🌞');
     INSERT INTO messages (texte) VALUES ('你好，世界！🐉');
     ```

5. **Consultation des données** 🧐
   - Affichez les données de la table `messages` :
     ```sql
     SELECT * FROM messages;
     ```

## Exercice 2: Comparaison de collations 🔄

### Étapes:

1. **Création d'une table pour tester les collations** 🛠️
   - Créez une table `comparaison` avec deux colonnes `texteA` et `texteB`, toutes deux de type `VARCHAR(50)` mais avec des collations différentes :
     ```sql
     CREATE TABLE comparaison (
       id INT AUTO_INCREMENT PRIMARY KEY,
       texteA VARCHAR(50) COLLATE utf8mb4_bin,
       texteB VARCHAR(50) COLLATE utf8mb4_general_ci
     );
     ```

2. **Insertion de données pour la comparaison** 📝
   - Insérez des données dans la table `comparaison` :
     ```sql
     INSERT INTO comparaison (texteA, texteB) VALUES ('café', 'Café');
     ```

3. **Comparaison des colonnes** 🧮
   - Comparez les colonnes `texteA` et `texteB` en utilisant l'opérateur `=` :
     ```sql
     SELECT * FROM comparaison WHERE texteA = texteB;
     ```

   - Notez les résultats. La collation `utf8mb4_bin` est sensible à la casse, tandis que `utf8mb4_general_ci` ne l'est pas. Observez comment cela affecte les résultats de la comparaison.

## Exercice 3: Modification des collations et jeux de caractères d'une table existante 🔄

### Étapes:

1. **Modification de la collation d'une colonne** 🛠️
   - Modifiez la collation de la colonne `texteA` de la table `comparaison` en `utf8mb4_unicode_ci` :
     ```sql
     ALTER TABLE comparaison MODIFY texteA VARCHAR(50) COLLATE utf8mb4_unicode_ci;
     ```

2. **Vérification des modifications** 🧐
   - Comparez à nouveau les colonnes `texteA` et `texteB` :
     ```sql
     SELECT * FROM comparaison WHERE texteA = texteB;
     ```

   - Notez les résultats. Les deux colonnes devraient maintenant être considérées comme égales car elles utilisent des collations insensibles à la casse.

## Exercice 4: Exploration des erreurs courantes liées aux jeux de caractères 🚫

### Étapes:

1. **Insertion de données avec un mauvais encodage** 📝
   - Essayez d'insérer un texte avec un emoji dans une colonne qui n'utilise pas `utf8mb4` :
     ```sql
     CREATE TABLE test_encodage (
       id INT AUTO_INCREMENT PRIMARY KEY,
       texte VARCHAR(50) CHARACTER SET utf8
     );

     INSERT INTO test_encodage (texte) VALUES ('Ceci est un test 😃');
     ```

   - Notez l'erreur retournée. MySQL ne peut pas stocker l'emoji car le jeu de caractères `utf8` ne le prend pas en charge.

2. **Correction de l'erreur** 🛠️
   - Modifiez la table pour utiliser le jeu de caractères `utf8mb4` :
     ```sql
     ALTER TABLE test_encodage MODIFY texte VARCHAR(50) CHARACTER SET utf8mb4;
     ```

   - Réessayez d'insérer le texte avec l'emoji :
     ```sql
     INSERT INTO test_encodage (texte) VALUES ('Ceci est un test 😃');
     ```

   - Vérifiez que l'insertion a réussi.

## Exercice 5: Recherche et tri avec différentes collations 🧮

### Étapes:

1. **Insertion de données pour la recherche et le tri** 📝
   - Insérez plusieurs valeurs dans la table `comparaison` :
     ```sql
     INSERT INTO comparaison (texteA, texteB) VALUES ('école', 'ecole');
     INSERT INTO comparaison (texteA, texteB) VALUES ('élève', 'eleve');
     INSERT INTO comparaison (texteA, texteB) VALUES ('étude', 'etude');
     ```

2. **Recherche avec collation** 🧐
   - Recherchez les entrées où `texteA` est égal à "eleve" :
     ```sql
     SELECT * FROM comparaison WHERE texteA = 'eleve';
     ```

   - Notez les résultats. En raison de la collation insensible aux accents, "élève" et "eleve" sont considérés comme égaux.

3. **Tri avec collation** 📊
   - Triez les entrées de la table `comparaison` par `texteA` :
     ```sql
     SELECT * FROM comparaison ORDER BY texteA;
     ```

   - Observez l'ordre des résultats. Avec une collation insensible aux accents, les mots avec des accents sont triés comme s'ils n'en avaient pas.

## Exercice 6: Projet Final - Gestion d'une bibliothèque multilingue 📚🌍

Dans cet exercice, vous allez créer et gérer une base de données pour une bibliothèque qui contient des livres de différentes langues et scripts. Vous allez mettre en pratique toutes les notions apprises sur les jeux de caractères et les collations.

### Objectifs:
- Créer une base de données avec le bon jeu de caractères et collation pour gérer des textes multilingues.
- Insérer, rechercher et trier des données en tenant compte des spécificités linguistiques.
- Modifier les jeux de caractères et collations lorsque nécessaire.

### Étapes:

1. **Création de la base de données** 🛠️
   - Créez une base de données `bibliotheque_multilingue` avec le jeu de caractères `utf8mb4` et la collation `utf8mb4_unicode_ci`.

2. **Création de la table `livres`** 📖
   - Cette table contiendra les colonnes suivantes :
     - `id` : identifiant unique du livre.
     - `titre` : titre du livre.
     - `auteur` : nom de l'auteur.
     - `langue` : langue du livre (par exemple, "français", "espagnol", "chinois", etc.).
     - `resume` : un bref résumé du livre.

3. **Insertion de données** 📝
   - Insérez au moins 10 livres dans la table. Assurez-vous d'inclure des livres dans différentes langues, avec des caractères spéciaux, des accents, et même des emojis dans les résumés.

4. **Recherche avec collation** 🧐
   - Recherchez tous les livres dont le titre contient le mot "école", en tenant compte des variations possibles (comme "école", "ecole", "ÉCOLE", etc.).
   - Recherchez tous les livres en espagnol et triez-les par titre, en tenant compte des spécificités de la langue espagnole.

5. **Modification des collations** 🔄
   - Modifiez la collation de la colonne `titre` pour être sensible à la casse.
   - Répétez la recherche du mot "école" dans le titre et notez les différences dans les résultats.

6. **Rapport final** 📄
   - Rédigez un bref rapport décrivant les étapes que vous avez suivies, les défis que vous avez rencontrés et comment vous les avez surmontés. Incluez également des captures d'écran ou des extraits de code pour illustrer votre travail.

### Rendu attendu:
- Script SQL contenant toutes les commandes que vous avez exécutées, commentées et organisées.
- Rapport final décrivant votre démarche, accompagné de captures d'écran ou d'exemples de code.
- Assurez-vous que votre script SQL est bien structuré, commenté et facile à suivre.

---

🌟 **Conseil**: Cet exercice est une excellente occasion de montrer votre compréhension des concepts et de démontrer votre capacité à appliquer ces concepts dans un contexte réel. Assurez-vous de tester chaque étape soigneusement et de documenter votre processus. Bonne chance! 🍀👩‍💻👨‍💻