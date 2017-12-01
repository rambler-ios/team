# Rambler Swift Style Guide

This document describes Swift language code style used in our company.

This style guide is based on different sources from the open source community and modified to our company standards. Credits can be found at the end of this document.

## Table of Contents

  * [Table of Contents](#table-of-contents)
  * [1. File structure](#1-file-structure)
  * [2. Code Formatting](#2-code-formatting)
  * [3. Naming](#3-naming)
  * [4. Code Organization](#4-code-organization)
  * [5. Coding Style](#5-coding-style)
    + [5.1 General](#51-general)
    + [5.2 Access Modifiers](#52-access-modifiers)
    + [5.3 Custom Operators](#53-custom-operators)
    + [5.4 Switch Statements and `enum`s](#54-switch-statements-and-enums)
    + [5.5 Optionals](#55-optionals)
    + [5.6 Properties](#56-properties)
    + [5.7 Closures](#57-closures)
    + [5.8 Arrays](#58-arrays)
    + [5.9 Error Handling **TODO**](#59-error-handling-todo)
    + [5.10 Using `guard` Statements](#510-using-guard-statements)
    + [5.11 Classes and Structures. Which one to use?](#511-classes-and-structures-which-one-to-use)
    + [5.12 Types](#512-types)
    + [5.13 Struct Initializers](#513-struct-initializers)
  * [5.14 Functions vs Methods](#514-functions-vs-methods)
  * [5.15 Selectors](#515-selectors)
  * [5.16 Correctness](#516-correctness)
  * [6. Documentation and Comments](#6-documentation-and-comments)
    + [6.1 Documentation](#61-documentation)
    + [6.2 Comments](#62-comments)
  * [7. Credits](#7-credits)

## 1. File structure

* **1.1** Filenames should be named after type they contain. Don't use abbreviations. Use PascalCase for filenames.

**ConnectionTableViewCell.swift**

```swift
class ConnectionTableViewCell: UITableViewCell {
}
```

**ModuleInput.swift**

```swift
protocol ModuleInput {
}
```

* **1.2** File folder structure should reflect Xcode project folder structure. XCode 9 will do it for you by default when adding new files to a project.



## 2. Code Formatting

* **2.1** Use 4 spaces for tabs.
* **2.2** Avoid uncomfortably long lines with a hard maximum of 160 characters per line.
* **2.3** Ensure that there is a newline at the end of every file.
* **2.4** Ensure that there is no trailing whitespace anywhere.
* **2.5** Do not place opening braces on new lines

```swift
class SomeClass {
    func someMethod() {
        if x == y {
            /* ... */
        } else if x == z {
            /* ... */
        } else {
            /* ... */
        }
    }

    /* ... */
}
```

* **2.6** Colons **MUST** have no space on the left and one space on the right. Exceptions are the ternary operator `? :` and empty dictionary `[:]`.

**Preferred:**

```swift
// specifying type
let pirateViewController: PirateViewController

// dictionary syntax (note that we left-align as opposed to aligning colons)
let ninjaDictionary: [String: AnyObject] = [
    "fightLikeDairyFarmer": false,
    "disgusting": true
]

// declaring a function
func myFunction<T, U: SomeProtocol>(firstArgument: U, secondArgument: T) where T.RelatedType == U {
    /* ... */
}

// calling a function
someFunction(someArgument: "Kitten")

// superclasses
class PirateViewController: UIViewController {
    /* ... */
}

// protocols
extension PirateViewController: UITableViewDataSource {
    /* ... */
}
```

```swift
class TestDatabase: Database {
var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}

let value = condition ? true : false
let empty: [String: String] = [:]
```

**Not Preferred:**

```swift
class TestDatabase : Database {
    var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```

* **2.7** In general, there should be a space following a comma.

```swift
let myArray = [1, 2, 3, 4, 5]
```

* **2.8** There should be a space before and after a binary operator such as `+`, `==`, or `->`. There should also not be a space after a `(` and before a `)`.

**Preferred:**

```swift
let myValue = 20 + (30 / 2) * 3
if 1 + 1 == 3 {
    fatalError("The universe is broken.")
}
func pancake(with syrup: Syrup) -> Pancake {
    /* ... */
}
```

**Not Preferred:**

```swift
let myValue = 20+(30/2)*3
if 1+1==3 {
    fatalError( "The universe is broken." )
}
func pancake( with syrup: Syrup )->Pancake {
    /* ... */
}
```

* **2.9** Follow Xcode's recommended indentation style (i.e. your code should not change if CTRL-I is pressed). When declaring a function that spans multiple lines, you SHOULD use that syntax to which Xcode, as of version 7.3, defaults.

```swift
// Xcode indentation for a function declaration that spans multiple lines
func myFunctionWithManyParameters(parameterOne: String,
                                  parameterTwo: String,
                                  parameterThree: String) {
    // Xcode indents to here for this kind of statement
    print("\(parameterOne) \(parameterTwo) \(parameterThree)")
}

// Xcode indentation for a multi-line `if` statement
if myFirstValue > (mySecondValue + myThirdValue)
    && myFourthValue == .someEnumValue {

    // Xcode indents to here for this kind of statement
    print("Hello, World!")
}
```

* **2.10** When calling a function that has many parameters, put each argument on a separate line with a single extra indentation.

```swift
someFunctionWithManyArguments(
    firstArgument: "Hello, I am a string",
    secondArgument: myVariable,
    thirdArgument: someOtherLocalProperty)
```

* **2.11** When dealing with an implicit array or dictionary large enough to warrant splitting it into multiple lines, treat the `[` and `]` as if they were braces in a method, `if` statement, etc. Closures in a method should be treated similarly.

```swift
someFunctionWithABunchOfArguments(
    someStringArgument: "hello I am a string",
    someArrayArgument: [
        "VIPER is a super-duper architecture",
        "but MVC is better"
    ],
    someDictionaryArgument: [
        "key 1": "value",
        "key 2": "another value"
    ],
    someClosure: { parameter1 in
        print(parameter1)
    })
```

* **2.12** Prefer using local constants or other mitigation techniques to avoid multi-line predicates where possible.

**Preferred**

```swift
let firstCondition = x == firstReallyReallyLongPredicateFunction()
let secondCondition = y == secondReallyReallyLongPredicateFunction()
let thirdCondition = z == thirdReallyReallyLongPredicateFunction()
if firstCondition && secondCondition && thirdCondition {
    // do something
}
```

**Not Preferred:**

```swift
if x == firstReallyReallyLongPredicateFunction()
    && y == secondReallyReallyLongPredicateFunction()
    && z == thirdReallyReallyLongPredicateFunction() {
    // do something
}
```

* **2.13** There **SHOULD** be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but having too many sections in a method often means you should refactor into several methods.

* **2.14** Semicolons. Swift does not require a semicolon after each statement in your code. 
 
* **2.15** Multiple statements on a single line separated by semicolons **MUST** be avoided. 

* **2.16** Parenthesis. Parenthesis around conditionals are not required and **MUST** be omitted.

**Preferred:**

```swift
if name == "Hello" {
    print("World")
}
```

**Not Preferred:**

```swift
if (name == "Hello") {
    print("World")
}
```

## 3. Naming

* **3.1** There is no need for Objective-C style prefixing in Swift (e.g. use just `GuybrushThreepwood` instead of `LIGuybrushThreepwood`). Swift types are automatically namespaced by the module that contains them and you **MUST NOT** add a class prefix. If two names from different modules collide you can disambiguate by prefixing the type name with the module name. However, only specify the module name when there is the possibility for confusion which should be rare.

```swift
import SomeModule

let myClass = MyModule.UsefulClass()
```

* **3.2** Use `PascalCase` for type names (e.g. `struct`, `enum`, `class`, `typedef`, `associatedtype`, etc.).

* **3.3** Use `camelCase` (initial lowercase letter) for function, method, property, constant, variable, argument names, enum cases, etc.).

**Preferred:**

```swift
private let maximumWidgetCount = 100

class WidgetContainer {
    var widgetButton: UIButton
    let widgetHeightPercentage = 0.85
}
```

**Not Preferred:**

```swift
let MAX_WIDGET_COUNT = 100

class app_widgetContainer {
    var wBut: UIButton
    let wHeightPct = 0.85
}
```

* **3.4** Abbreviations and acronyms **SHOULD** generally be avoided. Following the Apple Design Guidelines, abbreviations and initialisms that appear in all uppercase **MUST** be uniformly uppercase or lowercase. Examples:

**Preferred**

```swift
let urlString: URLString
let userID: UserID
```

**Not Preferred**

```swift
let uRLString: UrlString
let userId: UserId
```

* **3.5** All constants other than singletons that are instance-independent should be `static`. All such `static` constants should be placed in a container `struct` type inside corresponding class. The naming of this container should be singular (e.g. `Constant` and **not** `Constants`) and it should be named such that it is relatively obvious that it is a constant container. If this is not obvious, you can add a `Constant` suffix to the name. You should use these containers to group constants that have similar or the same prefixes, suffixes and/or use cases. 
* 
**Preferred**

```swift
struct CellIdentifier {
    static let Blue = "BlueCellIdentifier"
    static let Large = "LargeCellIdentifier"
}

struct FontSize {
    static let Large: CGFloat = 14.0
    static let Small: CGFloat = 10.0
}
```

**Not Preferred**

```swift
	static let kBlueCellIdentifiers = "pirate_button"
	static let fontSizeLarge: CGFloat = 14.0
}
```

* **3.6** Separate constants usage on a class basis. Use project/module-level constant only when neccesary and when unable to find appropriate class for them.

* **3.7** When using module-level constants try to group them into groups by their semantics. I.e UIConstant, APIConstant. Discuss on using single global namespace for all module-level constants such as Constant.

* **3.8** For generics and associated types, use a `PascalCase` word that describes the generic. If this word clashes with a protocol that it conforms to or a superclass that it subclasses, you can append a `Type` suffix to the associated type or generic name.

```swift
class SomeClass<Model> { /* ... */ }
protocol Modelable {
    associatedtype Model
}
protocol Sequence {
    associatedtype IteratorType: Iterator
}
```

* **3.9** Names should be descriptive and unambiguous.

**Preferred**

```swift
class RoundAnimatingButton: UIButton { /* ... */ }
```

**Not Preferred**

```swift
class CustomButton: UIButton { /* ... */ }
```

* **3.10** Do not abbreviate, use shortened names, or single letter names.

**Preferred**

```swift
class RoundAnimatingButton: UIButton {
    let animationDuration: NSTimeInterval

func startAnimating() {
    let firstSubview = subviews.first
}

}
```

**Not Preferred**

```swift
class RoundAnimating: UIButton {
    let aniDur: NSTimeInterval

    func srtAnmating() {
        let v = subviews.first
    }
}
```

* **3.11** Include type information in constant or variable names when it is not obvious otherwise.

**Preferred**

```swift
class ConnectionTableViewCell: UITableViewCell {
let personImageView: UIImageView

let animationDuration: TimeInterval

// it is ok not to include string in the ivar name here because it's obvious
// that it's a string from the property name
let firstName: String

// though not preferred, it is OK to use `Controller` instead of `ViewController`
let popupController: UIViewController
let popupViewController: UIViewController

// when working with a subclass of `UIViewController` such as a table view
// controller, collection view controller, split view controller, etc.,
// fully indicate the type in the name.
let popupTableViewController: UITableViewController

// when working with outlets, make sure to specify the outlet type in the
// property name.
@IBOutlet weak var submitButton: UIButton!
@IBOutlet weak var emailTextField: UITextField!
@IBOutlet weak var nameLabel: UILabel!

}
```

**Not Preferred**

```swift
class ConnectionTableViewCell: UITableViewCell {
// this isn't a `UIImage`, so shouldn't be called image
// use personImageView instead
let personImage: UIImageView

// this isn't a `String`, so it should be `textLabel`
let text: UILabel

// `animation` is not clearly a time interval
// use `animationDuration` or `animationTimeInterval` instead
let animation: TimeInterval

// this is not obviously a `String`
// use `transitionText` or `transitionString` instead
let transition: String

// this is a view controller - not a view
let popupView: UIViewController

// as mentioned previously, we don't want to use abbreviations, so don't use
// `VC` instead of `ViewController`
let popupVC: UIViewController

// even though this is still technically a `UIViewController`, this property
// should indicate that we are working with a *Table* View Controller
let popupViewController: UITableViewController

// for the sake of consistency, we should put the type name at the end of the
// property name and not at the start
@IBOutlet weak var btnSubmit: UIButton!
@IBOutlet weak var buttonSubmit: UIButton!

// we should always have a type in the property name when dealing with outlets
// for example, here, we should have `firstNameLabel` instead
@IBOutlet weak var firstName: UILabel!
}
```

* **3.12** When naming function arguments, make sure that the function can be read easily to understand the purpose of each argument.

* **3.13** As per [Apple's API Design Guidelines](https://swift.org/documentation/api-design-guidelines/), a `protocol` should be named as nouns if they describe what something is doing (e.g. `Collection`) and using the suffixes `-able`, `-ible`, or `-ing` if it describes a capability (e.g. `Equatable`, `ProgressReporting`). If neither of those options makes sense for your use case, you can add a `Protocol` suffix to the protocol's name as well. Some example `protocol`s are below.

```swift
// here, the name is a noun that describes what the protocol does
protocol TableViewSectionProvider {
func rowHeight(at row: Int) -> CGFloat
var numberOfRows: Int { get }
/* ... */
}

// here, the protocol is a capability, and we name it appropriately
protocol Loggable {
func logCurrentState()
/* ... */
}

// suppose we have an `InputTextView` class, but we also want a protocol
// to generalize some of the functionality - it might be appropriate to
// use the `Protocol` suffix here
protocol InputTextViewProtocol {
func sendTrackingEvent()
func inputText() -> String
/* ... */
}
```

* **3.14** When a type name doesn't have a meaningful relationship or role, use a traditional single uppercase letter such as `T`, `U`, or `V`.

**Preferred:**

```swift
func max<T: Comparable>(x: T, _ y: T) -> T
```

**Not Preferred:**

```swift
func max<Thing: Comparable>(x: Thing, _ y: Thing) -> Thing
```

* **3.15** US English spelling **MUST** be used to match Apple's API.

**Preferred:**

```swift
let color = "red"
```

**Not Preferred:**

```swift
let colour = "red"
```

* **3.16** The shortcut versions of type declarations over the full generics syntax **SHOULD** be used.

**Preferred:**

```swift
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
```

**Not Preferred:**

```swift
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```


## 4. Code Organization

* **4.1** Each logical blocks of functionality **SHOULD** be set off with a `// MARK: -` comment to keep things well-organized. Leave a newline after the comment line.

* **4.2** When adding protocol conformance to a model, prefer adding a separate group (commented with `// MARK: -`) for the protocol methods. This keeps the related methods grouped together with the protocol. Keep in mind that when using an extension, however, the methods in the extension can't be overridden by a subclass, which can make testing difficult.

**Preferred:**

```swift
class MyViewcontroller: UIViewController {
    // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewcontroller: UITableViewDataSource {
    // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewcontroller: UIScrollViewDelegate {
    // scroll view delegate methods
}
```

**Not Preferred:**

```swift
class MyViewcontroller: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
    // all methods
}
```

* **4.3** For UIKit view controllers, consider grouping lifecycle, custom accessors, and IBAction in separate marked groups.

* **4.4** Unused (dead) code, including Xcode template code and placeholder comments, **MUST** be removed. An exception is when your tutorial or book instructs the user to use the commented code. Don't leave code blocks commented for *future* use. Use version control systems (i.e Git) for this.

* **4.5** Aspirational methods not directly associated with the tutorial whose implementation simply calls the super class should also be removed. This includes any empty/unused UIApplicationDelegate methods.

**Not Preferred:**

```swift
override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
}

override func numberOfSectionsInTableView(tableView: UITableView) -> Int {
    // #warning Incomplete implementation, return the number of sections
    return 1
}

override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    // #warning Incomplete implementation, return the number of rows
    return Database.contacts.count
}

```

**Preferred:**

```swift
override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return Database.contacts.count
}
```

* **4.6** Keep imports minimal. For example, don't import `UIKit` when importing `Foundation` will suffice.

## 5. Coding Style

### 5.1 General

* **5.1.1** Prefer `let` to `var` whenever possible. **Tip:** A good technique is to define everything using `let` and only change it to `var` if the compiler complains!

* **5.1.2** Prefer the composition of `map`, `filter`, `reduce`, etc. over iterating when transforming from one collection to another. Make sure to avoid using closures that have side effects when using these methods.

**Preferred:**

```swift
let stringOfInts = [1, 2, 3].flatMap { String($0) }
// ["1", "2", "3"]
```

**Not Preferred:**

```swift
var stringOfInts: [String] = []
for integer in [1, 2, 3] {
    stringOfInts.append(String(integer))
}
```

**Preferred:**

```swift
let evenNumbers = [4, 8, 15, 16, 23, 42].filter { $0 % 2 == 0 }
// [4, 8, 16, 42]
```

**Not Preferred:**

```swift
var evenNumbers: [Int] = []
for integer in [4, 8, 15, 16, 23, 42] {
    if integer % 2 == 0 {
        evenNumbers.append(integer)
    }
}
```

* **5.1.3** Prefer the `for-in` style of `for` loop over the `while-condition-increment` style.

**Preferred:**

```swift
for _ in 0..<3 {
    print("Hello three times")
}

for (index, person) in attendeeList.enumerate() {
    print("\(person) is at position #\(index)")
}

for index in 0.stride(to: items.count, by: 2) {
    print(index)
}

for index in (0...3).reverse() {
    print(index)
}
```

**Not Preferred:**

```swift
var i = 0
while i < 3 {
    print("Hello three times")
    i += 1
}


var i = 0
while i < attendeeList.count {
    let person = attendeeList[i]
    print("\(person) is at position #\(i)")
    i += 1
}
```

* **5.1.4** Prefer not declaring types for constants or variables if they can be inferred anyway. Prefer compact code and let the compiler infer the type for constants or variables of single instances. Type inference is also appropriate for small (non-empty) arrays and dictionaries. When required, specify the specific type such as `CGFloat` or `Int16`.

**Preferred:**

```swift
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5
```

**Not Preferred:**

```swift
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
let names = [String]()
```

* **5.1.5** If a function returns multiple values, prefer returning a tuple to using `inout` arguments (it’s best to use labeled tuples for clarity on what you’re returning if it is not otherwise obvious). If you use a certain tuple more than once, consider using a `typealias`. If you’re returning 3 or more items in a tuple, consider using a `struct` or `class` instead. **TODO: discuss**

```swift
func pirateName() -> (firstName: String, lastName: String) {
    return ("Guybrush", "Threepwood")
}

let name = pirateName()
let firstName = name.firstName
let lastName = name.lastName
```

* **5.1.6** Be wary of retain cycles when creating delegates/protocols for your classes; typically, these properties should be declared `weak`.

* **5.1.7** Be careful when calling `self` directly from an escaping closure as this can cause a retain cycle - use a [capture list](https://developer.apple.com/library/ios/documentation/swift/conceptual/Swift_Programming_Language/Closures.html#//apple_ref/doc/uid/TP40014097-CH11-XID_163) when this might be the case. Extend object lifetime using the `[weak self]` and `guard let strongSelf = self else { return }` idiom. `[weak self]` is preferred to `[unowned self]` where it is not immediately obvious that `self` outlives the closure. Explicitly extending lifetime is preferred to optional unwrapping.

**Preferred**
```swift
resource.request().onComplete { [weak self] response in
    guard let strongSelf = self else { return }
    let model = strongSelf.updateModel(response)
    strongSelf.updateUI(model)
}
```

**Not Preferred**
```swift
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
    let model = self.updateModel(response)
    self.updateUI(model)
}
```

**Not Preferred**
```swift
// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
    let model = self?.updateModel(response)
    self?.updateUI(model)
}
```


* **5.1.8** Don't use labeled breaks.

* **5.1.9** Avoid writing out an `enum` type where possible - use shorthand.

**Preferred:**

```swift
imageView.setImageWithURL(url, type: .person)
```

**Not Preferred:**

```swift
imageView.setImageWithURL(url, type: AsyncImageView.Type.person)
```

* **5.1.10** Don’t use shorthand for class methods since it is generally more difficult to infer the context from class methods as opposed to `enum`s.

**Preferred:**

```swift
// .white is not enum
imageView.backgroundColor = UIColor.white
```

**Not Preferred:**

```swift
imageView.backgroundColor = .white
```

* **5.1.11** Prefer not writing `self.` unless it is required.

* **5.1.12** When writing methods, keep in mind whether the method is intended to be overridden or not. If not, mark it as `final`, though keep in mind that this will prevent the method from being overwritten for testing purposes. In general, `final` methods result in improved compilation times, so it is good to use this when applicable. Be particularly careful, however, when applying the `final` keyword in a library since it is non-trivial to change something to be non-`final` in a library as opposed to have changing something to be non-`final` in your local project.

* **5.1.13** When using a statement such as `else`, `catch`, etc. that follows a block, put this keyword on the same line as the block. Again, we are following the [1TBS style](https://en.m.wikipedia.org/wiki/Indent_style#Variant:_1TBS) here. Example `if`/`else` and `do`/`catch` code is below.

```swift
if someBoolean {
    // do something
} else {
    // do something else
}

do {
    let fileContents = try readFile("filename.txt")
} catch {
    print(error)
}
```

* **5.1.14** Prefer `static` to `class` when declaring a function or property that is associated with a class as opposed to an instance of that class. Only use `class` if you specifically need the functionality of overriding that function or property in a subclass, though consider using a `protocol` to achieve this instead.

* **5.1.15** If you have a function that takes no arguments, has no side effects and returns some object or value, prefer using a computed property instead. For conciseness, if a computed property is read-only, the get clause **MUST** be omitted. The get clause is required only when a set clause is provided. **TODO: discuss** 

**Preferred:**

```swift
var diameter: Double {
    return radius * 2
}
```

**Not Preferred:**

```swift
var diameter: Double {
    get {
        return radius * 2
    }
}
```

* **5.1.16** Consider using lazy initialization for finer grain control over object lifetime. This is especially true for `UIViewController` that loads views lazily. You can either use a closure that is immediately called `{ }()` or call a private factory method. Example:

```swift
lazy var locationManager: CLLocationManager = self.makeLocationManager()

private func makeLocationManager() -> CLLocationManager {
    let manager = CLLocationManager()

    manager.desiredAccuracy = kCLLocationAccuracyBest
    manager.delegate = self
    manager.requestAlwaysAuthorization()

    return manager
}
```

### 5.2 Access Modifiers

* **5.2.1** Write the access modifier keyword first if it is needed. The only things that should come before access control are the `static` specifier or attributes such as `@IBAction` and `@IBOutlet`.

**Preferred:**

```swift
fileprivate dynamic lazy var fluxCapacitor = FluxCapacitor()
static fileprivate let viperModuleName = "Main"
@IBOutlet private weak var submitButton: UIButton!
```

**Not Preferred:**

```swift
lazy dynamic fileprivate var fluxCapacitor = FluxCapacitor()
fileprivate static let viperModuleName = "Main"
private @IBOutlet weak var submitButton: UIButton!
```

* **5.2.2** The access modifier keyword should not be on a line by itself - keep it inline with what it is describing.

**Preferred:**

```swift
open class Pirate {
    /* ... */
}
```

**Not Preferred:**

```swift
open
class Pirate {
    /* ... */
}
```

* **5.2.3** In general, do not write the `internal` access modifier keyword since it is the default.

* **5.2.4** If a property needs to be accessed by unit tests, you will have to make it `internal` to use `@testable import ModuleName`. If a property *should* be private, but you declare it to be `internal` for the purposes of unit testing, make sure you add an appropriate bit of documentation commenting that explains this. You can make use of the `- warning:` markup syntax for clarity as shown below. **TODO: discuss**

```swift
/**
 This property defines the pirate's name.
 - warning: Not `private` for `@testable`.
 */
let pirateName = "LeChuck"
```

* **5.2.5** Prefer `private` to `fileprivate` where possible.

* **5.2.6** When choosing between `public` and `open`, prefer `open` if you intend for something to be subclassable outside of a given module and `public` otherwise. Note that anything `internal` and above can be subclassed in tests by using `@testable import`, so this shouldn't be a reason to use `open`. In general, lean towards being a bit more liberal with using `open` when it comes to libraries, but a bit more conservative when it comes to modules in a codebase such as an app where it is easy to change things in multiple modules simultaneously.


### 5.3 Custom Operators

* **5.3.1** Prefer creating named functions to custom operators.

* **5.3.2** If you want to introduce a custom operator, make sure that you have a *very* good reason why you want to introduce a new operator into global scope as opposed to using some other construct. You can override existing operators to support new types (especially `==`). However, your new definitions must preserve the semantics of the operator. For example, `==` must always test equality and return a boolean.

### 5.4 Switch Statements and `enum`s

* **5.4.1** When using a switch statement that has a finite set of possibilities (`enum`), do *NOT* include a `default` case. Instead, place unused cases at the bottom and use the `break` keyword to prevent execution. This will help to avoid undefined behavior when adding new cases to enums.

* **5.4.2** Since `switch` cases in Swift break by default, do not include the `break` keyword if it is not needed.

* **5.4.3** The `case` statements should line up with the `switch` statement itself as per default Swift standards.

* **5.4.4** When defining a case that has an associated value, make sure that this value is appropriately labeled as opposed to just types (e.g. `case Hunger(hungerLevel: Int)` instead of `case Hunger(Int)`).

```swift
enum Problem {
    case attitude
    case hair
    case hunger(hungerLevel: Int)
}

func handleProblem(problem: Problem) {
    switch problem {
    case .attitude:
        print("At least I don't have a hair problem.")
    case .hair:
        print("Your barber didn't know when to stop.")
    case .hunger(let hungerLevel):
        print("The hunger level is \(hungerLevel).")
    }
}
```

* **5.4.5** Prefer lists of possibilities (e.g. `case 1, 2, 3:`) to using the `fallthrough` keyword where possible).

* **5.4.6** If you have a default case that shouldn't be reached, preferably throw an error (or handle it some other similar way such as asserting).

```swift
func handleDigit(_ digit: Int) throws {
    switch digit {
    case 0, 1, 2, 3, 4, 5, 6, 7, 8, 9:
        print("Yes, \(digit) is a digit!")
    default:
        throw Error(message: "The given number was not a digit.")
    }
}
```

### 5.5 Optionals

* **5.5.1** The only time you should be using implicitly unwrapped optionals is with `@IBOutlet`s. In every other case, it is better to use a non-optional or regular optional property. Yes, there are cases in which you can probably "guarantee" that the property will never be `nil` when used, but it is better to be safe and consistent. 
* 
* **5.5.2** When using Dependency Injection prefer injection through initializers rather then property-based. Similarly, don't use force unwraps. **TODO: discuss**

* **5.5.3** Don't use `as!` or `try!`.

* **5.5.4** If you don't plan on actually using the value stored in an optional, but need to determine whether or not this value is `nil`, explicitly check this value against `nil` as opposed to using `if let` syntax.

**Preferred:**

```swift
if someOptional != nil {
    // do something
}
```

**Not Preferred:**

```swift
if let _ = someOptional {
    // do something
}
```

* **5.5.5** Don't use `unowned`. You can think of `unowned` as somewhat of an equivalent of a `weak` property that is implicitly unwrapped (though `unowned` has slight performance improvements on account of completely ignoring reference counting). Since we don't ever want to have implicit unwraps, we similarly don't want `unowned` properties.

**Preferred:**

```swift
weak var parentViewController: UIViewController?

```

**Not Preferred:**

```swift
weak var parentViewController: UIViewController!
unowned var parentViewController: UIViewController
```

* **5.5.6** When unwrapping optionals, use the same name for the unwrapped constant or variable where appropriate. Use one-liner for single return statement.

```swift
guard let myValue = myValue else {
	logSomething()
    return
}

guard let result = result else { return }
```

* **5.5.7** When accessing an optional value, use optional chaining if the value is only accessed once or if there are many optionals in the chain:

```swift
self.textContainer?.textLabel?.setNeedsDisplay()
```

* **5.5.8** Use optional binding when it's more convenient to unwrap once and perform multiple operations:

```swift
if let textContainer = self.textContainer {
    // do many things with textContainer
}
```

### 5.6 Properties

* **5.6.1** When using `get {}`, `set {}`, `willSet`, and `didSet`, indent these blocks.
* **5.6.2** Though you can create a custom name for the new or old value for `willSet`/`didSet` and `set`, use the standard `newValue`/`oldValue` identifiers that are provided by default.

```swift
var storedProperty: String = "I'm selling these fine leather jackets." {
    willSet {
        print("will set to \(newValue)")
    }
    didSet {
        print("did set from \(oldValue) to \(storedProperty)")
    }
}

var computedProperty: String  {
    get {
        if someBool {
            return "I'm a mighty pirate!"
        }
        return storedProperty
    }
    set {
        storedProperty = newValue
    }
}
```

* **5.6.3** You can declare a singleton property as follows:

```swift
class PirateManager {
    static let shared = PirateManager()

    /* ... */
}
```

### 5.7 Closures

* **5.7.1** If the types of the parameters are obvious, it is OK to omit the type name, but being explicit is also OK. Sometimes readability is enhanced by adding clarifying detail and sometimes by taking repetitive parts away - use your best judgment and be consistent.

```swift
// omitting the type
doSomethingWithClosure() { response in
    print(response)
}

// explicit type
doSomethingWithClosure() { response: NSURLResponse in
    print(response)
}

// using shorthand in a map statement
[1, 2, 3].flatMap { String($0) }
```

* **5.7.2** If specifying a closure as a type, you don’t need to wrap it in parentheses unless it is required (e.g. if the type is optional or the closure is within another closure). Always wrap the arguments in the closure in a set of parentheses - use `()` to indicate no arguments and use `Void` to indicate that nothing is returned.

```swift
let completionBlock: (Bool) -> Void = { (success) in
    print("Success? \(success)")
}

let completionBlock: () -> Void = {
    print("Completed!")
}

let completionBlock: (() -> Void)? = nil
```

* **5.7.3** Keep parameter names on the same line as the opening brace for closures when possible without too much horizontal overflow (i.e. ensure lines are less than 160 characters).

* **5.7.4** Use trailing closure syntax unless the meaning of the closure is not obvious without the parameter name (an example of this could be if a method has parameters for success and failure closures).

```swift
// trailing closure
doSomething(1.0) { (parameter1) in
    print("Parameter 1 is \(parameter1)")
}

// no trailing closure
doSomething(1.0, success: { (parameter1) in
    print("Success with \(parameter1)")
}, failure: { (parameter1) in
    print("Failure with \(parameter1)")
})
```

* **5.7.5** For single-expression closures where the context is clear, use implicit returns: **TODO: discuss**

```swift
attendeeList.sort { a, b in
    a > b
}
```

* **5.7.6** Chained methods using trailing closures **SHOULD** be clear and easy to read in context. Decisions on spacing, line breaks, and when to use named versus anonymous arguments is left to the discretion of the author. Examples: **TODO: discuss** (#2)

```swift
let value = numbers.map { $0 * 2 }.filter { $0 % 3 == 0 }.indexOf(90)

let value = numbers
   .map {$0 * 2}
   .filter {$0 > 50}
   .map {$0 + 10}
```

### 5.8 Arrays

* **5.8.1** In general, avoid accessing an array directly with subscripts. When possible, use accessors such as `.first` or `.last`, which are optional and won’t crash. Prefer using a `for item in items` syntax when possible as opposed to something like `for i in 0 ..< items.count`. If you need to access an array subscript directly, make sure to do proper bounds checking. You can use `for (index, value) in items.enumerated()` to get both the index and the value.

* **5.8.2** Never use the `+=` or `+` operator to append/concatenate to arrays. Instead, use `.append()` or `.append(contentsOf:)` as these are far more performant (at least with respect to compilation) in Swift's current state. If you are declaring an array that is based on other arrays and want to keep it immutable, instead of `let myNewArray = arr1 + arr2`, use `let myNewArray = [arr1, arr2].joined()`.


* **5.8.3** For empty arrays and dictionaries, use type annotation. (For an array or dictionary assigned to a large, multi-line literal, use type annotation.)

**Preferred:**

```swift
var names: [String] = []
var lookup: [String: Int] = [:]
```

**Not Preferred:**

```swift
var names = [String]()
var lookup = [String: Int]()
```

**NOTE**: Following this guideline means picking descriptive names is even more important than before.

* ** 5.8.4** Never use optional arrays because it leads to ambiguous state if array is empty or nil. **TODO: discuss**

### 5.9 Error Handling **TODO**

* ** 5.9.1** Suppose a function `myFunction` is supposed to return a `String`, however, at some point, it can run into an error. A common approach is to have this function return an optional `String?` where we return `nil` if something went wrong.

Example:

```swift
func readFile(named filename: String) -> String? {
    guard let file = openFile(named: filename) else {
        return nil
    }

    let fileContents = file.read()
    file.close()
    return fileContents
}

func printSomeFile() {
    let filename = "somefile.txt"
    guard let fileContents = readFile(named: filename) else {
        print("Unable to open file \(filename).")
        return
    }
    print(fileContents)
}
```

Instead, we should be using Swift's `try`/`catch` behavior when it is appropriate to know the reason for the failure.

You can use a `struct` such as the following:

```swift
struct Error: Swift.Error {
    public let file: StaticString
    public let function: StaticString
    public let line: UInt
    public let message: String

    public init(message: String, file: StaticString = #file, function: StaticString = #function, line: UInt = #line) {
        self.file = file
        self.function = function
        self.line = line
        self.message = message
    }
}
```

Example usage:

```swift
func readFile(named filename: String) throws -> String {
    guard let file = openFile(named: filename) else {
        throw Error(message: "Unable to open file named \(filename).")
    }

    let fileContents = file.read()
    file.close()
    return fileContents
}

func printSomeFile() {
    do {
        let fileContents = try readFile(named: filename)
        print(fileContents)
    } catch {
        print(error)
    }
}
```

* **5.9.2** There are some exceptions in which it does make sense to use an optional as opposed to error handling. When the result should *semantically* potentially be `nil` as opposed to something going wrong while retrieving the result, it makes sense to return an optional instead of using error handling.

* **5.9.3** In general, if a method can "fail", and the reason for the failure is not immediately obvious if using an optional return type, it probably makes sense for the method to throw an error.

* **5.9.4** If you don't want to deal with thrown error and just want to have an optional value use `try?`.

* **5.9.5** Also consider using returning enum with error, empty and value cases with appropriate associated values. **TODO: discuss**

### 5.10 Using `guard` Statements

* **5.10.1** In general, prefer to use an "early return" strategy where applicable as opposed to nesting code in `if` statements. Using `guard` statements for this use-case is often helpful and can improve the readability of the code.

**Preferred:**

```swift
func eatDoughnut(at index: Int) {
    guard index >= 0 && index < doughnuts.count else {
        // return early because the index is out of bounds
        return
    }

    let doughnut = doughnuts[index]
    eat(doughnut)
}
```

**Not Preferred:**

```swift
func eatDoughnut(at index: Int) {
    if index >= 0 && index < doughnuts.count {
        let doughnut = doughnuts[index]
        eat(doughnut)
    }
}
```

* **5.10.2** When unwrapping optionals, prefer `guard` statements as opposed to `if` statements to decrease the amount of nested indentation in your code.

**Preferred:**

```swift
guard let monkeyIsland = monkeyIsland else {
    return
}
bookVacation(on: monkeyIsland)
bragAboutVacation(at: monkeyIsland)
```

**Not Preferred:**

```swift
if let monkeyIsland = monkeyIsland {
    bookVacation(on: monkeyIsland)
    bragAboutVacation(at: monkeyIsland)
}
```

**Not Preferred at all:**

```swift
if monkeyIsland == nil {
    return
}
bookVacation(on: monkeyIsland!)
bragAboutVacation(at: monkeyIsland!)
```

* **5.10.3** When deciding between using an `if` statement or a `guard` statement when unwrapping optionals is *not* involved, the most important thing to keep in mind is the readability of the code. There are many possible cases here, such as depending on two different booleans, a complicated logical statement involving multiple comparisons, etc., so in general, use your best judgment to write code that is readable and consistent. If you are unsure whether `guard` or `if` is more readable or they seem equally readable, prefer using `guard`.

```swift
// an `if` statement is readable here
if operationFailed {
    return
}

// a `guard` statement is readable here
guard isSuccessful else {
    return
}

// double negative logic like this can get hard to read - i.e. don't do this
guard !operationFailed else {
    return
}
```

* **5.10.4** If choosing between two different states, it makes more sense to use an `if` statement as opposed to a `guard` statement.

**Preferred:**

```swift
if isFriendly {
    print("Hello, nice to meet you!")
} else {
    print("You have the manners of a beggar.")
}
```

**Not Preferred:**

```swift
guard isFriendly else {
    print("You have the manners of a beggar.")
    return
}

print("Hello, nice to meet you!")
```

* **5.10.5** You should also use `guard` only if a failure should result in exiting the current context. Large code blocks should be avoided. Below is an example in which it makes more sense to use two `if` statements instead of using two `guard`s - we have two unrelated conditions that should not block one another.

```swift
if let monkeyIsland = monkeyIsland {
    bookVacation(onIsland: monkeyIsland)
}

if let woodchuck = woodchuck, canChuckWood(woodchuck) {
    woodchuck.chuckWood()
}
```

* **5.10.6** Often, we can run into a situation in which we need to unwrap multiple optionals using `guard` statements. In general, combine unwraps into a single `guard` statement if handling the failure of each unwrap is identical (e.g. just a `return`, `break`, `continue`, `throw`, or some other `@noescape`).

```swift
// combined because we just return
guard let thingOne = thingOne,
    let thingTwo = thingTwo,
    let thingThree = thingThree else {
    return
}

// separate statements because we handle a specific error in each case
guard let thingOne = thingOne else {
    throw Error(message: "Unwrapping thingOne failed.")
}

guard let thingTwo = thingTwo else {
    throw Error(message: "Unwrapping thingTwo failed.")
}

guard let thingThree = thingThree else {
    throw Error(message: "Unwrapping thingThree failed.")
}
```

* **5.10.7** Don’t use one-liners for `guard` statements. Exception is for single return statement. **TODO: discuss**

**Preferred:**

```swift
guard let thingOne = thingOne else {
	 someAction()
    return
}

guard let thingOne = thingOne else { return }
```

**Not Preferred:**

```swift
guard let thingOne = thingOne else { someAction(); return }
```

* **5.10.8** If cleanup code is required for multiple exit points, consider using a `defer` block to avoid cleanup code duplication. You can use multiple `defer` blocks. Place them logically near the resource they are cleaning so you can easily locate them. **Note** `defer` blocks are executed in the reverse order of their appearance. This reverse order is a vital detail, ensuring everything that was in scope when a deferred block was created will still be in scope when the block is executed.

```swift
func resizeImage(url: NSURL) -> UIImage? {
    // ...
    let dataSize: Int = ...
    let destData = UnsafeMutablePointer<UInt8>.alloc(dataSize)
    defer {
        destData.dealloc(dataSize)
    }

    var destBuffer = vImage_Buffer(data: destData, ...)

    // scale the image from sourceBuffer to destBuffer
    var error = vImageScale_ARGB8888(&sourceBuffer, &destBuffer, ...)
    guard error == kvImageNoError 
        else { return nil }

    // create a CGImage from the destBuffer
    guard let destCGImage = vImageCreateCGImageFromBuffer(&destBuffer, &format, ...) 
        else { return nil }
    // ...
}
```

### 5.11 Classes and Structures. Which one to use?

Remember, structs have [value semantics](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_144). Use structs for things that do not have an identity. An array that contains [a, b, c] is really the same as another array that contains [a, b, c] and they are completely interchangeable. It doesn't matter whether you use the first array or the second because they represent the exact same thing. That's why arrays are structs.

Classes have [reference semantics](https://developer.apple.com/library/mac/documentation/Swift/Conceptual/Swift_Programming_Language/ClassesAndStructures.html#//apple_ref/doc/uid/TP40014097-CH13-XID_145). Use classes for things that do have an identity or a specific life cycle. You would model a person as a class because two person objects are two different things. Just because two people have the same name and birthdate, doesn't mean they are the same person. But the person's birthdate would be a struct because a date of 3 March 1950 is the same as any other date object for 3 March 1950. The date itself doesn't have an identity.

Sometimes, things should be structs but need to conform to `AnyObject` or are historically modeled as classes already (`NSDate`, `NSSet`). Try to follow these guidelines as closely as possible.

Here's an example of a well-styled class definition:

```swift
class Circle: Shape {

    var x: Int, y: Int
    var radius: Double
    var diameter: Double {
        get {
            return radius * 2
        }
        set {
            radius = newValue / 2
        }
    }

    init(x: Int, y: Int, radius: Double) {
        self.x = x
        self.y = y
        self.radius = radius
    }

    convenience init(x: Int, y: Int, diameter: Double) {
        self.init(x: x, y: y, radius: diameter / 2)
      }

    func describe() -> String {
        return "I am a circle at \(centerString()) with an area of \(computeArea())"
    }

    override func computeArea() -> Double {
        return M_PI * radius * radius
    }

    private func centerString() -> String {
        return "(\(x), \(y))"
    }
}
```

The example above demonstrates the following style guidelines:

* Specify types for properties, variables, constants, argument declarations and other statements with space after the colon but not before, e.g. `x: Int`, and `Circle: Shape`.
* Define multiple variables and structures on a single line if they share a common purpose/context.
* Indent getter and setter definitions and property observers.
* Don't add modifiers such as `internal` when they're already the default. Similarly, don't repeat the access modifier when overriding a method.


### 5.12 Types

* **5.12.1** Always use Swift's native types when available. Swift offers bridging to Objective-C so you can still use the full set of methods as needed.

**Preferred:**

```swift
let width = 120.0                                    // Double
let widthString = (width as NSNumber).stringValue    // String
```

**Not Preferred:**

```swift
let width: NSNumber = 120.0                          // NSNumber
let widthString: NSString = width.stringValue        // NSString
```

* **5.12.2** In UIKit code, use `CGFloat` if it makes the code more succinct by avoiding too many conversions.


### 5.13 Struct Initializers

* **5.13.1** Use the native Swift struct initializers rather than the legacy CGGeometry constructors.

**Preferred:**

```swift
let bounds = CGRect(x: 40, y: 20, width: 120, height: 80)
let centerPoint = CGPoint(x: 96, y: 42)
```

**Not Preferred:**

```swift
let bounds = CGRectMake(40, 20, 120, 80)
let centerPoint = CGPointMake(96, 42)
```

* **5.13.2** Prefer the struct-scope constants `CGRect.infinite`, `CGRect.null`, etc. over global constants `CGRectInfinite`, `CGRectNull`, etc. For existing variables, you can use the shorter `.zero

* **5.13.3** Use CGRect helper functions.

**Preferred:**

```swift
let minX = view.frame.minX
let minY = view.frame.minY

let width = view.frame.width
let height = view.frame.height
```

**Not Preferred:**

```swift
let minX = view.frame.origin.x
let minY = view.frame.origin.y

let width = view.frame.size.width
let height = view.frame.size.height
```

## 5.14 Functions vs Methods

* **5.14.1** Free functions, which aren't attached to a class or type, **SHOULD** be used sparingly. When possible, prefer to use a method instead of a free function. This aids in readability and discoverability. Free functions are most appropriate when they aren't associated with any particular type or instance.

**Preferred**

```swift
let sorted = items.mergeSort()  // easily discoverable
rocket.launch()  // clearly acts on the model
```

**Not Preferred**

```swift
let sorted = mergeSort(items)  // hard to discover
launch(&rocket)
```

**Free Function Exceptions**

```swift
let tuples = zip(a, b)  // feels natural as a free function (symmetry)
let value = max(x,y,z)  // another free function that feels natural
```

## 5.15 Selectors

* **5.15.1** Selectors are Obj-C methods that act as handlers for many Cocoa and Cocoa Touch APIs. Strings **MUST NOT** be used for specifying selectors. **Fully qualified** type safe selector **MUST** be used. Often, however, you can use context to shorten the expression. This is the preferred style.

**Preferred:**

```swift
let sel = #selector(viewDidLoad)
```

**Not Preferred:**

```swift
let sel = #selector(ViewController.viewDidLoad)
```

## 5.16 Correctness

* **5.16.1** Consider compiler warnings to be errors. This rule informs many stylistic decisions such as not to use the `++` or `--` operators, C-style for loops, or strings as selectors.

## 6. Documentation and Comments

### 6.1 Documentation

* **6.1.1** If a function is more complicated than a simple O(1) operation, you should generally consider adding a doc comment for the function since there could be some information that the method signature does not make immediately obvious. If there are any quirks to the way that something was implemented, whether technically interesting, tricky, not obvious, etc., this should be documented. Documentation should be added for complex classes/structs/enums/protocols and properties. 

* **6.1.2** All `public` functions/classes/properties/constants/structs/enums/protocols/etc. should be documented as well (provided, again, that their signature/name does not make their meaning/functionality immediately obvious).

* **6.1.3** After writing a doc comment, you should option-click the function/property/class/etc. to make sure that everything is formatted correctly. Be sure to check out the full set of features available in Swift's comment markup [described in Apple's Documentation](https://developer.apple.com/library/content/documentation/Xcode/Reference/xcode_markup_formatting_ref/index.html).

* **6.1.4** 160 character column limit (like the rest of the code).

* **6.1.5** Even if the doc comment takes up one line, use block (`/** */`).

* **6.1.6** Do not prefix each additional line with a `*`.

* **6.1.7** Use the new `- parameter` syntax as opposed to the old `:param:` syntax (make sure to use lower case `parameter` and not `Parameter`).
* 
* **6.1.8** If you’re going to be documenting the parameters/returns/throws of a method, document all of them, even if some of the documentation ends up being somewhat repetitive (this is preferable to having the documentation look incomplete). Sometimes, if only a single parameter warrants documentation, it might be better to just mention it in the description instead.

* **6.1.9** For complicated classes describe the usage of the class with some potential examples as seems appropriate. Remember that markdown syntax is valid in Swift's comment docs. Newlines, lists, etc. are therefore appropriate. **TODO: discuss**

```swift
/**
 ## Feature Support

 This class does some awesome things. It supports:

 - Feature 1
 - Feature 2
 - Feature 3

 ## Examples

 Here is an example use case indented by four spaces because that indicates a
 code block:

     let myAwesomeThing = MyAwesomeClass()
     myAwesomeThing.makeMoney()

 ## Warnings

 There are some things you should be careful of:

 1. Thing one
 2. Thing two
 3. Thing three
 */
class MyAwesomeClass {
    /* ... */
}
```

* **6.1.10** When mentioning code, use code ticks - \`

```swift
/**
 This does something with a `UIViewController`, perchance.
 - warning: Make sure that `someValue` is `true` before running this function.
 */
func myFunction() {
    /* ... */
}
```

* **6.1.11** When writing doc comments, prefer brevity where possible.

### 6.2 Comments

* **6.2.1** For internal company projects use Russian language. For open-source projects (i.e publicly hosted on GitHub) use English comments. **TODO: discuss**

* **6.2.2** Always leave a space after `//`.
* **6.2.3** Always leave comments on their own line.

* **6.2.4** When referring to functions in prose (tutorials, books, comments) include the required parameter names from the caller's perspective or `_` for unnamed parameters. Examples:

> Call `convertPointAt(column:row:)` from your own `init` implementation.
>
> If you call `dateFromString(_:)` make sure that you provide a string with the format "yyyy-MM-dd".
>
> If you call `timedAction(afterDelay:perform:)` from `viewDidLoad()` remember to provide an adjusted delay value and an action to perform.
>
> You shouldn't call the data source method `tableView(_:cellForRowAtIndexPath:)` directly.


## 7. Credits

Used guidelines:

* [The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
* [Style guide & coding conventions for Swift projects](https://github.com/github/swift-style-guide)
* [LinkedIn's Official Swift Style Guide](https://github.com/linkedin/swift-style-guide)


Apple’s reference material on Swift:

* [The Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
* [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/index.html)
* [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html)
* [Swift Standard Library Reference](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/index.html)
