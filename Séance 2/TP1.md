# Exploration de l'Architecture MySQL 🚀

## Découverte des Composants de l'Architecture MySQL 🧐
**Durée estimée :** 45 minutes

### Objectifs
- Se familiariser avec l'architecture interne de MySQL.
- Utiliser des commandes pour visualiser les informations concernant le serveur.
- Identifier les principaux composants tels que le gestionnaire de connexions, le gestionnaire de requêtes, les moteurs de stockage et les fichiers journaux.

### Étapes

1. **Connectez-vous au serveur MySQL** 🖥️
   Utilisez la commande suivante pour vous connecter:
   ```bash
   mysql -u [username] -p
   ```

2. **Visualisation des Variables du Serveur** 🌐
   Utilisez la commande `SHOW VARIABLES;` pour afficher une liste de toutes les variables système que MySQL supporte.
   Par exemple:
   ```sql
   SHOW VARIABLES LIKE 'datadir';
   ```
   Cela vous montrera où les fichiers de données MySQL sont stockés.

3. **Consultation du Statut du Serveur** 🔍
   Avec la commande `SHOW STATUS;`, vous pouvez visualiser le statut actuel de votre serveur MySQL.
   Par exemple:
   ```sql
   SHOW STATUS LIKE 'Connections';
   ```
   Cela affichera le nombre total de connexions qui ont été tentées sur le serveur MySQL depuis son dernier démarrage.

4. **Explorez les Composants de l'Architecture** 🏗️
   - **Gestionnaire de connexions:** Lorsqu'une connexion est établie, le serveur doit gérer cette connexion. Pour ce faire, il utilise le gestionnaire de connexions.
   - **Gestionnaire de requêtes:** Après avoir établi une connexion, chaque requête envoyée est traitée par le gestionnaire de requêtes.
   - **Moteurs de stockage:** MySQL supporte plusieurs moteurs de stockage, chacun ayant ses propres avantages. Vous pouvez les voir en utilisant:
     ```sql
     SHOW ENGINES;
     ```
   - **Fichiers journaux:** Ce sont des fichiers qui enregistrent les modifications apportées à la base de données. Ils sont cruciaux pour la restauration des données et la réplication.

5. **Réflexion sur l'Architecture** 💭
   - Quels sont, selon vous, les avantages d'avoir plusieurs moteurs de stockage ?
   - Pourquoi est-il crucial d'avoir des fichiers journaux?

### Exercice 1: Analyse des Variables du Serveur 🔍

**Objectif:** Approfondir votre compréhension des variables système de MySQL et comment elles affectent le comportement du serveur.

1. Listez toutes les variables qui ont trait à la taille du buffer:
   ```sql
   SHOW VARIABLES LIKE '%buffer%';
   ```

2. Quelle est la taille actuelle du buffer de requête ? Estimez-vous que cette taille est adéquate pour un petit site web ? Pourquoi ?

3. Trouvez la version de votre serveur MySQL:

---

### Exercice 2: Exploration des Statistiques du Serveur 📊

**Objectif:** Comprendre les différentes métriques et ce qu'elles signifient pour la performance et la santé du serveur.

1. Combien de requêtes ont été exécutées depuis le dernier redémarrage du serveur MySQL ?
   ```sql
   SHOW STATUS LIKE 'Questions';
   ```

2. Quelle est la durée moyenne de connexion au serveur?
   ```sql
   SHOW STATUS LIKE 'Uptime';
   ```

3. Combien de requêtes ont échoué?
   ```sql
   SHOW STATUS LIKE 'Failed_queries';
   ```

---

### Exercice 3: Moteurs de Stockage 🚂

**Objectif:** Se familiariser davantage avec les différents moteurs de stockage disponibles dans MySQL.

1. Quel est le moteur de stockage par défaut de votre installation MySQL?
   ```sql
   SHOW VARIABLES LIKE 'default_storage_engine';
   ```

2. Créez une petite table en utilisant le moteur MyISAM, puis une autre en utilisant InnoDB. Par exemple:
   ```sql
   CREATE TABLE table_myisam (id INT) ENGINE=MyISAM;
   CREATE TABLE table_innodb (id INT) ENGINE=InnoDB;
   ```

3. Comparez les deux tables. Quelles sont les principales différences entre elles en termes de fonctionnalités? (Vous pourriez avoir besoin de faire quelques recherches pour répondre à cette question!)

---

### Exercice 4: Scénarios du Monde Réel 🌎

**Objectif:** Utiliser les informations que vous avez recueillies pour prendre des décisions dans des scénarios du monde réel.

1. Imaginez que vous avez remarqué que votre serveur MySQL est lent lors de la réalisation de nombreuses petites transactions. Quelles variables pourriez-vous ajuster pour améliorer les performances?

2. Votre application web a soudainement reçu beaucoup de trafic. Quelles commandes utilisez-vous pour vérifier l'état actuel de votre serveur?

3. Vous prévoyez d'importer une énorme quantité de données dans votre base de données. Comment préparez-vous votre serveur pour cette opération?

---

Comme toujours, n'hésitez pas à poser des questions et à discuter avec vos camarades. 🎉👩‍💻👨‍💻