## MVI Architecture POC Note
###Online references on MVI

[The Contract of Model-View-Intent Architecture](https://proandroiddev.com/the-contract-of-the-model-view-intent-architecture-777f95706c1e)

[Unidirectional data flow on Android using Kotlin](https://proandroiddev.com/unidirectional-data-flow-on-android-the-blog-post-part-1-cadcf88c72f5)

[MVI posts by Hannes Dorfmann](http://hannesdorfmann.com/android/mosby3-mvi-1)

[What is MVI and why move from MVP and MVVM to MVI](https://fueled.com/blog/what-is-mvi-model-view-intent/)

[MVI architecture on Android - Getting Started](https://www.raywenderlich.com/817602-mvi-architecture-for-android-tutorial-getting-started)

### RXJava2
* RxJava operators in general:
  - The **order** matters in the operators of RxJava (or ReactiveX). Each operator works on the result of the previous operator. 
  The comparison case would be the builder pattern, which the order of each methods doesn't matter and the methods work on the object independently.
  <br/>[Operators list of ReativeX official site](http://reactivex.io/documentation/operators.html)
  - One thing I learned from the POC was that when working on the operator chain of an observable, we need to pay special attention
  on the **order** and the **position** of a operator within the current chain. Especially when working with the operator
  which has a function as parameter and in Kotlin we usually pass in as a lambda, the concept is, a operator only works on the
  observable it **directly** attach to, it is unlikely to have the effect on the entire chain. But it requires trial and error.
  - There is always an operator for everything in RxJava
  <br/>[Common Operators](https://medium.com/mindorks/learn-actually-rxjava-rxjava2-operators-by-examples-2f7a7cd343f0)
* RxJava `SubscribeOn()` and `ObserveOn()`:
  - `SubscribeOn()` affect to the entire chain but `ObserveOn()` affect only the chain after it.
  - If there is multiple SubscribeOn(), only the first one takes effect, which is different from the ObserveOn()
* RxJava schedulers:
  <br/>[James' article on the above two items](https://proandroiddev.com/understanding-rxjava-subscribeon-and-observeon-744b0c6a41ea)

### Unit Test
* JUnit and Mockito General

* Test with LiveData and ViewModel architecture component.

* Set up @Rule for thread related testing.

* Issue - Mocked object still executing the actual method.
  - Kotlin [all fields are final](https://github.com/mockito/mockito/issues/1053), need to have all the fields open.
  - Or [set up `mock-maker-inline` in file](https://blog.mindorks.com/mockito-cannot-mock-in-kotlin)
