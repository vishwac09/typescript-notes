### Typescript notes

> Notes on typescript taken from the Udemy Course [TypeScript for Professionals](https://www.udemy.com/course/typescript-for-professionals) by **Basarat Ali Syed**
---

#### <ins>Index</ins>

1. **Basics**
   - [Primitive Types](#primitive-types)
   - [Instance Types](#instance-types)
   - [Array & Tuple](#array--tuples)
   - [Object Types & Type Aliases](#object-types--type-aliases)
   - [Const declaration](#const-declaration)
   - [Functions](#functions)
   - [Structural Typing](#structural-typing)
   - [Classes](#classes)
   - [Generics](#generics)
   - [Type any & Unknown](#type-any--unknown)
   - [Type Assertions](#type-assertions)
   - [Type Casting](#type-casting)
2. **Intermediate**
   - [Lexical this](#lexical-this)
   - [Readonly modifier](#readonly-modifier)
   - [Union Types](#union-types)
   - [Literal Types](#literal-types)
   - [Type Narrowing](#type-narrowing)
   - [Class Parameter Properties](#class-parameter-properties)
   - [Null vs Undefined](#null-vs-undefined)
   - [Intersection Types](#intersection-types)
   - [Optional Modifier](#optional-modifier)
   - [Non-null Assertion Operator](#non-null-assertion-operator)
3. **Advanced**
  - [Implements Keyword](#implements-keyword)
  - [Definitive Assignment operator](#definitive-assignment-operator)
  - [User Defined Type Guards](#user-defined-type-guards)
  - [Function Overloading](#function-overloading)
---

### Basics

1. #### Primitive Types
```ts
let isBoolean: boolean = false/true;
let isNumber: number = 66.6;
let isString: string = 'hello world'

let isUndefined: undefined = undefined;
let isNull: null = null;

let isBigint: bigint = 24n;
```

2. #### Instance Types
```ts
let date: Date = new Date();
let regex: RegExp = new RegExp('abc');

let array: Array<number> =  [1, 2, 3];
let s: Set<number> = new Set([1, 2, 3]);

// Stack class to push/pop items.
class Stack<T> {
  private data: Array<T> = [];
  push(item: T) {this.data.push(item)}
  pop(): T | undefined {return this.data.pop()}
}

let stack: Stack<number> = new Stack<number>();
stack.push(1);
console.log(stack.pop());
```

3. #### Array & tuples
```ts
// Array
let array: string[] = ['abc', 'def', 'ijk'];
// Usage
array = ['mno']
array = [1] // error as array is declared as string[]

// Tuple
let tuple: [number, number] = [1. 2];
tuple = [5, 6];
tuple = [5, 99];
tuple = [5, 6, 11]; // Error
tuple = [5]; // Error
```
4. #### Object Types & Type Aliases
```ts
type Point = {
  x: number;
  y: number;
};

let center: Point = {
  x: 11,
  y: 12
}
```
5. #### const declaration
```ts
const helloWorld = 'Hello World'
helloWorld = 'New world' // error
```

6. #### Functions
```ts
// returns addition of two numbers.
function add(a: number, b: number): number {
  return a+b;
}
console.log(add(5, 2));

// returns nothing.
function log(message: string): void {
  console.log('Message ' + message);
}
```

7. #### Structural Typing
```ts
type Point2D = {x: number, y: number};
type Point3D = {x: number, y: number, z: number};

let point2D: Point2D = { x: 11, y: 12 };
let point3D: Point2D = { x: 11, y: 12, z: 13 };

point2D = point3D; // no error
point3D = point2D // error
```

8. #### Classes
```ts
class Vehicle {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  drive() {
    console.log('Vehicle ' + this.name + ' is moving');
  }
}

let v = new Vehicle('truck');
v.drive();
```

9. #### Generics
```ts
class Stack<T> {
  private data: Array<T> = [];
  push(item: T) {this.data.push(item)}
  pop(): T | undefined {return this.data.pop()}
}

let stack: Stack<number> = new Stack<number>();
stack.push(1);
console.log(stack.pop());

let stackString: Stack<string> = new Stack<string>();
stackString.push('ab');
console.log(stackString.pop());
```

10. #### Type any & Unknown
```ts
let typeAny: any = 1;
typeAny = 'hello world';
typeAny = 111;
typeAny = false;

let typeBoolean: boolean = typeAny; // No, error

let typeUnknown: unknown = 1;
typeUnknown = 'hello world';
typeUnknown = 111;
typeUnknown = false;

let typeBoolean: boolean = typeUnknown; // Error
// correct
if (typeof typeUnknown === "boolean") {
  let typeBoolean: boolean = typeUnknown;
}
```

11. #### Type Assertions
```ts
let hello = 'Hello World';

let stringLength = (hello as string).length;
// only works in ts file.
stringLength = (<string>hello).length;
```

12. #### Type Casting
```ts
let yearString = '2023';
console.log(typeof yearString); // string

const yearNumber = +yearString;
console.log(typeof yearNumber); // number
```

---

### Intermediate

1. #### Lexical this
###### Example 1
```ts
class Vehicle {
  constructor(public name: string){}
  drive() {
    console.log('Vehicle ' + this.name + ' is driving');
  }
}

let vehicle = new Vehicle('Truck');
vehicle.drive(); // No, error
let drive = vehicle.drive;
drive(); // Error, this is undefined
```
###### Example 2
```ts
class Vehicle {
  constructor(public name: string){}
  // using arrow function preserves the called context
  drive = () => {
    console.log('Vehicle ' + this.name + ' is driving');
  }
}

let vehicle = new Vehicle('Truck');
vehicle.drive(); // No, error
let drive = vehicle.drive;
drive(); // No, error
```

2. #### Readonly modifier
```ts
class Vehicle {
  constructor(public readonly name: string){}
  // using arrow function preserves the called context
  drive = () => {
    console.log('Vehicle ' + this.name + ' is driving');
  }
}

let vehicle = new Vehicle('Truck');
vehicle.name = 'Bus'; // Error, property name is readonly
```

3. #### Union Types
```ts
// Accept & Return variables of different types string | string[]
function reverse(data: string | string[]): string | string[] {
  if (typeof data === 'string') {
    return data.split('').reverse().join('');
  }  
  return data.reverse();
}

console.log(reverse('Hello')); // olleH
console.log(reverse(['H', 'E', 'L', 'L', 'O'])); // ["O", "L", "L", "E", "H"]
```

4. #### Literal Types
```ts
let car: string;
car = 'baleno';
car = 'b@leno';

let car: 'Baleno' | 'Nexon';
car = 'Nexon'; // No, error
car = 'Baleno'; // No, error
car = 'B@leno' // Error

type DiceValue = 1 | 2 | 3 | 4 | 5 | 6;
let face: DiceValue = 2; // No, error
face = 9; // Error
```

5. #### Type Narrowing
```ts
let age: number = 1;
let checkIsNumber = typeof age === 'number';

class Car {
  constructor(public name: string){}
  drive() {
    console.log('Car ' + this.name + ' is driving.')
  }
}
let car = new Car('Maruti');
let isCarInstance = car instanceof Car;
```


6. #### Class Parameter Properties
```ts
class Car {
  constructor(public name: string, private ownerAddress: string){}
  drive() {
    console.log('Car ' + this.name + ' is driving.')
  }
  showOwner() {
    console.log('Owner is + ' . this.owner);
  }
}
```

7. #### Null vs Undefined
```ts
let isUndefined = undefined;
let isNull = null;

console.log(isUndefined === isNull) // false
console.log(isUndefined == isNull) // true
```

8. #### Intersection Types
```ts
type Point2D = {
  x: number,
  y: number,
}

type Point3D = Point2D & {
  z: number,
}
```

9. #### Optional Modifier
```ts
type Person = {
  name: string,
  email: string,
  phone?: string
}

const person1: Person = {
  name: 'abc',
  email: 'abc@google.com'
}

class Person {
  public name: string;
  public email: string;
  public phone?: string;
}
```

10. #### Non-null Assertion Operator
```ts
type Point = {
  x: number;
}

let point: Point;
function getPoint() {
  point = { x: 10 };
}

getPoint();
console.log(point!.x)
```

---

### Advanced

1. #### Implements Keyword
```ts
type Vehicle = {
  name: string;
  drive(): void;
}

// Class honda implements Vehicle type/interface
class Honda implements Vehicle {
  constructor(public name: string) {}
  drive() {
    console.log('Vehicle ' + this.name + ' is driving');
  }
}

let hondaCar = new Honda('Honda Civic');
hondaCar.drive();
```

2. #### Definitive Assignment operator
```ts
// Exclamation mark denotes this variable will never be null.
let point!: number;

function initializePoint() {
  point = 1;
}

initializePoint();

console.log(point === null) // false
```

3. #### User Defined Type Guards
```ts
class Dog {
  bark() {
    console.log('Dog sound');
  }
}

class Cat {
  meow() {
    console.log('Cat sound');
  }
}

type Animal = Cat | Dog;

// User defined type guard
function isCat(animal: Animal): animal is Cat {
  return animal instanceof Cat;
}

// User defined type guard
function isDog(animal: Animal): animal is Dog {
  return animal instanceof Dog;
}

function makeSound(animal: Animal) {
  if (isCat(animal)) {
    animal.meow();
  }
  if (isDog(animal)) {
    animal.bark();
  }
}

makeSound(new Dog());
makeSound(new Cat());
```

4. #### Function Overloading
```ts
function reverse(str: string[]): string[];
function reverse(str: string): string;
function reverse(str: string | string[]): string | string[] {
  if (typeof str === 'string') {
    return str.split('').reverse().join('');
  } else {
    return str.reverse();
  }
}
// type of hello == string
const hello = reverse("hello");
console.log(hello)
```

5. #### Call Signature
```ts
// Short hand syntax for a function declaration.
type Add = (a: number, b: number) => number;

const add: Add = (a: number, b: number): number => {
  return a+b;
}

console.log(add(1, 4));
```