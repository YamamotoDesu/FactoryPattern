# FactoryPattern    

<img src="https://github.com/YamamotoDesu/FactoryPattern/blob/main/Factory.playground/Resources/Factory_Diagram.png" width="600" height="300">  
The factory pattern is a way to encapsulate the implementation details of creating objects, which adheres to a common base class or interface.  
The factory pattern provides a way to create objects without exposing creation logic. It involves two types:  

The factory creates objects.  
The products are the objects that are created. 

## Code Example  
```swift  
public struct JobApplicant {
    public enum Status {
        case new
        case interview
        case hired
        case rejected
    }
    
    public let name: String
    public let email: String
    public var status: Status
}

public struct Email {
    public let saubject: String
    public let messageBody: String
    public let recipientEmail: String
    public let senderEmail: String
}

public struct EmailFactory {
    public let senderEmail: String
    
    public func createEmail(to recepient: JobApplicant) -> Email {
        let subject: String
        let messageBody: String
        switch recepient.status {
        case .new:
            subject = "We Received Your Application"
            messageBody = "Thanks for applying for a jpb here!" +
            "You should hear from us in 17-42 business days."
        case .interview:
            subject = "We Want to Interview You"
            messageBody = "Thanks for your resime, \(recepient.name)! " +
            "Can you come in for an interview in 30 minutes?"
        case .hired:
            subject = "We Want to Hire You"
            messageBody = "Congratulations, \(recepient.name) !" +
            "We liked your code, and you smelled nice. " + "We want to offer you a position! Cha-ching! $$$$"
        case .rejected:
            subject = "Thanks for Your Application"
            messageBody = "Thank you for applying, \(recepient.name)!" +
            "Please remeber to wear pants next time!"
        }
        
        return Email(subject: subject, messageBody: messageBody, recipientEmail: recepient.email, senderEmail: senderEmail)
    }
}

// Example
var jackson = JobApplicant(name: "Jackson Smith", email: "jackson.smith@example.com", status: .new)
let emailFactory = EmailFactory(senderEmail: "RaysMinions@RayWenderlich.com")
print(emailFactory.createEmail(to: jackson), "\n")

jackson.status = .interview
print(emailFactory.createEmail(to: jackson), "\n")

jackson.status = .hired
print(emailFactory.createEmail(to: jackson), "\n")

```
