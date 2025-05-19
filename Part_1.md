# 1. Concepts
## 1.1. From JavaScript To TypeScript
- JS was developed in 10 days (wow!)
- Typescript is a:
  - Programming langage
  - Type checker
  - Compiler
  - Language Service
- Type checking example: 
  ```ts
  const firstName = "Georgia";
  const nameLength = firstName.length();
  ```
  Through TS's type checker analysis, it's able to tell you in real time if you are writing code that will compile. Standard JS cannot do that. Similar to Python.
- Interface:
  ```ts
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
## 1.3. Unions and Literals
There are two core concepts to understand here:
- **Unions** Expanding a value's type to be two or more possible types.
- **Narrowing** Reducing a value's allowed type to not be one or more possible types.

### 1.3.1. Unions
- This is the `amogus` variable 
  ```ts
  let amongus = Math.random() > 0.5
    ? "red"
    : 5;
  ```
  Here `amogus` can either be a string or a number. We know it's either or.
- We can declare variables like this
  ```ts
  let amogus: string | number = 5;
  if (Math.random() > 0.5) {
    amongus = "imposter"
  } 
  ```

### 1.3.2 Narrowing
Narrowing is when Typescipt infers from you code that a value is more specifc than what was initially declared. Once a type as been narrowed, you can use it as that type. There are two types of narrowing.
1. **Assignment Narrowing**
2. **Conditional Checks**
3. **TypeOf Checks**

#### 1.3.2.1. Assignment Narrowing
This is pretty simple:
```ts
let admiral: number | string;
admiral = "Grace Hopper";

let inventor: number | string = "Hedy Lamarr"
```
`admiral` is now a string. In the second example, the variable was declared as a union and initialized to a string. Therefore it is treated as a string.

#### 1.3.2.2. Conditional Checks
You can also use if statements to narrow. 
```ts
 let scientist = Math.random() > 0.5
    ? "Rosalind Franklin"
    : 51;
 if (scientist === "Rosalind Franklin") {
    // Type of scientist: string
    scientist.toUpperCase(); // Ok
 }
 ```

 #### 1.3.2.2. `typeOf` Checks
```ts
 typeof researcher === "string"
    ? researcher.toUpperCase() // Ok: string
    : researcher.toFixed();
```

### 1.3.3. Literal Types
Literal types are more specific versions of primitive types. Take this for example:
```ts
const philosopher = "Hypatia";
```
`philosopher` is a string, but more specifically, it's the value `"Hypatia". Using this notion, type annotations can be more specific:
```ts
let persona = string | 3 | 4 | 5

persona = "3 Reload"
persona = 5

persona = true; 
// Error: Type 'true' is not assignable to
// type 'string | 3 | 4 | 5'
```


