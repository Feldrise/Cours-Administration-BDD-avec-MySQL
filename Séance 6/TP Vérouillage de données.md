# Travaux Pratiques: Exploration du Verrouillage des Données 🔒

## Partie 1: Comprendre le Verrouillage des Données

### Objectifs
- Comprendre les principes et l'importance du verrouillage des données dans la gestion des bases de données.
- Identifier les différents types de verrous et leurs utilisations.

### Théorie et Contexte

Le verrouillage des données est crucial dans un environnement multi-utilisateurs pour préserver l'intégrité et la cohérence des données. Lorsque plusieurs utilisateurs interagissent avec les mêmes données, des verrous sont utilisés pour prévenir les conflits et les anomalies.

#### Types de Verrous et Exemples:

1. **Verrou partagé (Shared Lock):**
   - **Utilisation:** Permet la lecture mais interdit la modification par d'autres transactions.
   - **Exemple MySQL:**
     ```sql
     START TRANSACTION;
     SELECT * FROM table_example WHERE id = 1 LOCK IN SHARE MODE;
     -- D'autres transactions peuvent lire id = 1, mais ne peuvent pas le modifier.
     COMMIT;
     ```

2. **Verrou exclusif (Exclusive Lock):**
   - **Utilisation:** Empêche d'autres transactions de lire ou modifier les données.
   - **Exemple MySQL:**
     ```sql
     START TRANSACTION;
     SELECT * FROM table_example WHERE id = 2 FOR UPDATE;
     -- D'autres transactions ne peuvent ni lire ni modifier id = 2.
     COMMIT;
     ```

3. **Verrous optimistes et pessimistes:**
   - **Optimiste:** 
     - **Principe:** Suppose que les conflits sont rares. Les vérifications se font à la validation.
     - **Exemple:** Généralement implémenté au niveau de l'application plutôt qu'au niveau de la base de données.
   - **Pessimiste:**
     - **Principe:** Présume des conflits fréquents. Les verrous sont appliqués dès le début.
     - **Exemple MySQL:** Comme le verrou exclusif ci-dessus.

#### Niveaux d'Isolation et Exemples:

1. **Read Uncommitted:**
   - **Caractéristique:** Lecture de données non validées.
   - **Exemple MySQL:**
     ```sql
     SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
     START TRANSACTION;
     SELECT * FROM table_example WHERE id = 3;
     -- Peut lire des modifications non commitées sur id = 3.
     COMMIT;
     ```

2. **Read Committed:**
   - **Caractéristique:** Lecture des données uniquement après leur validation.
   - **Exemple MySQL:**
     ```sql
     SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
     START TRANSACTION;
     SELECT * FROM table_example WHERE id = 4;
     -- Lecture des données de id = 4 seulement après leur commit.
     COMMIT;
     ```

3. **Repeatable Read:**
   - **Caractéristique:** Garantie de relire les mêmes données.
   - **Exemple MySQL:**
     ```sql
     SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
     START TRANSACTION;
     SELECT * FROM table_example WHERE id = 5;
     -- Les données de id = 5 restent constantes tout au long de la transaction.
     COMMIT;
     ```

4. **Serializable:**
   - **Caractéristique:** Isolation complète des transactions.
   - **Exemple MySQL:**
     ```sql
     SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
     START TRANSACTION;
     SELECT * FROM table_example WHERE id = 6;
     -- Les autres transactions sont complètement bloquées sur id = 6.
     COMMIT;
     ```

## Partie 2: Mise en Pratique avec MySQL
### Objectifs
- Appliquer les concepts de verrouillage dans des scénarios réels et complexes.
- Observer l'effet des verrous sur les transactions concurrentes.

### Étapes et Exemples
1. **Configuration de l'Environnement MySQL:**
   - Préparer une base de données avec des tables de test.
   - Exemple de table: `CREATE TABLE test (id INT PRIMARY KEY, valeur VARCHAR(50));`

2. **Expérimentation avec les Verrous Partagés:**
   - Appliquer un verrou partagé et tenter une écriture concurrente.
   - Exemple:
     ```sql
     START TRANSACTION;
     SELECT * FROM test WHERE id = 1 FOR SHARE;
     -- Dans une autre session, tenter:
     UPDATE test SET valeur = 'Nouvelle Valeur' WHERE id = 1;
     COMMIT;
     ```

3. **Utilisation des Verrous Exclusifs:**
   - Verrouiller une ligne pour écriture et observer l'effet sur les lectures concurrentes.
   - Exemple:
     ```sql
     START TRANSACTION;
     SELECT * FROM test WHERE id = 1 FOR UPDATE;
     -- Dans une autre session, tenter:
     SELECT * FROM test WHERE id = 1;
     COMMIT;
     ```

4. **Gestion des Deadlocks:**
   - Créer intentionnellement un deadlock pour observer sa résolution.
   - Exemple:
     ```sql
     -- Session 1:
     START TRANSACTION;
     UPDATE test SET valeur = 'Valeur A' WHERE id = 1;

     -- Session 2:
     START TRANSACTION;
     UPDATE test SET valeur = 'Valeur B' WHERE id = 2;

     -- Puis dans Session 1:
     UPDATE test SET valeur = 'Valeur A' WHERE id = 2;

     -- Et dans Session 2:
     UPDATE test SET valeur = 'Valeur B' WHERE id = 1;
     ```

### Analyse et Rapport
Après les expérimentations, rédigez un rapport détaillé sur vos observations. Incluez des discussions sur l'efficacité des différents types de verrous dans divers scénarios et comment gérer les deadlocks et les problèmes de performance.

---

Cet exercice vise à fournir une compréhension pratique du verrouillage des données, une compétence essentielle dans l'administration des bases de données. Bonne chance, et n'hésitez pas à poser des questions si besoin! 🚀📚