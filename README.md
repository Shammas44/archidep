---
title: "Révision Archidep"
author: [Sébastien Traber, Sandro Picciola, Timothée Dione]
syntax: markdown
date: "29.01.2022"
keywords: [TODO]
tags: [TODO]
---

# Sujets à traiter

[Les objectifs du test](https://github.com/MediaComem/comem-archidep/blob/main/TEST-MATTER.md)
- [x] ligne de commande: __Séb__
- [x] Secure Shell: __Séb__
- [x] Git: __Séb__
- [x] Git branch: __Séb__
- [x] Collaborer avec Git: __Séb__
- [x] OWASP: __Séb__
- [x] Cloud computing: __Séb__
- [x] Linux: __Séb__
- [x] Unix basic administration __Séb__
- [x] Unix processes __Séb__
- [x] Unix networing __(Séb)Tim__
- [x] Twelve Factor App  __Tim__
- [x] Unix environnement variables __Tim__
- [x] Linux process management: __San__
- [x] DNS: __San__
- [x] Reverse Proxying: __San__
- [x] TLS/SSL certificats: __(San)Tim__
- [x] Shell scripting __Tim__
- [x] Git hooks __Tim__
- [x] Heroku __Tim__
- [ ] Diagram d'architecture

# [Ligne de commande](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/cli?home=MediaComem%2Fcomem-archidep%23readme)

## Introduction à la ligne de commande

__CLI (command line interface)__

un outils permettant d'intéragir avec un ordinateur au moyen de commandes textuelles en se passer de la souris.

__Commande__

Une commande est un mot qu'il faut entrer dans un CLI pour indiquer à l'ordinateur quoi faire.

```
nomDelaCommande argument1 argument2 argument3 ...
```

__Option vs argument__

Les options spécifie comment une commande doit se comporter. Par convention elles sont précédés par `-` ou `--` lorsque disponible.

```bash
man -h -v
man --help --version
man -hv
```

__Option avec valeur__

Certaines options requière une valeur. Dans cette exemple `compressed.tar.gz` est la valeur de l'option `-f`

```bash
tar -c -v -f compressed.tar.gz filename
```

## Unix paths

- `.` Répertoire courant
- `..` Répertoire parent du répertoire courant
- `~` Répertoire de l'utilisateur (chemin absolue)
 
## Chemin relatif et absolue

- `/etc/systemd/system/` chemin absolue: chemin complet jusqu'a la ressource
- `Desktop/archidep/` chemin relatif: relatif au répertoire courant
 
## La variable `PATH`

Une variable d'environnement qui stocke l'ensemble des répertoires (chemins absolues) dans lesquels se trouvent les commandes linux. Les fichiers exécutables dans ses dossiers peuvent être appelés juste au moyen de leurs nom au lieu d'avoir à spécifier leurs chemin relatif ou absolue.

c'est pour ça que on peux appeler la command ls juste en tappant `ls` au lieu de `/bin/ls`

## Les commandes de base `cd`, `ls`, `pwd`

- `cd` **Change directory:** permet de se déplacer dans le système de fichier linux
- `pwd` **print working directory:** affiche le chemin absolue du répertoire courant
- `ls` Affiche le contenu d'un répertoire, par défault le répertoire courant

# [Secure Shell (SSH)](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/ssh?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi SSH et à quoi ça sers

SSH est un protocole de réseau cryptographique permettant d'exploiter des services réseau en toute sécurité sur un réseau non sécurisé.

Ses principales utilisations sont la connexion en ligne de commande à distance et la sécurisation des services réseau tels que Git ou FTP.

## Fonctionnement

__Etape 1__

SSH établit un canal sécurisé en utilisant diverses techniques cryptographiques. Ceci est géré automatiquement par le client et le serveur SSH.

__Etape 2__

L'utilisateur ou le service qui souhaite se connecter au serveur SSH doit s'authentifier pour y accéder, par exemple avec un mot de passe.

__Etape 3__

L'utilisateur ou le service connecté peut faire des choses sur le serveur.

> ⚠️  l'étape 1 et 2 sont deux procesus distinct

__Syntaxe de la commande__

```bash
ssh user@hostname
```

## Authentification par mot de passe

Lorsqu'on se connecte en ssh pour la première fois à un serveur, on reçois un message de ce genre

```
The authenticity of host 'example.com (192.168.50.4)' can't be established.
ECDSA key fingerprint is SHA256:colYVucS/YU0JSK7woiLAf5ChPgJYAR1BWJlET2EwDI=
Are you sure you want to continue connecting (yes/no)?
```

> ⚠️ lorsque SSH nous avertit que l'authenticité de l'hôte ne peut pas être établie la première fois que l'on se connecte à un serveur, il est de notre responsabilité de vérifier que la clé publique du serveur est la bonne avant de répondre oui. Sinon, on s'expose à une attaque __Man-in-the-Middle__. 

__Désaventage de l'authentification par mot de passe__

- Un attaquant peut essayer de __brut force__ votre mot de passe.
- Si une attaque __Man-in-the-Middle__ réussie, l'attaquant peut voler votre mot de passe.
- Si le serveur est compromis, un attaquant peut modifier le serveur SSH pour voler votre mot de passe.

## Authentification par clée privée

Si vous avez une paire de clés privée-publique, vous pouvez donner votre __clé publique__ au serveur. En utilisant votre __clé privée__, votre client SSH peut prouver au serveur SSH que vous êtes le propriétaire de cette clé publique.

__Avantage par rapport à l'authentification par mot de passe__

- Il est pratiquement impossible de forcer brutalement. 
- Votre clé privée ne sera pas compromise par une attaque __man-in-the-middle__ ou si le serveur est compromis, car elle n'est jamais transmise au serveur.

> ⚠️  l'authentification par clé publique est aussi sécurisée que le fichier contenant votre clé privée. Si vous publiez ce fichier n'importe où ou permettez à votre machine locale d'être compromise, l'attaquant pourra se faire passer pour vous sur n'importe quel serveur ou service où vous placez votre clé publique.

# [Git: introduction](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi le control de version ?

Système qui enregistre les modifications apportées à un fichier ou à un ensemble de fichiers au fil du temps afin de pouvoir accéder ultérieurement à des versions spécifique desdits fichiers.

__Que ce que ça permet de faire ?__

- Rétablir des fichiers spécifiques (ou un projet entier) à un état antérieur.
- Comparez les changements dans le temps.
- Voir qui a modifié en dernier quelque chose qui pourrait causer un problème, quand le problème a été introduit.
- Récupérez des fichiers perdus ou malencontreusement modifés
- Collaborez à plusieurs sur un projet.
 
## C'est quoi Git ?

Git est un système de contrôle de version, originellement crée par Linux Torwald, le créateur de Linux

__Des snapshots, pas de changement basé sur des fichiers__

Contrairement à d'autres systèmes de contrôle de version, Git stocke ses données sous forme de __snapshots__ au lieu de modifications basées sur des fichiers.

Étant donné que Git stocke localement toutes les versions de tous les fichiers, la plupart des opérations Git sont presque instantanées et ne nécessitent pas de connexion à un serveur:

__Clé SHA-1__

Tout les object Git sont identifié par une clé __SHA-1__ unique qui ressemble à ça:

```
24b9da6552252987aa493b52f8696cd6d3b00373
```

Étant donné que tout le contenu est __haché__, il est pratiquement impossible que des fichiers soient perdus ou corrompus sans que Git le sache.

## Projet Git

La structure d'un projet Git ressemble à ça:

```
my-project:
  .git:
    HEAD
    config
    hooks
    index
    objects
    ...
  file1.txt
  file2.txt
  dir:
    file3.txt
```
__Un projet Git à trois parties prinicpales__

- le répertoire Git _(Git directory)_
- le dossier de travail _(working directory)_
- l'aire de chargement _(staging area)_ aussi appelé _index_

__Working directory__

Le _Git directory_ est l'endroit où Git stocke toutes les snapshots des différentes versions de vos fichiers. C'est la partie la plus importante de Git, et c'est ce qui est copié lorsque vous clonez un __repository__.

> ⚠️  Ce dossier s'appée `.git` et ne doit jamais être modifié par l'utilisateur

__Working directory aussi appelé working tree__

Contient les fichiers sur lesquels vous travaillez actuellement; c'est-à-dire une version spécifique de votre projet. Ces fichiers sont extraits de la base de données compressée dans le répertoire Git et placés dans le répertoire de votre projet. 

__Staging area aussi appelé index__

Un fichier, généralement contenu dans votre répertoire Git, qui stocke des informations sur ce qui ira dans le prochain commit. 

Avant que les snapshots de fichiers ne soient validés dans le répertoire Git, ils doivent passer par cette zone de chargement.

## Git workflow

1. __Checkout:__  Extraction d'une version spécifique de vos fichiers dans le répertoire de travail.
2. __Modification, ajouts, suppresion__ de fichiers dans le répertoire de travail.
3. __Staging:__  préparations des fichiers, en ajoutant des snapshots d'eux à la zone de chargement.
4. __Commit:__ prend les fichiers tels qu'ils sont dans la zone de staging et stocke ces snapshots de manière permanente dans le répertoire Git.

## Commandes Git

- `git checkout` Changer de branche
- `git add` Ajouter des fichier à la zone de chargement
- `git commit` Enregistrer les changements dans le répertoire Git
- `git init` Crée un repository Git (crée un répertoire `.git` contenant une base de données vide)
- `git log` Affiche l'historique des commits
- `git status` permet de savoir quels fichier est dans quels états

## Ignorer des fichiers

On peut demander à Git de ne pas tracker certains fichiers. Pour ce faire il suffit de crée un fichier nommé `.gitignore` à la racine du repository. Dans ce fichier on peut lister les fichier et répertoires qui doivent être ignoré.

__Exemple du contenu d'un fichier .gitignore__

```
*.log
node_modules
```

> ⚠️  Ne pas oublier d'ajouter ce fichier à la zone de chargement et de faire un commit pour que ce fichier soit pris en compte.

# [Git: branches](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git-branching?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi une branche et pourquoi c'est utile ?

Les branches permettent de divérger de la ligne principal du projet tout en continuant à développer mais, sans intérférer avec la ligne principale du projet.

__Créer chaque fonctionalité sur une branche séparée permets:__

- Chacun peut travailler en étant isolé des changements produits par ses collégues.
- On peut récupérer les changement fais par les autres membres de l'équipe quand on le souhaite.
- L'équipe peut choisir quelle fonctionalité sortir et quand le faire.

__Chaque commit contient:__

- Un __pointer__ vers la snpashot du contenu ajouté
- Nom d'utilisateur et email de l'auteur du commit
- Date de création du commit
- Un __pointer__ vers le commit précédant

__Une branche est simplement un pointer vers un commit__

- La branche prinicpale s'appèle générallement `main` ou `master`
- Le __pointer__ nommé `HEAD` indique la branche courante
- A chaque commit le __pointer__ `HEAD` se déplace automatiquement sur le dernier commit.

## C'est quoi un répository distant ?

Un __remote repository__ est une version du projet hebergé quelque part sur internet ou sur un réseaux. On peut en avoir plusieurs. Colaborer avec d'autres personnes implique de devoir __pousser__ des changement sur le repo remote ou de __tirer__ vers soit des changement effectué sur le repo remote.

## Les commandes principales

- `git clone` Permet de cloner un __remote repository__ sur une machine.
- `git push` permet d'envoyer des commits vers un __remote repository__
- `git pull` permet de récupérer des commits d'un __remote repository__ et de fusionner (_merge_) les changements avec le projet local.

## Pourquoi GitHub peux refuser un push ?

Afin de pouvoir __push__ sur un __remote repository__, le repository local doit être à jour avec le __remote repository__, avant de __push__ des changements, il es nécéssaire de ne pas avoir des commits de retard sur le __remote repository__. Si c'est le cas, il faut __pull__ pour se mettre à jour.

# [Sécurité - OWASP](https://owasp.org/www-project-top-ten/)

L'Open Web Application Security Project® (OWASP) est une fondation à but non lucratif qui travaille à améliorer la sécurité des logiciels. Grâce à des projets de logiciels open source dirigés par la communauté, des dizaines de milliers de membres et des conférences éducatives.

- OWASP tiens à jour une liste des 10 des principaux risques de sécurité dans une application web.
- OWASP mets gratuitement à dispositions des ressources éducatives pour contrer les principales attaques.
 
__Pourquoi il ne faut pas lancer une application web avec root ?__

Car si la moindre faille de sécurité est présente dans l'application et que un hacker arrive à l'exploiter, ce dernier peut prendre contrôle dans l'entiéreté du serveur sans aucunnes restrictions.

# [Cloud computing](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/cloud?home=MediaComem%2Fcomem-archidep%23readme)

## Le modèle client-serveur

Le modèle client-serveur est l'un des principaux modes d'organisation des systèmes informatiques distribués et en réseau aujourd'hui. Dans ce modèle, les serveurs partagent leurs ressources avec des clients, qui demandent le contenu ou les services d'un serveur.

> La communication n'est pas à sens unique. Dans les applications Web modernes, les serveurs peuvent également envoyer des données à leurs clients. 

## Différents type d'hébergement web

### Shared hosting (hébergement partagé)

Plusieurs sites Web (de quelques à quelques centaines) sont placés sur le même serveur et partagent un pool commun de ressources (par exemple, CPU, RAM). 

- __Aventages:__ C'est le modèle le moins cher
- __Désaventage:__ C'est le modèle le moins flexible
 
### Dedicated hosting (hébergement dédié)

Les clients obtiennent un contrôle total sur leur(s) propre(s) serveur(s) physique(s). Ils sont responsables de la sécurité et de la maintenance du ou des serveurs.

- __Aventages:__ plus grande flexibilité, meilleures performences
- __Désaventage:__ le client doit tout gérer 
 
### Virtual hosting (hébergement virtuel)

Grâce à la virtualisation, les ressources des serveurs physiques peuvent être divisées en serveurs virtuels. Les clients bénéficient d'un accès complet à leur propre espace virtuel. 

La virtualisation matérielle fait référence à la création d'une machine virtuelle qui agit comme un véritable ordinateur avec un système d'exploitation.

__Hyperviseur__

Un hyperviseur est installé sur la machine hôte. Il virtualise le CPU, la mémoire, le réseau et le stockage.

__Machine invitée__

Une machine virtuelle, également appelée machine invitée, exécute un autre système d'exploitation isolé de la machine hôte.

__Avantages__

- les applications peuvent s'exécuter chacune dans un environnement isolé et adapté à leurs besoins (système d'exploitation, bibliothèques, etc.).
- De nouveaux serveurs virtuels peuvent être créés en quelques minutes.
- L'utilisation des ressources est maximisée au lieu d'avoir du matériel inactif.

