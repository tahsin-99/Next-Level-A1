# TypeScript's Type System: `any`, `unknown`, and `never`

TypeScript's type system provides different types that behave differently from normal types, such as `any`, `unknown`, and `never`.

Think of types as **sets of possible values**.

- `unknown` is the **top type**. Every value is assignable to it. It represents the set of all possible values.
- `never` is the **bottom type**. No value is assignable to it. It represents the empty set, and it is assignable to every other type.
- `any` is a special **escape hatch** that sits outside the normal type hierarchy. It behaves as both a top type and a bottom type, so the compiler stops checking.

---

## `any`

`any` is a type that tells TypeScript to **stop checking the type** of a value.

If we explicitly use `any`, TypeScript allows us to perform almost any operation on that value without checking whether the operation is valid.

### Example

```ts
let value: any = "Hello";

value = 100;
value = true;
```

We can also call methods without checking whether they actually exist:

```ts
let data: any = "Hello";

data.toUpperCase();
data.toFixed();
data.someRandomFunction();
```

TypeScript allows these operations because `data` is `any`.

However, this can lead to **runtime errors** when the operation does not actually exist for the value.

For example:

```ts
let data: any = "Hello";

data.toFixed();
```

TypeScript does not complain, but `toFixed()` is not a string method, so this can cause an error at runtime.

---

## `unknown`

The `unknown` type also allows a value to contain **any kind of data**, but it is much safer than `any`.

The main difference is that we **cannot directly perform operations on an `unknown` value** without first checking its type.

For example:

```ts
let data: unknown = "Hello";

data.toUpperCase(); // Error
```

TypeScript gives an error because it does not know whether `data` is actually a string.

We have to check the type first.

```ts
if (typeof data === "string") {
    data.toUpperCase();
}
```

After the `typeof` check, TypeScript knows that `data` is a string, so `toUpperCase()` is safe to use.

### Why is `unknown` safer?

With `any`:

```ts
let data: any = "Hello";

data.toUpperCase();
data.toFixed();
data.someRandomFunction();
```

TypeScript allows all of these because the type is `any`.

This can lead to runtime errors.

With `unknown`:

```ts
let data: unknown = "Hello";

data.toUpperCase(); // Error
```

We must first determine the actual type:

```ts
if (typeof data === "string") {
    data.toUpperCase();
}
```

This forces us to handle the value safely.

---

## `unknown` for External Data

`unknown` is especially useful when handling **external data**, such as API responses.

When data comes from an external source, we cannot always be certain about its type or structure.

Using `unknown` makes us check the data before using it.

For example:

```ts
const response: unknown = await fetchData();

if (typeof response === "string") {
    console.log(response.toUpperCase());
}
```

This is safer than using `any` because TypeScript requires us to verify the type before accessing its properties or methods.

---

## `never`

The `never` type represents a value that **never occurs**.

A function that always throws an error is a good example:

```ts
function throwError(message: string): never {
    throw new Error(message);
}
```

This function never reaches a normal return statement because it always throws an error.

Therefore, its return type is `never`.

Another example is an infinite loop:

```ts
function infiniteLoop(): never {
    while (true) {
        console.log("Running...");
    }
}
```

This function also never reaches a normal return statement.

---



A simple way to remember:

```text
any
↓
"I don't care about the type."

unknown
↓
"I don't know the type yet, so check it first."

never
↓
"This value can never exist."
```

---

## Why Should We Use `unknown` Over `any`?

Whenever the actual type of a value is not known, `unknown` is generally preferred over `any` because it preserves TypeScript's type safety.

Using `unknown` provides:

- **Better type safety**
- **Fewer runtime errors**
- **Better code reliability**
- **Better IDE support**
- **More predictable code**
- **Safer handling of external data**







