
## Delegation Pattern Using Protocol

```swift
protocol DisplayNameDelegate {
    func displayName(name:String)
}


struct Person {
    
    var displayNameDelegate:DisplayNameDelegate
    
    var firstName = "" {
        didSet {
            displayNameDelegate.displayName(name: getFullName())
        }
    }
    
    var lastName = "" {
        didSet {
            displayNameDelegate.displayName(name: getFullName())
        }
    }
    
    init(displayNameDelegate:DisplayNameDelegate) {
        self.displayNameDelegate = displayNameDelegate
    }
    
    func getFullName() ->String {
        return "\(firstName) \(lastName)"
    }
}

struct MyDisplayNameDelegate :DisplayNameDelegate {
    func displayName(name: String) {
        print("Name: \(name)")
    }
}


var myDisplayDelegate = MyDisplayNameDelegate()
var person = Person(displayNameDelegate: myDisplayDelegate)
person.firstName = "Madhav"
person.lastName = "Raj Verma"
```