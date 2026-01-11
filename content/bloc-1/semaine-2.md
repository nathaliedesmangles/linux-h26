+++
pre = 'Semaine 2 : '
title = 'Arborescence et navigation'
weight = 20
+++



## Objectif de la semaine

* Connaitre et comprendre la structure des fichiers sous Linux
* Se déplacer dans le système et manipuler des fichiers sans souris. 

> [!warning]

> C'est le cours le plus important pour arriver à s'orienter dans l'architecture de Linux.


**Fichier pour les exercices (en classe)**

Utiliser le fichier **exo-semaine2.docx** pour y mettre vos réponses et captures d'écran.  
{{% button href="/docs/Exercices/exo-semaine2.docx" icon="download" %}}Télécharger le fichier docx{{% /button %}}


---


# Théorie


## Windows vs Linux

Sous Windows, vous avez des lecteurs physiques : `C:\` (Disque système), `D:\` (USB), `Z:\` (Réseau).
Sous Linux, **tout est un fichier** et tout commence au même endroit .

![Arborescence](../arborescence.png?width=50vw)

* **La Racine (`/`) :** C'est le point de départ unique. Il n'y a pas de "C:". Tout ce qui est branché à l'ordinateur (disque dur, clé USB, DVD) apparaît comme un dossier quelque part sous la racine.
* **La distinction majuscule/minuscule (Case Sensitivity) :**
* Windows : `Dossier` = `dossier`.
* Linux : `Dossier`, `dossier` et `DOSSIER` sont trois dossiers différents.


## Les incontournables du système de fichiers

Pas besoin de tout connaître, mais vous devez reconnaître ceux-ci :

* `/` (Slash) : La Racine (The Root). Le début de tout.
* `/home` : Vos documents. C'est l'équivalent de `C:\Users`. C'est le *seul* endroit où vous avez le droit d'écrire par défaut.
* `/root` : Le dossier personnel de l'administrateur suprême. (Ne pas confondre avec `/`).
* `/etc` : **Etc**etera. Contient les fichiers de configuration système.
* `/bin` & `/usr/bin` : **Bin**aries. Contient les programmes (les commandes comme `ls`, `cp`).
* `/var` : **Var**iable. Ce qui change souvent (Logs, site web, bases de données).


## Chemins absolus vs relatifs


> [!warning]

> C'est la cause #1 des erreurs au début **ET AUSSI** aussi dans les cours de programmation.


* **Chemin absolu (L'adresse postale complète) :**
   * Commence **toujours** par `/`.
   * Fonctionne peu importe où vous êtes.
   * *Ex:* `/home/etudiant/Documents/devoir.txt`

* **Chemin relatif (Les indications locales) :**
   * Ne commence **jamais** par `/`.
   * Dépend de votre position actuelle.
   * *Ex:* Si je suis déjà dans `/home/etudiant`, je tape juste `Documents/devoir.txt`.

* **Les raccourcis magiques :**
   * `.` (Un point) = Ici (Dossier courant).
   * `..` (Deux points) = Le dossier parent (Remonter d'un cran).
   * `~` (Tilde) = Ma maison (`/home/etudiant`).



## L'anatomie d'un prompt typique

`etudiant@linux-mint:~/Documents$`

1.  `etudiant` : **QUI** je suis ? (Mon identité).
2.  `@linux-mint` : **OÙ** je suis ? (Sur quelle machine ? Important quand on fera du SSH).
3.  `~/Documents` : **DANS QUEL DOSSIER** je suis ? (Mon emplacement).
4.  `$` : **QUEL POUVOIR** j'ai ?
    * `$` = Utilisateur normal (Pistolet à eau).
    * `#` = Root / Superutilisateur (Bazooka). <span style="color:red;"><b>Si vous voyez ça, faites gaffe</b></span>.



## La syntaxe d'une commande

Une commande suit presque toujours cette logique :  
   ```
   COMMANDE + OPTIONS + CIBLE
   ```

Exemple : `ls -l /etc`
* **Quoi faire ?** `ls` (Lister).
* **Comment ?** `-l` (Format long/détails).
* **Où ?** `/etc` (Dans le dossier de config).


### 🟢 Exercice 1 (en classe)


*À réaliser individuellement. Vous devez trouver les réponses en explorant.*

1. Allez dans le dossier `/etc`. Combien y a-t-il de fichiers (approximativement) ? (`ls` est votre ami).
2. Trouvez le fichier nommé `passwd` dans `/etc`. Copiez-le dans votre dossier personnel (`~`).
3. Renommez votre copie `utilisateurs_backup.txt`.
4. Créez un dossier `Confidentiel` dans votre home.
5. Déplacez `utilisateurs_backup.txt` à l'intérieur de `Confidentiel`.
6. Revenez à votre point de départ (`~`) et supprimez le dossier `Confidentiel` et son contenu en une seule commande.


## Aide intégrée

**Commandes** : `man`, `apropos`, `history`