__Désaventage__

- Les machines virtuelles nécessitent un effort de gestion supplémentaire
- Les performances ne sont pas aussi bonnes que les serveurs dédiés

> Pour de nombreux cas d'utilisation, les avantages l'emportent sur les coûts, c'est pourquoi la virtualisation est largement utilisée dans le cloud computing.

## C'est quoi le cloud computing et pourquoi c'est utile ?

Il s'agit simplement d'un pool de ressources informatiques configurables.  Ces ressources peuvent être des serveurs ou une infrastructure pour ces serveurs (par exemple, réseau, stockage) ou des applications s'exécutant sur ces serveurs (par exemple, des applications Web). 

Les ressources de cloud computing peuvent être rapidement provisionnées avec un effort de gestion minimal, ce qui permet de réaliser de grandes économies d'échelle.

__Aventages__

- Les entreprises utilisant le cloud computing peuvent se concentrer sur leur cœur de métier au lieu de consacrer des ressources à l'infrastructure et à la maintenance informatiques.
- Les modèles de paiement à l'utilisation minimisent les coûts initiaux d'infrastructure informatique.
- Ils permettent de s'adapter plus rapidement aux demandes informatiques fluctuantes et imprévisibles.

__Désaventages__

- Les options de personnalisation sont limitées puisque vous n'avez pas un contrôle total sur l'infrastructure.
- La sécurité et la confidentialité peuvent être une préoccupation en fonction des exigences légales d'une entreprise.
 
