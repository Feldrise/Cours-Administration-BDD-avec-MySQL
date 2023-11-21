# Travaux Pratiques: Dépannage Avancé des Problèmes Courants en Administration de Base de Données MySQL

## Partie Unique: Diagnostic et Résolution de Problèmes
**Durée estimée : 1 heures**

### Objectifs
🔍 Maîtriser le diagnostic et la résolution des problèmes d'administration courants dans MySQL.
🔍 Développer une approche systématique pour le dépannage.

### Notions Théoriques et Exemples

#### 1. Problèmes de Connexion
- **Théorie:** 
  - Causes typiques : erreurs de réseau, mauvaise configuration du serveur, problèmes de permission.
  - MySQL utilise un système de permissions basé sur les utilisateurs et les adresses IP.

- **Exemple Pratique:**
  - Simuler une erreur de connexion en changeant les permissions de l'utilisateur.
  - Utiliser `mysql_error()` après une tentative de connexion échouée pour diagnostiquer.
  - Résoudre en vérifiant et ajustant les permissions via `GRANT` ou `REVOKE`.

#### 2. Corruption de Données
- **Théorie:** 
  - Causes possibles : arrêts inattendus, problèmes matériels, bugs logiciels.
  - Utiliser `CHECK TABLE` et `REPAIR TABLE` pour diagnostiquer et réparer.

- **Exemple Pratique:**
  - Provoquer une corruption en arrêtant le serveur durant une écriture.
  - Identifier la corruption avec `CHECK TABLE`.
  - Réparer avec `REPAIR TABLE`.

#### 3. Performances et Goulots d'Étranglement
- **Théorie:** 
  - Causes : requêtes mal optimisées, configuration du serveur, contraintes matérielles.
  - `EXPLAIN` et les logs des requêtes lentes pour identifier les inefficacités.

- **Exemple Pratique:**
  - Analyser une requête lente avec `EXPLAIN`.
  - Optimiser la requête avec des index ou en la réécrivant.

#### 4. Problèmes de Réplication
- **Théorie:** 
  - Problèmes : désynchronisation des données, erreurs de configuration, retards.
  - `SHOW SLAVE STATUS` et `SHOW MASTER STATUS` pour le diagnostic.

- **Exemple Pratique:**
  - Simuler un retard de réplication avec des opérations lourdes sur le maître.
  - Utiliser `SHOW SLAVE STATUS` pour identifier le retard.
  - Résoudre avec des ajustements de configuration ou optimisation des opérations.

#### 5. Problèmes de Verrouillage
- **Théorie:**
  - Verrouillages longs ou concurrents pouvant causer des ralentissements.
  - Utilisation de `SHOW ENGINE INNODB STATUS` pour examiner les verrouillages.

- **Exemple Pratique:**
  - Créer des scénarios de verrouillage concurrent.
  - Identifier les verrouillages problématiques et les résoudre.

#### 6. Gestion des Sauvegardes et Restaurations Échouées
- **Théorie:**
  - Importance des sauvegardes régulières, risques de sauvegardes corrompues ou incomplètes.
  - Procédures pour vérifier l'intégrité des sauvegardes et restaurer avec prudence.

- **Exemple Pratique:**
  - Tenter de restaurer à partir d'une sauvegarde corrompue.
  - Diagnostiquer le problème et explorer des solutions alternatives.