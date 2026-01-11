+++
pre = 'Semaine 9 : '
title = 'Redirections, Pipes et filtres'
weight = 90
+++


## Objectif de la semaine

* Comprendre comment manipuler les flux de données pour combiner des commandes simples et réaliser des tâches complexes.

**Fichier pour les exercices (en classe)**
Utiliser le fichier **exo-semaine9.docx** pour y mettre vos réponses et captures d'écran.  
{{% button href="/docs/Exercices/exo-semaine9.docx" icon="download" %}}Télécharger le fichier docx{{% /button %}}

---

## Théorie

Imaginez qu'une commande Linux est une **machine industrielle**. Elle a besoin de matières premières pour fonctionner et elle produit quelque chose en sortie.

Il existe trois "tuyaux" connectés par défaut à chaque commande :

| Canal | Nom technique | ID | Description | Direction par défaut |
| --- | --- | --- | --- | --- |
| **Entrée** | `stdin` | 0 | Les données brutes | Votre **Clavier** |
| **Sortie** | `stdout` | 1 | Le bon résultat | Votre **Écran** |
| **Erreur** | `stderr` | 2 | Les messages de panne | Votre **Écran** |

> **Analogie :** C'est comme une créature qui **mange** (stdin), **parle** (stdout) et parfois **crie** quand elle a mal (stderr).


## Les redirections

Par défaut, la "rivière" de données coule vers l'écran. Nous pouvons utiliser des chevrons pour détourner ce flux vers un **fichier**.

### 1. Le destructeur (`>`)

Le chevron simple redirige la sortie vers un fichier.

* **Attention :** Si le fichier existe, il est **écrasé** (vidé et remplacé).
* **Moyen mnémotechnique :** Le fichier est remis à zéro.

```bash
echo "Liste de courses" > courses.txt
# Le fichier courses.txt contient maintenant uniquement : Liste de courses
```

### 2. Le constructeur (`>>`)

Le double chevron ajoute les données à la **fin** du fichier existant.

* **Sécurité :** Il ne détruit pas l'ancien contenu.

```bash
echo "- Pommes" >> courses.txt
echo "- Bananes" >> courses.txt
# Le fichier contient maintenant le titre ET les fruits.
```

### 🟢 Exercice #1 (En classe)

**Objectif :** Visualiser la différence entre écraser et ajouter.

1. Demandez aux étudiants de taper : `echo "Bonjour" > test.txt`
2. Puis : `echo "Monde" > test.txt`
3. Vérifiez le contenu (`cat test.txt`). Que s'est-il passé ? (Réponse : "Bonjour" a disparu).
4. Corrigez le tir : `echo "Bonjour" >> test.txt` (Pour avoir Monde et Bonjour).



## Le Tube (Pipe `|`) : L'Assemblage

C'est le super-pouvoir de Linux. Le caractère `|` (Alt Gr + 6) connecte la sortie de la commande de gauche à l'entrée de la commande de droite.

**La règle d'or :** Pas de fichier intermédiaire. Tout se passe en mémoire vive (RAM).

> **Analogie de l'usine :**
> `Machine A (Fabrique le biscuit)` **|** `Machine B (Met le chocolat)` **|** `Machine C (Emballe)`

### 1. Les filtres indispensables

Le Pipe sert à envoyer des données vers des filtres. Voici les plus utilisés :

* **`sort`** : Trie les lignes par ordre alphabétique ou numérique.
* **`uniq`** : Supprime les doublons **adjacents** (il faut souvent trier avant !).
* **`grep "mot"`** : Ne garde que les lignes contenant "mot".
* **`wc -l`** : Compte le nombre de lignes (*Word Count -lines*).
* **`head` / `tail**` : Affiche les premières ou dernières lignes.


### 🟢 Exercice #2 (En classe)

* Le dossier `/etc` contient des centaines de fichiers de configuration.
* Afficher uniquement les fichiers contenant "conf" dans leur nom, et les trier à l'envers.

<!--
**Reponse**
```bash
ls /etc | grep "conf" | sort -r
```
-->

*Discussion : Que se passe si on enlève le `grep`?*

### 🟢 Exercice #3 (En classe)

* On veut savoir combien d'objets se trouvent dans le dossier `/bin` (là où sont stockées les commandes comme ls, cp, etc.).
* Compter les fichiers.

<!--
Reponse
```bash
ls /bin | wc -l
```
-->

