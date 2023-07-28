# Swift Language Tour Notes
Following notes were taken from [Swift Language Tour Notes.](https://docs.swift.org/swift-book/GuidedTour/GuidedTour.html)

```swift
//
//  main.swift
//  Swift Tour
//
//  Created by Süha Tanrıverdi on 7.12.2022.
//
import Foundation

print("Genesis Corp!")

// and "var" to make a variable.
var myVariable = 23
myVariable = 13

// Use "let" to make a constant
let myConstant: Int = 42
let myConstant2: Double = 12.0
let myFloat: Float = 4

let label = "Genesis"
let width = 95
let newLabel = label + String(width)

let apples = 10
let oranges = 5
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""

var fruits = ["C", "B", "A"]
var fruits_map = [
    "C": 21,
    "B": 5,
    "A": 12,
]
print(fruits)
fruits.append("AB")
print(fruits)
fruits_map["T"] = 213
print("fruits_map", fruits_map)

var emptyLists: [String] = []
let emptyList: [String] = []

var emptyMap: [String: Int] = [:]

var balls: [Int] = []


let scores = [1,2,3,4]
var teamScore = 0

for score in scores {
    if score > 2 {
        teamScore += 1
    }
    else {
        teamScore += 2
    }
}
print("teamScore:",teamScore)

var optionalString: String? = "Hello"
print(optionalString == nil)

var optionalName: String? = nil
var greeting = "Hello!"

if let name = optionalName {
    greeting = "Hello, \(name)"
}

print(greeting)

let nickname: String? = nil
let fullName: String? = "Genesis"
let informalGreeting = "Hi \(nickname ?? fullName ?? "HE")"

print(informalGreeting)

if let nickname {
    print(nickname)
}

let vegetable = "red pepper"

switch vegetable {
case "celery":
    print("A")
case "a", "b":
    print("A")
case let x where x.hasPrefix("red"):
    print("YEAAH!")
default:
    print("<3")
}


let interestingNumbers = [
    "Prime": [2,3,5,7,11],
    "Fibo": [1,1,2,3,5,8],
    "Square": [1, 4, 9, 25]
]

var largest = 0
var largest_name = ""

for (name, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
            largest_name = name
        }
    }
}

print("largest:", largest_name, largest)

var n = 2
while n < 100 {
    n *= 2
}
print(n)

var m = 2
repeat {
    m *= 2
} while m < 10

print(m)


for i in 0...4 {
    print(i)
}

for i in 0..<4 {
    print(i)
}

func greet(person: String, day: String) -> String {
    return "..."
}

print(greet(person: "A", day: "B"))

func parameterTest(_ person: String, on day: String) -> String {
    return "Aas" + day
}

let a = parameterTest("asd", on: "Wednesday")


func calculate(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    let min = scores[0]
    let max = scores[1]
    let sum = scores[2]
    
    return (min, max, sum)
}

let statistics = calculate(scores: [3,4,5])
print(statistics)
print(statistics.sum)
print(statistics.2)

func returnFift() -> Int {
    var y = 0
    func add() {
        y = 5
    }
    add()
    return y
}

print(returnFift())

func makeIncrementer() -> ( (Int) -> Int ) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}

var increment = makeIncrementer()
print(increment(7))

func hasAnyMatches(list: [Int], condition: ((Int) -> Bool)) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}

func lessThanTen(number: Int) -> Bool {
    return number < 10
}

let has = hasAnyMatches(list: [1,2,12,15], condition: lessThanTen)
print(has)

let numbers: [Int] = [1,2,3,4,5]

let aas = numbers.map({
    (number: Int) -> Int in
    let result = 3 * number
    return result
})

print(aas)

let aab = numbers.map({
    (number: Int) -> Int in
    return (number % 2 == 1) ? 0 : number
})

print(aab)

let mappedNumbers = numbers.map({
    number in 10 * number
})

print(mappedNumbers)

// Sort numbers in descending order
let sortedNumbers = numbers.sorted {
    $0 > $1
}

print(sortedNumbers)

class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}

class Shape: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
    }
    
    func area() -> Double {
        return sideLength * sideLength
    }
    
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
    
    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        
        set {
            sideLength = newValue / 3.0
        }
    }
}


var shape = Shape(sideLength: 123, name: "Triangle")
print(shape.sideLength)
print(shape.name)
print(shape.perimeter)
shape.perimeter = 123


let optionalValue: String? = ""

let sideOptional = optionalValue?.count

enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine
    case jack, queen, king
    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}

let ace = Rank.ace
let aceRawValue = ace.rawValue

print(ace)
print(aceRawValue)

let mace = Rank.six
print(mace, mace.rawValue)

if let convertedRank = Rank(rawValue: 3) {
    print(convertedRank.simpleDescription())
}

// structures are always copied when they’re passed around in your code,
// but classes are passed by reference.
struct Card {
    var rank: Rank
    var suit: Rank
    func simpleDescription() -> String {
        return ""
    }
}

let myCard = Card(rank: .six, suit: .ace)

// Use async to mark a function that runs asynchronously.
func fetchUserID(from server: String) async -> Int {
    if server == "primary" {
        return 97
    }
    return 501
}

func fetchUsername(from server: String) async -> String {
    let userID = await fetchUserID(from: server)
    if userID == 501 {
        return "John Appleseed"
    }
    return "Guest"
}

func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let userName = fetchUsername(from: server)
    let greeting = await "Hello \(userName), user ID \(userID)"
    print(greeting)
}

// Use Task to call asynchronous functions from synchronous code,
// without waiting for them to return.
Task {
    await connectUser(to: "primary")
}

/*
 In swift, classes are reference type whereas structures and enumerations are value types. The properties of value types cannot be modified within its instance methods by default. In order to modify the properties of a value type, you have to use the mutating keyword in the instance method. With this keyword, your method can then have the ability to mutate the values of the properties and write it back to the original structure when the method implementation ends.
 */

/*
 In Swift, a protocol defines a blueprint of methods or properties that can then be adopted by classes (or any other types).
 */
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}

// Classes, enumerations, and structures can all adopt protocols.
class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "Genesis"
    var anotherProporty: Int = 2
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}

var simpleClass = SimpleClass()
simpleClass.adjust()
print(simpleClass.simpleDescription)

/*
 Notice the use of the mutating keyword in the declaration of SimpleStructure to mark a method that modifies the structure. The declaration of SimpleClass doesn’t need any of its methods marked as mutating because methods on a class can always modify the class.
 */
struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "struccct"
    mutating func adjust() {
        simpleDescription += " Adjusted!"
    }
}

var simpleStruct = SimpleStructure()
simpleStruct.adjust()
print(simpleStruct.simpleDescription)

extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}

print(7.simpleDescription)

func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
//        throw PrinterError.noToner
    }
    return "Job sent"
}

do {
//    let printerResponse = try send(job: 1040, toPrinter: "Genesis")
    let printerResponse = try send(job: 1040, toPrinter: "Never Has Toner")
    print(printerResponse)
} catch {
    print(error)
}

let printerSuccess = try? send(job: 1884, toPrinter: "Genesis")

var fridgeIsOpen = false
let fridgeContent: [String] = ["milk", "eggs", "leftovers"]

func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    
    defer {
        fridgeIsOpen = false
    }
    
    let result = fridgeContent.contains(food)
    return result
}
print(fridgeContains("banana"))
print(fridgeIsOpen)

// Generics
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result: [Item] = []
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}

let repeated_arr = makeArray(repeating: "knock", numberOfTimes: 4)
print(repeated_arr)

```
