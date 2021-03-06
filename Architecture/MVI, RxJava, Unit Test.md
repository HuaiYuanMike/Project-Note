### Online references on MVI

[The Contract of Model-View-Intent Architecture](https://proandroiddev.com/the-contract-of-the-model-view-intent-architecture-777f95706c1e)

[Unidirectional data flow on Android using Kotlin](https://proandroiddev.com/unidirectional-data-flow-on-android-the-blog-post-part-1-cadcf88c72f5)

[MVI posts by Hannes Dorfmann](http://hannesdorfmann.com/android/mosby3-mvi-1)

[What is MVI and why move from MVP and MVVM to MVI](https://fueled.com/blog/what-is-mvi-model-view-intent/)

[MVI architecture on Android - Getting Started](https://www.raywenderlich.com/817602-mvi-architecture-for-android-tutorial-getting-started)

[MVI a Reactive Architecture Pattern](https://medium.com/mindorks/mvi-a-reactive-architecture-pattern-45c6f5096ab7)

### RXJava2 Tips

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

### Unit Testing (with RxJava)

* JUnit and Mockito General

* Test with LiveData and ViewModel architecture component.

* @Rule to annotate a `TestRule` object which is very similar to @Before annotation, but is convenient to share between test classes.

* Threading and asynchronous testing 
- The same thread -> Test synchronously with `TestSubscriber`.
- Different Thread -> Test with overriding the RxJava thread handling with the help of `RxJavaPlugins` and `RxAndroidPlugins` within the TestRule. RxJava (1) does it by the RxJavaSchedulerHook and RxAndroidScheduler hook.

[Reference](https://fedepaol.github.io/blog/2015/09/13/testing-rxjava-observables-subscriptions/)

* Issue - Mocked object still executing the actual method.
  - Kotlin [all fields are final](https://github.com/mockito/mockito/issues/1053), need to have all the fields open.
  - Or [set up `mock-maker-inline` in file](https://blog.mindorks.com/mockito-cannot-mock-in-kotlin)
  
  
 ### Android Architecture Component LiveData
 
* Don't expose the LiveData to outter layer
  - In the scenario of keeping the states as a `LiveData` within the `ViewModel`, we should only expose the `LiveData` as a `ImmutableLiveData` to the outer layer observer.
 <br/>[Don't expose LiveData](https://gist.github.com/humblehacker/0eb6458b1df6cf3049e031f36f0615f5)
