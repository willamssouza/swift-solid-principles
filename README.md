# SOLID Principles

The SOLID principles are a set of five design principles that help developers create more understandable, flexible, and maintainable software systems. I'll describe each of the SOLID principles and provide examples in Swift to illustrate how they can be applied.

## 1. Single Responsibility Principle (SRP)

This principle states that a class should have only one reason to change, meaning it should have only one job or responsibility.

Example in Swift:

```swift
// Violating the SRP
class UserSettings {
    func changeUsername(newUsername: String) {
        // changes the username
    }
    func saveSettings() {
        // saves settings to disk
    }
}

// Following the SRP
class User {
    func changeUsername(newUsername: String) {
        // changes the username
    }
}

class UserSettingsStorage {
    func saveSettings() {
        // saves settings to disk
    }
}
```

## 2. Open/Closed Principle (OCP)

Classes, modules, functions, etc., should be open for extension but closed for modification.

Example in Swift:

```swift
protocol Shape {
    func area() -> Double
}

class Rectangle: Shape {
    var width: Double
    var height: Double
    
    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }
    
    func area() -> Double {
        return width * height
    }
}

class Circle: Shape {
    var radius: Double
    
    init(radius: Double) {
        self.radius = radius
    }
    
    func area() -> Double {
        return .pi * radius * radius
    }
}

// The AreaCalculator class is open for extension but closed for modification.
class AreaCalculator {
    static func calculateArea(shapes: [Shape]) -> Double {
        shapes.reduce(0) { $0 + $1.area() }
    }
}
```

## 3. Liskov Substitution Principle (LSP)

Objects of a superclass should be replaceable with objects of its subclasses without breaking the application.

Example in Swift:

``` swift
protocol Bird {
    func fly()
}

class Sparrow: Bird {
    func fly() {
        print("Sparrow flying")
    }
}

class Ostrich: Bird {
    func fly() {
        fatalError("Ostriches cannot fly")
    }
}

// A better approach would be to separate behaviors that are not common to all birds.
protocol FlyingBird {
    func fly()
}

protocol NonFlyingBird {
}

class Sparrow: FlyingBird {
    func fly() {
        print("Sparrow flying")
    }
}

class Ostrich: NonFlyingBird {
    // Ostrich doesn't need to implement fly()
}
```

## 4. Interface Segregation Principle (ISP)

Clients should not be forced to depend on interfaces they do not use.

Example in Swift:

```swift
protocol Worker {
    func work()
    func eat()
}

// Segregating the interface
protocol Workable {
    func work()
}

protocol Eatable {
    func eat()
}

class Human: Workable, Eatable {
    func work() {
        // working
    }
    func eat() {
        // eating
    }
}
```

## 5. Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions. Moreover, abstractions should not depend on details. Details should depend on abstractions.

Example in Swift:

```swift
protocol Storage {
    func save(data: String)
}

class DiskStorage: Storage {
    func save(data: String) {
        // saves data to disk
    }
}

class CloudStorage: Storage {
    func save(data: String) {
        // saves data to the cloud
    }
}

class DataManager {
    let storage: Storage
    
    init(storage: Storage) {
        self.storage = storage
    }
    
    func saveData(data: String) {
        storage.save(data: data)
    }
}
```

Each of these principles helps in creating software that is easier to maintain and extend over time. By applying these principles in Swift, you can significantly improve the quality of your code and the architecture of your application.
