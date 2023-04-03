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
   - [Abstract Classes](#abstract-classes)
   - [Readonly Arrays & Tuples](#readonly-arrays--tuples)
   - [Double Assertions](#double-assertions)
   - [Const Assertion](#const-assertion)
   - [Generic Constraints](#generic-constraints)
4. **Expert (Type manipulation)**
   - [Typeof type operator](#typeof-type-operator)
   - [Lookup Types](#lookup-types)
   - [Keyof type Operator](#keyof-type-operator)
   - [Mapped Types](#mapped-types)
   - [Mapped type modifiers](#mapped-type-modifiers)
   - [Template literal type](#template-literal-type)
   - [Conditional Types](#conditional-types)
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

6. #### Abstract Classes
```ts
abstract class Vehicle {
  constructor(public name: string){}
  abstract drive(): void;
}

let vehicle = new Vehicle(); // Error, not possible.

class Maruti extends Vehicle {
  drive() {
    console.log('Vehicle ' + this.name + ' is driving');
  }
}

let maruti = new Maruti('Ritz');
```

7. #### Index Signature
```ts
type Person = {
  name: string,
}

type PersonDictionary = {
  [username: string]: Person,
}

// The index will be a string.
const persons: PersonDictionary = {
  abc: {name: 'ABC'}
}
```

8. #### Readonly Arrays & Tuples
```ts
const readonlyArray: readonly number[] = [1, 2];
console.log(readonlyArray); // [1, 2]
readonlyArray[] = 3; // Error

type readonlyArray_1 = ReadonlyArray<number>;
type readonlyArray_2 = readonly number[];

function reverseArray(input: readonlyArray_1) {
  return input.slice().reverse();
}

console.log(reverseArray([1,2, 3, 4])); // [4, 3, 2, 1]

```

9. #### Double Assertions
```ts
type Point2D = {x:number, y:number}
type Point3D = {x:number, y:number, z:number}
type Person = {name: string, age: number}

let point2D: Point2D = {x: 1, y: 2};
let point3D: Point3D = {x: 1, y: 2, z: 5};
let person: Person = {name: 'abc', age: 12};

point2D = point3D; // No, Error
point3D = point2D as Point3D; // Error avoided with asserting
```

10. #### Const Assertion
```ts
const person = {
  name: 'abc',
  age: 11
}

person.name = 'xyz'; // No, Error

const vehicle = {
  name: 'abc_xyz',
  year: '2023'
} as const; // Const assertion usage.

vehicle.name = 'abc' // Error
```

11. #### this parameter
```ts
function sqrt(this: {num: number}): number {
  return this.num * this.num; 
};

const getSquareRoot = {
  num: 10,
  sqrt: sqrt
};

console.log(getSquareRoot.sqrt());
```

12. #### Generic Constraints
```ts
type Email = {
  email: string;
}

type Person = {
  name: string;
  age: number;
}

function printUSerDetails<T extends Email>(user: T): void {
  console.log("User Details");
  console.log("Email - " + user.email);
}

let person: Person = {name: 'abc', age: 12};
const userDetails = {
  ...person,
  email: 'abc@gmail.com'
}
printUSerDetails(userDetails);
```

---

### Expert (Type manipulation)

1. #### Typeof type operator
```ts
const Point = {
  x: 10,
  y: 10
};

// The new type created is similar to Point.
type newPoint = typeof Point;

// Short hand way of declaring variable
const anotherPoint: typeof Point = {
  x: 1,
  y: 1
}
```

2. #### Lookup Types
```ts
type Login200Response = {
  token: {
    user: {
      email: string;
      age: number;
    }
  },
  session: {
    exp: number;
    created: number;
    isValid: boolean;
  }
}

// The return type of the function is a subset of type Login200Response
const checkSession = (): Login200Response['session'] => {
  return {
    exp: Date.now(),
    created: Date.now(),
    isValid: false
  };
}
```

3. #### Keyof type Operator
```ts
type Person = {
  name: string;
  age: number;
  gender: string;
}

const person1: Person = {
  name: 'John',
  age: 22,
  gender: 'Male'
};

// Normal implementation
function getObjectValues(obj: Person, index: keyof Person) {
  return obj[index];
}

// Generic implementation
function getObjectValuesGeneric<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

console.log(getObjectValues(person1, 'age')); // No, Error
console.log(getObjectValues(person1, 'age1')); // Error

console.log(getObjectValuesGeneric(person1, 'age')); // No, Error
console.log(getObjectValuesGeneric(person1, 'age1')); // Error
```

4. #### Mapped Types
```ts
type Point = {
  x: number;
  y: number;
  z: number;
}

// Example 1
type ReadonlyType = {
  readonly [Item in 'x' | 'y' | 'z']: number;
}

const point_1: ReadonlyType = {
  x: 1,
  y: 2,
  z: 3
};

// Example 2
type ReadonlyType_2 = {
  readonly [Item in keyof Point]: number | Point[Item];
}

const point_2: ReadonlyType_2 = {
  x: 1,
  y: 2,
  z: 3
};

console.log(point_2);

// Example 3
const point_3: Readonly<Point> = {
  x: 1,
  y: 2,
  z: 3
}

console.log(point_3);
```

5. #### Mapped type modifiers
```ts
type Point = {
  x?: number;
  readonly y?: number;
  z?: number;
}

// Example 1
// Remove modifiers readonly & optional from above type by using '-' sign.
type ReadonlyType_2 = {
  -readonly [Item in keyof Point]-?: number | Point[Item];
}

// None of the members are optional or readonly now.
const point_1: ReadonlyType_2 = {
  x: 1,
  y: 2,
  z: 3
};

// Example 2
class State<T> {
  constructor(public current: T) {}
  getState(): T {
    return this.current;
  }
  // The Partial type modifier is provided by typescript, it makes all the members
  // of the passed object or the variable itself as optional.
  updateState(next: Partial<T>) {
    this.current = {...this.current, ...next};
  }
}

const s = new State({x: 1, y: 2});
console.log(s.getState());
s.updateState({y: 9});
```

6. #### Template literal type
```ts
let word: Hello;
word = 'Hello'; // No, error
word = 'Heelo'; // Error
```

7. #### Conditional Types
```ts
// Syntax : condition ? condition_is_True : condition_is_false, similar to javascript ternary operator.

interface Animal {
  move(): void;
}

interface Dog extends Animal {
  bark(): void;
}

interface Cat {
  meow(): void;
}

type Other = {
  paws: 4;
}

type Puppy = Dog extends Animal ? Dog : 'other'; // Type inferred is Dog

type PersianCat = Cat extends Animal ? Cat : Other; // Type inferred is 'other'.

// As Persian cat type expects a property whose value is a number.
const y: PersianCat = {
  paws: 4
}
```