## C'est quoi le cloud public ?

La plupart des fournisseurs de cloud computing publics tels qu'Amazon, Google et Microsoft possèdent et exploitent l'infrastructure de leur(s) centre(s) de données et fournissent des ressources cloud via Internet.

## Les 3 modèles de cloud computing les plus populaires

### IaaS

Fournit une infrastructure informatique fondamentale comme le __stockage__, __les réseaux__ et les __machines virtuelles__ à partir du ou des centres de données du fournisseur.

- Le client fournit une __image__ du système d'exploitation, par exemple Ubuntu, qui est exécutée sur une machine virtuelle par le fournisseur.
- le client paie par machine virtuelle, généralement toutes les heures.
- Le client ne gère pas l'infrastructure physique mais a un contrôle total sur le système d'exploitation.
- La mise en place de l'environnement d'exécution (bases de données, serveurs web, monitoring, etc.) des applications est à la charge du client.

### PaaS

Les plates-formes PaaS fournissent un environnement d'exécution dans lequel les clients peuvent exécuter leurs applications sans avoir à maintenir l'infrastructure associée.

- Le client fournir l'application. La plate-forme l'exécutera avec les composants supplémentaires nécessaires 
- Le prix est par application, souvent horaire.
 
__Aventages__
 
- Plus rapide car les applications peuvent être déployées avec une configuration minimale, sans la complexité de la configuration de l'environnement d'exécution. 

