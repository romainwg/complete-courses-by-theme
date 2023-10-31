
# Tutoriel sur l'Écriture de Conventional Commits

<!-- https://www.conventionalcommits.org/en/v1.0.0/ -->
<!-- https://github.com/conventional-changelog/commitlint/blob/master/%40commitlint/config-conventional/README.md -->

Les Conventional Commits sont un système de nommage des commits qui ajoute de la clarté et une structure standardisée aux messages de commit. Ce tutoriel vous guidera à travers les étapes et les meilleures pratiques pour écrire des Conventional Commits.

- [Tutoriel sur l'Écriture de Conventional Commits](#tutoriel-sur-lécriture-de-conventional-commits)
  - [Qu'est-ce qu'un Conventional Commit ?](#quest-ce-quun-conventional-commit-)
  - [Structure de Base d'un Conventional Commit](#structure-de-base-dun-conventional-commit)
    - [Éléments Structurels](#éléments-structurels)
    - [Types de Commit Communs](#types-de-commit-communs)
    - [Types de Commit Étendus](#types-de-commit-étendus)
  - [Comment Écrire un Conventional Commit](#comment-écrire-un-conventional-commit)
  - [Bonnes Pratiques](#bonnes-pratiques)
  - [Avantages des Conventional Commits](#avantages-des-conventional-commits)
  - [Exemples](#exemples)
  - [Utilisation dans VSCode avec vscode-conventional-commits](#utilisation-dans-vscode-avec-vscode-conventional-commits)
    - [Utilisation](#utilisation)
  - [Règles de Linting avec `@commitlint/config-conventional`](#règles-de-linting-avec-commitlintconfig-conventional)
    - [Règles de linting - Conventional commits](#règles-de-linting---conventional-commits)

---

## Qu'est-ce qu'un Conventional Commit ?

Un Conventional Commit est un message de commit qui suit une certaine structure et des conventions spécifiques pour décrire de manière claire et concise les changements apportés dans un commit. Cette spécification vise à rendre les messages de commit lisibles par l'homme et par la machine.

## Structure de Base d'un Conventional Commit

Un message de commit Conventional doit suivre cette structure :

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Éléments Structurels

1. **Type** : Indique la nature du commit (ex : `fix`, `feat`).
2. **Scope** (Optionnel) : Contexte supplémentaire (ex : `feat(parser):`).
3. **Description** : Résumé concis des changements.
4. **Body** (Optionnel) : Détails et contexte additionnels.
5. **Footer(s)** (Optionnel) : Infos supplémentaires, telles que `BREAKING CHANGE`.

### Types de Commit Communs

- `fix` : Corrige un bug (correspond à PATCH dans SemVer).
- `feat` : Ajoute une nouvelle fonctionnalité (correspond à MINOR dans SemVer).
- `BREAKING CHANGE` : Changement majeur (correspond à MAJOR dans SemVer).

### Types de Commit Étendus

En plus des types de base `fix` et `feat`, les Conventional Commits peuvent utiliser les types suivants pour une meilleure catégorisation :

- `build` : Modifications affectant le système de build ou les dépendances externes.
- `chore` : Mises à jour mineures ou tâches de maintenance ne modifiant ni le code source, ni les tests.
- `ci` : Changements liés aux fichiers et scripts de configuration CI (Intégration Continue).
- `docs` : Ajout ou modification de la documentation.
- `perf` : Amélioration des performances.
- `refactor` : Refactorisation du code qui ne corrige pas un bug ni n'ajoute une fonctionnalité.
- `revert` : Annulation d'un commit précédent.
- `style` : Changements qui n'affectent pas le sens du code (formatage, manque de points-virgules, etc.).
- `test` : Ajout ou modification de tests.

## Comment Écrire un Conventional Commit

1. **Déterminer le Type** : Commencez par identifier si votre commit est un correctif (`fix`), une nouvelle fonctionnalité (`feat`) ou un autre type (`docs`, `refactor`, `test`, etc.).

2. **Ajouter un Scope (si nécessaire)** : Si votre commit concerne une partie spécifique du projet, ajoutez un scope. Par exemple, `feat(parser):`.

3. **Rédiger une Description Claire** : Écrivez un résumé concis de ce que fait le commit.

4. **Ajouter un Body (optionnel)** : Si nécessaire, fournissez des détails supplémentaires sur les changements.

5. **Inclure un ou plusieurs Footers (optionnel)** : Utilisez cette section pour des informations complémentaires, comme indiquer un `BREAKING CHANGE`.

## Bonnes Pratiques

- Préfixez les commits par un type, suivi d'un scope optionnel et d'un point d'exclamation si c'est un changement majeur.
- Assurez-vous que la description suit immédiatement le type/scope.
- Séparez le body et les footers de la description par une ligne vide.
- N'hésitez pas à utiliser d'autres types que `feat` et `fix`.

## Avantages des Conventional Commits

- Facilite la génération automatique de CHANGELOGs.
- Permet la détermination automatique des versions selon SemVer.
- Assure une communication claire sur la nature des changements.
- Améliore les contributions et la maintenance du projet.

En suivant ces lignes directrices, vos messages de commit seront non seulement informatifs et structurés, mais également très utiles pour l'automatisation des outils et la gestion des versions de votre projet.

## Exemples

1. **Commit avec Changement Majeur** :

   ```text
   feat: allow provided config object to extend other configs

   BREAKING CHANGE: `extends` key in config file is now used for extending other config files
   ```

2. **Commit avec Changement Majeur et !** :

   ```text
   feat!: send an email to the customer when a product is shipped
   ```

3. **Commit avec Scope et !** :

   ```text
   feat(api)!: send an email to the customer when a product is shipped
   ```

4. **Commit avec Body et Plusieurs Footers** :

   ```text
   fix: prevent racing of requests

   Introduce a request id and a reference to latest request. Dismiss
   incoming responses other than from latest request.

   Reviewed-by: Z
   Refs: #123
   ```

## Utilisation dans VSCode avec [vscode-conventional-commits](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits)

L'extension "Conventional Commits" pour Visual Studio Code aide à formuler des messages de commit conformes aux Conventional Commits.

⚠️ Par défault, l'outil commit automatiquement après avoir spécifié le conventional commit.

### Utilisation

- Accédez à l'extension de deux manières :
  1. Commande + Shift + P ou Ctrl + Shift + P, entrez "Conventional Commits" et appuyez sur Entrée.
  2. Cliquez sur l'icône dans le menu Source Control.

## Règles de Linting avec `@commitlint/config-conventional`

Pour assurer que les Conventional Commits respectent les normes établies, l'utilisation de `@commitlint/config-conventional` est recommandée. Voici un résumé des règles de linting et des exemples :

### Règles de linting - Conventional commits

1. **type-enum**
   - Assure que le `type` est dans la liste prédéfinie.
   - `error` si non respecté.
   - Exemples : `echo "foo: some message"` échoue, `echo "fix: some message"` réussit.

2. **type-case**
   - Vérifie que le `type` est en minuscules.
   - `error` si non respecté.
   - Exemples : `echo "FIX: some message"` échoue, `echo "fix: some message"` réussit.

3. **type-empty**
   - Interdit un `type` vide.
   - `error` si non respecté.
   - Exemples : `echo ": some message"` échoue, `echo "fix: some message"` réussit.

4. **subject-case**
   - Interdit certains cas pour le `subject`.
   - `error` si non respecté.
   - Exemples : `echo "fix(SCOPE): Some message"` échoue, `echo "fix(scope): some message"` réussit.

5. **subject-empty**
   - Interdit un `subject` vide.
   - `error` si non respecté.
   - Exemples : `echo "fix:"` échoue, `echo "fix: some message"` réussit.

6. **subject-full-stop**
   - Interdit un `subject` finissant par un point.
   - `error` si non respecté.
   - Exemples : `echo "fix: some message."` échoue, `echo "fix: some message"` réussit.

7. **header-max-length**
   - Limite la longueur du `header` à 100 caractères.
   - `error` si non respecté.
   - Exemples : `echo "fix: some message that is way too long..."` échoue, `echo "fix: some message"` réussit.

8. **footer-leading-blank**
   - Exige une ligne vide au début du `footer`.
   - `warning` si non respecté.
   - Exemples : `echo "fix: some message\nBREAKING CHANGE: It will be significant"` avertit.

9. **footer-max-line-length**
   - Limite la longueur des lignes du `footer` à 100 caractères.
   - `error` si non respecté.
   - Exemples : `echo "fix: some message\nBREAKING CHANGE: footer too long..."` échoue.

10. **body-leading-blank**
    - Exige une ligne vide au début du `body`.
    - `warning` si non respecté.
    - Exemples : `echo "fix: some message\nbody"` avertit.

11. **body-max-line-length**
    - Limite la longueur des lignes du `body` à 100 caractères.
    - `error` si non respecté.
    - Exemples : `echo "fix: some message\nbody too long..."` échoue.

En respectant ces règles, vos commits seront non seulement conformes aux standards des Conventional Commits, mais aussi plus faciles à lire et à comprendre pour toute personne contribuant à votre projet.