| Besoin | Commande | Explication |
|--------|----------|-------------|
| Lire la documentation | `man commande` | Manuel officiel |
| Quitter | `q` | Très important |
| Chercher une commande | `apropos mot` | Recherche par mot-clé |
| Voir l’historique | `history` | Toutes les commandes récentes |


**Commande `man`**

* La commande `man` affiche les pages de manuel des commandes.
* On l'utilise pour comprendre comment une commande fonctionne grâce à son **manuel**.

```bash
man ls
man cp
man chmod
```

Les sections importantes :

| Section     | Ce qu’elle contient                                |
| ----------- | -------------------------------------------------- |
| **NAME**        | Nom + courte description                           |
| **SYNOPSIS**    | Format général de la commande (arguments, options) |
| **DESCRIPTION** | Détails sur le fonctionnement                      |
| **OPTIONS**     | Toutes les options disponibles                     |
| **EXAMPLES**    | Exemples (si la page en contient)                  |


**Commande `apropos`**

* On l'utilise quand on **ne connaît pas** la commande mais qu’on connaît l’action souhaitée. 
* Elle permet de trouver la bonne commande quand on **ne la connaît pas**.
* Elle renvoie une liste de commandes dont la description contient le mot recherché.

```bash
apropos directory
apropos remove
apropos copy
```

### 🟢 Exercice 2 (en classe)

1. Quelle est la différence entre `man` et `apropos` ?
2. Que représente la section **SYNOPSIS** dans une page `man` ?
3. Comment chercher une chaîne de texte **à l’intérieur d’un manuel** ?
   *(indice : `/texte`)*
4. Quelle touche du clavier permet de **quitter** le manuel ?
5. Quel symbole indique qu’un argument est **optionnel** dans le SYNOPSIS ?
   *(réponse : `[ ]`)*


## 💡 Astuces de la semaine


> **L'autocomplétion (Tab)**
> Ne tapez jamais les noms de fichiers en entier !
> Tapez les 3 premières lettres (ex: `cd Doc`) et appuyez sur la touche **TAB**.
> Linux finira le mot pour vous (`cd Documents/`).
> *Si ça ne marche pas, appuyez 2 fois sur TAB : Linux vous montrera les choix possibles.*

> **Historique (Flèches)**
> Vous avez fait une faute de frappe dans une longue commande ?
> Appuyez sur la **Flèche du Haut** pour rappeler la dernière commande et corrigez-la.


---

# LABORATOIRE

## Objectif

* Développer la "mémoire musculaire" des commandes de base.

Utiliser le fichier **labo2.docx** pour y mettre vos réponses et captures d'écran.  
{{% button href="/docs/Labos/labo2.docx" icon="download" %}}Télécharger le fichier docx{{% /button %}}

### Exercice #1 : Trouver la bonne commande

À l’aide de **`apropos`**, trouve une commande qui permet :

1. D’afficher l’heure.
2. De changer les permissions.
3. D’arrêter le système.
4. De rechercher du texte dans un fichier.
5. De compter les lignes d’un fichier.

> **Écris la commande trouvée + sa courte description.**


### Exercice #2 : Lire un manuel

Avec **`man`**, trouve dans la commande :

1. Dans `man ls` :

   * Quelle option permet **d’afficher les fichiers cachés** ?
   * Quelle option donne un **listing détaillé** ?
2. Dans `man cp` :

   * Quelle est la syntaxe (ligne complète du SYNOPSIS) ?
   * Quelle option permet de demander une **confirmation avant d’écraser** un fichier ?
3. Dans `man rm` :

   * Quelle option permet une suppression **interactive** ?
   * Quelle option force la suppression sans confirmation ?

4. Dans `man mkdir` :

   * Le SYNOPSIS indique `mkdir [OPTION]... DIRECTORY...`.
   	* Que signifie `...` ?
   	* Peut-on créer plusieurs répertoires à la fois ?
   * Trouve comment créer un répertoire **avec ses sous-répertoires automatiquement** (option recursive).

Avec **uniquement** **`apropos`**, trouve dans la commande qui permet de trouver :

   * L’espace disque libre.
   * L’utilisation du CPU.
   * L'informations sur les partitions.

> Puis utilise `man` pour trouver **une option utile** pour chacune des commandes trouvées.



### Exercice #3 : Exploration et manipulation

#### Étape 0 : Ouvrir le Terminal (10 min)

* Raccourci clavier (souvent `Ctrl+Alt+T`) ou via le menu.
* Analyser le prompt : `etudiant@station-linux:~$`
* Qui ? `etudiant`
* Où ? `~` (Dans mon home).


#### Étape 1 : Exploration (30 min)

**Commandes** : `pwd`, `ls`, `cd`

1. **Où suis-je ?** Tapez `pwd` (Print Working Directory). Confirmez que vous êtes dans `/home/etudiant`.
2. **Qu'est-ce qu'il y a ici ?** Tapez `ls`.
3. **Voir l'invisible :** Tapez `ls -a`. Remarquez les fichiers commençant par un point (ex: `.bashrc`). Ce sont les fichiers cachés.
4. **Aller ailleurs :**
	* Allez à la racine : `cd /`
	* Vérifiez avec `pwd`.
	* Listez le contenu : `ls`. Voyez-vous les dossiers `bin`, `etc`, `home` ?