__Désaventages__

- Moins flexible car le contrôle de l'environnement d'exécution et de sa configuration est limité.
- Tendance à être plus cher à grande échelle.

### SaaS

- SaaS fournit des logiciels à la demande sur Internet.
- Le logiciel est entièrement développé, géré et exécuté par le fournisseur, de sorte que le client n'a rien d'autre à faire que de payer et de l'utiliser. Le prix est souvent par utilisateur et mensuel.

__Désaventage__

Ce modèle offre le moins de flexibilité, car le client n'a aucun contrôle sur le fonctionnement ou le déploiement du logiciel, et un contrôle limité sur sa configuration.

# [Linux](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/linux?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi linux ?

Linux est une famille de systèmes d'exploitation open source construits autour du noyau Linux, un noyau de système d'exploitation publié pour la première fois en 1991 par __Linus Torvalds__.

Il est basé sur __Unix__, un système d'exploitation lancé en 1971 dans les laboratoires Bell d'AT&T aux États-Unis. Comme il s'agissait d'un logiciel propriétaire, Linus Torvalds a décidé de publier son propre noyau open source.

Linux n'est pas qu'un seul système d'exploitation, c'est une famille de systèmes appelés distributions Linux. Par exemple, sur ordinateur ou serveur, le plus populaire est __Ubuntu__.

# [Unix basics & administration](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-admin?home=MediaComem%2Fcomem-archidep%23readme)

## Système de fichier et permissions

__Linux est sensible à la casse__

Lorsque vous utilisez __MacOS__ ou __Windows__, votre système de fichiers est probablement HFS, APFS ou NTFS. Ces systèmes de fichiers sont insensibles à la casse, contrairement à linux qui est sensible à la casse.

__Root directory__

Contrairement à __Windows__ les OS de type linux ont un seul répertoire racine. Le chemin jusqu'à ce répertoire est: `/`

__Multiutilisateur__

Toutes les distributions Linux sont multiutilisateur. Ce qui signifie que plusieurs utilisateur peuvent utiliser le système en même temps. Un utilisateur peut être n'importe qui utilisatn le système, à savoir:

