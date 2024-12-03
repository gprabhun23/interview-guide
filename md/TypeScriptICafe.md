### **1. What is the difference between `.ts` and `.tsx` extensions in TypeScript?**

- `.ts` files are used for standard TypeScript code without JSX syntax.  
- `.tsx` files support TypeScript code with JSX, enabling React component development.  
- JSX stands for JavaScript XML, used for defining React elements and components.  
- Example: In a React project, `.tsx` is used to define components:  

```tsx
const Button: React.FC = () => <button>Click Me</button>;
```

---

### **2. Do we need to compile TypeScript files and why?**

- TypeScript must be compiled because browsers understand only JavaScript.  
- The TypeScript compiler converts `.ts` files into plain JavaScript.  
- Compilation helps catch type-related errors during development.  
- Example: While creating a Node.js server, I compiled `.ts` files using `tsc`:

```bash
tsc server.ts
```

---

### **3. What are the benefits of TypeScript?**

- Provides static typing, reducing runtime errors.  
- Supports modern JavaScript features, making code maintainable.  
- Enhances developer productivity with autocompletion and tooling.  
- Example: Static typing helped me avoid null issues in a React app:

```tsx
const greet = (name: string): string => `Hello, ${name}`;
```

---

### **4. What is TypeScript, and why would I use it in place of JavaScript?**

- TypeScript is a superset of JavaScript that adds static typing.  
- It improves code quality by detecting issues at compile time.  
- Enhances teamwork through clear contracts and documentation.  
- Example: I migrated a JS codebase to TypeScript for better type safety:

```ts
const add = (a: number, b: number): number => a + b;
```

---

### **5. How to call a base class constructor from a child class in TypeScript?**

- Use the `super` keyword to invoke the base class constructor.  
- Ensure `super` is called before accessing `this` in the child class.  
- Pass necessary arguments to the `super` function as needed.  
- Example: I used `super` to extend a user class in an auth module:

```ts
class User {
  constructor(public name: string) {}
}

class Admin extends User {
  constructor(name: string, public adminLevel: number) {
    super(name);
  }
}
```

---

### **6. What is TypeScript, and why do we need it?**

- TypeScript adds strong typing to JavaScript for better error detection.  
- It supports ES6+ features and compiles them to ES5 for browser compatibility.  
- Boosts productivity with features like interfaces, modules, and type inference.  
- Example: Using interfaces improved consistency in a team project:

```ts
interface User {
  id: number;
  name: string;
}
```

---

### **7. What is TypeScript, and why should one use it?**

- TypeScript provides advanced IDE support, catching errors at compile time.  
- Helps manage complex projects with type annotations and strict rules.  
- Bridges the gap between JavaScript's flexibility and robust programming practices.  
- Example: I implemented TypeScript in a REST API to enforce typing for request bodies:

```ts
interface RequestBody {
  username: string;
  password: string;
}
```

---

### **8. How to perform string interpolation in TypeScript?**

