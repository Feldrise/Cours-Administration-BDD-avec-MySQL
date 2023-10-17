# Atelier de Configuration du Serveur MySQL 🛠️

**Durée estimée:** 1 heure

## Partie 1: Exploration et Modification du fichier de configuration 📁

### Objectifs:
- Découvrir le fichier de configuration de MySQL.
- Apprendre à ajuster les principaux paramètres pour optimiser les performances du serveur.

### Étapes:

1. **Identification du fichier de configuration**
   - Ouvrez le fichier de configuration MySQL, généralement situé à:
     ```bash
     /etc/my.cnf
     ```
     ou sur certains systèmes:
     ```bash
     /etc/mysql/my.ini
     ```
   - Jetez un coup d'œil aux différentes sections et paramètres disponibles. 🧐

2. **Modification de la mémoire tampon InnoDB**
   - Dans la section `[mysqld]`, trouvez ou ajoutez la ligne suivante pour ajuster la taille de la mémoire tampon InnoDB:
     ```bash
     innodb_buffer_pool_size = 512M
     ```
   - Cet exemple fixe la mémoire tampon à 512 Mo. Vous pouvez ajuster cette valeur en fonction de vos besoins! 😊

3. **Ajustement du nombre maximum de connexions**
   - Toujours dans la section `[mysqld]`, trouvez ou ajoutez la ligne:
     ```bash
     max_connections = 150
     ```
   - Cela permet d'autoriser jusqu'à 150 connexions simultanées. Ajustez selon les besoins de votre serveur. 👥

4. **Sauvegardez vos modifications** et fermez le fichier.

---

## Partie 2: Redémarrage du serveur et vérification des modifications 🔄

### Objectifs:
- Apprendre à redémarrer MySQL après une modification.
- Vérifier que les modifications ont bien été prises en compte.

### Étapes:

1. **Redémarrage du serveur MySQL**
   - Utilisez la commande suivante pour redémarrer votre serveur:
     ```bash
     sudo service mysql restart
     ```

2. **Vérification des modifications**
   - Connectez-vous à MySQL:
     ```bash
     mysql -u root -p
     ```
   - Pour vérifier la taille de la mémoire tampon InnoDB, utilisez la commande:
     ```sql
     SHOW VARIABLES LIKE 'innodb_buffer_pool_size';
     ```
   - Pour vérifier le nombre maximum de connexions, tapez:
     ```sql
     SHOW VARIABLES LIKE 'max_connections';
     ```

3. Comparez les valeurs obtenues avec celles que vous avez configurées. Tout est bon? Bravo! 🎉

---

## Partie 3: Gestion du Journal des Requêtes Lentes 🐢

### Objectifs:
- Découvrir et activer le journal des requêtes lentes.
- Identifier et corriger les requêtes potentiellement problématiques.

### Étapes:

1. **Activation du Journal des Requêtes Lentes**
   - Dans votre fichier de configuration MySQL, sous la section `[mysqld]`, ajoutez ou modifiez les lignes suivantes :
     ```bash
     slow_query_log = 1
     slow_query_log_file = /var/log/mysql-slow.log
     long_query_time = 2
     ```
   - Cela activera le journal des requêtes lentes, enregistrant toutes les requêtes qui prennent plus de 2 secondes pour s'exécuter.

2. **Redémarrez MySQL** pour que les changements prennent effet.

3. **Analyse des Requêtes Lentes**
   - Une fois quelques requêtes enregistrées, ouvrez le fichier `/var/log/mysql-slow.log`.
   - Identifiez quelques requêtes qui y sont enregistrées. Pourquoi pensez-vous qu'elles sont lentes ?

4. **Optimisation des Requêtes**
   - Choisissez une des requêtes lentes et essayez de l'optimiser. Pourriez-vous ajouter des index ? La requête pourrait-elle être réécrite pour être plus efficace ?

---

## Partie 4: Sécurité et Utilisateurs ⛔

### Objectifs:
- Découvrir comment créer, modifier et supprimer des utilisateurs.
- Configurer des permissions appropriées pour chaque utilisateur.

### Étapes:

1. **Création d'un Nouvel Utilisateur**
   - Connectez-vous à MySQL et exécutez la commande suivante pour créer un nouvel utilisateur :
     ```sql
     CREATE USER 'nouvel_utilisateur'@'localhost' IDENTIFIED BY 'mot_de_passe';
     ```

2. **Attribution des Permissions**
   - Attribuez des permissions à votre nouvel utilisateur :
     ```sql
     GRANT SELECT, INSERT ON *.* TO 'nouvel_utilisateur'@'localhost';
     ```

3. **Vérification des Permissions**
   - Connectez-vous à MySQL avec le nouvel utilisateur et essayez d'exécuter différentes requêtes. Quelles opérations sont autorisées? Lesquelles sont interdites?

4. **Modification des Permissions**
   - Reconnectez-vous avec l'utilisateur root. Revoquez l'autorisation INSERT de l'utilisateur précédemment créé :
     ```sql
     REVOKE INSERT ON *.* FROM 'nouvel_utilisateur'@'localhost';
     ```

5. **Suppression de l'Utilisateur**
   - Une fois que vous avez terminé avec l'utilisateur, supprimez-le :
     ```sql
     DROP USER 'nouvel_utilisateur'@'localhost';
     ```

---

## Partie 5: Tests de Charge 🔄
**Durée estimée:** 30 minutes

### Objectifs:
- Évaluer comment MySQL réagit sous des charges élevées.
- Identifier et corriger les goulets d'étranglement.

### Étapes:

1. **Création d'un Script de Test**
   - Utilisez un outil de votre choix (comme Apache JMeter ou MySQL Workbench) pour générer un grand nombre de requêtes simultanées vers votre base de données.

2. **Exécution du Script**
   - Lancez le script et observez la charge sur votre serveur MySQL. Utilisez des outils comme `htop` ou `top` pour surveiller les ressources système.

3. **Analyse des Résultats**
   - Quelles requêtes sont les plus lentes? Y a-t-il des erreurs ou des refus de connexions?

4. **Optimisation**
   - Apportez des modifications à la configuration de votre serveur MySQL pour tenter d'améliorer les performances sous une charge élevée.

## Partie 3: 🎖️
**Durée estimée:** 15 minutes

### Objectifs:
- Pousser un peu plus vos compétences et votre compréhension.
- S'habituer à d'autres paramètres couramment modifiés.

### Étapes:

1. Essayez d'ajuster d'autres paramètres que vous trouvez pertinents dans le fichier de configuration.
   
2. Redémarrez le serveur et vérifiez vos modifications comme vous l'avez appris.

3. Partagez vos découvertes avec le groupe! 🚀

---

Bonne chance à tous! N'hésitez pas à poser des questions si vous avez des doutes ou des problèmes. 😊👍