- une personne (Ex. Bob)
- un service (Ex. MySql) 
- __Le SuperUser__ appelé `root` (à tout les droits sur le système)

__Les groupes__

La notion da __groupe__ permet d'allouer des permission spécial à tout les utilisateur d'un groupe. Chaque utilisateur appartient à un groupe principale et éventuellement d'autres sous-groupes.

> Par défault tout les utilisateurs appartiennent à un groupe du même nom que le nom d'utilisateur.

__Consulter les permissions__

Il est possible de consulter les permissions pour l'utilisateur actif dans un répertoire avec la commande `ls -l`

```
$> ls -l
-rw-r--r--  1 bob  bob  17951  3 jan 23:05 TEST-MATTER.md
-rw-r--r--  1 bob  bob  24047 31 jan 13:38 archidep-preparation-examen.md
-rw-r--r--  1 bob  bob    140 31 jan 11:18 archidep.md
```

| Permissions | Fichiers          | Repertoires                     |
|:-----------:|-------------------|---------------------------------|
|     `r`     | Lire le contenu   | Lister le contenu               |
|     `w`     | Modifier          | Créer ou supprimer des fichiers |
|     `x`     | Exécuter          | Traverser le repertoire         |
|     `-`     | Pas de permission | Pas de permission               |

__Catégorie d'utilisateur__

Chacunnes des permissions précédantes sont assigné pour les catégories d'utilisateur suivants:

| Catégorie | Description                          |
|:---------:|--------------------------------------|
|  `owner`  | L'utilisateur qui détient le fichier |
|  `group`  | Le groupe qui détient le fichier     |
|  `other`  | N'importe quel autre utilisateur     |

__La commande sudo__

La commande `sudo` (qui signifie __superuser do__) offre une autre approche pour donner aux utilisateurs un accès administratif.

Lorsque des utilisateurs de confiance précèdent une commande administrative avec `sudo`, ils sont invités à saisir leur propre mot de passe. Une fois authentifiée, la commande d'administration est exécutée comme par l'utilisateur __root__.

> ⚠️  Seuls les utilisateurs de confiance peuvent utiliser `sudo`. Toutes utilisation non autorisée de `sudo` sera consignée. 

__/etc/sudoers__

le fichier `/etc/sudoers` définis quels utilisateurs ont le droits d'utiliser la commande `sudo`. ⚠️  Ne jamais éditer ce fichier à la main pour éviter des problèmes.

__Manager les permissions__

Les commandes suivantes permettent de changer les permissions pour un ou plusierus fichiers.

| Commande | But                                               |
|----------|---------------------------------------------------|
| `chmod`  | Change les permissions (r,w,x)                    |
| `chown`  | Change le propriétaire + éventuellement le groupe |


## [Unix processes](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-processes?home=MediaComem%2Fcomem-archidep%23readme)

__C'est quoi un processus__

Un processus est une instance d'un programme informatique en cours d'exécution.  Chaque fois que vous exécutez un fichier exécutable ou une application, un processus est créé.

Les programmes simples ne nécessitent qu'un seul processus. Des applications plus complexes peuvent lancer d'autres processus enfants pour de meilleures performances. 

__Process ID__

Un nombre unique permettant d'identifier un processus à un temps donnée

__Lister les processus en cours d'éxécution__

Cette opération est possible grâce à la commande `ps` (process list)

__Exit status__

L'état de sortie d'un processus est un petit nombre (généralement compris entre 0 et 255) passé d'un processus enfant à son processus parent lorsqu'il a fini de s'exécuter.

- Il est destiné à permettre au processus enfant d'indiquer comment ou pourquoi il s'est arrêté.
- Il est courant que l'état de sortie des programmes Unix/Linux soit `0` pour indiquer le succès, et `supérieur à 0` pour indiquer une erreur.

> ⚠️  la signification d'un code d'erreur est propre au programme.

__Pipeline__

Un pipeline représenté par `|` permet de chaîner des commandes les unes avec les autres. L'utilisation d'un pipeline consiste à envoyer le résultat d'une première commande comme argument à un seconde commande. Ce procédé peut être répété indéfiniment. 

Par exemple on peut compter le nombre de mots dans un text de la manière suivante: `cat nomDuFichier.txt | wc -w`

Parce que les programmes Unix peuvent être facilement enchaînés, ils ont tendance à être plus simples et plus petits. Des tâches complexes peuvent être réalisées en enchaînant de nombreux petits programmes.

> Bien que de nombreux programmes gèrent des __flux de texte__ (text stream), d'autres gèrent également les __flux binaires__ (binary stream). Par exemple, la bibliothèque _ImageMagick_ peut traiter des images.

### C'est quoi un signal Unix ?

Un signal est une notification asynchrone envoyée à un processus pour l'informer qu'un événement s'est produit.

Si le processus a enregistré un gestionnaire de signal (signal handler) pour ce signal spécifique, il est exécuté. Sinon, le gestionnaire de signal par défaut est exécuté. 

