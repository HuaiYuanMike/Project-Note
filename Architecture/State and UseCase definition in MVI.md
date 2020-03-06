1. ***Does a variable in state need to be shown in the screen***
Or as long as it affect the rendering in certain way. 
For example `the adZoneIdFormat` and `adZoneSectionValue` in the below:
```java
void requestSection(Observable<Section> sectionObservable) {
        ...
        .zipWith(contentManager.getAdZoneMap(), new Func2<Section, AdZoneMap, Section>() {
            @Override
            public Section call(Section section, AdZoneMap adZoneMap) {
/// TODO:  this is beating the call to receiveSection in subscribe below, so no adzone map ?
                adZoneIdFormat = adZoneMap.zoneIdFormat;
                adZoneSectionValue = adZoneMap.sectionMap.get(section.getSectionRef().getKey());
                return section;
            }
        })
        ...
        .subscribe(new Action1<Section>() {
            @Override
            public void call(Section section) {
                receiveSection(section);
            }
        }, new Action1<Throwable>() {
            @Override
            public void call(Throwable throwable) {
                failedSection(throwable);
            }
        });
    }
```

2. *** How do we deal with the inherited methods in the parent fragment class ***
For the methods which is shared between multiple childs of the parent class and is invoked within the parent class's lifecycle callbacks.
Do we
(1) Have a `ViewModel` connets to the parent UI component (Fragment or Activity) and triggers the action. Just like we have before the MVI.
(2) Have the shared action triggered in the separated ViewModel of the child UI components. Which means that they are no longer shared the parent.
For example in the below:
```java
```

3. *** Does the repository have the states?***
What do we want our repository methods to return? 
(1) A `Change` which contains states?
(2) Just the data from the data source?
```java
```
