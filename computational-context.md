How do you get the number 5 out of the list `[2, 5, 4]`? You might access it by index.

```typescript
let list = [2, 5, 4]
let five = list[1]
```

Or you might search for the element.

```typescript
let list = [2, 5, 4]
let five = list.find((element) => { element == 5 })
```

There are many ways of getting numbers out of lists. But, what do these examples have in common? It might seem too obvious; you have to deal with the fact that 5 is inside the list. You must interact with the list before you can have the 5.

What about a `Promise` in Typescript? What if you expected to get the number 5 from an HTTP request in the form of a Promise?
```typescript
//typescript example of a Promise
```
Just like the List in the previous example, you have to interact with the Promise first before you can access the 5.

Can you see the similarity in structure between the List and the Promise? In both cases, you have to work with the container before you can use the value.

Let's take a moment to examine the idea of containment. When we see `List<number>`, we might say "The List contains numbers" or for the type `Tree<string>` "The Tree contains strings", but what about a Promise? Does `Promise<number>` mean "The Promise contains a number"? Well, kind of. But kind of not. An HTTP request is communication, not a container. Instead of using the containment language, what if we instead said "When the Promise resolves successfully, it will give you a number"? While not using containment, this seems to discribe it fairly well. What about `List<number>`? "When the List resolves successfully, it will give you a number". That's true, you have to access the insides of the list before you get the 5. And for `Tree<string>`, "if you resolve the Tree-ness, it will give you a string".

TODO: Add examples about Maybe and Either

Hopefully this sheds some light on the historically confusing type in Haskell, the `IO` type. Unlike other types, it doesn't feel like it contains anything. We know it comes from interacting with user input or the file system. Just like with the Promise, when you see something like `IO String`, it means "if you resolve the IO-ness of the value, then you will get a string".

[Next: Mappable](./mappable.md)