__La commande kill__

La commande `kill` envoie un signal à un processus. Étant donné que le gestionnaire de signaux par défaut pour la plupart des signaux consiste à terminer le processus, il a souvent cet effet, d'où le nom `kill`

# [Unix networking](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-networking?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi HTTP, TCP et comment ils sont reliés ?

Il s'agit de protocoles de communication. Ils sont interreliés dans la mesure où ils constituent le protocole internet, avec HTTP au niveau application et TCP au niveau transport.

Une communication http passe habituellement par l'établissement d'une connection tcp au port 80.

## C'est quoi une adresse IP, un port et comment ils sont relié à TCP ?

Une adresse IP est une suite unique de deux fois 16 bits, propre à chaque machine, qui permet aux routeurs de transmettre l'information. Les 16 premiers identifient le réseaux, et les 16 suivants la machine au sein du réseaux. 

Un port est un endpoint of communication. Il permet notamment de spécifier le protocol de communication utilisé. Pour tcp, c'est le port 80 qui est utilisé. 

## C'est quoi le `hostname` `localhost` et l'adresse IP `127.0.0.1`

Il s'agit d'une adresse "fictive" qui pointe vers la machine qui efectue la requête. Il s'agit donc de contacter son propre ordinateur dans le cas d'une requeête effectuée en localhost sur sa machine.

## Les ports standart HTTP(S)

- __HTTP__: 80
- __HTTPS__: 443

## Les ports systèmes connus

Il s'agit des ports 0 à 1023, qui sont utilisés par les processus systèmes pour fournir des services très répendus comme SSH par exemple. 

Sur un systpme Unix, ils doivent être utilisés avec un utilisateur qui dispose des super privilèges.

## C'est quoi Domain Name Système (DNS) ?

Il s'agit d'un système de nommage qui transforme des adresses binaires en adresses lisibles par les humains, du type Google.com <-> 0.0.126.12 

# [Twelve-factor app](https://12factor.net/)

## Pourquoi C'est une bonne pratique de stocker des configurations dans l'environnement ?

Si un hacker parvient à récupérer le fichier qui contient le mot de passe, il sera potentiellement en mesure de faire des modifications non souhaitables sur une BDD, un fichier ou encore même le serveur. Les stocker en tant que variable d'environnement protège le système, même si les fichiers sont obtenus.

# [Unix environment variables](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-env-vars?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi un variable d'environnement et à quoi ça sers ?

Les vaiables d'envrionement permettent de modifier le comportement des programmes sans les modifier directement. Elles peuvent par exemple servir à sécuriser l'accès à une base de données.
Elles sont exclusivement des chaînes de caractères, et peuvent être accessibles sur le shell avec la commande env, ou depuis un programme avec des commandes variables selon le langage.

- __La variable HOME__ permet de stocker le chemin de l'utilisateur qui lance le processus.
- __La variable TMP__ permet d'indiquer dans quel directory stocker les fichier temporairement.
- __La variable LANG__ permet de définir la "default locale".


# [Linux process management](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/linux-process-management?home=MediaComem%2Fcomem-archidep%23readme)

## Ce qu'est un gestionnaire de processus et que les systèmes d'exploitation en intègrent généralement un

Réponse: Les gestionnaires de processus sont des programmes qui remplissent ce rôle : ils s'assurent que les bons processus sont exécutés dans le bon ordre et sont ensuite gérés correctement.Les processus doivent également être gérés, c'est-à-dire qu'il doit être facile de les démarrer, de les arrêter, de les redémarrer ou de les configurer pour qu'ils redémarrent automatiquement en cas de panne. Dans notre cas, nous avons utiliser SystemD.

## Que Systemd est l'outil standard de gestion des processus sur de nombreux systèmes Linux comme Ubuntu

Systemd fournit non seulement la gestion des processus, mais aussi les blocs de construction fondamentaux d'un système d'exploitation Linux, comme un système init. Systemd enregistre les instructions sur la façon de lancer et de gérer un processus dans un fichier de configuration appelé fichier unité. Il prend en charge de nombreux types de fichiers unitaires tels que service, socket, timer, etc.

## Que Systemd utilise des fichiers unitaires pour configurer la gestion des processus

- `[Unité]` est une section du fichier de configuration. Il y aura d'autres sections en fonction du type de fichier d'unité.
- `[Install]` est une section facultative qui peut être utilisée pour exprimer les dépendances entre les unités. Ici, l'option WantedBy spécifie que cette unité sera lancée après que l'unité quelque chose d'autre ait été lancée.

Les fichiers unitaires qui nous intéressent sont les services, qui vont configurer, lancer et gérer un processus à long terme tel qu'une base de données ou une application.

