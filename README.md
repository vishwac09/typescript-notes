### Typescript notes

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
