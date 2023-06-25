# Functions as Values

***TLDR:*** *In functional programming, functions are values. They can be passed as arguments to functions and can be the return values of other functions.*

If you're not familiar with function syntax, here are some resources to get you started:
 - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
 - https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#functions
 - https://www.tutorialspoint.com/haskell/haskell_functions.htm

As a programmer, you probably have written code using loops. 

```typescript
let array = [1, 2, 3, 4, 5]
for(let i = 0; i < array.length; i++){
    console.log(array[i].toString())
}
```

You might have loops accessing the element itself, and you don't worry about the index
```typescript
let array = [1, 2, 3, 4, 5, 6, 7]
for (let element in array) {
    if element % 3 === 0 {
        console.log('fizz')
    } else if element % 5 === 0 {
        console.log('buzz')
    } else if element % 3 === 0 && element % 5 === 0 {
        console.log('fizzbuzz')
    } else {
        console.log(element)
    }
}
```

Often times, the loops that are written have the same structure. There is the `for` section which controls the loop, and the body of the loop which can pretty much be anything else.

I want to point out in these examples is that there is some sort of 'outer' behavior which is the same, and there is some sort of 'inner' behavior that varies. 

Writing `for(let element in array)` every time we want to loop isn't terrible, but it can be a little tedious. What if we wanted to be more expressive, and hide away and encapsulate the loop so we could focus on the behavior rather than the structure? For starters, we can create a function.

```typescript
function loop(array: Array<number>) {
    for (let element in array) {
        ???
    }
}
```

This function now defines iterating behavior, but now what needs to be done with the `???` question marks. How do we give this function custom behavior? In functional programming, functions are considered values, just like Ints, Strings, Arrays, or any other object. Therefore functions can be passed into other functions as parameters. So if we want to replace the `???` so that it can do anything, we will need to pass in a function, then execute it in the loop.

```typescript
function loop(array: Array<number>, func: (element: number) => null) {
    for (let element in array) {
        func(element)
    }
}
```

`func` is the second parameter of loop, which is itself a function. `func` takes a parameter `element` of type `number`. Then in the body of the loop, `func` is executed by passing in each element of the array.

Now, we can give `loop` pretty much any function that takes a `number` and returns nothing. Rewriting the examples from above, we get this:
```typescript
function printIntStrings(num: number) {
    console.log(num.toString())
}

let array = [1, 2, 3, 4, 5]
loop(array, printIntStrings)
```

```typescript
function fizzBuzzLogic(num: number) {
    if number % 3 === 0 {
        console.log('fizz')
    } else if number % 5 === 0 {
        console.log('buzz')
    } else if number % 3 === 0 && number % 5 === 0 {
        console.log('fizzbuzz')
    } else {
        console.log(number)
    }
}

let array = [1, 2, 3, 4, 5, 6, 7]
loop(array, fizzBuzzLogic)
```

Using functions as value isn't only useful for encapsulating looping behavior. It can be used any time you want to allow the function users to vary behavior, particularly when that behavior is surrounded by other, unchanging behavior.

TODO: FUNCTIONS AS RETURN VALUES GOES HERE

When you get further into your programming journey, you will (if you haven't already) see functions without names. Anonymous functions are a convenient way to define behavior without creating a 'real' function. They look something like this:

TypeScript
```typescript
function normalFunctionSyntax(param: string): null {
    //do something...
}

let anonymousFunction = (param: string): null => {
    //do something...

//Execute the functions
normalFunctionSyntax('this is executing a normal function')
anonymousFunction('this is executing an anonymous function')
}
```

Purescript/Haskell
```haskell
normalFunction :: String -> Int
normalFunction param = --do something...

anonymousFunction :: String -> Int
anonymousFunction = (
    \param -> --do something...
)
```

This example shows how anonymous functions look very similar to normal functions. In Typescript, they both have parameters in parentheses and have a function body. The only difference is that the normal function has a name, while the anonymous function has an arrow `=>` after the parameters. Similarily in Purescript and Haskell, both have parameters, but the anonymous function begins with a `\` and has a `->` between the parameters and body.

For the above examples, we can use anonymous functions instead of normal functions.

```typescript
let array = [1, 2, 3, 4, 5]
loop(array, (num: number) => { console.log(num.toString()) })
```

```typescript
let array = [1, 2, 3, 4, 5, 6, 7]
loop(array, (num: number) => {
    if number % 3 === 0 {
        console.log('fizz')
    } else if number % 5 === 0 {
        console.log('buzz')
    } else if number % 3 === 0 && number % 5 === 0 {
        console.log('fizzbuzz')
    } else {
        console.log(number)
    }
})
```

If you are very familiar with Object Oriented Patterns, then you might have recognized that this is the (TODO: Strategy? Delegator? ...) pattern, but without the need for classes and objects.

[Next: Currying](./currying.md)