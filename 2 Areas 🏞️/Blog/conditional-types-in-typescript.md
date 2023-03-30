---
title: "Conditional Types in Typescript"
description: "How to use conditional types to your advantage"
pubDate: "Mar 23 2023"
---

#typescript #effective-typescript

This would allow us to pass in a number but receive a string. Not what we want.
```typescript
function double(x: string | number): string | number
function double(x: any) {
	return x + x
}
```

This is better... 
```typescript
function double<T extends string | number>(x: T): T
function double(x: any) {
	return x + x
}
```

However, if we pass a string _literal_ the type T is inferred as the strings literal type:
```typescript
function double<"hello world">(x: "hello world"): "hello world"
```

This is close:
```typescript
function double(x: string): string
function double(x: number): number
function double(x: any) {
	return x + x
}
```

However, it doesn't accept a type of `string|number`.

This works for all scenarios:
```typescript
function double<T extends string | number>(x: any): T extends string ? string : number {
  return x + x
}
```