# Functor

***TLDR:*** *A functor is a type that is mappable.*

Yup, that's it. If you can define a `map` function for it, it is a Functor.

Therefore, `Array`s and `List`s are functors because they have a `map` function. Same with `Maybe`s and `Either`s. You could also find a way to `map` over a `Stack` or `Queue`.

In fact, you can define a `map` function for any generic type, so every generic type is a Functor.

[Next: Flat-Mappable](./flat-mappable.md)
