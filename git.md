Cours git
==

Intruduction
--

Git est un outil de gestion de version (SCM = Source Code Manager) de fichier (principalement texte).

Il est particulièrement adapté au développement logiciel et facilite la collaboration.
Il a été crée par Linus Torvalds pour le développement du noyau Linux.


Résumé start
---

    echo "# testingtruc" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/NicolasHerin/testingtruc.git
    git push -u origin master
    

Création d'un dépôt Git (repository Git)
--

Si le projet est nouveau :

    git init

Commandes de base
--

Une modification peut passer par trois états :

* untracked : pas prise en compte pour la prochaine version.
* cached/indexed : prise en compte pour la prochaine version.
* commited : sauvegardée.

Pour surveiller l'état des modifications on utilise la commande :

    git status -u

Pour prendre en compte une modification dans un fichier, on utilise la commande :

    git add chemin_vers_le_fichier.ext
    git add --all

Pour créer une version à partir des fichiers ajoutés à l'index :

    git commit -m "description des modifications"
    
Pour voir l'historique des modifications :

    git log
    git log --oneline

Ignorer des fichiers.
--
Pour ignorer un fichier, il suffit de versionner un fichier nommé .gitignore et y indiquer tous les fichiers ou dossiers à ignorer.
(*.extension pour ignorer les fichiers avec une extension donnée)

    .idea
    *.tmp
    *.psd
    vendor

Comparer deux version :
(version_1 = 73e3162 ou ac666835 etc... numéro de version unique)

    git diff version_1..version2
    
Cloner un dépôt.
--

    git clone URL_du_depot
    git clone https://github.com/bioub/Formation_Git_2017_01.git
    
Après clonage, se mettre dans le repertoire du projet et appeler composer

    composer install
    
Synchroniser des dépôts.
--
Rappatrier les commit (-u origin master sur la première utilisation seulement)

    git pull -u origin master
    git pull
    
Publier vos commits

    git push

Pour pouvoir faire un 'git push' il faut être à jour, c'est-à-dire faire un 'git pull' si nécessaire.


Vérifier le remote repository en cours

    git remote show origin
    git remote show CoursSymfony (si on a changé l'origin)
    
Supprimer le repository
Accéder à la partie setting du repository en cours en modifiant l'url

    https://github.com/NicolasHerin/CoursSymfony/settings
    
