# Cours : Notions fondamentales sur l'encodage et la manipulation des données en Go

- [Cours : Notions fondamentales sur l'encodage et la manipulation des données en Go](#cours--notions-fondamentales-sur-lencodage-et-la-manipulation-des-données-en-go)
  - [Introduction](#introduction)
  - [Chapitre 1 : Comprendre l'encodage](#chapitre-1--comprendre-lencodage)
    - [1.1 Qu'est-ce que l'encodage?](#11-quest-ce-que-lencodage)
    - [1.2 Windows-1252 : Un encodage populaire](#12-windows-1252--un-encodage-populaire)
    - [1.3 Comment fonctionne l'encodage en Go?](#13-comment-fonctionne-lencodage-en-go)
    - [1.4 Importance de choisir le bon encodage](#14-importance-de-choisir-le-bon-encodage)
    - [Conclusion du Chapitre 1](#conclusion-du-chapitre-1)
  - [Chapitre 2 : La manipulation de chaînes en Go](#chapitre-2--la-manipulation-de-chaînes-en-go)
    - [2.1 Introduction aux chaînes en Go](#21-introduction-aux-chaînes-en-go)
    - [2.2 La bibliothèque `strings`](#22-la-bibliothèque-strings)
      - [2.2.1 Diviser une chaîne : `strings.Split`](#221-diviser-une-chaîne--stringssplit)
      - [2.2.2 Enlever les espaces superflus : `strings.TrimSpace`](#222-enlever-les-espaces-superflus--stringstrimspace)
    - [2.3 Convertir des chaînes en octets et vice-versa](#23-convertir-des-chaînes-en-octets-et-vice-versa)
      - [2.3.1 Convertir une chaîne en slice d'octets](#231-convertir-une-chaîne-en-slice-doctets)
      - [2.3.2 Convertir une slice d'octets en chaîne](#232-convertir-une-slice-doctets-en-chaîne)
    - [2.4 Quelques autres fonctions utiles de la bibliothèque `strings`](#24-quelques-autres-fonctions-utiles-de-la-bibliothèque-strings)
      - [2.4.1 Rechercher une sous-chaîne : `strings.Contains`](#241-rechercher-une-sous-chaîne--stringscontains)
      - [2.4.2 Remplacer des sous-chaînes : `strings.Replace`](#242-remplacer-des-sous-chaînes--stringsreplace)
      - [2.4.3 Convertir en majuscules ou en minuscules : `strings.ToUpper` et `strings.ToLower`](#243-convertir-en-majuscules-ou-en-minuscules--stringstoupper-et-stringstolower)
    - [2.5 Conclusion](#25-conclusion)
  - [Chapitre 3 : Les tampons (Buffers) en Go](#chapitre-3--les-tampons-buffers-en-go)
    - [3.1 Qu'est-ce qu'un tampon (Buffer)?](#31-quest-ce-quun-tampon-buffer)
    - [3.2 Création d'un tampon](#32-création-dun-tampon)
    - [3.3 Écriture dans un tampon](#33-écriture-dans-un-tampon)
    - [3.4 Lecture d'un tampon](#34-lecture-dun-tampon)
    - [3.5 Autres opérations utiles](#35-autres-opérations-utiles)
    - [3.6 Cas d'utilisation](#36-cas-dutilisation)
      - [Traitement de fichiers](#traitement-de-fichiers)
      - [Construction de chaînes](#construction-de-chaînes)
    - [Conclusion chapitre 3](#conclusion-chapitre-3)
  - [Chapitre 4 : Lire et écrire des flux de données avec `io.Reader` et `io.Writer`](#chapitre-4--lire-et-écrire-des-flux-de-données-avec-ioreader-et-iowriter)
    - [4.1 Les interfaces fondamentales : `io.Reader` et `io.Writer`](#41-les-interfaces-fondamentales--ioreader-et-iowriter)
      - [4.1.1 `io.Reader`](#411-ioreader)
      - [4.1.2 `io.Writer`](#412-iowriter)
    - [4.2 Cas d'utilisation courants](#42-cas-dutilisation-courants)
      - [4.2.1 Lire un fichier](#421-lire-un-fichier)
      - [4.2.2 Écrire dans un fichier](#422-écrire-dans-un-fichier)
      - [4.2.3 Copier des données](#423-copier-des-données)
    - [4.3 Entrée et sortie standard : `os.Stdin` et `os.Stdout`](#43-entrée-et-sortie-standard--osstdin-et-osstdout)
      - [4.3.1 `os.Stdin`](#431-osstdin)
        - [Parenthèse - Buffer niveau OS](#parenthèse---buffer-niveau-os)
        - [Parenthèse - Golang buffer bloquant/non bloquant](#parenthèse---golang-buffer-bloquantnon-bloquant)
          - [1. Mode Bloquant](#1-mode-bloquant)
          - [2. Mode Non Bloquant](#2-mode-non-bloquant)
      - [4.3.2 `os.Stdout`](#432-osstdout)
    - [4.4 Combinaison de `Reader` et `Writer`](#44-combinaison-de-reader-et-writer)
    - [Conclusion chapitre 4](#conclusion-chapitre-4)
  - [Chapitre 5 : Application pratique - Encodage et manipulation de données](#chapitre-5--application-pratique---encodage-et-manipulation-de-données)
    - [5.1 Encodage en Windows-1252](#51-encodage-en-windows-1252)
    - [5.2 Manipulation des flux de données avec `io.Reader` et `io.Writer`](#52-manipulation-des-flux-de-données-avec-ioreader-et-iowriter)
    - [5.3 Cas d'utilisation : Transformation de données CSV](#53-cas-dutilisation--transformation-de-données-csv)
    - [Conclusion du chapitre 5](#conclusion-du-chapitre-5)
  - [Conclusion générale](#conclusion-générale)

## Introduction

L'univers du développement logiciel est vaste et varié, et Go, en tant que langage de programmation, offre un ensemble robuste d'outils pour gérer et manipuler des données. Dans ce cours, nous plongerons dans le monde de l'encodage des données, de la manipulation des chaînes de caractères et des flux de données en Go. Que vous soyez un débutant curieux ou un expert cherchant à approfondir vos connaissances, ce cours est fait pour vous.

## Chapitre 1 : Comprendre l'encodage

L'encodage est un concept fondamental en informatique, car il permet de représenter, stocker et transférer des informations sous forme de séquences d'octets. Pour comprendre son importance, prenons l'exemple de la lecture d'un texte dans différentes langues. Sans le bon encodage, les caractères peuvent apparaître déformés ou inintelligibles.

### 1.1 Qu'est-ce que l'encodage?

À la base, les ordinateurs ne comprennent que les chiffres : 0 et 1. Chaque bit peut être soit un 0 soit un 1. L'encodage est le processus qui convertit les données en une séquence de ces bits. Par exemple, en ASCII, la lettre "A" est encodée par le nombre 65 ou `01000001` en binaire.

L'encodage est crucial car il permet :

1. **Représentation** : Comment les données sont stockées.
2. **Interprétation** : Comment les données sont lues et comprises.
3. **Transmission** : Comment les données sont envoyées et reçues entre les systèmes.

### 1.2 Windows-1252 : Un encodage populaire

Windows-1252, parfois appelé simplement "ANSI", est une page de code largement utilisée pour les langues occidentales. Elle a été développée par Microsoft pour Windows.

**Caractéristiques clés**:

- Supporte la majorité des caractères utilisés dans les langues occidentales.
- Ressemble à ISO-8859-1 mais contient des caractères supplémentaires entre 128 et 159, là où ISO-8859-1 a des caractères de contrôle.
- Diffère de l'UTF-8, qui est un encodage universel capable de représenter tous les caractères de tous les scripts du monde.

**Cas d'utilisation**:

Imaginons que vous receviez un fichier texte d'une ancienne application Windows qui stocke des noms. Certains noms ont des caractères spéciaux, comme "Müller" ou "Françoise". Si ce fichier est encodé en Windows-1252, lire le fichier avec un autre encodage comme UTF-8 pourrait déformer ces caractères spéciaux.

### 1.3 Comment fonctionne l'encodage en Go?

En Go, la bibliothèque `golang.org/x/text/encoding/charmap` fournit des encodeurs et des décodeurs pour différents encodages, dont Windows-1252.

**Exemple** :

```go
import (
 "bytes"
 "golang.org/x/text/encoding/charmap"
 "log"
)

func encodeToWindows1252(input string) []byte {
 buf := &bytes.Buffer{}
 writer := charmap.Windows1252.NewEncoder().Writer(buf)
 _, err := writer.Write([]byte(input))
 if err != nil {
  log.Fatal(err)
 }
 return buf.Bytes()
}

func main() {
 data := encodeToWindows1252("Müller")
 // Utilisez ces données comme vous le souhaitez, par exemple pour les écrire dans un fichier.
}
```

Dans cet exemple, la fonction `encodeToWindows1252` prend une chaîne, l'encode en Windows-1252 et renvoie les données encodées comme une slice d'octets.

### 1.4 Importance de choisir le bon encodage

Si vous choisissez le mauvais encodage pour lire des données, les résultats peuvent être déroutants. Des caractères peuvent apparaître comme des symboles étranges, ou même des questions "?" signifiant que l'encodage utilisé ne peut pas représenter le caractère donné.

**Conseil**: Si vous n'êtes pas sûr de l'encodage d'une source de données, des outils et des bibliothèques peuvent vous aider à le détecter. Mais dans la plupart des cas, la meilleure approche est d'avoir une documentation ou une communication claire avec la source des données.

### Conclusion du Chapitre 1

L'encodage est la pierre angulaire de la représentation des données dans les systèmes informatiques. Choisir le bon encodage et comprendre comment les données sont encodées est essentiel pour garantir que les informations sont correctement représentées, stockées et transmises.

## Chapitre 2 : La manipulation de chaînes en Go

Les chaînes de caractères, ou `strings`, sont l'un des types de données fondamentaux dans presque tous les langages de programmation, et Go ne fait pas exception à cette règle. Dans ce chapitre, nous allons explorer les différentes manières de manipuler des chaînes en Go, en utilisant la bibliothèque `strings`.

### 2.1 Introduction aux chaînes en Go

En Go, une chaîne est une séquence immuable de bytes. C'est important à noter : une fois qu'une chaîne est définie, elle ne peut pas être modifiée.

```go
s := "Bonjour"
fmt.Println(s) // "Bonjour"
```

### 2.2 La bibliothèque `strings`

La bibliothèque `strings` fournit des fonctions pour manipuler des chaînes de caractères.

#### 2.2.1 Diviser une chaîne : `strings.Split`

Cette fonction divise une chaîne en une slice de sous-chaînes basée sur un séparateur donné.

```go
data := "a,b,c"
parts := strings.Split(data, ",")
fmt.Println(parts) // [a b c]
```

#### 2.2.2 Enlever les espaces superflus : `strings.TrimSpace`

Elle supprime les espaces au début et à la fin d'une chaîne.

```go
data := "  espace avant et après  "
cleaned := strings.TrimSpace(data)
fmt.Println(cleaned) // "espace avant et après"
```

### 2.3 Convertir des chaînes en octets et vice-versa

Les chaînes en Go sont, en coulisses, représentées comme des séquences d'octets. Ainsi, il est souvent nécessaire de convertir une chaîne en slice d'octets et vice versa.

#### 2.3.1 Convertir une chaîne en slice d'octets

```go
str := "GoLang"
byteSlice := []byte(str)
fmt.Println(byteSlice) // [71 111 76 97 110 103]
```

#### 2.3.2 Convertir une slice d'octets en chaîne

```go
byteSlice := []byte{71, 111, 76, 97, 110, 103}
str := string(byteSlice)
fmt.Println(str) // "GoLang"
```

### 2.4 Quelques autres fonctions utiles de la bibliothèque `strings`

#### 2.4.1 Rechercher une sous-chaîne : `strings.Contains`

Vérifie si une chaîne en contient une autre.

```go
str := "Bonjour le monde"
result := strings.Contains(str, "monde")
fmt.Println(result) // true
```

#### 2.4.2 Remplacer des sous-chaînes : `strings.Replace`

```go
str := "Bonjour le monde"
newStr := strings.Replace(str, "monde", "univers", 1)
fmt.Println(newStr) // "Bonjour le univers"
```

#### 2.4.3 Convertir en majuscules ou en minuscules : `strings.ToUpper` et `strings.ToLower`

```go
str := "GoLang"
fmt.Println(strings.ToUpper(str)) // "GOLANG"
fmt.Println(strings.ToLower(str)) // "golang"
```

### 2.5 Conclusion

Manipuler des chaînes de caractères est un besoin fondamental en programmation. Go, grâce à sa bibliothèque `strings`, offre une multitude de fonctions pour traiter efficacement et facilement ces opérations. Que ce soit pour diviser, nettoyer, rechercher ou remplacer, vous avez tous les outils nécessaires pour gérer les chaînes de caractères en Go.

## Chapitre 3 : Les tampons (Buffers) en Go

Dans ce chapitre, nous allons explorer le concept de tampons (buffers) en Go. Les tampons sont essentiels pour la manipulation efficace de séquences d'octets. Le package `bytes` de Go fournit des outils pour travailler avec ces structures.

### 3.1 Qu'est-ce qu'un tampon (Buffer)?

Un tampon est une structure qui permet de stocker temporairement des données, souvent avant qu'elles ne soient écrites dans un autre endroit ou avant qu'elles ne soient traitées d'une manière ou d'une autre. En Go, un `Buffer` est une séquence d'octets dans la mémoire.

L'avantage de l'utilisation d'un tampon est qu'il permet des opérations d'écriture et de lecture efficaces sans avoir à interagir directement avec, par exemple, un disque ou un réseau, ce qui serait plus lent.

### 3.2 Création d'un tampon

En Go, un nouveau tampon est généralement créé en utilisant la fonction `NewBuffer` ou simplement en initialisant une nouvelle instance de `Buffer` de la bibliothèque `bytes`.

```go
var buf bytes.Buffer
```

ou

```go
data := []byte("initial content")
buf := bytes.NewBuffer(data)
```

### 3.3 Écriture dans un tampon

La méthode `Write` est utilisée pour écrire des données dans un tampon. Elle prend un `[]byte` comme argument et ajoute ces octets à la fin du tampon.

```go
buf.Write([]byte("Hello, "))
buf.Write([]byte("World!"))
fmt.Println(buf.String()) // Affiche : "Hello, World!"
```

### 3.4 Lecture d'un tampon

La méthode `Read` est utilisée pour lire des données depuis un tampon. Elle supprime les données lues du tampon.

```go
data := make([]byte, 5)
buf.Read(data)
fmt.Println(string(data)) // Affiche : "Hello"
```

Après cette opération, seulement ", World!" reste dans le tampon.

### 3.5 Autres opérations utiles

- `buf.Bytes()`: Renvoie une slice d'octets avec le contenu actuel du tampon sans le supprimer.
- `buf.String()`: Convertit le contenu actuel du tampon en une chaîne.
- `buf.Len()`: Renvoie le nombre d'octets non lus dans le tampon.
- `buf.Reset()`: Vide le tampon.

### 3.6 Cas d'utilisation

#### Traitement de fichiers

Lorsque vous lisez un petit fichier et que vous souhaitez effectuer des manipulations sur son contenu, vous pouvez utiliser un tampon pour stocker et traiter le fichier.

```go
fileData, _ := ioutil.ReadFile("myfile.txt")
buf := bytes.NewBuffer(fileData)
```

#### Construction de chaînes

Lors de la construction de chaînes, en particulier lorsqu'il s'agit de nombreuses petites opérations d'ajout, utiliser un `Buffer` peut être plus efficace que la concaténation de chaînes.

```go
var buf bytes.Buffer
for _, word := range []string{"Go", "is", "awesome!"} {
 buf.WriteString(word)
 buf.WriteByte(' ')
}
fmt.Println(buf.String())
```

### Conclusion chapitre 3

Le tampon est un outil essentiel pour traiter efficacement des séquences d'octets en Go. Grâce à sa flexibilité et à ses performances, il est largement utilisé pour la manipulation de chaînes, la lecture/écriture de fichiers et bien d'autres cas d'utilisation dans les applications Go.

## Chapitre 4 : Lire et écrire des flux de données avec `io.Reader` et `io.Writer`

L'interface est un concept central en Go. Parmi les interfaces les plus utilisées, `io.Reader` et `io.Writer` se distinguent comme des fondations pour la manipulation des flux de données. Quand on parle de "flux de données", on fait référence à un ensemble séquentiel de données qui peut être lu ou écrit.

### 4.1 Les interfaces fondamentales : `io.Reader` et `io.Writer`

#### 4.1.1 `io.Reader`

L'interface `io.Reader` est probablement l'une des interfaces les plus influentes de Go. Elle présente une seule méthode :

```go
Read(p []byte) (n int, err error)
```

Tout type qui implémente cette méthode satisfait l'interface `io.Reader`. Elle tente de remplir le slice d'octets fourni (`p`) et renvoie le nombre d'octets lus (`n`) ainsi que toute erreur rencontrée.

#### 4.1.2 `io.Writer`

`io.Writer` est l'interface complémentaire de `io.Reader`. Elle est définie comme :

```go
Write(p []byte) (n int, err error)
```

Tout comme avec `io.Reader`, n'importe quel type qui implémente cette méthode satisfait l'interface `io.Writer`. Elle tente d'écrire le slice d'octets fourni (`p`) et renvoie le nombre d'octets écrits (`n`) ainsi que toute erreur rencontrée.

### 4.2 Cas d'utilisation courants

De nombreux types en Go satisfont ces interfaces, notamment les fichiers, les tampons, les connexions réseau et d'autres. Cela permet une grande modularité et réutilisabilité.

#### 4.2.1 Lire un fichier

```go
file, err := os.Open("monFichier.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

data := make([]byte, 100)
n, err := file.Read(data)
if err != nil {
    log.Fatal(err)
}
fmt.Println(string(data[:n]))
```

#### 4.2.2 Écrire dans un fichier

```go
file, err := os.Create("monFichier.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

n, err := file.Write([]byte("Bonjour, monde!"))
if err != nil {
    log.Fatal(err)
}
fmt.Printf("%d octets écrits\n", n)
```

#### 4.2.3 Copier des données

La bibliothèque `io` fournit une fonction `Copy` qui utilise à la fois `Reader` et `Writer` :

```go
srcFile, _ := os.Open("source.txt")
destFile, _ := os.Create("destination.txt")
defer srcFile.Close()
defer destFile.Close()

bytesCopied, _ := io.Copy(destFile, srcFile)
fmt.Printf("%d octets copiés\n", bytesCopied)
```

### 4.3 Entrée et sortie standard : `os.Stdin` et `os.Stdout`

#### 4.3.1 `os.Stdin`

`os.Stdin` est une instance globale de type `*os.File` qui représente l'entrée standard de votre programme. Elle est typiquement utilisée pour lire des données directement depuis le clavier ou depuis une redirection.

**Exemple :** Lire une ligne depuis l'entrée standard :

```go
reader := bufio.NewReader(os.Stdin)
fmt.Print("Entrez du texte : ")
text, _ := reader.ReadString('\n')
fmt.Println("Vous avez écrit :", text)
```

##### Parenthèse - Buffer niveau OS

La fonctionnalité de blocage, en particulier lors de la lecture de l'entrée de l'utilisateur ou d'autres sources de données, est généralement implémentée au niveau du système d'exploitation. Voici une explication détaillée de la manière dont cela fonctionne :

1. **Appels système**:

   Lorsqu'un programme souhaite lire des données, par exemple depuis `stdin`, il effectue un appel système. Un appel système est une interface permettant à un programme de demander un service au noyau du système d'exploitation.

2. **Noyau et descripteurs de fichier**:

   Dans la plupart des systèmes d'exploitation de type UNIX, tout est traité comme un fichier, y compris `stdin`. Lorsqu'un programme demande à lire depuis `stdin`, il demande en réalité à lire depuis un descripteur de fichier qui est associé à `stdin`.

3. **État de blocage**:

   Si les données demandées ne sont pas encore disponibles (par exemple, si l'utilisateur n'a pas encore appuyé sur "Entrée"), le noyau met le processus en état de "blocage" ou "sommeil". Cela signifie que le processus est mis en pause et n'utilise pas activement le CPU.

4. **Réveil du processus**:

   Lorsque les données deviennent disponibles (par exemple, lorsque l'utilisateur appuie sur "Entrée"), le noyau réveille le processus. Le programme reprend son exécution à partir du point où il s'était arrêté (après l'appel système) et peut maintenant lire les données disponibles.

5. **Mode non bloquant**:

   Il est également possible de configurer des descripteurs de fichier pour qu'ils fonctionnent en mode non bloquant. Dans ce mode, si les données ne sont pas disponibles, l'appel système renverra immédiatement une erreur plutôt que de bloquer. Cela peut être utile pour des applications qui doivent effectuer d'autres tâches en attendant les données.

6. **Multiplexage d'entrée/sortie**:

   Dans des situations où un programme doit surveiller plusieurs sources de données simultanément (par exemple, plusieurs connexions réseau), des techniques de multiplexage d'entrée/sortie comme `select()`, `poll()`, ou `epoll()` (sur Linux) peuvent être utilisées. Ces fonctions permettent à un programme de surveiller plusieurs descripteurs de fichier simultanément et de déterminer lesquels sont prêts pour la lecture ou l'écriture sans blocage.

En résumé, le blocage lors de la lecture est géré par le noyau du système d'exploitation. Lorsqu'un programme demande à lire des données et que ces données ne sont pas encore disponibles, le noyau met le programme en état de blocage jusqu'à ce que les données soient prêtes. Cette approche permet d'économiser les ressources CPU, car le programme n'est pas en train de "tourner en boucle" activement en attendant les données.

##### Parenthèse - Golang buffer bloquant/non bloquant

Le langage Go (ou Golang) offre une prise en charge native de la concurrence grâce aux goroutines, ce qui permet d'implémenter facilement des scénarios bloquants et non bloquants. Lorsqu'il s'agit de lire des buffers ou d'autres opérations d'entrée/sortie, Go utilise un modèle de blocage par défaut, mais avec l'utilisation des goroutines, on peut facilement créer des scénarios non bloquants.

###### 1. Mode Bloquant

Dans cet exemple, nous utilisons la fonction `ReadString` de la bibliothèque `bufio` pour lire une ligne de `os.Stdin`. Cette fonction bloquera jusqu'à ce qu'elle rencontre un `\n` (lorsque vous appuyez sur "Entrée") :

```go
package main

import (
 "bufio"
 "fmt"
 "os"
)

func main() {
 reader := bufio.NewReader(os.Stdin)
 fmt.Print("Entrez quelque chose : ")
 text, _ := reader.ReadString('\n')
 fmt.Printf("Vous avez écrit : %s", text)
}
```

Lorsque vous exécutez ce programme, il attendra en mode bloquant que vous entriez une ligne de texte.

###### 2. Mode Non Bloquant

Dans cet exemple, nous utilisons les goroutines pour lire de `os.Stdin` de manière non bloquante. Cela signifie que le programme principal peut continuer à s'exécuter pendant que nous attendons une entrée:

```go
package main

import (
 "bufio"
 "fmt"
 "os"
 "time"
)

func readInput(output chan<- string) {
 reader := bufio.NewReader(os.Stdin)
 fmt.Print("Entrez quelque chose : ")
 text, _ := reader.ReadString('\n')
 output <- text
}

func main() {
 inputChannel := make(chan string)

 go readInput(inputChannel)

 select {
 case text := <-inputChannel:
  fmt.Printf("Vous avez écrit : %s", text)
 case <-time.After(5 * time.Second):
  fmt.Println("Temps écoulé! Aucune entrée reçue.")
 }
}
```

Lorsque vous exécutez ce programme, il attendra une entrée pendant 5 secondes. Si vous entrez quelque chose en moins de 5 secondes, il affichera le texte. Sinon, il affichera "Temps écoulé! Aucune entrée reçue." et se terminera.

Dans cet exemple, nous utilisons une goroutine pour lire l'entrée et un `select` avec un timer pour créer un délai d'expiration. C'est un exemple de la manière dont Go peut être utilisé pour créer un comportement non bloquant tout en conservant un code relativement simple et clair.

#### 4.3.2 `os.Stdout`

Tout comme `os.Stdin` représente l'entrée standard, `os.Stdout` représente la sortie standard. Il est souvent utilisé pour écrire des données directement dans la console.

**Exemple :** Écrire dans la sortie standard :

```go
io.WriteString(os.Stdout, "Ceci est un message pour la sortie standard!\n")
```

### 4.4 Combinaison de `Reader` et `Writer`

Les interfaces `io.Reader` et `io.Writer` peuvent être combinées de manière puissante pour créer des chaînes de traitement de données.

**Exemple :** Convertir des données en majuscules lors de la copie :

```go
func ToUpperReader(r io.Reader) io.Reader {
    return &upperReader{r}
}

type upperReader struct {
    src io.Reader
}

func (u *upperReader) Read(p []byte) (int, error) {
    n, err := u.src.Read(p)
    for i := 0; i < n; i++ {
        p[i] = byte(unicode.ToUpper(rune(p[i])))
    }
    return n, err
}

func main() {
    src := strings.NewReader("Ceci est un test.")
    dst := ToUpperReader(src)
    io.Copy(os.Stdout, dst)
}
```

Ce programme lira la chaîne "Ceci est un test.", la convertira en "CECI EST UN TEST.", puis écrira le résultat dans la sortie standard.

### Conclusion chapitre 4

Les interfaces `io.Reader` et `io.Writer` sont des outils puissants et flexibles en Go qui permettent de manipuler des flux de données de manière efficace. Grâce à leur simplicité et à leur universalité, elles forment la base de nombreuses opérations d'entrée/sortie en Go, de la lecture et de l'écriture de fichiers à la manipulation de flux de données en temps réel.

## Chapitre 5 : Application pratique - Encodage et manipulation de données

La compréhension des concepts est renforcée lorsqu'elle est mise en application. Dans ce chapitre, nous plongerons dans l'encodage spécifique Windows-1252, l'utilisation de tampons, et la manipulation de flux de données avec `io.Reader` et `io.Writer` en Go. Nous utiliserons des fonctions spécifiques comme exemples pour illustrer ces concepts.

### 5.1 Encodage en Windows-1252

**Pourquoi Windows-1252?**

Bien que l'UTF-8 soit de nos jours le standard d'encodage universel des caractères, Windows-1252 a longtemps été le choix privilégié, en particulier pour les applications Windows plus anciennes. Il est donc parfois nécessaire de travailler avec cet encodage, surtout lorsqu'il s'agit de données plus anciennes ou d'intégrations avec des systèmes hérités.

**Comment encoder en Windows-1252 en Go?**

En Go, la bibliothèque `golang.org/x/text/encoding/charmap` offre des méthodes pour encoder et décoder en Windows-1252. Voici comment cela fonctionne à l'aide d'une fonction illustrative:

```go
// Importation des packages nécessaires
import (
 "bytes"
 "log"
 "golang.org/x/text/encoding/charmap"
)

// encodeWindows1252 prend une chaîne en entrée et la convertit en Windows-1252
func encodeWindows1252(input string) *bytes.Reader {
 // Initialisation d'un tampon pour stocker les données encodées
 buf := &bytes.Buffer{}
 
 // Création d'un nouvel encodeur Windows-1252
 writer := charmap.Windows1252.NewEncoder().Writer(buf)
 
 // Écriture de la chaîne d'entrée dans le tampon en utilisant l'encodeur
 _, err := writer.Write([]byte(input))
 if err != nil {
  log.Println(err) // Affichage d'une erreur si elle se produit
 }
 
 // Retourne un Reader pour les données encodées
 return bytes.NewReader(buf.Bytes())
}
```

L'essence de cette fonction est de convertir une chaîne en son équivalent Windows-1252. L'utilisation d'un `bytes.Buffer` facilite la manipulation des données en mémoire.

### 5.2 Manipulation des flux de données avec `io.Reader` et `io.Writer`

L'interface `io.Reader` est un outil central en Go pour la lecture de données depuis n'importe quelle source implémentant cette interface. Similairement, `io.Writer` est utilisé pour écrire des données vers une quelconque destination.

**Exemple avec la fonction `run`**:

`run(src io.Reader, dst io.Writer)` illustre parfaitement la polyvalence de ces interfaces. Elle prend des données depuis une source (`src`), éventuellement les traite, puis les réachemine vers une destination (`dst`).

Dans l'appel `run(os.Stdin, os.Stdout)`, `os.Stdin` est utilisé comme source (ce qui signifie une lecture depuis l'entrée standard, comme le clavier) et `os.Stdout` comme destination (pour écrire vers la console). La beauté de cette approche réside dans sa flexibilité : tant que les objets satisfont les interfaces `io.Reader` et `io.Writer`, la fonction peut traiter différents types de sources et de destinations, qu'il s'agisse de fichiers, de tampons, de connexions réseau, etc.

### 5.3 Cas d'utilisation : Transformation de données CSV

Supposez que vous ayez un fichier CSV où les données sont séparées par des `|`. Vous voulez le retraiter pour enlever certains en-têtes et reformater les données. L'utilisation des flux de données serait parfaite pour une telle tâche.

```go
package main

import (
 "bufio"
 "fmt"
 "io"
 "log"
 "os"
 "strings"
)

func main() {
 // Ouverture du fichier CSV en lecture
 file, err := os.Open("data.csv")
 if err != nil {
  log.Fatalf("Erreur à l'ouverture de data.csv: %v", err)
 }
 defer closeFile(file, "data.csv")

 // Ouverture (ou création) d'un fichier en écriture pour le résultat
 outFile, err := os.Create("transformed.csv")
 if err != nil {
  log.Fatalf("Erreur à la création de transformed.csv: %v", err)
 }
 defer closeFile(outFile, "transformed.csv")

 // Utilisation de la fonction `run` pour transformer le fichier
 if err := run(file, outFile); err != nil {
  log.Fatalf("Erreur lors de la transformation : %v", err)
 }
}

// closeFile est une fonction utilitaire pour fermer un fichier et loguer une erreur
func closeFile(f *os.File, filename string) {
 if err := f.Close(); err != nil {
  log.Printf("Erreur à la fermeture du fichier %s: %v", filename, err)
 }
}

// run lit le contenu de src, effectue une transformation, puis écrit le résultat dans dst
func run(src io.Reader, dst io.Writer) error {
 scanner := bufio.NewScanner(src)
 writer := bufio.NewWriter(dst)

 // Suppression de la première ligne (supposition : c'est un en-tête)
 if !scanner.Scan() {
  if err := scanner.Err(); err != nil {
   return fmt.Errorf("Erreur à la lecture de l'en-tête: %v", err)
  }
  // si l'en-tête est manquant ou le fichier est vide
  return fmt.Errorf("Fichier source vide ou manquant d'en-tête")
 }

 // Parcours et transformation des lignes suivantes
 for scanner.Scan() {
  line := scanner.Text()

  // Validation (ajoutez plus de validations selon vos besoins)
  if line == "" {
   continue // sauter les lignes vides
  }

  // Remplacement des séparateurs | par des ,
  transformedLine := strings.ReplaceAll(line, "|", ",")

  // Écriture de la ligne transformée dans le fichier de destination
  if _, err := writer.WriteString(transformedLine + "\n"); err != nil {
   return fmt.Errorf("Erreur à l'écriture de la ligne transformée : %v", err)
  }
 }

 // Gestion des erreurs de scanner
 if err := scanner.Err(); err != nil {
  return fmt.Errorf("Erreur à la lecture du fichier source: %v", err)
 }

 // Assurez-vous que tout est écrit dans dst
 if err := writer.Flush(); err != nil {
  return fmt.Errorf("Erreur lors de la finalisation de l'écriture : %v", err)
 }

 return nil
}

```

En utilisant l'exemple ci-dessus, le contenu de `data.csv` est lu, transformé et le résultat est sauvegardé dans `transformed.csv`.

---

Il serait également possible d'utiliser les redirections d'entrée/sortie standard du shell pour exécuter votre programme.
Si vous voulez utiliser cette méthode, il y aurait quelques ajustements à faire dans votre code pour qu'il lise de l'entrée standard et écrive sur la sortie standard. Voici comment :

1. Dans la fonction `main`, au lieu d'ouvrir `data.csv` avec `os.Open`, vous utiliserez `os.Stdin` comme source de données.
2. Au lieu de créer `transformed.csv` avec `os.Create`, vous utiliserez `os.Stdout` comme destination de sortie.

```go
package main

// ... (importations)

func main() {
    // Utilisation de la fonction `run` pour transformer les données
    if err := run(os.Stdin, os.Stdout); err != nil {
  log.Fatalf("Erreur lors de la transformation : %v", err)
 }
}

// ... (reste du code)
```

```bash
go run main.go <data.csv >transformed.csv
```

- `<data.csv` redirige le contenu du fichier `data.csv` vers l'entrée standard (`stdin`) de votre programme.
- `>transformed.csv` redirige la sortie standard (`stdout`) de votre programme vers le fichier `transformed.csv`.

N'oubliez pas que, dans ce cas, il n'est pas nécessaire de fermer `os.Stdin` ou `os.Stdout`, car ils seront automatiquement fermés lorsque votre programme se terminera.

### Conclusion du chapitre 5

En combinant les concepts d'encodage, de tampons et d'interfaces `io.Reader`/`io.Writer`, Go offre une grande flexibilité pour manipuler et transformer des données. En comprenant ces notions et en les mettant en pratique, vous serez mieux équipé pour traiter des scénarios réels complexes en matière de traitement de données.

## Conclusion générale

Le monde de l'encodage et de la manipulation des données en Go est riche et varié. Avec les outils et les concepts que nous avons explorés, vous êtes maintenant mieux équipé pour lire, écrire et transformer des données avec assurance et efficacité en Go.
