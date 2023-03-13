### Typescript notes

---

#### Index

1. **Basics**
   - Primitive Types
   - Instance Types
   - Array & Tuple
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
  console.lop(stack.pop());
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