- Use template literals with backticks (`` ` ``).  
- Embed expressions inside `${}` within template literals.  
- Supports multiline strings and dynamic content seamlessly.  
- Example: I used string interpolation for dynamic greeting messages:

```ts
const greet = (name: string) => `Hello, ${name}!`;
```

---

### **9. What are Modules in TypeScript?**

- Modules encapsulate code into reusable and manageable units.  
- TypeScript supports ES6 modules with `import` and `export` syntax.  
- Helps avoid global scope pollution and simplifies dependency management.  
- Example: I used modules to organize components in an Angular project:

```ts
export const greet = (name: string) => `Hello, ${name}`;
import { greet } from './greet';
```

---

### **10. Explain generics in TypeScript.**

- Generics provide a way to write reusable, type-safe functions or classes.  
- They allow specifying types at the time of usage, maintaining flexibility.  
- Useful for functions or data structures like arrays, maps, etc.  
- Example: I used generics in a utility function to type arrays dynamically:

```ts
function identity<T>(value: T): T {
  return value;
}
```

---

### **11. List the built-in types in TypeScript.**

- TypeScript includes `number`, `string`, `boolean`, `null`, `undefined`, and more.  
- Advanced types: `any`, `unknown`, `never`, `void`, and `object`.  
- Supports array and tuple types for collection management.  
- Example: I used tuple types to represent fixed-length arrays in a project:

```ts
let userInfo: [string, number] = ["John", 25];
```

---

### **12. What is Optional Chaining in TypeScript?**

- Optional chaining (`?.`) safely accesses properties on nullish values.  
- Avoids runtime errors when accessing nested object properties.  
- Returns `undefined` instead of throwing an error for nullish objects.  
- Example: I used optional chaining to check for nested data in an API response:

```ts
const userCity = user?.address?.city;
```

---

### **13. How can we use optional chaining in TypeScript?**

- Use `?.` to safely access object properties, methods, or array elements.  
- Combine with nullish coalescing (`??`) to provide fallback values.  
- Reduces the need for repetitive null checks.  
- Example: Optional chaining prevented crashes in dynamic data handling:

```ts
const zipCode = user?.address?.postalCode ?? 'Not Available';
```

---

### **14. How to make arrays that can only be specific types in TypeScript?**

- Use type annotations with arrays like `string[]` or `Array<number>`.  
- Employ union types for arrays that accept multiple types.  
- Leverage tuple types for arrays with fixed-length and specific types.  
- Example: I used a tuple type to enforce structure in a data-processing task:

```ts
let response: [number, string] = [200, "OK"];
```

---

### **15. Describe what conditional types are in TypeScript.**

- Conditional types allow type selection based on conditions.  
- They follow the `T extends U ? X : Y` syntax for type evaluation.  
- Useful for creating flexible and reusable types.  
- Example: I implemented conditional types for narrowing based on input:

```ts
type IsString<T> = T extends string ? true : false;
```

---
### **16. What does the pipe symbol mean in TypeScript?**

- The pipe symbol (`|`) is used to define union types.  
- Union types allow a variable to hold multiple possible types.  
- It ensures flexibility while maintaining type safety.  
- Example: I used a union type for a function parameter to accept string or number:

```ts
function format(input: string | number): string {
  return input.toString();
}
```

---

### **17. How do we create an enum with string values in TypeScript?**

- Use the `enum` keyword with string assignments for each member.  
- String enums allow descriptive and readable values.  
- Access enum members via their names or string values.  
- Example: I used a string enum to define API status responses:

```ts
enum Status {
  SUCCESS = "Success",
  ERROR = "Error",
  PENDING = "Pending"
}
```

---

### **18. What is the difference between types `String` and `string` in TypeScript?**

- `string` is a primitive type representing text.  
- `String` is an object type, which wraps the primitive type.  
- Prefer `string` for type annotations to avoid unnecessary overhead.  
- Example: I consistently used `string` in my project for simplicity:

```ts
let name: string = "John Doe";
```

---

### **19. What is a TypeScript Map file?**

- A Map file links TypeScript code to its JavaScript output for debugging.  
- It allows developers to trace errors in the original TypeScript code.  
- Generated with the `sourceMap` compiler option in `tsconfig.json`.  
- Example: I enabled `sourceMap` to debug issues in a compiled project:

```json
{
  "compilerOptions": {
    "sourceMap": true
  }
}
```

---

### **20. What is the purpose of the Nullish Coalescing operator in TypeScript?**

- The `??` operator provides a default value for `null` or `undefined`.  
- It prevents false positives with falsy values like `0` or an empty string.  
- Combines well with optional chaining for clean error handling.  
- Example: I used `??` to set a default username in a form:

```ts
const username = userInput ?? "Guest";
```

---

### **21. What are assertion functions in TypeScript?**

- Assertion functions ensure certain conditions are met during runtime.  
- Use `asserts` to refine the type within specific code paths.  
- Helpful for narrowing down complex types.  
- Example: I used assertion functions to validate API response structures:

```ts
function assertIsString(value: any): asserts value is string {
  if (typeof value !== "string") {
    throw new Error("Not a string!");
  }
}
```

---

### **22. Which access modifiers are implied when not specified in TypeScript?**

- Members without explicit modifiers are considered `public`.  
- Public members are accessible anywhere.  
- `private` and `protected` restrict access to specific scopes.  
- Example: I relied on default public access for a utility class:

```ts
class Utils {
  calculateSum(a: number, b: number): number {
    return a + b;
  }
}
```

---

### **23. What is Type Erasure in TypeScript?**

- Type erasure removes type annotations during compilation to JavaScript.  
- Ensures TypeScript's type safety doesn't impact runtime performance.  
- Enables compatibility with plain JavaScript environments.  
- Example: Type annotations in this function are erased in the output:

```ts
function greet(name: string): string {
  return `Hello, ${name}`;
}
```

---

### **24. What is the difference between Classes and Interfaces in TypeScript?**

- Classes define behavior and implementation; interfaces specify structure.  
- Interfaces cannot contain implementation logic, only type definitions.  
- Classes support inheritance, while interfaces allow multiple type extensions.  
- Example: I used interfaces to enforce structure in class implementation:

```ts
interface IUser {
  id: number;
  name: string;
}

class User implements IUser {
  constructor(public id: number, public name: string) {}
}
```

---

### **25. What are Decorators in TypeScript?**

- Decorators are special functions used to modify classes or methods.  
- They are applied using the `@` syntax before class or method declarations.  
- Requires enabling the `experimentalDecorators` compiler option.  
- Example: I used a decorator for logging method calls in a service class:

```ts
function Log(target: any, propertyName: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Method ${propertyName} called with arguments:`, args);
    return originalMethod.apply(this, args);
  };
}

class Service {
  @Log
  fetchData() {
    return "Data fetched";
  }
}
```

---

### **26. How could you check for `null` and `undefined` in TypeScript?**

- Use strict equality (`===`) to differentiate between `null` and `undefined`.  
- Combine nullish coalescing (`??`) with conditional checks for fallback values.  
- TypeScript's `strictNullChecks` flag enhances null/undefined type safety.  
- Example: I implemented a utility function to validate input values:

```ts
function validateInput(value: any): boolean {
  return value !== null && value !== undefined;
}
```

---

### **27. Could we use TypeScript on the backend, and how?**

- Yes, TypeScript works seamlessly with Node.js and other backend frameworks.  
- Helps build type-safe APIs and maintainable backend codebases.  
- Requires compilation to JavaScript using the TypeScript compiler.  
- Example: I created a REST API using TypeScript with Express:

```ts
import express, { Request, Response } from 'express';
const app = express();
app.get('/api', (req: Request, res: Response) => res.send('Hello, TypeScript!'));
app.listen(3000);
```

---

### **28. What are the differences between TypeScript and JavaScript?**

- TypeScript adds static typing; JavaScript is dynamically typed.  
- TypeScript compiles to JavaScript; JavaScript runs directly in browsers.  
- TypeScript supports advanced features like interfaces and generics.  
- Example: I migrated a JS codebase to TS for enhanced maintainability:

```ts
let isActive: boolean = true; // Static typing
```

---

### **29. What is an Interface in TypeScript?**

- Interfaces define the structure of objects, ensuring consistent properties.  
- They are purely compile-time constructs with no runtime output.  
- Supports optional and readonly properties for better flexibility.  
- Example: I used an interface for type-safe API responses:

```ts
interface ApiResponse {
  data: string;
  status: number;
}
```

---

### **30. Does TypeScript support all object-oriented principles?**

- TypeScript supports encapsulation, inheritance, polymorphism, and abstraction.  
- Classes, interfaces, and access modifiers implement these principles.  
- Enables robust OOP design patterns in JavaScript projects.  
- Example: I used OOP principles to design a library management system:

```ts
class Book {
  constructor(public title: string, public author: string) {}
}
```

---

### **31. How to implement class constants in TypeScript?**

- Use the `readonly` modifier for class fields to make them immutable.  
- Define constants directly inside the class or as `static readonly` for shared access.  
- TypeScript enforces immutability at compile time for readonly fields.  
- Example: I used `readonly` to define a constant in a configuration class:

```ts
class Config {
  static readonly APP_NAME = "MyApp";
}
console.log(Config.APP_NAME); // MyApp
```

---

### **32. When to use interfaces and when to use classes in TypeScript?**

- Use interfaces to define structures without implementation logic.  
- Use classes when defining both structure and behavior.  
- Interfaces are ideal for contracts, while classes encapsulate functionality.  
- Example: I used interfaces for API types and classes for service logic:

```ts
interface IUser {
  id: number;
  name: string;
}

class UserService {
  getUser(id: number): IUser {
    return { id, name: "John Doe" };
  }
}
```

---

### **33. What is the purpose of getters/setters in TypeScript?**

- Getters and setters control access to class properties.  
- They provide a mechanism to encapsulate data and validate inputs.  
- Ensures separation of concerns by managing logic inside accessors.  
- Example: I used getters/setters to manage user details securely:

```ts
class User {
  private _name: string = "";

  get name(): string {
    return this._name;
  }

  set name(value: string) {
    if (!value) throw new Error("Invalid name");
    this._name = value;
  }
}
```

---

### **34. Which object-oriented terms are supported by TypeScript?**

- TypeScript supports inheritance, polymorphism, encapsulation, and abstraction.  
- Implements these through classes, interfaces, and access modifiers.  
- Enhances OOP practices with optional static typing.  
- Example: I used inheritance and polymorphism in a vehicle system:

```ts
class Vehicle {
  drive(): string {
    return "Driving";
  }
}

class Car extends Vehicle {
  drive(): string {
    return "Car driving";
  }
}
```

---

### **35. What are the use cases for a `const` assertion in TypeScript?**

- Prevents type widening by making a value immutable and its type literal.  
- Ensures stricter type checking with fixed values.  
- Useful for immutable configuration objects or literal-based enums.  
- Example: I used `const` assertion to fix an array type:

```ts
const roles = ["Admin", "User", "Guest"] as const;
type Role = typeof roles[number]; // "Admin" | "User" | "Guest"
```

---

### **36. What are some use cases of template literal types in TypeScript?**

- Enables dynamic string types based on existing literal types.  
- Useful for creating string-based patterns or configurations.  
- Commonly used in utility types and API request definitions.  
- Example: I defined dynamic route parameters with template literal types:

```ts
type Route = `/user/${string}`;
const userProfile: Route = "/user/123";
```

---

### **37. What is a Mixin Class in TypeScript?**

- Mixins allow combining multiple behaviors into a single class.  
- They provide a flexible way to reuse functionality without traditional inheritance.  
- Implemented using functions that extend base classes.  
- Example: I used mixins for reusable logging functionality:

```ts
class Logger {
  log(message: string) {
    console.log(message);
  }
}

function applyMixins(derivedCtor: any, baseCtors: any[]) {
  baseCtors.forEach((baseCtor) => {
    Object.getOwnPropertyNames(baseCtor.prototype).forEach((name) => {
      derivedCtor.prototype[name] = baseCtor.prototype[name];
    });
  });
}

class App {}
applyMixins(App, [Logger]);
```

---

### **38. List a few rules of private fields in TypeScript.**

- Private fields start with `#` and are truly private to the class.  
- Cannot be accessed or modified outside their containing class.  
- Different from `private`, as they are not accessible even via prototype.  
- Example: I used private fields to enforce strict encapsulation:

```ts
class User {
  #password: string;

  constructor(password: string) {
    this.#password = password;
  }
}
```

---

### **39. How to choose between `never`, `unknown`, and `any` types in TypeScript?**

- Use `never` for unreachable code or impossible states.  
- Use `unknown` for values of an uncertain type, requiring runtime checks.  
- Use `any` when type safety is not a concern (not recommended).  
- Example: I used `unknown` for runtime type checking in a utility function:

```ts
function process(value: unknown): void {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  }
}
```

---

### **40. Explain how and why we could use property decorators in TypeScript.**

- Property decorators modify or annotate class properties.  
- Useful for metadata generation, validation, or dependency injection.  
- Requires enabling `experimentalDecorators` in `tsconfig.json`.  
- Example: I used a decorator to validate property values:

```ts
function MinLength(length: number) {
  return function (target: any, propertyKey: string) {
    let value: string;

    const getter = () => value;
    const setter = (newValue: string) => {
      if (newValue.length < length) {
        throw new Error(`${propertyKey} must be at least ${length} characters.`);
      }
      value = newValue;
    };

    Object.defineProperty(target, propertyKey, {
      get: getter,
      set: setter,
    });
  };
}

class User {
  @MinLength(5)
  username: string = "";
}
```

---

### **41. What does Short-Circuiting mean in TypeScript?**

- Short-circuiting stops further evaluation if a condition is already resolved.  
- Common with logical operators like `&&` and `||`.  
- Useful for performance optimization and conditional execution.  
- Example: I used short-circuiting to set default values in a function:

```ts
const getValue = (value?: string): string => value || "Default";
```

---

### **42. What is the `unique symbol` used for in TypeScript?**

- The `unique symbol` ensures a symbol is globally unique and immutable.  
- Used for creating strongly typed properties or constants.  
- Prevents accidental name clashes in large applications.  
- Example: I used `unique symbol` to define private keys in an API:

```ts
const UNIQUE_KEY: unique symbol = Symbol("UNIQUE_KEY");
```

---

### **43. How to make a readonly tuple type in TypeScript?**

- Use `readonly` before tuple types for immutability.  
- Prevents modification of tuple elements after initialization.  
- Enhances type safety for fixed-length, immutable arrays.  
- Example: I used readonly tuples for a configuration array:

```ts
const settings: readonly [string, number] = ["Theme", 1];
```

---

### **44. What is the fundamental difference between Optional Chaining and Non-null assertion operator in TypeScript?**

- Optional chaining (`?.`) safely accesses properties, returning `undefined` if nullish.  
- Non-null assertion (`!`) explicitly tells TypeScript a value is non-null.  
- Optional chaining avoids errors, while non-null assertion risks runtime failures.  
- Example: I used optional chaining for accessing API data safely:

```ts
const city = user?.address?.city;
```

---

### **45. Explain Project References and its benefits in TypeScript.**

- Project references enable modular TypeScript project compilation.  
- Facilitates faster builds by reusing compiled outputs of referenced projects.  
- Encourages code reusability and better project structure.  
- Example: I used project references in a monorepo to manage dependencies:

```json
{
  "references": [{ "path": "./shared" }]
}
```

---

### **46. How to check the type of a variable or constant in TypeScript?**

- Use the `typeof` operator to check primitive types at runtime.  
- For custom types, use `instanceof` for class instances.  
- Type guards and user-defined type predicates can also be used.  
- Example: I implemented type checks for a flexible utility function:

```ts
function process(input: unknown) {
  if (typeof input === "string") {
    console.log(input.toUpperCase());
  } else if (input instanceof Array) {
    console.log(input.length);
  }
}
```

---

### **47. How TypeScript is an optionally statically typed language?**

- TypeScript allows optional typing, meaning variables can be untyped (`any`).  
- Developers can use static types where necessary or avoid them entirely.  
- This flexibility helps in gradual migration from JavaScript.  
- Example: I used optional typing for a dynamic configuration loader:

```ts
let config: any = {};
config = { mode: "production" }; // Valid due to dynamic typing
```

---

### **48. What is the default access modifier for members of a class in TypeScript?**

- The default access modifier for class members is `public`.  
- Members are accessible from any part of the program unless specified otherwise.  
- Explicitly specifying modifiers is a best practice for clarity.  
- Example: I relied on the default `public` behavior for a shared utility class:

```ts
class User {
  name: string; // public by default
  constructor(name: string) {
    this.name = name;
  }
}
```

---

### **49. What are the different components of TypeScript?**

- **Type System**: Provides static typing to catch errors at compile time.  
- **Compiler (tsc)**: Transpiles TypeScript into JavaScript.  
- **Language Features**: Includes OOP features like classes, interfaces, generics.  
- Example: I used TypeScript components to build a maintainable enterprise app.

---

### **50. How to use external plain JavaScript libraries in TypeScript?**

- Install type definitions using `@types` package if available.  
- Use the `declare` keyword to define types manually for unsupported libraries.  
- Import the library and use it as per its defined API.  
- Example: I integrated a JavaScript charting library with TypeScript:

```ts
import Chart from "chart.js";

const ctx = document.getElementById("myChart") as HTMLCanvasElement;
const chart = new Chart(ctx, { type: "bar", data: { labels: [], datasets: [] } });
```

---

### **51. What is the difference between type and interface in TypeScript?**

- `Type` can alias primitive, union, intersection, or tuple types.  
- `Interface` is used to define object shapes and is extensible.  
- Interfaces are more commonly used for object types.  
- Example: I used a type for union types and an interface for object contracts:

```ts
type ID = string | number;
interface User {
  id: ID;
  name: string;
}
```

---

### **52. How to add types to an interface from another interface or extend types in TypeScript?**

- Use the `extends` keyword to inherit from another interface.  
- This enables reusability and modular design in type definitions.  
- Combine multiple interfaces for composite types.  
- Example: I extended interfaces to define related models:

```ts
interface Person {
  name: string;
}

interface Employee extends Person {
  employeeId: number;
}
```

---

### **53. Does TypeScript support function overloading?**

- Yes, TypeScript allows function overloading with multiple type signatures.  
- The implementation must match one of the declared overloads.  
- Useful for defining functions with multiple valid input/output types.  
- Example: I used overloading for a data processing utility:

```ts
function process(value: string): string;
function process(value: number): number;
function process(value: any): any {
  return typeof value === "string" ? value.toUpperCase() : value * 2;
}
```

---

### **54. What is the difference between Private and Protected variables in TypeScript?**

- `Private` variables are accessible only within the class they are defined.  
- `Protected` variables are accessible in the class and its subclasses.  
- Protected is useful for extending functionality while keeping some scope restricted.  
- Example: I used protected fields for shared behavior in derived classes:

```ts
class Base {
  protected id: number;
  constructor(id: number) {
    this.id = id;
  }
}

class Derived extends Base {
  displayId() {
    console.log(this.id);
  }
}
```

---

### **55. What is Typings in TypeScript?**

- Typings are definition files (`.d.ts`) that describe the types in libraries.  
- Allow TypeScript to understand JavaScript libraries during compilation.  
- Available through `@types` packages or manually written.  
- Example: I added typings for a legacy library in a project:

```ts
declare module "legacy-lib" {
  export function legacyMethod(): void;
}
```

---

### **56. What is the difference between enum and const enum in TypeScript?**

- `Enum` is fully compiled to JavaScript and can be used dynamically.  
- `Const enum` is inlined at compile time, reducing runtime overhead.  
- Use `const enum` for performance-critical applications.  
- Example: I used `const enum` to improve performance in a mapping function:

```ts
const enum Direction {
  Up,
  Down,
}
console.log(Direction.Up); // Compiles to 0
```

---

### **57. Why do we need to use the abstract keyword for classes and their methods in TypeScript?**

- Abstract classes define shared behavior but cannot be instantiated directly.  
- Abstract methods must be implemented in derived classes.  
- Used to enforce structure while allowing flexibility.  
- Example: I used an abstract class for a shared vehicle interface:

```ts
abstract class Vehicle {
  abstract drive(): void;
}

class Car extends Vehicle {
  drive() {
    console.log("Driving a car");
  }
}
```

---

### **58. What is Structural Typing in TypeScript?**

- Structural typing focuses on the shape of an object rather than its explicit type.  
- Enables compatibility between objects with matching structures.  
- Used for flexible and duck-typing-friendly designs.  
- Example: I relied on structural typing for third-party API data handling:

```ts
interface Point {
  x: number;
  y: number;
}

let pt: Point = { x: 10, y: 20 };
```

---

### **59. How can you allow classes defined in a module to be accessible outside of the module?**

- Use the `export` keyword to make classes accessible outside the module.  
- Import the class where needed using `import` statements.  
- Encapsulates functionality while enabling modularity.  
- Example: I exported a utility class for use in multiple modules:

```ts
export class Helper {
  static greet() {
    console.log("Hello!");
  }
}
```

---

### **60. Explain what is Currying in TypeScript.**

- Currying transforms a function with multiple arguments into a series of unary functions.  
- Helps in creating reusable, partial applications.  
- Common in functional programming and cleaner callback management.  
- Example: I used currying to create flexible query builders:

```ts
function multiply(a: number) {
  return (b: number) => a * b;
}

const double = multiply(2);
console.log(double(5)); // 10
```

---

### **61. How to exclude a property from a type in TypeScript?**

- Use the `Omit` utility type to exclude specific properties.  
- Pass the base type and the property key(s) to `Omit`.  
- This creates a new type without the excluded property.  
- Example: I excluded sensitive fields from a user data model:

```ts
interface User {
  id: number;
  name: string;
  password: string;
}

type PublicUser = Omit<User, "password">;

const user: PublicUser = { id: 1, name: "Alice" }; // Valid
```

---

### **62. How to define a TypeScript class with an index signature?**

- Use an index signature to define a class that allows dynamic properties.  
- Specify the property key type and value type in the index signature.  
- Ensure other members align with the dynamic property definition.  
- Example: I created a class for flexible configuration storage:

```ts
class Config {
  [key: string]: string;
  appName = "MyApp";
}

const config = new Config();
config.theme = "dark";
```

---

### **63. Why do we need Index Signature in TypeScript?**

- Index signatures allow defining types for dynamic object keys.  
- Useful when the object structure isn’t fixed or keys are runtime-defined.  
- Enforces type safety for dynamic properties.  
- Example: I used index signatures for a translation dictionary:

```ts
interface Translation {
  [key: string]: string;
}

const en: Translation = { hello: "Hello", bye: "Goodbye" };
```

---

### **64. What is the difference between unknown and any type in TypeScript?**

- `unknown` is a safer version of `any` and requires type assertions or checks before usage.  
- `any` bypasses type checking entirely, potentially causing runtime errors.  
- Use `unknown` for uncertain types to enforce type safety.  
- Example: I used `unknown` to validate API response types:

```ts
function process(data: unknown) {
  if (typeof data === "string") {
    console.log(data.toUpperCase());
  }
}
```

---

### **65. Why is the infer keyword needed in TypeScript?**

- `infer` is used in conditional types to infer types based on a condition.  
- Enables extraction or manipulation of types at compile time.  
- Simplifies complex type computations in generic scenarios.  
- Example: I used `infer` to extract the return type of a function:

```ts
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

function getValue(): string {
  return "Hello";
}

type ValueType = ReturnType<typeof getValue>; // string
```

---

### **66. Explain what is the never datatype in TypeScript.**

- `never` represents values that never occur (e.g., function throws or infinite loops).  
- It’s used for exhaustive checks in conditional types or switch cases.  
- Helps enforce complete case handling in logic.  
- Example: I used `never` to ensure exhaustive case handling:

```ts
function handle(value: "a" | "b") {
  switch (value) {
    case "a":
      console.log("A");
      break;
    case "b":
      console.log("B");
      break;
    default:
      const _exhaustive: never = value;
  }
}
```

---

### **67. What is dynamic import expression in TypeScript?**

- Dynamic import loads modules asynchronously using `import()`.  
- Useful for code-splitting and lazy-loading in applications.  
- Returns a promise that resolves to the module.  
- Example: I used dynamic import for loading a configuration module:

```ts
async function loadConfig() {
  const config = await import("./config");
  console.log(config.default);
}
loadConfig();
```

---

### **68. What is the difference between interface and type statements in TypeScript?**

- `Interface` is mainly for defining object shapes and can be extended.  
- `Type` is more flexible, supporting unions, intersections, and primitives.  
- Interfaces are better for class-based designs.  
- Example: I combined both for a flexible type system:

```ts
interface Person {
  name: string;
}

type PersonWithAge = Person & { age: number };
```

---

### **69. What is Mixin Constructor Type in TypeScript?**

- A mixin constructor type combines multiple classes into one.  
- Helps in achieving reusable behavior across classes.  
- Uses generics to extend a base constructor.  
- Example: I used mixins for a feature-rich component class:

```ts
type Constructor<T = {}> = new (...args: any[]) => T;

function Timestamped<T extends Constructor>(Base: T) {
  return class extends Base {
    timestamp = Date.now();
  };
}

class Entity {}
const TimestampedEntity = Timestamped(Entity);
```

---

### **70. How does the override keyword work in TypeScript?**

- The `override` keyword ensures the method overrides a base class method.  
- Prevents accidental method shadowing when the base method doesn’t exist.  
- Increases code clarity and avoids runtime errors.  
- Example: I used `override` to override a base logging method:

```ts
class Base {
  log() {
    console.log("Base log");
  }
}

class Derived extends Base {
  override log() {
    console.log("Derived log");
  }
}
```

---

### **71. Explain when to use the declare keyword in TypeScript.**

- Use `declare` to describe types or variables defined elsewhere (e.g., global scope).  
- It avoids TypeScript compilation errors for external or global declarations.  
- Commonly used for type definitions of external libraries.  
- Example: I used `declare` for a global configuration object:

```ts
declare const CONFIG: { apiUrl: string };
console.log(CONFIG.apiUrl);
```

---

### **72. Is it possible to generate TypeScript declaration files from a JavaScript library?**

- Yes, use the `--declaration` flag with `tsc` to generate `.d.ts` files.  
- This helps TypeScript users consume the library with type support.  
- Combine it with `--allowJs` for JavaScript-based projects.  
- Example: I generated typings for a shared utility library:

```sh
tsc --declaration --allowJs --emitDeclarationOnly
```

---

### **73. What does the tsconfig option lib do?**

- The `lib` option specifies the TypeScript standard libraries to include.  
- It helps restrict or expand the available built-in APIs.  
- Useful for targeting specific environments like ES5 or DOM.  
- Example: I configured `lib` to include ES2020 and DOM APIs:

```json
{
  "compilerOptions": {
    "lib": ["ES2020", "DOM"]
  }
}
```

---

### **74. How to make a union type from a type alias or interface properties in TypeScript?**

- Use `keyof` and `Extract` to create a union type from properties.  
- Helps in dynamically deriving types based on an interface or alias.  
- Useful for utility types or type-safe operations.  
- Example: I extracted keys for a validation utility:

```ts
interface User {
  id: number;
  name: string;
}

type UserKeys = keyof User; // "id" | "name"
```

---

### **75. What are Ambients in TypeScript and when to use them?**

- Ambients declare global types, variables, or modules in `.d.ts` files.  
- Used for external libraries or APIs without native TypeScript support.  
- Helps in integrating TypeScript with JavaScript ecosystems.  
- Example: I defined ambient types for a third-party analytics script:

```ts
declare module "analytics" {
  export function track(event: string): void;
}
```

---

### **76. What is the benefit of import assertions features in TypeScript?**

- Import assertions validate the type of imported modules (e.g., JSON, CSS).  
- Prevents runtime errors by enforcing expected module formats.  
- Supports modern workflows like JSON modules or WebAssembly.  
- Example: I used import assertions to load a JSON configuration:

```ts
import config from "./config.json" assert { type: "json" };
console.log(config.apiUrl);
```

---

### **77. What is one thing you would change about TypeScript?**

- Enhance type inference for deeply nested object types.  
- Provide better tooling for debugging complex types in large codebases.  
- Include built-in support for runtime type validation.  
- Example: While working with deeply nested APIs, explicit types were often cumbersome.

---

### **78. Explain the difference between declare enum vs declare const enum.**

- `declare enum` defines an external enum in ambient declarations.  
- `declare const enum` creates optimized enums by inlining values.  
- Use `declare const enum` for performance-sensitive scenarios.  
- Example: I used `declare const enum` for configuration keys:

```ts
declare const enum Config {
  BaseUrl = "https://api.example.com"
}

const url = Config.BaseUrl; // Inlined as string
```

---

### **79. What are the differences between the private keyword and private fields in TypeScript?**

- `private` keyword enforces access only within the class or subclasses (TypeScript-specific).  
- `#private` fields are part of JavaScript and accessible only within the declaring class.  
- `#private` ensures runtime-level encapsulation.  
- Example: I used `#private` for secure internal state handling:

```ts
class Secure {
  #token: string = "secret";

  getToken() {
    return this.#token;
  }
}
```

---

### **80. How the never datatype can be useful in TypeScript?**

- Represents functions or expressions that never produce a value.  
- Ensures exhaustive checks in conditional types or control flows.  
- Helps catch unhandled cases at compile time.  
- Example: I used `never` to ensure no unhandled enum cases:

```ts
type Colors = "Red" | "Blue";

function getColorName(color: Colors): string {
  switch (color) {
    case "Red":
      return "Red Color";
    case "Blue":
      return "Blue Color";
    default:
      const exhaustiveCheck: never = color;
      return exhaustiveCheck;
  }
}
```

---

### **81. What is the need for the incremental flag in TypeScript?**

- The `--incremental` flag enables faster compilation by caching.  
- It compiles only changed files, improving development efficiency.  
- Creates a `.tsbuildinfo` file to store metadata for reuse.  
- Example: I enabled it for a large project with frequent changes:

```json
{
  "compilerOptions": {
    "incremental": true
  }
}
```

---

### **82. Is there a way to check for both null and undefined in TypeScript?**

- Use `==` or `===` comparisons for strict or loose checks.  
- Combine `null` and `undefined` in a single comparison using `x == null`.  
- Optional chaining and nullish coalescing simplify handling.  
- Example: I checked for null/undefined during data validation:

```ts
function process(data?: string | null) {
  if (data == null) {
    console.log("Data is null or undefined");
  }
}
```

---

### **83. How to make an array with a specific length or elements in TypeScript?**

- Use `Array` constructor or tuple types for specific lengths.  
- Define exact element types for precise constraints.  
- Combine generics for flexible yet strict array types.  
- Example: I defined a tuple for fixed-length RGB values:

```ts
type RGB = [number, number, number];
const color: RGB = [255, 0, 0];
```

---

### **84. What's wrong with that code?**

- Analyze issues like type mismatches, missing return types, or unsafe operations.  
- Debug by reviewing errors or enabling strict compiler options.  
- Use TypeScript tooling (e.g., `tsc` or IDE) for detailed diagnostics.  
- Example: I debugged an incorrect return type in a utility function:

```ts
function add(a: number, b: number): string {
  return a + b; // Error: Type 'number' is not assignable to type 'string'
}
```

---

### **85. Are strongly-typed functions as parameters possible in TypeScript?**

- Yes, use function types or interfaces to define parameter signatures.  
- Enforce input and return types for type safety.  
- Useful for callbacks, event handlers, or higher-order functions.  
- Example: I used a strongly-typed callback in a utility:

```ts
type Callback = (value: number) => void;

function process(callback: Callback) {
  callback(42);
}
```

---

### **86. Is that TypeScript code valid? Explain why.**

- Validate code against TypeScript rules like strict typing and access modifiers.  
- Check for compliance with compiler options in `tsconfig.json`.  
- Ensure compatibility with TypeScript’s type system.  
- Example: I debugged invalid parameter types in a function:

```ts
function multiply(a: string, b: string): number {
  return parseInt(a) * parseInt(b); // Fix: Ensure inputs are numeric
}
```

---

### **87. What will be the result of this code execution?**

- Analyze behavior based on runtime and type system rules.  
- Understand how TypeScript translates to JavaScript for execution.  
- Predict results considering strict mode and implicit conversions.  
- Example: I evaluated a conditional operation in TypeScript:

```ts
const value = undefined ?? "default"; // Result: "default"
```

---

### **88. In the expression a?.b.c, if a.b is null or undefined, will a.b.c evaluate to undefined?**

- No, if `a?.b` evaluates to `null` or `undefined`, `a?.b.c` will not execute.  
- Optional chaining halts further property access on `null` or `undefined`.  
- Avoids runtime errors by safely accessing nested properties.  
- Example: I used this for deep API response validation:

```ts
const response = { user: null };
console.log(response?.user?.name); // undefined
```

---

### **89. What does the const assertion mean in TypeScript?**

- `const` assertion freezes the type as literal and prevents widening.  
- Useful for defining immutable values.  
- Simplifies narrowing of inferred types.  
- Example: I used `const` assertion for exact API responses:

```ts
const config = {
  apiUrl: "https://example.com",
} as const;

config.apiUrl = "newUrl"; // Error: Cannot assign to 'apiUrl'
```

---

### **90. Explain why that code is marked as WRONG?**

- Identify issues like mismatched types, incorrect scopes, or access violations.  
- Ensure adherence to strict typing and declared members.  
- Example: I corrected wrong variable access in a nested function:

```ts
function outer() {
  let count = 0;
  function inner() {
    count++; // Correct: Ensure access to `count` is valid
  }
}
```

---

### **91. How would you overload a class constructor in TypeScript?**

- Define multiple constructor signatures for flexibility.  
- Use a single implementation to handle different parameter combinations.  
- Employ `if` or `switch` to process arguments based on type or count.  
- Example: I implemented constructor overloading for a `User` class:

```ts
class User {
  name: string;
  age: number;

  constructor(name: string);
  constructor(name: string, age: number);
  constructor(name: string, age?: number) {
    this.name = name;
    this.age = age ?? 0;
  }
}

const user1 = new User("Alice");
const user2 = new User("Bob", 30);
```

---

### **92. What are the use cases for the keyof operator in TypeScript?**

- Retrieves keys of a type as a union of string literals.  
- Useful for creating generic functions that operate on object keys.  
- Enables type-safe property access and key validation.  
- Example: I used `keyof` for a reusable utility function:

```ts
type User = { name: string; age: number };
type UserKeys = keyof User; // "name" | "age"

function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user: User = { name: "Alice", age: 30 };
console.log(getProperty(user, "name")); // Alice
```

---

### **93. How to use mapped types in TypeScript?**

- Mapped types transform properties of an existing type.  
- Apply operations like making properties optional, readonly, or modifying values.  
- Use `keyof` and indexed access to iterate over keys.  
- Example: I created a utility type for partial objects:

```ts
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type User = { name: string; age: number };
type PartialUser = Partial<User>;

const user: PartialUser = { name: "Alice" };
```

---

### **94. What are type guards in TypeScript?**

- Type guards narrow types using conditions or functions.  
- Built-in guards include `typeof` and `instanceof`.  
- Custom guards use functions returning `arg is Type`.  
- Example: I implemented a type guard for API responses:

```ts
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function printLength(input: unknown) {
  if (isString(input)) {
    console.log(input.length);
  }
}
```

---

### **95. What is the purpose of a type predicate in TypeScript?**

- A type predicate narrows a type in conditional checks.  
- Declared in the return type as `paramName is Type`.  
- Enables type-safe code paths after checks.  
- Example: I used a predicate for validating user inputs:

```ts
function isUser(input: any): input is { name: string; age: number } {
  return input && typeof input.name === "string" && typeof input.age === "number";
}

const obj = { name: "Alice", age: 30 };
if (isUser(obj)) {
  console.log(obj.name); // Safe access
}
```

---

### **96. How do template literal types work in TypeScript?**

- Combine string literals and unions to define complex string patterns.  
- Useful for creating strict string formats or dynamic keys.  
- Extendable with generic and mapped types.  
- Example: I created strict route paths using template literals:

```ts
type Route = `/user/${string}`;

const validRoute: Route = "/user/123";
const invalidRoute: Route = "/product/123"; // Error
```

---

### **97. How to combine multiple interfaces in TypeScript?**

- Use intersection types or `extends` for composition.  
- Intersection types merge properties into a single type.  
- Ensure compatibility for overlapping property types.  
- Example: I combined interfaces for modular design:

```ts
interface Address {
  street: string;
  city: string;
}

interface User {
  name: string;
}

type UserWithAddress = User & Address;

const user: UserWithAddress = {
  name: "Alice",
  street: "Main St",
  city: "Wonderland",
};
```

---

### **98. What are type assertions in TypeScript?**

- Force a value to a specific type using `as` or `<type>`.  
- Bypass compiler checks when confident about the type.  
- Use cautiously to avoid runtime errors.  
- Example: I asserted a value during DOM manipulation:

```ts
const input = document.getElementById("username") as HTMLInputElement;
input.value = "Alice";
```

---

### **99. How does the infer keyword work in TypeScript?**

- Extracts types within conditional types.  
- Enables reusability and dynamic inference of complex types.  
- Commonly used in utility types like `ReturnType` or `Parameters`.  
- Example: I inferred the return type of a function:

```ts
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

function greet(): string {
  return "Hello";
}

type GreetReturnType = GetReturnType<typeof greet>; // string
```

---

### **100. What are the benefits of TypeScript’s strict mode?**

- Enforces better code quality and error prevention.  
- Includes features like `noImplicitAny`, `strictNullChecks`, and more.  
- Reduces runtime issues through strict type-checking.  
- Example: I enabled strict mode for a safer codebase:

```json
{
  "compilerOptions": {
    "strict": true
  }
}
```

---

### **101. How do you create a readonly tuple in TypeScript?**

- Use `readonly` keyword before tuple definition.  
- Prevents reassigning elements in the tuple.  
- Immutable tuples enhance safety in complex data structures.  
- Example: I used readonly tuples for API constants:

```ts
const settings: readonly [number, string] = [10, "Light"];
settings[0] = 20; // Error
```

---

### **102. Explain how utility types like Omit work in TypeScript.**

- `Omit` removes specified keys from a type.  
- Simplifies type transformations in reusable code.  
- Often combined with other utility types for flexibility.  
- Example: I omitted sensitive fields in a response type:

```ts
type User = { name: string; age: number; password: string };
type PublicUser = Omit<User, "password">;

const user: PublicUser = { name: "Alice", age: 30 };
```

---

### **103. How does TypeScript handle function overloading?**

- Define multiple signatures for varying parameter combinations.  
- Use a single implementation to fulfill all overloads.  
- Compiler enforces parameter types based on signature.  
- Example: I overloaded a string processing function:

```ts
function process(input: string): string;
function process(input: string[]): string[];
function process(input: any): any {
  return Array.isArray(input) ? input.map(i => i.toUpperCase()) : input.toUpperCase();
}

console.log(process("test")); // TEST
console.log(process(["a", "b"])); // ["A", "B"]
```

---

### **104. What are conditional types in TypeScript?**

- Enable type transformations based on conditions.  
- Use syntax `T extends U ? X : Y`.  
- Flexible for creating advanced generic utilities.  
- Example: I applied conditional types for array handling:

```ts
type ElementType<T> = T extends Array<infer U> ? U : T;

type StringArray = ElementType<string[]>; // string
type NumberType = ElementType<number>; // number
```

---

### **105. How does TypeScript ensure type safety in promise handling?**

- Promises are strongly typed with their resolved value.  
- Ensures proper chaining and error handling.  
- Use `async/await` for clean syntax and type safety.  
- Example: I enforced type-safe API calls with promises:

```ts
async function fetchData(): Promise<string> {
  return "Data";
}

fetchData().then(data => console.log(data)); // Typed as string
```

---