**Discussion** : Pourquoi ne pas simplement faire `ls /bin` et compter à la main ? 
<!--(Réponse : Trop long, risque d'erreur, automatisation impossible).-->


---

# Laboratoire

Utiliser le fichier **labo9.docx** pour y mettre vos réponses et captures d'écran.  
{{% button href="/docs/Labos/labo9.docx" icon="download" %}}Télécharger le fichier docx{{% /button %}}

Vous êtes administrateur système. On vous donne une liste brute d'utilisateurs suspects et de tentatives de connexion. Votre but est de nettoyer ces données pour en extraire des statistiques utiles.

### Étape 1 : Création des données (Setup)

Créez un fichier sale avec des doublons et des données désordonnées. Copiez/collez ces commandes :

```bash
echo "Martin" > utilisateurs.txt
echo "Julie" >> utilisateurs.txt
echo "Martin" >> utilisateurs.txt
echo "Alain" >> utilisateurs.txt
echo "Julie" >> utilisateurs.txt
echo "Zoe" >> utilisateurs.txt
echo "Martin" >> utilisateurs.txt
```

### Étape 2 : Le nettoyage (Sort & Uniq)

Si vous faites `uniq utilisateurs.txt`, cela ne fonctionnera pas parfaitement car `uniq` ne voit que les doublons qui se touchent.

1. Affichez le contenu brut 
2. Triez le fichier et affichez le résultat à l'écran
3. Utilisez le pipe pour trier PUIS supprimer les doublons

<!--
Reponse
```bash
cat utilisateurs.txt | sort | uniq
```
-->

4. **Défi :** Redirigez cette liste propre vers un nouveau fichier nommé `utilisateurs_propres.txt`.

### Étape 3 : L'enquête (Grep & Wc)

Nous allons simuler un fichier de journal système (log).

```bash
# Création du fichier log (copiez tout le bloc)
echo "[INFO] Connexion réussie : Martin" > system.log
echo "[ERREUR] Échec de connexion : Hacker" >> system.log
echo "[INFO] Connexion réussie : Julie" >> system.log
echo "[ERREUR] Échec de connexion : Hacker" >> system.log
echo "[INFO] Connexion réussie : Alain" >> system.log
echo "[ERREUR] Échec de connexion : Hacker" >> system.log
```

1. Utilisez `grep` pour n'afficher que les lignes contenant "ERREUR".
2. Utilisez un pipe et `wc -l` pour compter combien de fois le mot "ERREUR" apparaît.

<!--**Commande attendue :**

```bash
cat system.log | grep "ERREUR" | wc -l
```
-->


### Étape 4 : Le grand final (History)

L'historique de votre terminal garde tout ce que vous avez tapé.

1. Utilisez la commande `history`.
2. Utilisez un pipe pour trouver combien de fois vous avez utilisé la commande `echo` aujourd'hui.

<!--**Solution :** `history | grep "echo" | wc -l` -->

<!--

### Note pédagogique pour l'enseignant

* **Erreur fréquente :** Les étudiants oublient souvent que `uniq` nécessite un `sort` au préalable. Insistez sur l'analogie : "On ne peut pas empiler les chemises identiques si elles sont éparpillées dans toute la pièce; il faut d'abord les trier par couleur/type."
* **Le danger du `>` :** Faites leur remarquer que s'ils font `cat fichier | sort > fichier`, ils risquent d'effacer le fichier avant même de le lire (selon le shell). Il vaut mieux rediriger vers un *nouveau* nom (`fichier_trié.txt`).
-->



==============================================


# LABORATOIRE

**Objectif :** Manipuler des logs et extraire de l'information précise.

## Étape 1 : Dompter les fichiers (Redirections)

*Pas d'éditeur de texte autorisé ici !*

1. Utilisez `echo` et `>` pour créer un fichier `mes_films.txt` avec le titre "Star Wars".
2. Utilisez `>>` pour ajouter "Le Seigneur des Anneaux" et "Matrix" (3 commandes distinctes).
3. Vérifiez avec `cat`.
4. Lancez une commande qui plante (ex: `ls /root` en tant qu'étudiant).
5. Relancez-la en cachant l'erreur : `ls /root 2> /dev/null`. Le terminal doit rester muet.

## Étape 2 : L'aiguille dans la botte de foin (`grep`)

*Le fichier `/etc/passwd` est parfait pour s'exercer.*

1. Affichez le fichier `/etc/passwd`. C'est illisible ?
2. Utilisez un Pipe et `head` pour voir seulement les 5 premiers utilisateurs.
3. Utilisez `grep` pour trouver la ligne correspondant à votre utilisateur (`etudiant`).
4. Utilisez `grep` pour trouver tous les utilisateurs qui n'ont **pas** de shell de connexion (cherchez `/usr/sbin/nologin`).
5. **Défi :** Comptez combien il y en a en ajoutant `| wc -l` à la fin.

## Étape 3 : Le détective (`find`)

*La commande `find` est différente, elle cherche des FICHIERS, pas du texte.*

1. Trouvez tous les fichiers qui se terminent par `.conf` dans `/etc` :
`find /etc -name "*.conf"`
*(Vous aurez plein d'erreurs "Permission denied". C'est normal !)*
2. Refaites la commande en envoyant les erreurs dans le néant pour avoir une liste propre :
`find /etc -name "*.conf" 2> /dev/null`
3. Trouvez tous les fichiers modifiés dans les dernières 24 heures dans votre dossier home :
`find ~ -mtime -1`

## Étape 4 : Le "CSI Linux" (Problème complexe) (15 min)

*Scénario :* Vous devez lister les 3 derniers utilisateurs créés sur le système, triés par ordre alphabétique.
*Indice : `/etc/passwd` contient les infos, `tail` prend la fin, `sort` trie, `cut` découpe.*

<!--
*Solution à faire trouver par les étudiants :*
`tail -n 3 /etc/passwd | cut -d: -f1 | sort`
-->

---

### 💡 Astuces de la semaine


> 
> 
> **Les 3 commandes en or :**
> * `grep "mot"` : Garde seulement les lignes avec "mot".
> * `wc -l` : Compte les lignes.
> * `sort` : Met en ordre.
> 
>
