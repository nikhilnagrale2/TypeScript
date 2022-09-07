# TypeScript

## What is a TypeScript

- A javascript superset
- A language building up on javascript
- adds new features + advantages to javascript
- typescript cant't be executed by javascript environments like browser.
- typescript compiled to javascript.

## Why Typescript

- example of adding a two function - mitigation strategies can be used in js to handle that but.....

## install typescript

## Advantages

- Types
- next-gen javscript features (compiled down for older browser)
- non javscript features like interfaces or Generics
- meta programmig features like decorators
- rich configuration options
- modern tooling that helps even in non-typescript projects

## Course Outline

- typescript basics
- compiler and configuration deep dive
- next gen js code
- classes and interfaces
- advanced types and typescript features
- Generics
- Decorators
- namespces and modules
- webpack and typescript
- Third party libraries & Typescript
- React + Typescript and Nodejs+typescript

## Set up a Code Editor

## TypeScript Basic and Types

### Core Types

- number ->
- string ->
- boolean ->
- object -> object types {}, object -
- Array -> any, string, number
- Tuple -> [type, type], exception push method
- Enum -> enum Role {ADMIN, READ_ONLY = 10, AUTHOR = 'AUTHOR'};
- Any -> Avoid it.

### Type Assignment and Type Inference

### Union Types

- Union -> number | string

### Literal Types

### Type Aliases / Custom Types

### Function Return types and "void"

- difference in void and undefined as function return type
- in void we can return but doesn't make sense;

### Functions as Types

- combineValues: (a: number, b: number) => number;

### Function Types and Callbacks

### The Unknown type

### The never type

## The TypeScript Compiler

### Watch Mode

- `tsc a.ts --watch`
- `tsc a.ts -w`

- **multiple files**
- `tsc --init`
- then just use `tsc` or `tsc -w`

### Including and Excluding files

- in tsconfig.js, add exclude array
- include array, files etc etc

### Setting a compilation target

### Typescript core libs

### AllowJS, CheckJS, jsx, etc explore on own.

### Source Maps, rootDir, OutDir, removeComments, noEmit, noEmitOnError, strict options, code Quality Options

### Debugging with vscode

## Next gen Javascript and Typescript

- let and const -> var is global and function scope, let - block scope
- arrow functions
- default function parameters
- spread operator
- rest parameters
- array and object desctructuring

## Classes and Interfaces

### What are classes

- what oop ? work with (real life) Entities in your code
- objects - the things you work with in code, instance of classes, class based creation is an alternative to using object literals
- classes - Blueprints for objects (thoretical defn), Define how objects look like which properties and method they have, classes make creation of multiple similar objects much easier

### Creating a class

```js
class Department {
  name: string;
  constructor(n: string) {
    this.name = n;
  }
}

const accounting = new Department("Accounting");
```

### Constructor functions and the this keyword

```js
class Department {
  name: string;
  constructor(n: string) {
    this.name = n;
  }

  describe() {
    console.log("Department: " + this.name);
    /// if we write just name here it will refer to some global variable
  }
}

const accounting = new Department("Accounting");
accounting.describe();

const accountingCopy = { describe: accounting.describe };
accountingCopy.describe(); // this will print name as undefined because this context changes to accountingCopy object

// to work around this scenarior we can use this argument in descibe method and Department as type.but you also need to add some name paramter in accountingCopy object
class Department {
  name: string;
  constructor(n: string) {
    this.name = n;
  }

  describe(this: Department) {
    console.log("Department: " + this.name);
    /// if we write just name here it will refer to some global variable
  }
}

const accounting = new Department("Accounting");
accounting.describe();

const accountingCopy = { name: "Dummy", describe: accounting.describe };
accountingCopy.describe();
```

### Private and Public Access Modifiers

```js
class Department {
  public name: string;
  private employees: string[] =  [];
  constructor(n: string) {
    this.name = n;
  }

  describe(this: Department) {
    console.log("Department: " + this.name);
    /// if we write just name here it will refer to some global variable
  }
}

// shorthand is we can add the properties in constructor with access modifier that will create global vars as well.

class Department {
//   public name: string;
  private employees: string[] =  [];
  constructor(private id:string, public name: string) {
    // like this
  }
}
```

### Read only properties

- typescript, should not be changed afterwards

### Inheritance

- extends keyword
- super() needs to be used

```ts
class ITDepartment extends Department {
  admins: string[];
  constructor(id: string,, admins: string[]) {
    super(id, "IT"); // calls constructor of base class
    this.admins = admins;
  }
}
new ITDepartment("d1", ["AB"]);
```

### Overriding Properties and The "Protected" Modifier

### Getters and Setters

```ts
class AccoutingDepartment extends Department {
  private lastReport: string;

  get mostRecentReport() {
    if (this.lastReport) return this.lastReport;

    throw new Error("No report found");
  }

  set mostRecentReport(value: string) {
    if (!value) {
      throw new Error("Please pass in a valid value");
    }
    this.addReport(value);
  }
}
```

### Static Method and Properties

- static methods are accessible without intializing a class.
- non static methods can't access the static properties with this keyword, u may use the ClassName.property

```ts
class Department {
  static createEmployee(name: string) {
    return {
      name: name,
    };
  }
}
```

### Abstract Classes

- abstract keyword such that every derived class need to implement the function

### Singletons and Private Constructors

- making the constructor private
- static method
- having only one object
- singleton pattern

```ts
class AccountingDepartment extends Department {
  private lastResort: string;
  private static instance: AccountingDepartment;

  private constructor(id: string, private reports: string[]) {
    super(id, "Accounting");
    this.lastReport = reports[0];
  }

  static getInstance() {
    if (AccountingDepartment.instance) {
      return this.instance;
    }
    this.instance = new AccountingDepartment("d2", ["max"]);
    return this.instance;
  }
}

const accounting = AccountingDepartment.getInstance();
```

### Interface

```ts
interface Person {
  name: string;
  age: number;

  greet(phrase: string): void;
}

let user1: Person;

user1 = {
  name: "Max",
  age: 30,
  greet(phrase: string) {
    console.log(phrase + " " + this.name);
  },
};
```

### Interface with Classes

```js
interface Greetable {
  name: string;

  greet(phrase: string): void;
}

class Person implements Greetable, AotherInterface {
  // need to implement interface here
}
```

### why interface

### readonly interface properties

### Extending Interfaces

### Interfaces as Function types

### Optional Parameters and Properties

## Tricks

- to add two strings as number you can use +num1 + +num2; js
- adding an exclamation mark at end of statment tell typescript that this will never yeild null.
