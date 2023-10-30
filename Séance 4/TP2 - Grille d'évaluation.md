# Grille d'évaluation : Projet Final - Gestion d'une bibliothèque multilingue 📚🌍

## 1. Création de la base de données (15 points)
- **Base de données créée** (5 points)
  - La base de données `bibliotheque_multilingue` est correctement créée.
  
- **Utilisation du bon jeu de caractères et collation** (10 points)
  - Le jeu de caractères `utf8mb4` et la collation `utf8mb4_unicode_ci` sont correctement appliqués.

## 2. Création de la table `livres` (20 points)
- **Structure de la table** (15 points)
  - Toutes les colonnes requises (`id`, `titre`, `auteur`, `langue`, `resume`) sont présentes.
  - Les types de données appropriés sont utilisés pour chaque colonne.
  
- **Clé primaire** (5 points)
  - La colonne `id` est correctement définie comme clé primaire et auto-increment.

## 3. Insertion de données (20 points)
- **Variété des données** (10 points)
  - Au moins 10 livres sont insérés.
  - Les livres de différentes langues sont inclus.
  
- **Utilisation de caractères spéciaux, accents et emojis** (10 points)
  - Les données insérées montrent une compréhension de l'utilisation des caractères spéciaux, des accents et des emojis.

## 4. Recherche avec collation (20 points)
- **Recherche de "école"** (10 points)
  - La requête renvoie correctement tous les livres dont le titre contient le mot "école" en tenant compte des variations.
  
- **Recherche et tri des livres en espagnol** (10 points)
  - La requête renvoie correctement tous les livres en espagnol et les trie par titre en tenant compte des spécificités de la langue espagnole.

## 5. Modification des collations et tests (15 points)
- **Modification de la collation de la colonne `titre`** (5 points)
  - La collation de la colonne `titre` est correctement modifiée pour être sensible à la casse.
  
- **Tests après modification** (10 points)
  - Les tests montrent une compréhension des effets de la modification de la collation.

## 6. Rapport final (10 points)
- **Clarté et organisation** (5 points)
  - Le rapport est bien structuré, clair et facile à suivre.
  
- **Réflexion et analyse** (5 points)
  - Le rapport montre une réflexion sur les étapes suivies, les défis rencontrés et comment ils ont été surmontés.

---

**Total : 100 points**

📝 **Remarques** : L'évaluation se concentre à la fois sur la réalisation technique (création de la base de données, insertion de données, etc.) et sur la compréhension des concepts (utilisation des jeux de caractères, collations, etc.). Il est important de fournir des commentaires ou des justifications pour chaque étape, en particulier dans le rapport final.