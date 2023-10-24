# Travaux Pratiques: Administration Courante avec MySQL

## Tâches d’Administration Courantes
**Durée estimée:** 2h

### Objectifs
- Se familiariser avec les tâches d'administration de base.
- Comprendre comment gérer les utilisateurs, les permissions et optimiser la BDD.

### Étapes
1. **Gestion des utilisateurs**
   - Créez un nouvel utilisateur:
     ```sql
     CREATE USER 'nouvel_utilisateur'@'localhost' IDENTIFIED BY 'mot_de_passe';
     ```
   - 🚀 Rappelez-vous de toujours utiliser des mots de passe forts!
   
2. **Gestion des permissions**
   - Accordez à l'utilisateur précédemment créé des privilèges sur une base de données spécifique:
     ```sql
     GRANT ALL PRIVILEGES ON nom_base_de_donnees.* TO 'nouvel_utilisateur'@'localhost';
     ```
   - Vérifiez les privilèges d'un utilisateur:
     ```sql
     SHOW GRANTS FOR 'nouvel_utilisateur'@'localhost';
     ```
   - 👍 Bonne pratique: N'accordez que les privilèges nécessaires, évitez d'utiliser `ALL PRIVILEGES` sauf si c'est vraiment nécessaire.

3. **Gestion avancée des permissions**
   - Révoquez certaines permissions de l'utilisateur:
     ```sql
     REVOKE SELECT ON nom_base_de_donnees.nom_table FROM 'nouvel_utilisateur'@'localhost';
     ```
   - 🧐 C'est crucial de savoir révoquer des permissions pour maintenir la sécurité!

4. **Vérification et réparation des tables**
   - Vérifiez l'intégrité d'une table:
     ```sql
     CHECK TABLE nom_table;
     ```
   - Si des problèmes sont détectés, réparez la table:
     ```sql
     REPAIR TABLE nom_table;
     ```
   - 👌 Faire des vérifications régulières peut prévenir des soucis majeurs.

5. **Surveillance de l'espace disque**
   - Vérifiez la taille des bases de données:
     ```sql
     SELECT table_schema AS "Database", 
     ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS "Size (MB)" 
     FROM information_schema.TABLES 
     GROUP BY table_schema;
     ```
   - 📈 Surveiller l'espace disque vous aidera à éviter de manquer d'espace, ce qui pourrait causer des erreurs.

6. **Gestion des connexions**
   - Voir les connexions actives:
     ```sql
     SHOW FULL PROCESSLIST;
     ```
   - Terminez une connexion spécifique (utilisez avec prudence!):
     ```sql
     KILL connection_ID;
     ```
   - 🚫 Parfois, il peut être nécessaire de terminer des connexions pour gérer les ressources ou résoudre des problèmes.

7. **Optimisation de la base de données**
   - Utilisez la commande `OPTIMIZE TABLE` pour optimiser une table particulière:
     ```sql
     OPTIMIZE TABLE nom_table;
     ```
   - 😁 Ceci peut aider à améliorer les performances, surtout après avoir supprimé un grand nombre de lignes d'une table!

8. **Utilisation de l'EXPLAIN**
   - Prenez une requête de votre choix (de préférence une requête JOIN) et utilisez la commande `EXPLAIN` pour l'analyser:
     ```sql
     EXPLAIN SELECT * FROM table1 JOIN table2 ON table1.id = table2.table1_id;
     ```
   - 🕵️‍♂️ Examinez le plan d'exécution pour identifier les éventuels goulets d'étranglement.

9. **Optimisation des requêtes**
   - Sur la base des résultats d'EXPLAIN, modifiez votre requête pour améliorer son efficacité.
   - Testez la différence de temps d'exécution avant et après optimisation.

10. **Backup et restauration**
   - Créez un backup de votre base de données:
     ```bash
     mysqldump -u username -p nom_base_de_donnees > backup.sql
     ```
   - Restaurez une base de données à partir d'un backup:
     ```bash
     mysql -u username -p nom_base_de_donnees < backup.sql
     ```
   - 😅 Toujours avoir un backup récent est une assurance contre de nombreux problèmes!