---
title: "When to Use Conditional Types vs Function Overloads in TypeScript"
description: "How to use conditional types to create more precise types"
pubDate: "Mar 23 2023"
---
## Introduction

TypeScript is a powerful language that provides a variety of ways to solve the same problem. Two of the features that help us solve the same problem are [conditional types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html) and [function overloads](https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads)
Today, I'm going to show you when to prefer conditional types over function overloads.

### The Challenge: Doubling Strings and Numbers

Imagine we want to create a `double` function that accepts either a string or a number as its argument and returns the doubled value. We want the returned type to match the input type i.e 2 doubled returns 4 but "two" doubled returns "twotwo".

Let's explore some potential solutions:

#### Attempt 1: Basic Union Types

You may at first be tempted to use a union type instead of overloads or conditional types:

```typescript
function double(x: string | number): string | number 
function double(x: any) { return x + x }`
```

While this function technically works, it's not ideal. We could pass in a number and receive a string and TypeScript wouldn't complain. Not what we want.

#### Attempt 2: Using Generics

You may also be tempted to use Generics:

```typescript
function double<T extends string | number>(x: T): T function double(x: any) { 	return x + x }
```

This version is better, but it has a caveat. If we pass a string _literal_, the type `T` is inferred as the string's literal type:

```typescript
function double<"hello world">(x: "hello world"): "hello world"`
```

#### Attempt 3: Overloading Functions

Let's try the function overload approach:

```typescript
function double(x: string): string 
function double(x: number): number function double(x: any) { 	return x + x }`
```

While this version is close to what we want, it doesn't accept a type of `string|number`. We _could_ go ahead and add another function overload to accept a type of `string|number` but there is a more consice method we could use.

#### The Solution: Conditional Types

Finally, we can use conditional types to create a function that works for all scenarios:

```typescript
function double<T extends string | number>(x: any): T extends string ? string : number {   return x + x }`
```

This version  accepts both strings and numbers and returns the correct type based on the input type. If `T` extends `string`, it returns a `string`. If `T` extends `number`, it returns a `number`. This implementation is both flexible and type-safe.

### Conclusion

Conditional types in TypeScript are a powerful tool that enables us to create flexible and type-safe functions. In this blog post, we've seen how to use conditional types to create a `double` function that works correctly with both strings and numbers. By harnessing the power of conditional types, you can create more robust and maintainable TypeScript code. Bada bing.