5. **Le ping-pong :**
	* Revenez chez vous avec le raccourci rapide : `cd` (sans argument) ou `cd ~`.
	* Remontez d'un niveau : `cd ..` (Vous êtes maintenant dans `/home`).


#### Étape 2 : Manipulation (45 min)

**Commandes** : `mkdir`, `touch`, `cp`, `mv`, `rm*`

1. **Créer une structure :**
	* Créez un dossier `Labo2` : `mkdir Labo2`
	* Entrez dedans : `cd Labo2`
	* Créez une structure complexe en une ligne : `mkdir -p Projet/Images/Icones`


2. **Créer des fichiers :**
	* Créez un fichier vide : `touch mon_fichier.txt`


3. **Copier (`cp`) :**
	* Copiez le fichier dans le dossier Projet : `cp mon_fichier.txt Projet/`
	* Vérifiez : `ls Projet/`


4. **Déplacer et Renommer (`mv`) :**
	* *Note : Linux n'a pas de commande "renommer". On "déplace" un fichier vers un nouveau nom.*
	* Renommez le fichier original : `mv mon_fichier.txt fichier_final.txt`
	* Déplacez-le dans Images : `mv fichier_final.txt Projet/Images/`


5. **Supprimer (`rm`) - ATTENTION :**
	* Essayez de supprimer le dossier Projet : `rm Projet` -> *Erreur ! C'est un dossier.*
	* Supprimez le dossier et tout son contenu : `rm -r Projet` (Recursive).
	* *Rappel : Il n'y a pas de corbeille en ligne de commande. C'est définitif.*

---


## Corrigé du laboratoire

> À venir (samedi ou dimanche)



<!--

=======================================================
## Exercice 1

1. `date` — print or set the system date and time
2. `chmod` — change file mode bits
3. `shutdown` — bring the system down
4. `grep` — print lines matching a pattern
5. `wc` — print newline, word, and byte counts

---

## Exercice 2

**1 — ls**

* Fichiers cachés : `-a`
* Listing détaillé : `-l`

**2 — cp**

* SYNOPSIS : `cp [OPTION]... SOURCE... DIRECTORY`
* Confirmation : `-i`

**3 — rm**

* Suppression interactive : `-i`
* Suppression forcée : `-f`

---

## Exercice 3

* Répertoire courant : `pwd`
* Créer un répertoire : `mkdir`
* Compresser un fichier : `gzip` / `zip`
* Décompresser `.gz` : `gunzip`
* Comparer deux fichiers texte : `diff`

---

## Exercice 4

1. `...` signifie **répétable plusieurs fois** → oui, on peut créer plusieurs dossiers.
2. Option recursive : `mkdir -p a/b/c`


### Exercice 2 : L'architecte (Création)

* **Concept clé :** L'option `-p` (Parents).
* Demandez-leur de créer `mkdir projet/site/images`.
    * *Erreur attendue :* "No such file or directory". (Car `projet` n'existe pas encore).
    * *Solution :* `mkdir -p projet/site/images`. Le `-p` force la création de tous les dossiers intermédiaires. C'est magique.
* Vérifiez votre travail avec la commande `tree` (s'ils l'ont) ou `ls -R`.


### Exercice 3 : Le piège du "Dossier Parent"

* Allez dans `/var/log`.
* Essayez de remonter dans `/var`.
    * Commande : `cd ..`
* Essayez de remonter à la racine `/`.
    * Commande : `cd ..`
* Essayez de remonter plus haut que la racine.
    * Commande : `cd ..`
    * *Observation :* On reste à la racine. On ne peut pas monter plus haut que le toit.
---


### Exercice 1 : La chasse au trésor (Navigation)

* Ouvrez le terminal.
* **Défi 1 :** Qui êtes-vous ? Où êtes-vous ? (Utilisez `pwd`).
* **Défi 2 :** Allez voir ce qu'il y a dans le dossier de configuration système.
    * `cd /etc`
    * `ls` (Regardez la quantité de fichiers ! C'est impressionnant).
* **Défi 3 :** Essayez de rentrer dans le dossier du chef.
    * `cd /root` -> **BOOM** : "Permission denied". (C'est normal, expliquez pourquoi).
* **Défi 4 :** Rentrez à la maison en 2 touches maximum.
    * Solution : `cd` (tout seul) ou `cd ~`.



### Le "Boss Fight" (Défi de fin de cours)

Écrivez ceci au tableau. Le premier qui réussit peut partir 5 minutes avant.
1.  Allez dans votre dossier `Documents`.
2.  Créez un dossier `Secret`.
3.  Entrez dedans.
4.  Affichez le chemin complet (GPS) pour prouver que vous y êtes.
5.  Revenez à la racine `/` en une seule commande.

-->

