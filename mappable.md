What would you do if you had a list of numbers, let's say `[1,2,3,4,5]`, and you want to add one to each? Try solving this in your favorite programming language now.

This is often done using a for loop:
```typescript
//typescript for loop
```

What if you had a list of strings, and you want to append `'s'` to each? Try solving this one too.
```typescript
//typescript for loop
```

What if you had a list of inventory items, and you want each one to be in a React component?
```typescript
//typescript for loop
```

Take a look at the structure of each of the examples. Do you see how the loops are manipulating the lists in the same way?
```typescript
//typescript for loop
```

In each of the examples, we are taking each item of the array and doing something to it based on the body of the for block.

One of the most important concepts in functional programming is mapping. Mapping is applying a function to each value in a structure. For example, assume we have an `Array` of `number`s in Typescript:

```typescript
let numbers: Array<number> = [1, 2, 3, 4, 5];
```

Then we can apply a function to each number in the array. We will add 1 to each:

```typescript
let numbers: Array<number> = [1, 2, 3, 4, 5];
let mappedNumbers: Array<number> = numbers.map((num: number) => num + 1);
mappedNumbers == [2, 3, 4, 5, 6];
```

In this example, we have mapped from a type `number`, to a `number`. But, we can also map to a different type, such as from a `number` to a `string`:

```typescript
let numbers: Array<number> = [1, 2, 3, 4, 5];
let intStrings: Array<string> = numbers.map((num: number) => num.toString());
intString == ['1', '2', '3', '4', '5'];
```

Now let's take this concept to Haskell.
We'll map over a list using the add 1 function:
```haskell
numbers :: List Int = [1, 2, 3, 4, 5]
mappedNumbers :: List Int = map (\num -> num + 1) numbers
mappedNumbers == [2, 3, 4, 5, 6]
```

And we can add `'s'` to strings:
```haskell
--add s mapping
```

In PureScript, `map` is defined as `map :: (a -> b) -> container a -> container b`. This says that the first argument is a function taking any type `a` and returning any type `b`. Then the second argument is a container (such as a `List`) containing elements that have the type `a`, and finally returns the container with type `b`. The `b` values are the `a` values that have been transformed by the provided function.

We can map to any type, including those that provide structure. This example maps each element from an `Int` to a list of ints (`List Int`):
```haskell
numbers :: List Int = [1, 2, 3, 4, 5]
listsOfNumbers :: List (List Int) = map (\num -> [num]) numbers
listOfNumbers == [[1], [2], [3], [4], [5]]
```

An important concept about mapping is that it leaves the surrounding structure unchanged. In the previous examples, we didn't change the number of elements in the array. In fact, we don't need to care about the contents of the array. If the array was empty, we could still map over it, but the resulting array would also be empty:

```haskell
emptyNumbers :: List Int = []
emptyMapped :: List Int = map (\num -> num * 8 + 1 - 93) emptyNumbers
emptyMapped == []
```

We can map values in structures other than lists. For example, we can map over the `Maybe`:
```haskell
maybeString :: Maybe String = Just "hello"
mappedMaybe :: Maybe String = map (\str -> length str)
mappedMaybe == Just 5
```

Since Maybe has both `Just` and `Nothing` values, we can also map over `Nothing`.
```haskell
nothing :: Maybe String = Nothing
mappedNothing :: Maybe Int = map (\str -> length str) nothing
mappedNothing == Nothing
```

Any generic type is mappable, as in we can define how `map` works for any generic type. For example in `Typescript`, `map` might be defined as such:
```typescript
class Array<A> {
    arr = []
    ...

    function map<B>(func: A => B): Array<B> {
        let newArray = [];
        for (element of arr) {
            newArray.push(func(element));
        }
        return newArray;
    }
    ...
}
```

In PureScript, this is how `map` is defined for `Maybe`.
```haskell
```