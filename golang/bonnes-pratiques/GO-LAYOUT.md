# Go Layout

- [Go Layout](#go-layout)
  - [Arborescence générale](#arborescence-générale)
  - [Exemple d'arborescence complète](#exemple-darborescence-complète)
  - [vendor](#vendor)
  - [pkg vs internal](#pkg-vs-internal)
    - [pkg](#pkg)

Pour plus de détail, voir le projet Github [project-layout](https://github.com/golang-standards/project-layout).

## Arborescence générale

La structure de l'arborescence d'un projet Go peut varier en fonction des préférences personnelles, des pratiques de l'équipe, et de la complexité du projet. Cependant, il existe des conventions courantes dans la communauté Go, dont certaines sont inspirées par le dépôt GitHub `golang-standards/project-layout` qui n'est pas officiel mais a été influent dans la communauté Go. Voici une structure d'arborescence de projet typique :

```text
/mon-projet
  /cmd
    /monappli
      main.go        # Point d'entrée pour l'exécutable monappli
  /internal          # Code interne non réutilisable en dehors du projet
    /paquet1
    /paquet2
  /pkg               # Bibliothèques réutilisables par d'autres projets
    /monpaquet
  /api               # Spécifications d'API, protobuf, etc.
  /configs           # Configurations, fichiers de paramètres
  /deployments       # Scripts et configurations de déploiement
  /scripts           # Scripts pour des opérations diverses
  /build             # Scripts de compilation et Packaging
  /tests             # Tests end-to-end, de charge, etc.
  /docs              # Documentation du projet
  /tools             # Outils supplémentaires liés au projet
  /examples          # Exemples d'utilisation des paquets publics
  /third_party       # Code tiers, comme des bibliothèques externes
  /vendor            # Dépendances gérées par le système de modules Go
  .gitignore         # Fichiers à ignorer dans le contrôle de version
  go.mod             # Dépendances du projet et versions
  go.sum             # Somme de contrôle des dépendances
  README.md          # Présentation du projet et instructions
  LICENSE            # Licence du projet
```

Explications détaillées des composants :

- `/cmd`: Contient les applications principales du projet, chaque sous-dossier représente un exécutable, et chaque exécutable a un `main.go`.

- `/internal`: Code spécifique à l'application qui n'est pas destiné à être utilisé en dehors du projet. L'accès est restreint par le compilateur Go.

- `/pkg`: Bibliothèques qui peuvent être réutilisées par d'autres applications ou projets.

- `/api`: Définitions des interfaces de programmation applicatives, souvent utilisées pour définir des contrats de services web, des fichiers protobuf, etc.

- `/configs`: Fichiers de configuration ou de paramètres typiques.

- `/deployments`: Fichiers et scripts liés au déploiement de l'application.

- `/scripts`: Scripts qui exécutent diverses tâches de build, installation, analyse, etc.

- `/build`: Contient les scripts et configurations nécessaires à la construction des exécutables.

- `/tests`: Tests additionnels qui ne sont pas des tests unitaires (comme les tests d'intégration ou E2E).

- `/docs`: Documentation pour le projet, telle que des tutoriels, des guides utilisateur, etc.

- `/tools`: Outils supplémentaires spécifiques au projet, qui peuvent inclure des scripts ou des applications d'assistance.

- `/examples`: Exemples de code montrant comment utiliser les bibliothèques ou paquets publics du projet.

- `/third_party`: Code tiers utilisé dans le projet, tel que les bibliothèques de dépendances qui ne sont pas gérées par les modules Go.

- `/vendor`: Dossier contenant les dépendances du projet, utilisé lorsque la gestion des dépendances est faite avec vendoring.

- `go.mod` et `go.sum`: Définissent les dépendances du projet et garantissent la cohérence des builds.

- `README.md`, `LICENSE`, `.gitignore`: Fichiers standard pour la documentation, les conditions de licence et l'exclusion de fichiers du contrôle de version.

Il est important de noter que cette structure est une suggestion et peut être adaptée selon les besoins du projet. Par exemple, des projets plus petits peuvent ne pas avoir besoin de certains dossiers ou pourraient combiner certaines fonctionnalités dans moins de dossiers. L'essentiel est de maintenir une organisation logique qui est intuitive pour les nouveaux contributeurs et conforme aux attentes de l'équipe de développement.

## Exemple d'arborescence complète

Voici une structure de projet Go élargie avec des exemples de fichiers et de dossiers supplémentaires pour illustrer comment les composants d'un projet typique pourraient être organisés :

```text
/mon-projet
  /cmd
    /monappli
      main.go                # Point d'entrée de l'exécutable 'monappli'
  /internal
    /auth
      authentication.go      # Gère l'authentification
    /database
      database.go            # Logique de connexion à la base de données
    /billing
      invoice.go             # Gère la création des factures
  /pkg
    /apiresponse
      response.go            # Formate les réponses de l'API
    /utils
      helpers.go             # Fonctions utilitaires
  /api
    /v1
      swagger.yaml           # Spécifications de l'API pour la v1
  /configs
    config.yaml              # Fichier de configuration principal
    /development
      dev.config.yaml        # Configuration pour le développement
    /production
      prod.config.yaml       # Configuration pour la production
  /deployments
    docker-compose.yml       # Configuration Docker Compose pour les déploiements locaux
    /kubernetes
      deployment.yaml        # Manifeste de déploiement Kubernetes
  /scripts
    initdb.sh                # Script d'initialisation de la base de données
    test_coverage.sh         # Script pour tester la couverture du code
  /build
    Dockerfile               # Pour construire une image Docker du projet
    Makefile                 # Fichier Make pour automatiser la construction et le déploiement
  /tests
    /integration
      integration_test.go    # Tests d'intégration
    /load
      load_test.go           # Tests de performance et de charge
  /docs
    QUICKSTART.md            # Guide de démarrage rapide
    API_GUIDE.md             # Documentation de l'API
  /tools
    /migrate
      migrate.go             # Outil de migration de base de données
  /examples
    /simple
      main.go                # Exemple simple d'utilisation des paquets publics
  /third_party
    /protobuf
      api.proto              # Fichiers protobuf tiers
  /vendor
    ...                      # Librairies externes (si le vendoring est utilisé)
  .gitignore
    # Ignore les fichiers de configuration et les fichiers temporaires
  go.mod
    # Liste des dépendances du module
  go.sum
    # Somme de contrôle pour la vérification de l'intégrité des dépendances
  README.md
    # Présentation du projet, statut, informations sur la contribution, etc.
  LICENSE
    # Informations sur la licence du projet
```

Cette structure fournit un cadre organisé pour le développement d'un projet Go, couvrant les divers aspects tels que le code de l'application, la réutilisation des bibliothèques, la configuration, le déploiement, l'outillage, la documentation, et plus encore. Cela aide à maintenir la cohérence, la compréhension facile du projet par les nouveaux développeurs, et la facilité de maintenance à long terme.

## vendor

Le dossier `/vendor` est utilisé pour le "vendoring", qui est une pratique consistant à inclure les copies des dépendances externes directement dans le répertoire d'un projet. Cela permet de garantir que le projet est isolé des changements dans ces dépendances et qu'il peut être construit de manière reproductible, même si les dépendances ne sont plus disponibles ou si leurs versions ont changé en amont.

Dans un projet Go, le vendoring est souvent géré par le gestionnaire de paquets de Go (`go mod`), qui crée et maintient le fichier `go.mod` pour suivre les dépendances et le fichier `go.sum` pour la somme de contrôle de chaque dépendance. À partir de Go 1.11, avec l'introduction des modules, le vendoring est devenu une option plutôt qu'une nécessité, car le système de modules peut télécharger les dépendances requises en fonction de `go.mod`.

Cependant, pour des raisons de contrôle et de sécurité, certaines équipes préfèrent toujours utiliser le dossier `/vendor`. L'utilisation du dossier `/vendor` est activée par la commande `go mod vendor`, qui copie les dépendances dans le dossier `/vendor`.

Voici un exemple de ce à quoi cela pourrait ressembler:

```text
/vendor
  /github.com
    /pelletier
      /go-toml
        ...                  # Fichiers sources de la bibliothèque go-toml
    /spf13
      /cobra
        ...                  # Fichiers sources de la bibliothèque cobra
  /golang.org
    /x
      /sys
        ...                  # Fichiers sources de la bibliothèque x/sys
  modules.txt               # Un fichier généré qui énumère les versions des dépendances
```

Dans cet exemple, le dossier `/vendor` contient des sous-dossiers qui correspondent aux importations de votre projet. Ces sous-dossiers incluent le code source exact qui serait utilisé lors de la compilation du projet. Le fichier `modules.txt` contient des informations sur les versions exactes des paquets qui sont vendored.

Enfin, pour compiler le projet en utilisant les dépendances dans le dossier `/vendor`, vous pouvez utiliser le drapeau `-mod=vendor` avec les commandes `go build` ou `go run`.

**Remarque :** Depuis Go 1.14, le mode module est activé par défaut et le flag `-mod=vendor` n'est nécessaire que si vous souhaitez vraiment forcer l'utilisation du dossier `/vendor`. La plupart des projets modernes s'appuient sur le proxy de modules Go par défaut pour gérer les dépendances, rendant moins courant l'utilisation de `/vendor`, bien qu'elle reste une pratique valable pour les raisons mentionnées ci-dessus.

## pkg vs internal

En Go, la décision d'utiliser `pkg` ou `internal` pour organiser un projet dépend principalement de la façon dont vous souhaitez exposer les paquets de votre projet, et de l'ampleur de celui-ci. Voici quelques lignes directrices :

**Utiliser `internal` :**

1. **Encapsulation de code :** Lorsque vous souhaitez garder des parties de votre code inaccessibles aux utilisateurs de votre bibliothèque ou application. Les paquets dans un répertoire `internal` sont seulement accessibles aux paquets qui résident dans le même répertoire parent ou dans le répertoire `internal` lui-même.

2. **Prévenir l'importation non désirée :** Si vous travaillez sur une librairie et que vous avez des parties du code qui sont susceptibles de changer ou que vous ne souhaitez pas exposer comme API publique, placez ces parties dans `internal`. Cela empêche les utilisateurs externes de votre module de compter sur ces détails d'implémentation, ce qui pourrait être problématique lors de mises à jour futures.

3. **Structure claire pour de grands projets :** Dans les grands projets, où vous avez de multiples composants ou services qui peuvent partager du code interne sans vouloir l'exposer en dehors du projet.

**Utiliser `pkg` :**

1. **Organisation de code réutilisable :** Pour les parties de votre application qui sont destinées à être réutilisées comme des bibliothèques par d'autres paquets au sein de votre projet, ou potentiellement par d'autres projets.

2. **Convention populaire :** Si vous contribuez à ou maintenez un projet qui suit déjà la convention `pkg` et que vous voulez rester cohérent avec l'écosystème existant de ce projet.

3. **Clarté pour les nouveaux contributeurs :** Si vous voulez que le projet soit facile à comprendre pour les nouveaux contributeurs, suivre une convention populaire comme `pkg` peut aider à naviguer dans le projet.

**Cas où ni `pkg` ni `internal` ne sont nécessaires :**

Pour les petits projets ou les paquets simples, vous pourriez ne pas avoir besoin d'une structure de répertoire complexe. Vous pouvez placer vos fichiers source Go directement dans le répertoire racine ou dans des sous-répertoires basés sur leur fonction, sans nécessité d'un répertoire `pkg` ou `internal`.

En résumé, `internal` est idéal pour cacher du code (empêcher son utilisation en dehors de votre projet), tandis que `pkg` est utile pour organiser des bibliothèques publiques dans de plus grands projets. Cependant, ce ne sont pas des règles absolues, et la meilleure structure dépendra des besoins spécifiques et des préférences de l'équipe de développement.

### pkg

Dans votre organisation, l'utilisation du dossier `pkg` dans le contexte d'un projet Go peut être guidée par plusieurs facteurs et besoins organisationnels :

1. **Réutilisabilité :** Si vous avez des bibliothèques ou du code que vous prévoyez de réutiliser à travers plusieurs paquets ou services au sein de votre organisation, les placer dans `pkg` peut être une bonne pratique. Cela indique clairement que le code est destiné à être importé par d'autres parties du projet.

2. **Clarté et Organisation :** Pour les grands projets avec de nombreuses parties mobiles, utiliser `pkg` peut aider à distinguer le code qui constitue votre API publique interne ou vos bibliothèques partagées, par opposition aux commandes spécifiques (`cmd`) et au code interne qui ne doit pas être réutilisé (`internal`).

3. **Convention et Standards :** Si votre organisation a adopté des standards ou des conventions qui incluent l'utilisation de `pkg`, suivre ces conventions peut aider à maintenir la cohérence et à faciliter l'intégration de nouveaux développeurs dans l'équipe.

4. **Séparation des Préoccupations :** Quand il y a une séparation claire entre le code qui est spécifiquement destiné à l'application (`cmd` et `internal`) et les bibliothèques ou paquets qui peuvent être utilisés par plusieurs applications ou services.

5. **Evolutivité :** Si votre organisation prévoit de rendre certains paquets open-source ou de les partager entre différents projets, les placer dans `pkg` pourrait faciliter le processus de découplage plus tard.

6. **Préférences de l'Equipe :** Parfois, l'utilisation de `pkg` peut être une préférence de l'équipe basée sur leur expérience précédente ou leur confort avec une certaine structure de projet.

En résumé, vous pourriez décider d'utiliser `pkg` dans votre organisation lorsque vous avez du code qui est destiné à être largement partagé et réutilisé au sein de multiples projets, tout en restant ouvert à la possibilité de devenir public ou open-source à l'avenir. C'est une façon de signaler aux développeurs de votre équipe et aux utilisateurs potentiels du projet que tout ce qui se trouve dans `pkg` est conçu pour être un point d'intégration stable.
