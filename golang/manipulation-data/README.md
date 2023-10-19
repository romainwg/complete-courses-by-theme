# Cours : Notions fondamentales sur l'encodage et la manipulation des données en Go

<!-- vscode-markdown-toc -->
* [Introduction](#introduction)
* [Chapitre 1 : Comprendre l'encodage](#Chapitre1:Comprendrelencodage)
  * [1.1 Qu'est-ce que l'encodage?](#Quest-cequelencodage)
  * [1.2 Windows-1252 : Un encodage populaire](#Windows-1252:Unencodagepopulaire)
  * [1.3 Comment fonctionne l'encodage en Go?](#CommentfonctionnelencodageenGo)
  * [1.4 Importance de choisir le bon encodage](#Importancedechoisirlebonencodage)
  * [Conclusion du Chapitre 1](#ConclusionduChapitre1)
* [Chapitre 2 : La manipulation de chaînes en Go](#Chapitre2:LamanipulationdechanesenGo)
  * [2.1 Introduction aux chaînes en Go](#IntroductionauxchanesenGo)
  * [2.2 La bibliothèque `strings`](#Labibliothquestrings)
    * [2.2.1 Diviser une chaîne : `strings.Split`](#Diviserunechane:strings.Split)
    * [2.2.2 Enlever les espaces superflus : `strings.TrimSpace`](#Enleverlesespacessuperflus:strings.TrimSpace)
  * [2.3 Convertir des chaînes en octets et vice-versa](#Convertirdeschanesenoctetsetvice-versa)
    * [2.3.1 Convertir une chaîne en slice d'octets](#Convertirunechaneenslicedoctets)
    * [2.3.2 Convertir une slice d'octets en chaîne](#Convertiruneslicedoctetsenchane)
  * [2.4 Quelques autres fonctions utiles de la bibliothèque `strings`](#Quelquesautresfonctionsutilesdelabibliothquestrings)
    * [2.4.1 Rechercher une sous-chaîne : `strings.Contains`](#Rechercherunesous-chane:strings.Contains)
    * [2.4.2 Remplacer des sous-chaînes : `strings.Replace`](#Remplacerdessous-chanes:strings.Replace)
    * [2.4.3 Convertir en majuscules ou en minuscules : `strings.ToUpper` et `strings.ToLower`](#Convertirenmajusculesouenminuscules:strings.ToUpperetstrings.ToLower)
  * [2.5 Conclusion](#Conclusion)
* [Chapitre 3 : Les tampons (Buffers) en Go](#Chapitre3:LestamponsBuffersenGo)
  * [3.1 Qu'est-ce qu'un tampon (Buffer)?](#Quest-cequuntamponBuffer)
  * [3.2 Création d'un tampon](#Crationduntampon)
  * [3.3 Écriture dans un tampon](#crituredansuntampon)
  * [3.4 Lecture d'un tampon](#Lectureduntampon)
  * [3.5 Autres opérations utiles](#Autresoprationsutiles)
  * [3.6 Cas d'utilisation](#Casdutilisation)
    * [Traitement de fichiers](#Traitementdefichiers)
    * [Construction de chaînes](#Constructiondechanes)
  * [Conclusion chapitre 3](#Conclusionchapitre3)
* [Chapitre 4 : Lire et écrire des flux de données avec `io.Reader` et `io.Writer`](#Chapitre4:Lireetcriredesfluxdedonnesavecio.Readeretio.Writer)
  * [4.1 Les interfaces fondamentales : `io.Reader` et `io.Writer`](#Lesinterfacesfondamentales:io.Readeretio.Writer)
    * [4.1.1 `io.Reader`](#io.Reader)
    * [4.1.2 `io.Writer`](#io.Writer)
  * [4.2 Cas d'utilisation courants](#Casdutilisationcourants)
    * [4.2.1 Lire un fichier](#Lireunfichier)
    * [4.2.2 Écrire dans un fichier](#criredansunfichier)
    * [4.2.3 Copier des données](#Copierdesdonnes)
  * [4.3 Entrée et sortie standard : `os.Stdin` et `os.Stdout`](#Entreetsortiestandard:os.Stdinetos.Stdout)
    * [4.3.1 `os.Stdin`](#os.Stdin)
    * [4.3.2 `os.Stdout`](#os.Stdout)
  * [4.4 Combinaison de `Reader` et `Writer`](#CombinaisondeReaderetWriter)
  * [Conclusion chapitre 4](#Conclusionchapitre4)
* [Chapitre 5 : Application pratique - Encodage et manipulation de données](#Chapitre5:Applicationpratique-Encodageetmanipulationdedonnes)
  * [5.1 Encodage en Windows-1252](#EncodageenWindows-1252)
  * [5.2 Manipulation des flux de données avec `io.Reader` et `io.Writer`](#Manipulationdesfluxdedonnesavecio.Readeretio.Writer)
  * [5.3 Cas d'utilisation : Transformation de données CSV](#Casdutilisation:TransformationdedonnesCSV)
  * [Conclusion du chapitre 5](#Conclusionduchapitre5)
* [Conclusion générale](#Conclusiongnrale)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=false
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

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

* Supporte la majorité des caractères utilisés dans les langues occidentales.
* Ressemble à ISO-8859-1 mais contient des caractères supplémentaires entre 128 et 159, là où ISO-8859-1 a des caractères de contrôle.
* Diffère de l'UTF-8, qui est un encodage universel capable de représenter tous les caractères de tous les scripts du monde.

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

* `buf.Bytes()`: Renvoie une slice d'octets avec le contenu actuel du tampon sans le supprimer.
* `buf.String()`: Convertit le contenu actuel du tampon en une chaîne.
* `buf.Len()`: Renvoie le nombre d'octets non lus dans le tampon.
* `buf.Reset()`: Vide le tampon.

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

Bien que l'UTF-8 soit désormais largement adopté pour l'encodage universel des caractères, Windows-1252 a été largement utilisé dans le passé, notamment pour les applications Windows. Lorsque nous traitons des données historiques ou interactuons avec des systèmes plus anciens, il peut être nécessaire de travailler avec cet encodage.

**Comment encoder en Windows-1252 en Go?**

En Go, la bibliothèque `golang.org/x/text/encoding/charmap` fournit des outils pour encoder/décoder en Windows-1252. Voici une fonction d'exemple:

```go
import (
 "bytes"
 "log"
 "golang.org/x/text/encoding/charmap"
)

func encodeWindows1252(input string) *bytes.Reader {
 buf := &bytes.Buffer{}
 writer := charmap.Windows1252.NewEncoder().Writer(buf)
 _, err := writer.Write([]byte(input))
 if err != nil {
  log.Println(err)
 }
 return bytes.NewReader(buf.Bytes())
}
```

Cette fonction utilise un tampon (`bytes.Buffer`) pour accumuler des données. L'encodeur Windows-1252 est utilisé pour écrire dans ce tampon. Enfin, la fonction renvoie un `bytes.Reader` contenant les données encodées.

### 5.2 Manipulation des flux de données avec `io.Reader` et `io.Writer`

L'interface `io.Reader` est l'un des outils les plus puissants de Go, car elle permet de lire des données depuis n'importe quelle source qui implémente cette interface. De même, `io.Writer` permet d'écrire des données vers n'importe quelle destination.

**Exemple de la fonction `run`**:

La fonction `run(src io.Reader, dst io.Writer)` est un exemple typique de la puissance de ces interfaces. Elle lit des données depuis une source (`src`), les transforme, puis les écrit dans une destination (`dst`).

L'utilisation de `os.Stdin` comme source (`src`) et `os.Stdout` comme destination (`dst`) dans `run(os.Stdin, os.Stdout)` est un cas courant qui signifie lire depuis l'entrée standard (clavier ou redirection) et écrire vers la sortie standard (console ou redirection).

La fonction `run` est flexible car elle peut fonctionner avec n'importe quelle source ou destination, tant qu'elles satisfont `io.Reader` et `io.Writer`. Cela pourrait être des fichiers, des tampons, des connexions réseau, etc.

### 5.3 Cas d'utilisation : Transformation de données CSV

Imaginez avoir un fichier CSV dont les données sont séparées par des `|` et que vous souhaitez le transformer pour enlever certains en-têtes et formater les données. Vous pourriez utiliser une fonction comme `run` pour cela.

```go
func main() {
    file, _ := os.Open("data.csv")
    defer file.Close()

    outFile, _ := os.Create("transformed.csv")
    defer outFile.Close()

    // Lire depuis `file`, écrire vers `outFile`
    run(file, outFile)
}
```

Ce code ouvre un fichier `data.csv`, puis transforme son contenu et écrit le résultat dans `transformed.csv` en utilisant la fonction `run`.

### Conclusion du chapitre 5

En combinant les concepts d'encodage, de tampons et d'interfaces `io.Reader`/`io.Writer`, Go offre une grande flexibilité pour manipuler et transformer des données. En comprenant ces notions et en les mettant en pratique, vous serez mieux équipé pour traiter des scénarios réels complexes en matière de traitement de données.

## Conclusion générale

Le monde de l'encodage et de la manipulation des données en Go est riche et varié. Avec les outils et les concepts que nous avons explorés, vous êtes maintenant mieux équipé pour lire, écrire et transformer des données avec assurance et efficacité en Go.
