# Travaux Pratiques: Mise en Place de Techniques de Haute Disponibilité dans MySQL

## Partie 3: Techniques de Haute Disponibilité
**Durée estimée : 1 heures**

### Objectifs
💪 Comprendre les stratégies et les mécanismes de haute disponibilité pour les bases de données MySQL.
💪 Pratiquer la mise en place d'une solution de haute disponibilité.

### Introduction Théorique
Avant de plonger dans la pratique, familiarisons-nous avec les concepts clés de la haute disponibilité :

1. **Haute Disponibilité (High Availability - HA):** Cela fait référence à la capacité d'un système à rester opérationnel et accessible, même en cas de défaillances partielles. L'objectif est de minimiser le temps d'arrêt et d'assurer une continuité de service.

2. **Réplication:** La réplication dans MySQL permet de copier les données d'une instance MySQL (le maître) à une ou plusieurs instances (les esclaves). Ceci assure que, en cas de défaillance du serveur maître, un ou plusieurs serveurs esclaves peuvent prendre le relais.

3. **Types de Réplication:**
   - **Réplication Asynchrone:** Les modifications sur le maître sont transmises aux esclaves, mais il peut y avoir un délai. C'est le mode le plus courant dans MySQL.
   - **Réplication Semi-synchrone:** Le serveur maître attend la confirmation d'au moins un esclave que la transaction a été reçue avant de considérer la transaction comme complète.
   - **Réplication Synchrone:** Chaque transaction est répliquée et confirmée par les esclaves avant que le maître ne poursuive, assurant une cohérence parfaite des données.

4. **Clustering:** Le clustering, tel que MySQL Cluster, permet de répartir la charge et de garantir la disponibilité. Les données sont répliquées sur plusieurs nœuds, permettant une tolérance aux pannes et une répartition de la charge.

### Étapes Pratiques

1. **Configuration de la Réplication Asynchrone:**
   - **Étape 1:** Configurer le serveur maître.
     - Modifier le fichier de configuration `my.cnf` pour activer la réplication.
     - Exemple de configuration:
       ```
       [mysqld]
       log-bin=mysql-bin
       server-id=1
       ```
   - **Étape 2:** Configurer le serveur esclave.
     - Modifier `my.cnf` avec un `server-id` unique.
     - Exemple de configuration:
       ```
       [mysqld]
       server-id=2
       ```
   - **Étape 3:** Établir la connexion de réplication.
     - Sur le maître, créer un utilisateur dédié à la réplication et noter la position du fichier binaire (`SHOW MASTER STATUS;`).
     - Sur l'esclave, utiliser `CHANGE MASTER TO` pour se connecter au maître.

2. **Test de la Réplication:**
   - Créer une table et insérer des données sur le serveur maître.
   - Vérifier si les données apparaissent sur l'esclave.
   - Exemple de vérification:
     ```
     SELECT * FROM replicated_table;
     ```

3. **Simuler une Défaillance et Basculement (Failover):**
   - Arrêter le serveur maître.
   - Promouvoir l'esclave en tant que nouveau maître (réajuster les configurations).
   - Discuter de l'impact et de la manière de minimiser le temps d'arrêt.

### Conclusion

Cette activité combine théorie et pratique pour fournir une compréhension approfondie de la mise en œuvre de la haute disponibilité dans MySQL. Il est crucial de pratiquer et d'expérimenter pour maîtriser ces concepts. Bon courage et amusez-vous bien! 🌐💻🔁