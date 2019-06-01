# Syntax Swift

Swift est un langage de programmation objet compilé, multi-paradigmes ayant pour objectif d'être simple, haute-performance et sûr, il est développé en open source.

* Documentation officielle : https://docs.swift.org/
* Type de syntaxe : CameCase | SnakeCase

## Déclaration de variables

Swift supporte entre autres les types Int, Double, Float, Char, String et Bool.
L'inférence du type est automatique, mais il peut être précisé, le type inférencé est ensuite statique.

### Constantes

```
let variableA = 42
let variableB = "hello"

let variableA: Int = 42
let variableB: String = "hello"
```

### Variables

```
var variableA = 42
var variableB = "hello"
```

### Tuples

```
let typleA = (variableA, variableB)

// Récupération de toutes les valeurs
let (valeurA, valeurB) = tupleA

// Récupération partielle
let (valeurA, _) = tupleA

// Récupération de la première valeur
let valeurA = tupleA.0

// Comparaison de tuples de même taille et même élément
(1, "apple") < (2, "pear")
```

## Les opérateurs basiques

* Unaire : `+a`
  * Opérateur : `+`, `-`
  * Not : `!`
  * UnWrap : `!`
* Binaire : `a+b`
  * opération plus l'affectation : `+=`, `-=`, `*=`, `/=`
  * comparaison : `==`, `!=`, `>=`, `<=`, `===`, `!==`
  * logique : `&&`, `||`
* Ternaire (condition) : `a ? b : c`
* Null coalescing `??`
```
let prenom: String? = nil
let nickname = prenom ?? "toto"
```
* Liste
** Closed Range : `let closedRange = 1...5`
** One-Sided Range : `let oneSidedRange = ...5` 
** Half-Open Range : `let halfOpenRange = ..<5`



## Les structures de contrôles

### Les conditions

```
if prenom == "toto" {
  print("Bonjour toto")
} else {
  print("Bonjour ?")
}
```

### Les boucles

Tant que
```
var i = 0

while i < 10 {
  print("Hello World")
  i += 1
}
```

Faire Tant que
```
var i = 0
repeat {
  print("Hello world")
  i += 1
} while i < 10
```

for ... in
```
let liste1 = [1,2,3,4]
for element in list1 {
  print(element)
}
```

```
for element in 1..4{
  print(element)
}
```

```
for tickMark in stride(from: 0, to: 60, by: 5){
  print(tickMark)
}
```

### Le switch

```
let value = 10

switch value{
  case 1:
    print("Value is 1")
  case 2..5:
    print("Value is between 2 and 5")
  case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
  default :
    print("Value not found")
}
```

Il permet de faire le matching de tuple.

Plus complexe

```
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
```

Pas de `fallthrough` implicite, il existe les contrôles de transfert suivant :

* Continue
* Break
* Fallthrough
* Return
* Throw

### Guard / Les optionnels

```
func exemple() {
    var response: NSData?

    guard let data = response else {
        return
    }

    data.writeToFile("path/", atomically: true)
}
```

```
if testNumber != nil{
  return ""
}
```

```
var testScores = ["Dave": [86, 12, 23], "Bev": [79, 23, 54]]
testScores["Dave"]?[0] = 91
testScores["Steve"]?[0] = 99
```

Permet de tester si `response` est vide, et dans ce cas ajoute data, sinon sort de la fonction :
https://blog.nathanaelcherrier.com/fr/le-mot-cle-guard-en-swift-2-0/

## Manipulation de chaînes

```
var title = "Hello"
print(title[...title.startIndex])
```

### Concaténation

```
var s1 = "Hello"
var s2 = "world"

print(s1+s2)

s1 += s2

print(s1)
```

```
var welome = "hello"
welcome.insert("!", at: welcome.endIndex)
welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
```

```
welcome.remove(at: welcome.index(before: welcome.endIndex))
let range = welcome.index(welcome.endIndex, offsetBy: -6..<welcome.endIndex)
welcome.removeSubrange(range)
```

### Interpolation

```
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) *2.5)"
```

### HereDocument

```
let chaine2 = """
{"menu": {
  "id": "file",
  "value": "File",
  "popup": {
    "menuitem": [
      {"value": "New", "onclick": "CreateNewDoc()"},
      {"value": "Open", "onclick": "OpenDoc()"},
      {"value": "Close", "onclick": "CloseDoc()"}
    ]
  }
}}
"""
```

## Les collections

### Types

* `Array[int]`
* `Set[int]` Comme un `Array`sauf qu'une seule occurrence de chaque objet peut exister, pas de doublon.
* `Dictionnary[String:Int]`

### Opérations

```
a.intersection(b)
a.symmetricDifference(b)
a.union(b)
a.substracting(b)
```

## Les fonctions

### Déclaration

Procédure :
```
func sayHello(){
  print("Hello World")
}
```

Fonction :
```
func sayHello() -> bool{
  print("Hello World")
  return true
}
```

```
func sayHello() -> (Int, Int){
  print("Hello World")
  return (10, 15)
}
```

Et des paramètres
```
func sayHello(SomeThing: String){
  print("Hello " + SomeThing)
}
```

### Appel

Appel, on doit donner le nom de l'argument :
```
sayHello(SomeThing: "World")
```

On peut passer par des variants :
```
func sayHello(firstArgument SomeThing: String, secondArgument Final:String){
  print("Hello " + SomeThing + " " + Final)
}
```

```
sayHello(firstArgument: "World", secondArgument: "!")
```

Ou définitivement plus simple :
```
func sayHello(_ SomeThing: String, _ Final:String){
  print("Hello " + SomeThing + " " + Final)
}
```

```
sayHello("World", "!")
```

