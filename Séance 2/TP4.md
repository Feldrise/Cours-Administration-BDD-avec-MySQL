# Exploration des Options du Serveur à l'Exécution 🚀

## Partie 1 : Ajustement en Direct de MySQL 🛠
**Durée estimée : 20 minutes**

### Objectifs
- Comprendre et maîtriser les commandes permettant d'ajuster les options de MySQL à la volée.
- Observer les impacts de ces changements sans redémarrer le serveur MySQL.

### Étapes

1. **Visualisation des Variables Actuelles** 🧐
    - Avant de faire des modifications, il est crucial de connaître l'état actuel. 
    - Utilisez la commande suivante pour afficher les variables courantes :
      ```sql
      SHOW VARIABLES;
      ```

2. **Modification d'une Variable à la Volée** 🌀
    - Dans cet exercice, vous allez augmenter la taille du cache de requête.
    - Utilisez la commande suivante pour modifier la taille du cache de requêtes :
      ```sql
      SET GLOBAL query_cache_size = 10485760; -- Ceci définit la taille à 10MB
      ```

3. **Vérification de la Modification** ✅
    - Vérifiez que votre changement a bien été pris en compte en utilisant :
      ```sql
      SHOW VARIABLES LIKE 'query_cache_size';
      ```

4. **Testez d'autres Modifications** 🎨
    - Essayez d'autres modifications à la volée pour voir comment elles affectent le serveur. 
    - Par exemple, vous pourriez ajuster le nombre maximal de connexions autorisées :
      ```sql
      SET GLOBAL max_connections = 150;
      ```

## Partie 2: Mesure de la Performance Suite aux Ajustements 🧪
**Durée estimée : 30 minutes**

### Objectifs
- Comprendre comment mesurer les performances du serveur MySQL suite à des modifications.
- Expérimenter l'impact des changements de configuration sur les performances en temps réel.
- Apprendre à interpréter les métriques clés de performance pour prendre des décisions éclairées.

### Étapes

1. **Création d'une Charge Simulée sur le Serveur** 🔄
    - Avant d'observer l'impact de vos modifications, générez du trafic sur votre serveur. Vous pouvez utiliser des outils comme `mysqlslap` pour simuler une charge.
      ```bash
      mysqlslap --user=username --password=password --host=localhost --concurrency=50 --iterations=5
      ```

2. **Modification du Nombre de Connexions** 🔌
    - Comme dans l'exemple précédent, ajustez le nombre maximal de connexions.
      ```sql
      SET GLOBAL max_connections = 300;
      ```

3. **Observation des Métriques de Performance** 📉
    - Utilisez différentes commandes pour surveiller les aspects clés du serveur.
   
   a. **Nombre de Threads Connectés** : 
      ```sql
      SHOW STATUS LIKE 'Threads_connected';
      ```
   b. **Utilisation de la Mémoire** :
      ```sql
      SHOW GLOBAL STATUS LIKE 'Innodb_buffer_pool_pages_data';
      SHOW GLOBAL STATUS LIKE 'Innodb_buffer_pool_pages_free';
      ```
   c. **Latence des Requêtes** :
      Pour cela, vous devrez avoir un outil de surveillance externe ou observer le temps d'exécution de requêtes répétées.

4. **Interprétation des Résultats** 📚
    - Notez la différence de performance entre les différentes configurations. 
    - Posez-vous des questions clés :
        - La latence des requêtes a-t-elle augmenté?
        - La mémoire est-elle sur-utilisée?
        - Y a-t-il des signes de contention ou de blocage sur le serveur?
        
5. **Optimisation et Ajustements** ⚙️
    - Sur la base de vos observations, essayez d'optimiser la performance. 
    - Par exemple, si vous observez une surutilisation de la mémoire, vous pourriez réduire la taille du buffer pool d'InnoDB :
      ```sql
      SET GLOBAL innodb_buffer_pool_size = 134217728;  -- Ceci définit la taille à 128MB
      ```

6. **Réévaluation et Ajustements Continus** 🔍
    - La performance n'est pas une cible fixe. Continuez d'ajuster, de mesurer et d'optimiser en fonction des besoins de votre serveur et de la charge.

🌟 Rappelez-vous que chaque serveur et application a des besoins uniques. L'optimisation et l'ajustement nécessitent une compréhension profonde des métriques et une volonté d'expérimenter pour trouver la meilleure configuration. 🚀

🎉 Félicitations ! Vous avez maintenant une meilleure compréhension de comment ajuster dynamiquement les options de MySQL. N'oubliez pas de toujours surveiller les performances et d'ajuster en conséquence. 😄