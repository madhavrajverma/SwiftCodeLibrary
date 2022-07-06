# Protocol in Swift

---

### Protocol Syntax

```swift
Protocol ProtocolName {
    // protocl Definition here
}
```


```swift

//MARK: - Property requirments

//MARK: - Method requirments

protocol FullName {
    
    var firstName:String { get set}
    var lastName:String{get set}
    
    func getFullName() -> String
}

```

### Optional requirments 

To use optional requirements, we need to start off by marking the protocol with the @objc attribute

#### Note 
- It is important to note that only classes can adopt protocols that use the **@objc** attribute. Structures and enumerations cannot adopt these protocol

- If we are using the @objc attribute, as shown in the previous example, we cannot use the **mutating** keyword because it isn't valid for classes


```swift

 //MARK: - optitonal Requirments

@objc protocol Phone {
    var phoneNumber:String { get set}
    @objc optional var emailAdrres:String { get set }
    func dialNumber()
    @objc optional func getEmail()
}

```


### Protocol Inheritance

- Syntax
```swift 
protocol ProtocolThree: ProtocolOne, ProtocolTwo { 
    //Add requirements here 
} 
```
-Example 

```swift 

protocol FullName {
    
    var firstName:String { get set}
    var lastName:String{get set}
    
    func getFullName() -> String
}

// inherit from full Name
protocol Person: FullName { 
    var age: Int {get set} 
}

```

### Protocol composition

Having a type conform to multiple protocols is a very important concept within protocol- oriented programming, as we will see later in this chapter and throughout this book. This concept is known as protocol composition


```swift
struct MyStruct: ProtocolOne, ProtocolTwo, Protocolthree { 
    //implementation  here 
}
```

### Using Protocol as a Type 

We can use protocols as parameters or return types for a function. We can also use them as the type for variables, constants, and collections

```swift 

protocol Person { 
    var firstName: String {get set}  
    var lastName: String {get set}  
    var birthDate: Date {get set}  
    var profession: String {get} 
    init (firstName: String, lastName: String, birthDate: Date) 
} 

// use a protocol as a parameter and return type for a function, method, or initializer

func updatePerson(person: Person) -> Person  { 
    var newPerson: Person 
    // Code to update person goes here  
    return newPerson 
} 
```

### Polymorphism With Protocol 

```swift

var myPerson: Person 
 
myPerson = SwiftProgrammer(firstName: "Jon", lastName: "Hoffman",birthDate: birthDateProgrammer) 
myPerson = FootballPlayer(firstName: "Dan", lastName: "Marino",birthdate: birthDatePlayer) 

```
- In this example, we had a single variable of the Person type. Polymorphism allowed us to set the variable to instances of any type that conforms to the Person protocol, such as the SwiftProgrammer or FootballPlayer types

### Associated Types in Protocol

The associated type basically says: we don't know the exact type to use; therefore, when a type adopts this protocol, it will define it

- In Non Generic Way

```swift 

protocol Queue {
    associatedtype QueueType
    mutating func addItem(item:QueueType)
    mutating func getItem() ->QueueType?
    func count() ->Int
}

struct IntQueue:Queue {
   
    var items = [Int]()
    
    mutating func addItem(item: Int) {
        items.append(item)
    }
    
    mutating func getItem() -> Int? {
        if items.count > 0 {
            return items.remove(at: 0)
        } else {
            return nil
        }
    }
    
    func count() -> Int {
        return items.count
    }
    
  
    
}

```