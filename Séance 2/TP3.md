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
     /etc/mysql/my.cnf
     ```
   - Jetez un coup d'œil aux différentes sections et paramètres disponibles. 🧐

2. **Modification de la mémoire tampon InnoDB**
   - Dans la section `[mysqld]`, trouvez ou ajoutez la ligne suivante pour ajuster la taille de la mémoire tampon InnoDB:
     ```bash
     innodb_buffer_pool_size = 512M
     ```
   > NOTE : Vous devez peut-être ajouter vous même la section en bas du fichier

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