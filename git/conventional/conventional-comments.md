# Tutoriel sur l'écriture de Conventional Comments

<!-- https://conventionalcomments.org/ -->

Les Conventional Comments offrent une manière structurée de donner des retours lors de revues, en utilisant des étiquettes spécifiques pour clarifier l'intention derrière chaque commentaire. Voici un guide simple pour vous aider à les utiliser efficacement.

- [Tutoriel sur l'écriture de Conventional Comments](#tutoriel-sur-lécriture-de-conventional-comments)
  - [1. Comprendre le format](#1-comprendre-le-format)
  - [2. Utiliser les étiquettes](#2-utiliser-les-étiquettes)
  - [3. Ajouter des décorations](#3-ajouter-des-décorations)
  - [4. Fournir une discussion](#4-fournir-une-discussion)
  - [5. Meilleures pratiques](#5-meilleures-pratiques)

---

## 1. Comprendre le format

Un Conventional Comment suit ce format :

```text
<étiquette> [décorations]: <sujet>
[discussion]
```

- **Étiquette** : Indique le type de commentaire.
- **Décorations** : (Optionnel) Fournit un contexte supplémentaire.
- **Sujet** : Le message principal du commentaire.
- **Discussion** : (Optionnel) Des détails supplémentaires ou une justification.

---

## 2. Utiliser les étiquettes

Voici quelques étiquettes couramment utilisées :

- **praise** : Pour complimenter quelque chose.
- **nitpick** : Pour un détail mineur ou une préférence personnelle.
- **suggestion** : Pour proposer une amélioration.
- **issue** : Pour signaler un problème.
- **question** : Pour poser une question ou demander des éclaircissements.
- **todo** : Pour indiquer une petite tâche à accomplir.

**Exemples** :

```text
praise: Excellent travail sur cette fonction !
nitpick: Pourriez-vous aligner ces variables pour une meilleure lisibilité ?
suggestion: Utiliser une boucle for ici pourrait rendre le code plus propre.
issue: Cette méthode pourrait provoquer une fuite de mémoire.
question: Pourquoi avons-nous choisi cette approche plutôt qu'une autre ?
todo: Ajouter des commentaires pour clarifier cette section.
```

---

## 3. Ajouter des décorations

Les décorations fournissent un contexte supplémentaire. Voici quelques décorations courantes :

- **(non-blocking)** : Le commentaire ne devrait pas empêcher l'approbation.
- **(blocking)** : Le commentaire doit être résolu avant l'approbation.

**Exemples** :

```text
suggestion (non-blocking): Peut-être pourrions-nous ajouter une animation ici ?
issue (blocking): Cette fonction ne vérifie pas les entrées, ce qui pourrait causer des bugs.
```

---

## 4. Fournir une discussion

La section de discussion est l'endroit où vous pouvez ajouter des détails, une justification ou des étapes pour résoudre le commentaire.

**Exemple** :

```text
suggestion: Utiliser une boucle for ici pourrait rendre le code plus propre.
Il serait plus efficace et faciliterait la maintenance à long terme.
```

---

## 5. Meilleures pratiques

- **Soyez constructif** : Visez à aider, pas à critiquer.
- **Soyez clair** : Assurez-vous que votre commentaire est compréhensible.
- **Utilisez "nous" au lieu de "vous"** : Cela crée un sentiment de collaboration.
- **Équilibrez les commentaires positifs et négatifs** : Essayez de trouver des points positifs à mentionner.

---

En suivant ce guide, vous serez en mesure de donner des retours clairs, constructifs et compréhensibles, rendant le processus de revue plus efficace et agréable pour tous.
