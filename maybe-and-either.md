In many programming languages, types can be nullable. For example in Typescript, this means that a variable with the type `number` can be numbers like `1`, `2`, `3`, or can be `null` or `undefined`.

```typescript
function add(x: number, y: number): number {
    return x + y;
}

add(5, null)
```
Here you can see the `add` function expects two numbers, but only receives one, and the other is null. While I admit this is a little contrived since you'd probably never intentionally pass `null` to a function, this illustrates what can happen when you aren't expecting null values.

One way to get around this is to use programming languanges that don't allow certain type to be null. There is a setting in the Typescript compiler that prohibits types from being null

Having non-nullable types is awesome, but what if you run into the situation where it's valid for a variable to be empty? You could add null as a possible to type for the variable. This is better because it forces you to check if it's null before using the variable.
```typescript
function addWithNull(x: number, y: number | null): number | null {
    if(y === null) {
        return null;
    }

    return x + y;
}
```
But the downside to this approach is that you have to check for null every single time this pattern is used, and your code will contain many `if(variable === null)`. This isn't horrible, but it feels like there could be a better way.

Instead of a nullable type, what if we could use types to model potentially empty values? Let's create some types:
```typescript

```

So you may be thinking, what's the point? Why not just use null?
Reasons
 - Functions that don't expect null don't have to check for null
 - When the value could be empty, you must have a plan for it