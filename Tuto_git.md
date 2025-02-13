# Tuto Git en local

## Présentation

- logiciel open source de gestion de versions
- cibles : développeurs, DevOps, etc.
- gestion des versions : compliqué...
surtout si on travaille à plusieurs !
- Windows, macOS Linux
1. Utiliser Git en local
2. Sur le réseau avec des services comme GitHub ou GitLab.

La suite concerne l'environnement machine Windows mais le fonctionnement est le même sur Linux ou macOS.

## Quelques définitions

1. ** Repository **

Dépôt : espace de stockage poour vos fichiers. Un dépôt peut être local ou distant (GitHub, GitLab, etc.).
1. **Master / Main**
Branche principale du projet qui correspond toujours à la dernière version.
1. **Branch**
Des branches peuvent s'ajouter à la branche "Master".
Pour travailler sur une nouvelle fonctionnalité, la correction d'un bug on peut créer de nouvelles branches. 
=> Permet d'avoir plusieurs versions des fichiers.
1. **Merge**
Action que l'on utilise pour fusionner une branche annexe avec la branche principale "Master" pour intégrer les modifications à la version principale.
1. **Commit**
Quand on travaille sur un fichier d'un dépôt Git, il faut synchroniser les modifications vers le dépôt : l'action "commit" permet de valider les modifications.
1. **Push**
Action poour envoyer les fichiers modifiés sur le serveur.
1. **Pull**
Action pour télécharger des fichiers à partir du dépôt distant sur notre machine en local.
1. **Clone**
Action de copier un projet situé sur un dépôt distant en local.
Utile pour télécharger un projet complet en vue de son installation.


## Installation de Git sous Windows

## Premiers pas avec Git

### Configurer votre profil utilisateur

```sh
git config --global user.name "Patrick FELIX"
git config --global user.email "felix@domaine.fr"
```
Afficher la configuration globale et vérifier vos noms et email :
```sh
git config --global --list
```

### Initialiser un nouveau projet Git

Depuis la racine de votre projet :
```sh
git init
```

Consulter le nouveau dossier créé ".git" (masqué) à la racine de notre projet : ce répertoire contient différents fichiers pour la gestion de version de votre projet (informations sur les branches, les modifications des fichiers du projet, etc.)

Une commande qui vous sera utile régulièrement :

```sh
git status
```

### Ajouter un fichier à notre projet Git

Ajouter un fichier à la racine du projet et relancer la commande `git status` : un message `Untracked files` signifie que votre fichier n'est pas encore suivi.

La commande `git add` ajoutera un fichier dans Git :
```sh
git add MonFichier.md
```

Pour ajouter tous les fichiers présents dans votre dossier :

```sh
git add .
```

### Effectuer l'action de commit
Réaliser un commit effectue un snapshot de votre code : il sera toujours possible de revenir en arrière et restaurer votre fichier dans l'état qu'il était au moment du commit.

L'option "-m" permet d'ajouter un commentaire.

```sh
git commit -m "Premier commit"
```

Pour visualiser un historique des commits :
```sh
git log
```

Pour visualiser les logs sur une branche :
```sh
git log --oneline master
```

### Basculer d'une branche à une autre

Pour créer une nouvelle branche "dev" :
```sh
git branch dev
```

Pour basculer d'une branche à une autre :
```sh
git switch dev
```

# Tuto Git en distant
