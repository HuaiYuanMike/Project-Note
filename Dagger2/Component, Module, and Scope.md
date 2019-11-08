## Why using Dagger2 ?

  To achieve Dependency Inversion 
  
* `@Module`, `@Inject`, and `@Provide`:

  - `@Inject` has two functionalities:<br/>
    a. At variable - Indicate that we need the dependency<br/>
    b. At constructor - Tell the Dagger to put this object into dependency graph.
    
  - `@Provide` and `@Module`: <br/>
    There are cases which we can not use @Inject to tell Degger that it should provide the dependency with the dependencies graph:
    a. Providing the 3-rd party library.<br/>
    b. An interface.<br/>
    c. Dependency which needs further configuration other than constructor.
    
    Therefore, we need to:<br/>
      
      a. Annotate a class with @Module<br/>
      b. Within the @Module annotated class we need to have methods which annotated with @Provide 
    and return the type of the dependencies we want with the @Module.<br/>
      c. Added the @Module to the `@Component`.
    
* `@Component`:
  -  The role of @Component is somehow like a root of the dependencies graph. 
  In order to get a dependency we need and which are provided by the dependencies graph, we could:<br/>
    
    a. Have a method that returns the desired object type that provided by the graph ( or simply using the default getter() by Kotlin, 
  which means we declare a variable within the @component class).<br/>
    b. Have a method that tells the system where we want to inject the graph into, 
  which will then require calling the inject() method within the desired class.

  - `@Component` depends on modules, dependencies provided by a module could be accessed by another if they are in the same component.
  
  - `@Component` is like a root of a dependencies graph, because the dependencies provided by the component could be accessed by the injected class.

* Component scope, custom scopes:<br/>
  [Referemnce](https://proandroiddev.com/dagger-2-part-ii-custom-scopes-component-dependencies-subcomponents-697c1fa1cfc)<br/>
  - `@Singleton` is like the following, the only difference between it and our custom scopes is that is is provided by the Dagger library.
    ```Java
    @Scope
    @Retention(RetentionPolicy.RUNTIME)
    public @interface Singleton {
    }
    ```
    __It’s we who are in charge for “scoped” objects lifecycle__
    
  - **Two dependent components cannot have the same scope**
  
  - There are two ways to add dependency of components to a component
  
    a. `@Component(dependencies = {...})`<br/>
    This way sub-component has the access to the dependencies exposed by the parent component
    b. 
