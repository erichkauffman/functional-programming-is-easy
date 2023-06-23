# Functional Programming in a Nutshell

***TLDR:*** *While functional programming takes some time to get used to, it is fairly similar to other programming paradigms. Functional programming simply prioritizes pure functions and immutable state.*

There's not much I can say here that hasn't been said already. The only thing I want to emphasize is that you don't have to throw out all your previous knowledge and experience to work with functional programming. Most of the concepts you already know are applicable to functional programming. All of the techniques and priciples used in creating good, readable code, such as KISS, DRY, SOLID, and YAGNI, are all just as useful in functional programming. If there's just two things that you will need to get used to with functional programming, it's that functions are always pure, and state is immutable.

If you aren't familiar with those terms, I'll quickly define them here. When a function is pure, it means that for every input, the corresponding output is always the same each time the function is run. Take for example this `add` function:

```typescript
function add(x: number, y: number) {
    return x + y;
}
```

Every time `add` is run with `x = 2` and `y = 2` (`add(2, 2)`) it will *always* return `4`. And `add(2, 3)` will *always* return `5`. But what about this?

```typescript
let counter = 0;

function addWithCounter(x: number, y: number) {
    let sum = x + y + counter;
    counter++;
    return sum;
}
```

`addWithCounter` is not a pure function because the output changes each execution. The first time `addWithCounter` is run with `x = 2` and `y = 2`, it will return `4`, but the next time it is run, it returns `5` even though the input values didn't change. If you don't know what the value of `counter` is, then it will be impossible to predict what `addWithCounter` will be when it is called, and that makes it difficult to understand how the program works.

In purely functional programming languages, this is impossible, and it's because of the next trait of functional programming, that state is immutable. This basically means the variables cannot change. Once data is set, it is set. In the case of `addWithCounter`, the `counter` variable could be outside of the function scope, but it can't change:

```haskell
counter = 0

addWithCounter :: Int -> Int -> Int
addWithCounter x y =
    --using counter from outside the scope of addWithCounter is completely fine
    let
        sum = x + y + counter
        --this line throws the error
        --"The value of counter is undefined here, so this reference is not allowed."
        counter = counter + 1
    in
        sum
```