### Utilisation comme type

```
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}

var mathFunction: (Int, Int) -> Int = addTwoInts

print("Result: \(mathFunction(2, 3))")
// Prints "Result: 5"
```

### Closures

Faire une closure
```
{ (parameters) -> return type in
    statements
}
```
https://docs.swift.org/swift-book/LanguageGuide/Closures.html

Ceci :
```
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}

var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

Devient avec une closure :
```
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

Sur une seule ligne, avec inférence automatique des variables avec la procédure `sorted(by:)`.
Le type de retour peut être implicite également.
```
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

Le `return`est implicite :
```
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

Raccourci de nommage :
```
reversedNames = names.sorted(by: { $0 > $1 } )
```

Opérateur de comparaison de la classe `String`
```
reversedNames = names.sorted(by: >)
```

## Entrée utilisateur


Lire l'entrée utilisateur :

```
let response = readLine()
```

## Les énumérations

```
enum CompassPoint {
  case north
  case south
  case east
  case west
}
```

```
enum CompassPoint: Int {
  case north = 1
  case south = 2
  case east = 3
  case west = 4
}
```

```
let directionToHead: CompassPoint = .south
switch directionToHead {
  case .north:
    print("Lots of planet have a north")
}
```


## Les objets

### Vocabulaire

* Variable de classe, propriété de type : `static`
* Variable d'instance, propriété d'instance
* Propriété stockée par défaut pour les propriétés
* `Lazy` propriété pour ne charger que lors de l'accès


### Déclaration

```
class  Point{
  var x: Double = 0.0, y: Double = 0.0

  static var numberOfPointsInWorld: Int = 0
}
```

### Lazy

```
class DataImporter {
    /*
    DataImporter is a class to import data from an external file.
    The class is assumed to take a nontrivial amount of time to initialize.
    */
    var filename = "data.txt"
    // the DataImporter class would provide data importing functionality here
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // the DataManager class would provide data management functionality here
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// the DataImporter instance for the importer property has not yet been created
```

### Déclaration de propriétés

```
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}
```

### Observation des propriétés

```
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```

### Déclaration des méthodes :

Méthode statique

```
class Point{
  static func printMe(){
    print("Hello, I'm the point class")
  }
}
```

Constructeur

```
class Point{
  init(x: Double){
    pointX = x
  }
}
```

### Heritage

```
class Moto: Vehicule {
  init(){
    super.init()
  }

  override func avancer(){
    ...
  }
}
```

Modificateur d'accès : `open|public|internal|fileprivate|private`

### Interface

```
protocol SomeProtocol{

  var mustBeSettable: Int { get set }

  func random() -> Double
}

class SomeClass: SomeSuperClass, FirstProtocol, AnotherProcol {}
```

### SubScript

Le subscript en Swift, est une fonction instructive du comportement d'un accès type key/value sur un objet.

```
let monDico = ["a": 10, "b": 100]
print(monDico["a"])


subscript(index: Int) -> Int {
  get{}
  set(newvalue){}
}
```

## Type Casting

Exemple d'objets :

```
class Movie: MediaItem {
    var director: String
    init(name: String, director: String) {
        self.director = director
        super.init(name: name)
    }
}

class Song: MediaItem {
    var artist: String
    init(name: String, artist: String) {
        self.artist = artist
        super.init(name: name)
    }
}
```

### is

```
for item in library {
    if item is Movie {
        movieCount += 1
    } else if item is Song {
        songCount += 1
    }
}
```

### as

`as?` Permet de caster en `Movie` 

```
for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.name), dir. \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}
```

### any

```
var things = [Any]()

things.append(0)
things.append(0.0)
things.append(42)
things.append(3.14159)
things.append("hello")
things.append((3.0, 5.0))
things.append(Movie(name: "Ghostbusters", director: "Ivan Reitman"))
things.append({ (name: String) -> String in "Hello, \(name)" })

for thing in things {
    switch thing {
    case 0 as Int:
        print("zero as an Int")
    case 0 as Double:
        print("zero as a Double")
    case let someInt as Int:
```

### anyobject

Même chose que pour `any` mais avec des objets.

## Gestion des exceptions

https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html

### Sur les fonctions

```
func canThrowErros() throws -> String
```

### Déclaration d'une exception

```
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

Et son appel 

```
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```

### try...catch

```
do {
    try expression
    statements
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
} catch {
    statements
}
```

```
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
do {
    try buyFavoriteSnack(person: "Alice", vendingMachine: vendingMachine)
    print("Success! Yum.")
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
} catch {
    print("Unexpected error: \(error).")
}
// Prints "Insufficient funds. Please insert an additional 2 coins."
```

Exemple avec la fonction :

```
func nourish(with item: String) throws {
    do {
        try vendingMachine.vend(itemNamed: item)
    } catch is VendingMachineError {
        print("Invalid selection, out of stock, or not enough money.")
    }
}
```

## Les génériques

https://docs.swift.org/swift-book/LanguageGuide/Generics.html

### Pour une fonction

```
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

### Pour une classe

Déclaration :

```
class MyGenericClass<T>{
  func myFunction<T>(_ x: T){
    print(x)
  }
}
```

Appel : 

```
MyGenericClass<String>.myFunction("Hello world")
```

### Extensions

```
extension Array{
  public func getFirst() -> Element? {
    guard self.count > 0 else {
      return nil
    }
    return self[0]
  }
}

print(["a", "b", "c"].getFirst())
```

```
extension Int{
  mutating func modifyIt(){
    self = 10
  }
}

var myVar = 4

myVar.modifyIt()
```

## Shell

https://repl.it/@grudov/Apprentissage-swift

```
```
