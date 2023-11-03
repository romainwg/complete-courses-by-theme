# Tutoriel Complété sur le Conventional Branch Naming avec Git/GitFlow

<!-- https://stackoverflow.com/a/6065944 -->
<!-- https://idiv-biodiversity.github.io/git-knowledge-base/branch-naming-conventions.html -->

Nous avons déjà couvert les branches de flux de code et les branches temporaires. Maintenant, intégrons des conventions supplémentaires de nommage des branches pour une meilleure organisation et gestion des workflows.

- [Tutoriel Complété sur le Conventional Branch Naming avec Git/GitFlow](#tutoriel-complété-sur-le-conventional-branch-naming-avec-gitgitflow)
  - [Conventions de Nommage des Branches](#conventions-de-nommage-des-branches)
    - [Utiliser des Tokens de Groupement](#utiliser-des-tokens-de-groupement)
    - [Tokens Courts et Bien Définis](#tokens-courts-et-bien-définis)
    - [Utiliser des Slashs pour Séparer les Parties](#utiliser-des-slashs-pour-séparer-les-parties)
    - [Éviter les Nombres Nus](#éviter-les-nombres-nus)
    - [Éviter les Noms Longs et Descriptifs pour les Branches à Long Terme](#éviter-les-noms-longs-et-descriptifs-pour-les-branches-à-long-terme)
  - [Exemples de Workflow avec Tokens et Groupement](#exemples-de-workflow-avec-tokens-et-groupement)
  - [Bonnes Pratiques Supplémentaires](#bonnes-pratiques-supplémentaires)

---

## Conventions de Nommage des Branches

### Utiliser des Tokens de Groupement

- **But** : Commencez vos noms de branches avec des tokens de groupement.
- **Exemples** :
  - `group1/foo`
  - `group2/bar`

### Tokens Courts et Bien Définis

- **But** : Utilisez des tokens courts et significatifs pour différencier les branches.
- **Exemples** :
  - `wip` (Work in Progress)
  - `feat` (Feature)
  - `bug` (Bug Fix)
  - `junk` (Expérimental)

### Utiliser des Slashs pour Séparer les Parties

- **But** : Faciliter la navigation et le filtrage des branches.
- **Avantage** : Permet de renommer des branches lors de push ou fetch.
- **Exemple de Commande** : `$ git push origin 'refs/heads/feature/*:refs/heads/phord/feat/*'`

### Éviter les Nombres Nus

- **Raison** : Éviter la confusion avec les SHA-1.
- **Solution** : Utiliser des préfixes devant les nombres.
- **Exemple** : `CR15032` au lieu de `15032`

### Éviter les Noms Longs et Descriptifs pour les Branches à Long Terme

- **Raison** : Éviter l'encombrement dans les journaux de commit.
- **Conseil** : Utiliser des noms courts mais descriptifs.

## Exemples de Workflow avec Tokens et Groupement

Imaginons que vous avez plusieurs branches pour différents cycles d'un changement : 'new', 'testing' et 'verified'.

- **Branches de Nouvelle Fonctionnalité** :
  - `new/frabnotz`
  - `new/foo`
- **Branches en Test** :
  - `test/foo`
  - `test/frabnotz`
- **Branches Vérifiées** :
  - `ver/foo`

Avec cette structure, il est facile de filtrer et de regrouper les branches :

- **Lister les Branches en Test** : `$ git branch --list "test/*"`
- **Lister les Branches Liées à "foo"** : `$ git branch --list "*/foo"`

## Bonnes Pratiques Supplémentaires

- **Tab Expansion** : Utilisez la touche TAB pour compléter les noms de branches. Par exemple, `git checkout new<TAB>` affichera un menu de branches commençant par `new/`.
- **Recherche de Branches** : Utilisez des commandes telles que `git branch --list "feature/*"` pour filtrer les branches.

En combinant les conventions initiales avec ces pratiques supplémentaires, vous pouvez créer un système de nommage de branches Git extrêmement efficace, organisé et facile à naviguer.
