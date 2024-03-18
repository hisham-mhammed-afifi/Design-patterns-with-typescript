The Factory Method Pattern is designed to address scenarios where you want to create objects, but you don't want to tie your code to specific classes at compile time. This pattern provides a way to delegate the responsibility of creating objects to subclasses.

Here's a breakdown of the problems this pattern aims to solve along with examples:

1. **Avoiding Tight Coupling**: In traditional object creation, you often have code that directly instantiates classes using the `new` keyword. This creates tight coupling between the creator and the product classes. If you decide to change the class being instantiated, you have to modify the creator's code. This violates the Open/Closed Principle of SOLID design principles.

   Example: Imagine you have a `VehicleFactory` class that directly instantiates `Car`, `Bike`, and `Truck` objects. If you want to add a new type of vehicle, such as `Boat`, you would need to modify the `VehicleFactory` class, violating the Open/Closed Principle.

2. **Flexibility and Extensibility**: The Factory Method Pattern allows for flexibility in object creation by deferring the instantiation to subclasses. This means that subclasses can decide which concrete class to instantiate based on specific conditions or configurations. It also allows for adding new product types without modifying existing code.

   Example: Continuing from the previous example, instead of directly instantiating `Car`, `Bike`, and `Truck` in the `VehicleFactory`, you define a factory method `createVehicle` which is abstract in the base class `VehicleFactory` and implemented in subclasses like `CarFactory`, `BikeFactory`, and `TruckFactory`. This way, adding a new vehicle type like `Boat` only requires creating a new `BoatFactory` subclass without modifying existing code.

3. **Encapsulation of Object Creation Logic**: By encapsulating the object creation logic within factory methods, you separate the concerns of object creation from the rest of the codebase. This improves code readability, maintainability, and testability.

   Example: Suppose you have a `PaymentProcessor` class that needs to create different types of payment methods such as `CreditCard`, `PayPal`, and `Bitcoin`. Instead of scattering the object creation logic across the `PaymentProcessor` class, you encapsulate it within factory methods like `createCreditCardPayment`, `createPayPalPayment`, etc.

In summary, the Factory Method Pattern helps in decoupling the client code from the concrete classes being instantiated, thus making the code more flexible, extensible, and easier to maintain. It promotes the principle of coding to interfaces rather than implementations, facilitating better software design practices.

---

Here are five practical scenarios where you can apply the Factory Method Pattern:

1. **GUI Component Factory**: In a graphical user interface (GUI) framework, you might have different types of components like buttons, text fields, and checkboxes. Using the Factory Method Pattern, you can create a `ComponentFactory` interface with methods like `createButton`, `createTextField`, etc. Concrete implementations of this interface, such as `WindowsComponentFactory` and `MacComponentFactory`, will handle the creation of platform-specific components.

2. **Database Connection Factory**: When working with databases, you might need to support multiple database management systems (DBMS) like MySQL, PostgreSQL, and MongoDB. Implementing a database connection factory using the Factory Method Pattern allows you to abstract the creation of database connections. Each DBMS will have its own concrete factory class responsible for creating connections tailored to that particular system.

3. **Logger Factory**: In logging libraries, you may want to support various logging mechanisms such as console logging, file logging, and database logging. Using the Factory Method Pattern, you can define a `LoggerFactory` interface with methods like `createConsoleLogger`, `createFileLogger`, etc. Concrete implementations of this interface will create instances of specific logger classes based on configuration or environment settings.

4. **Document Converter Factory**: In a document conversion application, you might need to convert documents between different formats like PDF, Word, and HTML. Implementing a document converter factory using the Factory Method Pattern allows you to encapsulate the logic for creating document converter objects. Each concrete factory class will handle the conversion to a specific format.

5. **Game Character Factory**: In a game development scenario, you may have different types of game characters like warriors, mages, and archers. Implementing a game character factory using the Factory Method Pattern allows you to create instances of these characters dynamically. Each concrete factory class can produce a specific type of character, with subclasses providing variations such as different weapons or abilities.

In each of these scenarios, the Factory Method Pattern helps in decoupling the client code from the concrete classes being instantiated, allowing for flexibility, extensibility, and maintainability of the codebase. It enables you to write code that is easier to understand, test, and extend, making it a valuable design pattern for real-world applications.

---

Let's build a small TypeScript application to demonstrate the Factory Method Pattern in the context of creating different types of vehicles. We'll create a base `Vehicle` interface, concrete vehicle classes (`Car`, `Bike`, `Truck`), and a `VehicleFactory` interface with concrete implementations (`CarFactory`, `BikeFactory`, `TruckFactory`) to demonstrate how the Factory Method Pattern works.

