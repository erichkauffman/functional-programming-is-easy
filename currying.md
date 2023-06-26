***TLDR:*** *Currying is a technique that makes functions have only one input and one output. If a function takes multiple parameters, when such a function is curried, it takes the first parameter, and returns a function that takes the next parameter. This transforms functions from `function(a, b, c, ...)` to `function(a)(b)(c)(...)`. Currying makes it easier to create new functions on the fly.*

What would you do if you wanted to create a function that multiplies every input by 10?

You would probably create a function that looks like this:
```typescript
function multiplyByTen(x: number): number {
    return x * 10;
}
```

This may seem simple enough, but let's think about it from multiplication's perspective. In order to perform multiplication, the operation needs two inputs. We have provided `10` and `x` here. But what if we thought about `x` as being "open", as in "we have given the multiplication operation one input `10` but have left the other input open."

Now what if multiplication was a function instead of an operator? It would probably look like this:
```typescript
function multiply(x: number, y: number): number {
    return x * y;
}
```

Then if we were to partially apply `10` to the `multiply` function, it should be very similar to the `multiplyByTen` function above:
```typescript
function multiplyByTen(x: number): number {
    return multiply(x, 10);
}
```

What if we wanted to make partial application of `multiply` more convenient?
```typescript
function curriedMultiply(x: number): number => number {
    return (y: number) => { return x * y }
}
```

At first glance, you may be wondering, how is this more convenient? I can barely read it! Let's take a thorough look at it. The beginning of the function should be fairly easy to grasp: this function takes a number `x`, which is pretty normal, but what's not so normal is that it returns a function which takes another `number` and itself returns a `number`. Now take a look at the `return` inside the body of `curriedMultiply`. It return a function which takes a number `y` and multiplies it with `x`. Let's play this out by calling `curriedMultiply` with `10`.

```typescript
let multiplyByTen = curriedMultiply(10)
```

If we look inside `multiplyByTen`, what do you think we would see? `x` is now `10`, but `y` isn't assigned a value yet:
```typescript
curriedMultiply(10): number => number {
    return (y: number) => { return 10 * y }
}

multiplyByTen === (y: number) => { return 10 * y }
```

So now `multiplyByTen` here performs the same computation as the `multiplyByTen` example above. We can call it with another value:
```typescript
let multiplyByTen = curriedMultiply(10)
let result = multiplyByTen(5)
result === 50
```

Since calling `curriedMultiply` returns a function, we can invoke that function immediately with another paretheses and input:
```typescript
curriedMultiply(10)(5) === 50
```

So effectively what we've done here is transform a function call from `function(a, b)` to `function(a)(b)`.

This technique is called "currying". To be a little more precise, the reason for currying is so a function has only one input and only one output. If we look back at `curriedMultiply`, it only has one input (`x`) and has only one output (the function that takes `y`).

With the currying technique, you can make new functions on the fly, for example:
```typescript
let times2 = curriedMultiply(2)

times2(5) === 10
times2(321) === 642

let flipSign = curriedMultiply(-1)

flipSign(7) === -7
flipSign(-3) === 3
```

In PureScript, currying is a built-in feature. Again if we had `multiply` as a function:
```purescript
multiply :: Int -> Int -> Int
multiply x y = x * y
```

We can pass in all the parameters at once:
```purescript
multiply 3 5 == 15
multiply 0 9 == 0
multiply 11 7 == 77
```

Or we can partially apply a value to `multiply` and create new functions:

```purescript
times2 = multiply 2
times2 5 == 10
times2 321 == 642

flipSign = multiply (-1)
flipSign 7 === (-7)
flipSign (-3) === 3
```

[Next: Defining Types](./defining-types.md)