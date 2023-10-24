# Travaux Pratiques: Gestion des Journaux

## Gestion des Journaux du Serveur MySQL
**Durée estimée:** 2h

### Objectifs
- Apprendre à activer les journaux sur MySQL.
- Savoir gérer et lire les journaux pour dépanner et optimiser la base de données.

### Étapes
1. **Activation du journal général**
   - Ouvrez le fichier de configuration MySQL.
   - Sous la section `[mysqld]`, ajoutez la ligne suivante:
     ```bash
     general_log = 1
     general_log_file = /var/log/mysql/mysql.log
     log_error = /var/log/mysql/mysql-errors.log
     ```
   - Redémarrez le serveur MySQL.
   - Vérifiez que le journal général a bien été activé en exécutant:
     ```sql
     SHOW VARIABLES LIKE 'general_log%';
     ```
   - 👉 Astuce : Le journal général est utile pour le dépannage, mais peut générer un volume important. Utilisez-le avec précaution!

3. **Activation du journal des requêtes lentes**
   - Dans le fichier de configuration MySQL, ajoutez ou modifiez:
     ```bash
     slow_query_log = 1
     slow_query_log_file = /var/log/mysql/mysql-slow.log
     long_query_time = 2
     ```

### Exercice 1: Analyse du Journal Général

0. Exécutez plusieurs requêtes SQL pour créer des bases de données, tables et séléctionner des données. Vous pouvez reprendre des TPs précédent comme exemple.

1. **Recherche de requêtes spécifiques**
   - Parcourez le journal général et identifiez au moins 5 requêtes `SELECT` et 5 requêtes `INSERT`. Notez-les pour une discussion ultérieure.
   - 😎 Astuce: Utilisez des commandes shell comme `grep` pour faciliter cette recherche si le fichier de journal est très long.

2. **Identification des requêtes fréquentes**
   - Identifiez une requête qui semble se répéter fréquemment dans le journal. Quelle pourrait être la raison de cette répétition?

### Exercice 2: Gestion du Journal des Requêtes Lentes

1. **Création de requêtes lentes pour le test**
   - Exécutez les requêtes suivantes pour générer des entrées dans le journal des requêtes lentes:
     ```sql
     SELECT SLEEP(3);
     SELECT SLEEP(5);
     ```
   
2. **Analyse du journal**
   - Consultez le journal des requêtes lentes et identifiez les requêtes que vous venez d'exécuter. Combien de temps chaque requête a-t-elle pris?

3. **Ajustement du temps de requête**
   - Modifiez la valeur de `long_query_time` dans le fichier de configuration à `1` seconde.
   - Redémarrez MySQL.
   - Exécutez à nouveau les requêtes `SLEEP` ci-dessus.
   - Observez le journal des requêtes lentes. Quelles différences notez-vous?

### Exercice 3: Rotation des Journaux

La rotation des journaux permet d'éviter que les fichiers de journal ne deviennent trop volumineux, ce qui pourrait causer des problèmes de performance et de gestion de l'espace disque.

1. **Rotation manuelle des journaux**
   - Exécutez la commande suivante pour effectuer une rotation des journaux:
     ```sql
     FLUSH LOGS;
     ```
   - 📖 Cette commande ferme et rouvre tous les fichiers de journal. Un nouveau fichier est créé à chaque fois.
   - Vérifiez vos dossiers de journaux. Notez les nouveaux fichiers créés et la structure de nommage.

2. **Configuration de la rotation automatique**
   - 😎 Astuce: Pour un environnement de production, vous souhaiteriez peut-être utiliser des outils comme `logrotate` sur Linux pour gérer la rotation de vos fichiers de journaux.
   - Consultez la documentation de [https://doc.ubuntu-fr.org/logrotate](logrotate) et tentez de le mettre en place

### Exercice 4: Analyse du Journal des Erreurs

MySQL dispose également d'un journal des erreurs qui enregistre les problèmes rencontrés par le serveur.

1. **Consultation du journal des erreurs**
   - Identifiez où se trouve le fichier du journal des erreurs en exécutant:
     ```sql
     SHOW VARIABLES LIKE 'log_error';
     ```
   - Ouvrez ce fichier et examinez son contenu. Repérez-vous des erreurs ou des avertissements ?

2. **Simulation d'une erreur**
   - Essayez d'exécuter une requête incorrecte, par exemple :
     ```sql
     SELECT * FROM table_inexistante;
     ```
   - Recherchez cette erreur dans le journal des erreurs. Que pouvez-vous apprendre de cette entrée ?

### Exercice 5: Niveaux de Gravité des Journaux

MySQL permet de définir différents niveaux de gravité pour le journal des erreurs.

1. **Consultation du niveau de gravité actuel**
   - Exécutez la commande suivante pour connaître le niveau de gravité actuel:
     ```sql
     SHOW VARIABLES LIKE 'log_error_verbosity';
     ```
   
2. **Modification du niveau de gravité**
   - Changez le niveau de gravité pour inclure les messages, les erreurs et les avertissements:
     ```sql
     SET GLOBAL log_error_verbosity = 3;
     ```
   - Effectuez quelques actions, puis consultez le journal des erreurs. Notez les différences.

3. **Réflexion**
   - 🤔 Quels pourraient être les avantages et inconvénients de la modification du niveau de gravité du journal des erreurs?

---

🌠 Ces exercices supplémentaires visent à renforcer votre compréhension de la gestion des journaux avec MySQL. L'examen régulier des journaux et la compréhension de leur contenu peuvent être cruciaux pour l'administration, le dépannage et la sécurité de votre base de données. 🌠

### Exercice 6: Désactivation des Journaux

1. **Désactivation du journal général**
   - Désactivez le journal général en modifiant le fichier de configuration:
     ```bash
     general_log = 0
     ```
   - Redémarrez MySQL et vérifiez que le journal général est désactivé.
   
2. **Désactivation du journal des requêtes lentes**
   - Désactivez le journal des requêtes lentes de la même manière que le journal général:
     ```bash
     slow_query_log = 0
     ```
   - Redémarrez MySQL et assurez-vous que le journal des requêtes lentes est désactivé.

3. **Réflexion**
   - 🤔 Pensez aux raisons pour lesquelles vous voudriez désactiver ces journaux. Quels sont les avantages et inconvénients de chaque option?

---

🚀 Après avoir terminé ces exercices, partagez vos réflexions et découvertes avec vos pairs. La discussion aidera à renforcer ce que vous avez appris et à découvrir de nouvelles perspectives. 🚀

---

🌟 Bravo! Vous avez appris à gérer les journaux et à effectuer des tâches d'administration courantes avec MySQL. Continuez à explorer ces concepts et à mettre en pratique ce que vous avez appris! 🌟