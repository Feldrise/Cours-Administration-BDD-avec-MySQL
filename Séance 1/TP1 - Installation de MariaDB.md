# Travaux Pratiques : Installation de MariaDB

## Installation de MariaDB
**Durée estimée : 20 minutes**

### Objectifs
- Installer MariaDB sur votre système d'exploitation.
- Vérifier que l'installation a été réussie.

### Étapes

1. **Système Windows**:
   - Rendez-vous sur le site officiel de MariaDB pour télécharger l'installeur pour Windows : [MariaDB Downloads](https://downloads.mariadb.org/)
   - Choisissez la version appropriée et téléchargez-la.
   - Exécutez l'installeur et suivez les instructions à l'écran.
   - Vérifiez l'installation en ouvrant la ligne de commande et en tapant `mysql --version`. Vous devriez voir le numéro de version affiché. 🎉

2. **Système Linux (basé sur Debian/Ubuntu)**:
   ```bash
   sudo apt update
   sudo apt install mariadb-server
   sudo systemctl start mariadb
   sudo mysql_secure_installation
   ```
   - Après avoir exécuté `mysql_secure_installation`, suivez les instructions à l'écran.
   - Vérifiez l'installation avec : `mysql --version`. Si tout va bien, la version devrait s'afficher. 🐧

3. **Système macOS**:
   - Si vous avez Homebrew, utilisez :
     ```bash
     brew update
     brew install mariadb
     brew services start mariadb
     ```
   - Sinon, allez sur le site officiel de MariaDB pour télécharger l'installeur pour macOS.
   - Vérifiez l'installation en ouvrant le terminal et en tapant `mysql --version`. Vous devriez voir le numéro de version. 🍏

4. Pour les autres systèmes d'exploitation, consultez la documentation officielle de MariaDB pour des instructions détaillées.

---

## Temps d'échange
**Durée : 10 minutes**

🙋‍♂️ C'est le moment de poser toutes vos questions concernant l'installation! Si vous avez rencontré des problèmes ou si quelque chose n'est pas clair, n'hésitez pas à demander. Nos assistants sont là pour vous aider. 🚀

Bonne chance à tous dans cette aventure MariaDB! 🌟🎉