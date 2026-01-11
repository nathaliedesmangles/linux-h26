+++
title = "Protocole de remise des exos et labos"
weight = 9
+++


Pour valider vos acquis, vous devez soumettre des preuves de votre travail pour **tous** les exercices effectués, qu'ils soient faits en classe ou durant les laboratoires.

> [!warning]

> Bien que les exercices (précédés de 🟢) et les laboratoires ne soient pas **sommativement** notés, ils servent d'entraînement intensif pour réussir les évaluations sommatives (examens).  
> Si vous ne les faites pas pendant les séances dédiées ou si vous ne les remettez pas, cela sera considéré comme une absence au cours et/ou laboratoire.


## Format des preuves (Captures d'écran)

Toutes les remises se font sous forme de captures d'écran insérées dans un document. Chaque capture doit respecter strictement les règles suivantes :

### 1. Pendant l'exercice
Pour chaque étape importante, votre capture d'écran doit montrer trois éléments indissociables :
1.  **Votre identifiant :** Le prompt du terminal doit être visible (ex: `etudiant@linux-mint:~$`).
2.  **La commande :** Ce que vous avez tapé.
3.  **Le résultat :** Ce que le système a répondu.

### 2. À la fin de chaque exercice (Obligatoire)
Une fois l'exercice terminé, vous devez **impérativement** lancer la commande suivante et en faire une capture d'écran :

```bash
history
```

Vous devez capturer **toutes** les commandes tapées pour réaliser l'exercice. Si la liste est longue, faites plusieurs captures.


## Politique du "Droit à l'erreur"

> [!primary]
> Je ne sanctionne pas les erreurs de parcours.
>
> Dans votre capture de la commande `history`, je m'attends à voir des commandes ratées, des fautes de frappe et des essais infructueux. **C'est normal, c'est comme ça qu'on apprend.**
>
> * **Tant que la dernière commande de la séquence est bonne et que le résultat est atteint, vous aurez tous vos points.**
> * Il n'y a **aucune pénalité** pour avoir échoué 10 fois avant de réussir.



## Exemple de remise valide

Voici à quoi doit ressembler une preuve valide pour l'exercice "Créer un dossier" :

**Étape 1 : La réalisation**
*(Capture d'écran montrant)* :

```text
etudiant@mint:~$ mkdir mon_dossier
etudiant@mint:~$ ls -l
drwxr-xr-x 2 etudiant etudiant 4096 jan 04 10:00 mon_dossier
```

**Étape 2 : La vérification (History)**
*(Capture d'écran finale)* :

```text
etudiant@mint:~$ history
  41  mkdi mon_dossier      <-- Erreur (pas grave !)
  42  mkdir mon_dossier     <-- Réussite
  43  ls -l
  44  history
```

> [!primary]
> Une remise sans la capture de la commande `history` sera considérée comme incomplète.

