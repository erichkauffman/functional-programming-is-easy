# Generics

***TLDR:*** *Generics allow us to define structure and behavior without caring about the types they contain.*

What if you had to create a Stack data structure which contains numbers?
```typescript
//This is object-oriented code, not functional :)
class NumberStack {
    stack: Array<number>;

    constructor() {
        this.stack = [];
    }

    push(num: number) {
        this.stack.push(num);
    }

    pop() {
        this.stack.pop();
    }

    top(): number {
        return this.stack.slice(-1)[0];
    }

    empty(): boolean {
        return this.stack.length === 0;
    }
}
```

Now how would you create a Stack of strings?
```typescript
//This is object-oriented code, not functional
class StringStack {
    stack: Array<string>;

    constructor() {
        this.stack = [];
    }

    push(str: string) {
        this.stack.push(str);
    }

    pop() {
        this.stack.pop();
    }

    top(): string {
        return this.stack.slice(-1)[0];
    }

    empty(): boolean {
        return this.stack.length === 0;
    }
}
```

Take a look at the similarities between the number Stack and the string Stack. Besides the types, they have identical behavior. The types of the Stack don't impact the behavior at all. What if instead of defining a Stack for every type, we had a way of leaving the type open so that any type could be used?

The good news is that we have generics! Generic types are types that can contain values of any other type. Take for example an array. You could have an array of ints, or and array of strings, or an array of any other objects. In Typescript, the type signature for an array looks like this:

```typescript
let intArray: Array<number>
```

Any type can be specified in the angle brackets `<>`. The type in the brackets must match the values' type in the array. There could be numbers
```typescript
let intArray: Array<number> = [1, 2, 3, 4, 5]
```

strings
```typescript
let stringArray: Array<string> = ['hello', 'world!']
```

or even other arrays
```typescript
let arrayArray: Array<Array<number>> = [[1, 2], [3], [], [4, 5]]
```


Generics are useful because they allow us to define behavior without caring about it's contents. Back to the Stack, instead of defining a new class for every type that the stack could contain, we can define it once using generics:

```typescript
//This is object-oriented code, not functional
class Stack<T> {
    stack: Array<T>;

    constructor() {
        this.stack = [];
    }

    push(element: T) {
        this.stack.push(element);
    }

    pop() {
        this.stack.pop();
    }

    top(): string {
        return this.stack.slice(-1)[0];
    }

    empty(): boolean {
        return this.stack.length === 0;
    }
}
```

You may be wondering what `<T>` is. Here `T` stands for 'any type'. Instead of using `T`, we can use any upper case word, such as `A`, `B`, `Type`, `StackType`, etc. When we use the new stack for numbers, then when we say `Stack<number>`, the `T` is replaced by `number`.

Here's more information on generics: https://www.typescriptlang.org/docs/handbook/2/generics.html