- `ExecStart`: Commande à exécuter pour démarrer le service
WorkingDirectory: Répertoire dans lequel exécuter la commande
- `User`: Utilisateur sous lequel exécuter le processus (peut être utilisé pour limiter l'accès)

## Que vous pouvez utiliser Systemd pour contrôler les processus (les démarrer, les arrêter, les redémarrer, etc.)

- `sudo systemctl status <unit>` Affiche l'état actuel d'une unité.
- `sudo systemctl start <unit>` Démarrer une unité.
- `sudo systemctl stop <unit>`Arrête une unité.
- `sudo systemctl restart <unit>`Redémarrer une unité.
- `sudo systemctl daemon-reload`Recharge les fichiers de l'unité après qu'ils aient été modifiés.

# [Domain Name System (DNS)](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/dns?home=MediaComem%2Fcomem-archidep%23readme)

## Ce qu'est le système de noms de domaine (DNS)

Le système de noms de domaine (DNS) est un     système de dénomination hiérarchique décentralisé pour les ordinateurs connectés à l'Internet ou à un réseau privé. Il traduit notamment les noms de domaine lisibles par l'homme (comme google.com) en adresses IP numériques (comme 40.127.1.70) nécessaires pour localiser les ordinateurs avec les protocoles réseau sous-jacents.
    
## Ce qu'est une zone DNS et un fichier de zone DNS

Zone DNS: Une zone DNS est un sous-ensemble de l'espace des noms de domaine pour lequel la responsabilité administrative a été déléguée à un seul gestionnaire.

Par exemple, Microsoft a acheté les droits de gestion du domaine microsoft.com et de tous ses sous-domaines auprès du gestionnaire du domaine de premier niveau (TLD) .com. Une fois qu'elle dispose de ces droits, elle peut créer un nombre illimité de sous-domaines pour ses besoins commerciaux.

Zone DNS File: A DNS zone file is a text file that describes a DNS zone. It contains mappings between domain name and IP addresses and other resources, in the form of resource records.

# [Reverse proxying](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/reverse-proxy?home=MediaComem%2Fcomem-archidep%23readme)

## Qu'est-ce que Reverse proxy ?

Réponses: Un serveur proxy est un ordinateur ou une application qui sert d'intermédiaire pour les demandes des clients qui cherchent des ressources auprès d'autres serveurs. Il retourne les informations contenues dans un autre serveur que lui à l'utilisateur.

## Les principales utilisations d'un reverse proxy (masquage de l'architecture interne ou des sites web à plusieurs composants, terminaison SSL et équilibrage de charge)

Les reverse proxies peuvent cacher l'existence et les caractéristiques des serveurs privés d'un réseau interne. Comme le client ne voit que le serveur proxy, il n'est pas conscient de la complexité de l'architecture interne et n'a pas à s'en préoccuper.

Les sites Web modernes peuvent être des applications complexes, souvent dotées d'un front-end et d'un back-end distincts, développés par des équipes différentes avec des technologies différentes. L'utilisation d'un proxy inverse permet de faire apparaître le site comme un seul site Web sur un seul nom de domaine, évitant ainsi les problèmes de CORS.
    
La gestion des certificats SSL pour fournir des sites Web en HTTPS est assez complexe. Il peut être difficile de configurer certains frameworks ou outils pour s'assurer qu'ils utilisent uniquement des communications sécurisées.

L'évolutivité est la capacité d'un système informatique à gérer une quantité croissante de travail, par exemple lorsque de nombreux clients adressent des demandes à une application en même temps.

## Que nginx est un serveur web et un reverse proxy
    
Nginx est un serveur HTTP et reverse proxy utilisé par plus de 25 % des sites les plus fréquentés en décembre 2018. Il a été développé pour résoudre le problème C10k, c'est-à-dire la capacité d'un système informatique à gérer dix mille connexions simultanées, grâce à son architecture orientée événements. Il dispose également de nombreuses autres fonctionnalités pour servir les applications web modernes.


# [TLS/SSL certificates](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/ssl?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi un certificats TLS et à quoi ça sers ?

Il s'agit d'un type de certificat de clé publique qui permet de garantir qu'un ordinateur (comme un serveur web) possède sa propre clé publique.

Il permet au serveur de communiquer en https une fois validé.

## Pourquoi un certificat TLS est considéré valid ou non ?

Pour être valide, un TLS doit être signé par une authorité reconnue. Sinon, il peut être autosigné, et généré rapidement par n'importe qui.

## C'est quoi un certificats TLS autosigné ?

Il s'agit d'un certificat qui n'a été signé que par son auteur, et aucune autorité recconnue.

## C'est quoi une chaîne de confiance dans le context de TLS ?

A root certificate signs an intermediate certificate with owner's public key and name, and root's name.
This certificate signs an end certificate, generated by an authority, which represents the intermediate certificate and contains the authority's public key 

## C'est quoi un certificats TLS root ?

Cela correspond à un certificat correspondant à l'utilisateur root de la machine qui a généré le certificat.

### C'est quoi un certificats root de confiance ?

Il s'agit d'un root certificate vérifié, non seulement par le certificat intermédiaire, mais aussi par une autorité de certification. 

## C'est quoi la validation de domain (domain validation) ?

Il s'agit de la procédure par laquelle un administrateur demandant un TLS certificate prouve qu'il est bien en possession du domaine concerné.

### Au moins une méthode de validation de domain 

__E-mail validation__: l'autorité de certification envoit un mail à une adresse à laquelle seule l'administrateur peut accéder. Le mail contient un lien, qui une fois suivit, prouve que c'est un administrateur légitime qui a fait la demande.

## C'est quoi `Let's Encrypt` et `Certbot` ?

Let's enscrypt est une autorité de certification gratuite et automatisée.
Certbot est un outil disponible sur Linux qui permet d'aider à obtenir un certificat, configurer le web server et renouveller la demande.

# [Shell scripting](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/shell-scripting?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi un shell script ?

Un fichier qui contient du code qui est interprété dynamiquement. Ils permettent d'automatiser certaines opérations.

## C'est quoi un shebang ?

Il s'agit d'une commande, située à la première ligne d'un script shell, qui respecte la notation:
#!interpreter optional-args 
L'interpreter est habituellement bin/bash.

Elle permet donc d'indiquer quel interpréteur est utilisé par la machine pour exécuter le code du script.

# [Git hooks](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git-hooks?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi un Git hook ?

Il s'agit d'un fichier éxécutable.
Ils contiennent des instructions, qui peuvent s'enclancher selon des conditions spécifiques.
Ils peuvent servir à automatiser des déploiements ou exécuter des tâches répétitives.

Il existe les types de hooks suivants:
post-recieve, post-commit, pre-commit, pre-recieve

# [Heroku](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/heroku?home=MediaComem%2Fcomem-archidep%23readme)

## C'est quoi Heroku et comment ça fonctionne ?

Il s'agit d'une plateforme as a service. Ils permettent de faciliter le déploiement d'applications web. Heroku réduit la complexité en manageant l'environement, mettant à jour les langages de programmation et les systèmes. Par exemple, ils permettent de connecter une base de données POSTGRES à une application sans avoir à télécharger et mettre à jour POSTGRES.

Heroku fonctionne parallèllement à Git: On clone un repo existant et fonctionnel sur notre machine sur l'une des leurs. À l'aide de hooks, ils configurent automatiquement les dépendances, lancent les processus appropriés et font tourner l'app avec un minimum de travail nécessaire. Ils s'occuppent en parallèle de maintenir à jour les technologies installées sur les serveurs qu'ils mettent à disposition.

## Configurer des variables d'environnement pour une applicaton Heroku

Il est possible de configurer des variables d'environnement pour une app Heroku.
À titre d'exemple, nodeJs permet de configurer des variables d'environnement comme suit:

```bash
node
process.env
{
  SHELL: '/bin/bash',
  USER: 'foo',
  PATH: '/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin',
  PWD: '/path/to/current/working/directory',
  LANG: 'en_US.utf-8',
  HOME: '/path/to/home' 
}
process.env.PATH
```

# Déssiner un diagram simple

Dessiner un schéma d'architecture simple représentant les principaux processus impliqués dans les déploiements effectués pendant le cours, et comment ils communiquent ou s'influencent les uns les autres.

__Un tel schéma doit contenir:__

- Les processus directement liés à l'exécution et à l'exposition de l'application ou du site Web déployé (par exemple, l'application, le proxy inverse).
- Processus qui gèrent d'autres processus (par exemple systemd).
- Communication entre processus (par exemple, l'application accède à la base de données) et communication entre processus et le monde extérieur (par exemple, un navigateur fait une requête sur un port qui est géré par un processus spécifique).

## Quelques Exemples

## [Deploy a PHP application with Git](https://github.com/MediaComem/comem-archidep/blob/main/ex/git-clone-deployment.md#architecture)

![image alt](https://terredesdinos.ch/wp-content/uploads/2022/02/sftp-deployment-simplified.png)

## [Domain Name Configuration](https://github.com/MediaComem/comem-archidep/blob/main/ex/dns-configuration.md)

![image alt](https://terredesdinos.ch/wp-content/uploads/2022/02/dns-configuration-simplified.png)

## [Deploy a static site with nginx](https://github.com/MediaComem/comem-archidep/blob/main/ex/nginx-static-deployment.md#architecture)

![image alt](https://terredesdinos.ch/wp-content/uploads/2022/02/nginx-static-deployment-simplified.png)

## [Provision an SSL certificate using Certbot by Let's Encrypt](https://github.com/MediaComem/comem-archidep/blob/main/ex/certbot-deployment.md#architecture)

![image alt](https://terredesdinos.ch/wp-content/uploads/2022/02/certbot-deployment-simplified.png)

## [Deploy Minesweeper, a Phoenix (Elixir) & Alpine.js application with a PostgreSQL database](https://github.com/MediaComem/comem-archidep/blob/main/ex/minesweeper-deployment.md#books-architecture)

![image alt](https://terredesdinos.ch/wp-content/uploads/2022/02/minesweeper-deployment-simplified.png)
