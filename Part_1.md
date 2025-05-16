# 1. Concepts
## 1.1. From JavaScript To TypeScript
- JS was developed in 10 days (wow!)
- Typescript is a:
  - Programming langage
  - Type checker
  - Compiler
  - Language Service
- ```ts
  const firstName = "Georgia";
  const nameLength = firstName.length();
  ```
  Through TS's type checker analysis, it's able to tell you in real time if you are writing code that will compile. Standard JS cannot do that. Similar to Python.
- ```ts
   interface Painter {
     finish(): boolean;
     ownMaterials: Material[];
     paint(painting: string, materials: Material[]): boolean;
   }
  ```
  I think this is an interface like you see in `C++` or something. You have class with a couple of methods and properties that can be strictly typed.

## 1.2. The Type System
- Here are the basic primitive types:
- | Primitive   | Example      |
  | ----------- | -----------  |
  | `null`      | `null`       |
  | `undefined` | `undefined`  |
  | `boolean`   | `true, false`|
  | `string`    | `bea`        |
  | `number`    | `0, 2.1`     |
  | `bigint`    | `0n`         |
  | `symbol`    | `Symbol("Franklin")` |
- The type system works by reading your code and understanding all types and values in existence. It compares all instances of those values to determine if everything is consistent.

### 1.2.1. Different Errors
- There are two main types of errors:
  - **Syntax Errors** There errors occur when the compiler can't understand the code. 

    ```ts
    let let among;
    ```
  - **Type Errors** These are errors raised by the type checker.
    ```ts
    let amongus = Math.random() > 0.5
        ? "red"
        : 5;
    let number = amongus + 2
    ```
    > `Operator '+' cannot be applied to types 'string | number' and 'number'.(2365)`

### 1.2.2. Assignability
- If a variable is instantiated as a certain type, it must continue to be that type unless reassigned later in the code.
  ```ts
  let lastName = "King";
  lastName = true;
  ```
- *Variables that can’t have their initial type inferred go through what’s called an* evolving any: *rather than enforce any particular type, TypeScript will evolve its understanding of the variable’s type each time a new value is assigned* 
  
  This is generally considered bad practice as it defeats the purpose of TypeScript. 
  ```ts
  // Do this!
  let rocker: string;
  rocker = "Joan Jett"

  // Not this :(
  let rocker;
  rocker = "Joan Jett";
  ```
### 1.2.3. Type Shapes (ts)
- Types can be complex shapes:
  ```ts
  let Name = {
    firstName: string,
    lastName: string,
  }
  ```
### 1.3. Unions and Literals
There are two core concepts to understand here:
- **Unions** Expanding a values type to be two or more possible types.