First, let's define the `Vehicle` interface and concrete vehicle classes:

```typescript
// Vehicle interface
interface Vehicle {
  drive(): void;
}

// Car class implementing Vehicle interface
class Car implements Vehicle {
  drive(): void {
    console.log("Driving a car");
  }
}

// Bike class implementing Vehicle interface
class Bike implements Vehicle {
  drive(): void {
    console.log("Riding a bike");
  }
}

// Truck class implementing Vehicle interface
class Truck implements Vehicle {
  drive(): void {
    console.log("Driving a truck");
  }
}
```

Next, let's define the `VehicleFactory` interface and concrete factory classes:

```typescript
// VehicleFactory interface
interface VehicleFactory {
  createVehicle(): Vehicle;
}

// CarFactory class implementing VehicleFactory interface
class CarFactory implements VehicleFactory {
  createVehicle(): Vehicle {
    return new Car();
  }
}

// BikeFactory class implementing VehicleFactory interface
class BikeFactory implements VehicleFactory {
  createVehicle(): Vehicle {
    return new Bike();
  }
}

// TruckFactory class implementing VehicleFactory interface
class TruckFactory implements VehicleFactory {
  createVehicle(): Vehicle {
    return new Truck();
  }
}
```

Now, let's create a client code to test the implementation:

```typescript
// Client code
class Client {
  private vehicleFactory: VehicleFactory;

  constructor(vehicleFactory: VehicleFactory) {
    this.vehicleFactory = vehicleFactory;
  }

  driveVehicle(): void {
    const vehicle = this.vehicleFactory.createVehicle();
    vehicle.drive();
  }
}

// Usage
const carFactory = new CarFactory();
const bikeFactory = new BikeFactory();
const truckFactory = new TruckFactory();

const client1 = new Client(carFactory);
client1.driveVehicle(); // Output: Driving a car

const client2 = new Client(bikeFactory);
client2.driveVehicle(); // Output: Riding a bike

const client3 = new Client(truckFactory);
client3.driveVehicle(); // Output: Driving a truck
```

This demonstrates how the Factory Method Pattern allows us to encapsulate object creation logic, making the client code independent of the concrete classes being instantiated.

---

Let's build a more complex scenario: a game development framework where we have different types of game characters with various abilities. We'll use the Factory Method Pattern to create different types of game characters dynamically.

First, let's define the `Character` interface and concrete character classes:

```typescript
// Character interface
interface Character {
  attack(): void;
}

// Warrior class implementing Character interface
class Warrior implements Character {
  attack(): void {
    console.log("Warrior attacks with a sword!");
  }
}

// Mage class implementing Character interface
class Mage implements Character {
  attack(): void {
    console.log("Mage casts a fireball spell!");
  }
}

// Archer class implementing Character interface
class Archer implements Character {
  attack(): void {
    console.log("Archer shoots an arrow!");
  }
}
```

Next, let's define the `CharacterFactory` interface and concrete factory classes:

```typescript
// CharacterFactory interface
interface CharacterFactory {
  createCharacter(): Character;
}

// WarriorFactory class implementing CharacterFactory interface
class WarriorFactory implements CharacterFactory {
  createCharacter(): Character {
    return new Warrior();
  }
}

// MageFactory class implementing CharacterFactory interface
class MageFactory implements CharacterFactory {
  createCharacter(): Character {
    return new Mage();
  }
}

// ArcherFactory class implementing CharacterFactory interface
class ArcherFactory implements CharacterFactory {
  createCharacter(): Character {
    return new Archer();
  }
}
```

Now, let's create a client code to test the implementation:

```typescript
// Client code
class Game {
  private characterFactory: CharacterFactory;

  constructor(characterFactory: CharacterFactory) {
    this.characterFactory = characterFactory;
  }

  startGame(): void {
    const character = this.characterFactory.createCharacter();
    character.attack();
  }
}

// Usage
const warriorFactory = new WarriorFactory();
const mageFactory = new MageFactory();
const archerFactory = new ArcherFactory();

const game1 = new Game(warriorFactory);
game1.startGame(); // Output: Warrior attacks with a sword!

const game2 = new Game(mageFactory);
game2.startGame(); // Output: Mage casts a fireball spell!

const game3 = new Game(archerFactory);
game3.startGame(); // Output: Archer shoots an arrow!
```

This demonstrates how the Factory Method Pattern allows us to encapsulate object creation logic, providing flexibility and extensibility in creating game characters dynamically.
