# Type Alias vs Interface in TypeScript

**Type aliases** and **interfaces** are two commonly used ways to define the structure and shape of data in TypeScript.

## Structure of a Type Alias

```ts
type User = {
  name: string;
  age: number;
  email: string;
};
```

## Structure of an Interface

```ts
interface User {
  name: string;
  age: number;
  email: string;
}
```

## Differences

### 1. Type Alias Supports More Types

A **type alias** can define object shapes as well as **unions, intersections, tuples, primitive types, and function types**. Interfaces primarily describe **object shapes** and can also be used to define contracts for classes.

### 2. Declaration Merging

**Type aliases do not support declaration merging**, whereas **interfaces support declaration merging**.

### 3. Contracts for Classes

Interfaces are commonly used to define **contracts for classes**. A class can implement an interface and must follow the structure defined by that interface.

Type aliases can also describe object structures, but interfaces are generally preferred when designing contracts for classes.



### Use `type` when:

- I need **union types**.
- I need **intersection types**.
- I need to define **tuples**.
- I need **function types**.
- I need **primitive type aliases**.

### Use `interface` when:

- I need to design **object structures**.
- I need to define **contracts for classes**.
- I am building **public APIs**.
- I am working with **object-oriented TypeScript code**.
- I want to take advantage of **declaration merging**.

## Conclusion

Both **type aliases** and **interfaces** are useful for different purposes.

I will use **`type`** when working with unions, intersections, tuples, function types, primitive aliases, or more complex type combinations.

I will use **`interface`** when designing object structures, defining contracts for classes, building public APIs, or writing object-oriented TypeScript code.