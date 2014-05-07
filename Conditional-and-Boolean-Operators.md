This section explains operators with which you conditionally emit or transform Observables, or can do boolean evaluations of them:

### Conditional Operators
* [**`amb( )`**](Conditional-and-Boolean-Operators#wiki-amb) — given two or more source Observables, emits all of the items from the first of these Observables to emit an item
* [**`defaultIfEmpty( )`**](Conditional-and-Boolean-Operators#wiki-defaultifempty) — emit items from the source Observable, or emit a default item if the source Observable completes after emitting no items
* (`contrib-computation-expressions`) [**`doWhile( )`**](Conditional-and-Boolean-Operators#wiki-dowhile) — emit the source Observable's sequence, and then repeat the sequence as long as a condition remains true
* (`contrib-computation-expressions`) [**`ifThen( )`**](Conditional-and-Boolean-Operators#wiki-ifthen) — only emit the source Observable's sequence if a condition is true, otherwise emit an empty or default sequence
* [**`skipUntil( )`**](Conditional-and-Boolean-Operators#wiki-skipuntil) — discard items emitted by a source Observable until a second Observable emits an item, then emit the remainder of the source Observable's items
* [**`skipWhile( )` and `skipWhileWithIndex( )`**](Conditional-and-Boolean-Operators#wiki-skipwhile-and-skipwhilewithindex) — discard items emitted by an Observable until a specified condition is false, then emit the remainder
* (`contrib-computation-expressions`) [**`switchCase( )`**](Conditional-and-Boolean-Operators#wiki-switchcase) — emit the sequence from a particular Observable based on the results of an evaluation
* [**`takeUntil( )`**](Conditional-and-Boolean-Operators#wiki-takeuntil) — emits the items from the source Observable until a second Observable emits an item
* [**`takeWhile( )` and `takeWhileWithIndex( )`**](Conditional-and-Boolean-Operators#wiki-takewhile-and-takewhilewithindex) — emit items emitted by an Observable as long as a specified condition is true, then skip the remainder
* (`contrib-computation-expressions`) [**`whileDo( )`**](Conditional-and-Boolean-Operators#wiki-whiledo) — if a condition is true, emit the source Observable's sequence and then repeat the sequence as long as the condition remains true

> (`contrib-computation-expressions`) — indicates that this operator is currently part of the optional `contrib-computation-expressions` package and is not included with the standard RxJava set of operators

### Boolean Operators
* [**`all( )`**](Conditional-and-Boolean-Operators#wiki-all) — determine whether all items emitted by an Observable meet some criteria
* [**`contains( )`**](Conditional-and-Boolean-Operators#wiki-contains) — determine whether an Observable emits a particular item or not
* [**`exists( )` and `isEmpty( )`**](Conditional-and-Boolean-Operators#wiki-exists-and-isempty) — determine whether an Observable emits any items or not
* [**`sequenceEqual( )`**](Conditional-and-Boolean-Operators#wiki-sequenceequal) — test the equality of the sequences emitted by two Observables

***

## amb( )
#### given two or more source Observables, emits all of the items from the first of these Observables to emit an item
[[images/rx-operators/amb.png]]

When you pass a number of source Observables to `amb( )`, it will pass through the emissions and messages of exactly one of these Observables: the first one that emits an item to `amb( )`. It will ignore and discard the emissions of all of the other source Observables.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#amb(java.lang.Iterable)">`amb()`</a> (several varieties)
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableambargs">`amb`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.amb(v=vs.103).aspx">`Amb`</a>

***

## defaultIfEmpty( )
#### emit items from the source Observable, or emit a default item if the source Observable completes after emitting no items
[[images/rx-operators/defaultIfEmpty.png]]

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#defaultIfEmpty(T)">`defaultIfEmpty(default)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypedefaultifemptydefaultvalue">`defaultIfEmpty`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.defaultifempty.aspx">`DefaultIfEmpty`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/06_Inspection.html#DefaultIfEmpty">Introduction to Rx: DefaultIfEmpty</a>

***

## doWhile( )
#### emit the source Observable's sequence, and then repeat the sequence as long as a condition remains true
[[images/rx-operators/doWhile.png]]

The `doWhile( )` operator emits the sequence emitted by the source Observable and then checks to see if a specified condition is true; if so it will resubscribe and reemit the source Observable's sequence, repeating this process until the condition becomes false.

#### see also:
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypedowhilecondition-source">`doWhile`</a>

***

## ifThen( )
#### only emit the source Observable's sequence if a condition is true, otherwise emit an empty or default sequence
[[images/rx-operators/ifThen.png]]

The `ifThen( )` operator evaluates a function and emits the source Observable's sequence if the function evaluates as true, and otherwise either emits an empty sequence or the sequence from an alternate Observable you specify.

#### see also:
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableifcondition-thensource-elsesource">`if`</a>
* <a href="http://weblogs.asp.net/podwysocki/archive/2010/06/18/introduction-to-the-reactive-extensions-for-javascript-conditionals.aspx#content2">Introduction to the Reactive Extensions for JavaScript – Conditionals</a>

***

## skipUntil( )
#### discard items emitted by a source Observable until a second Observable emits an item, then emit the remainder of the source Observable's items
[[images/rx-operators/skipUntil.png]]

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#skipUntil(rx.Observable)">`skipUntil(other)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeskipuntilother">`skipUntil`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh229358.aspx">`SkipUntil`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/05_Filtering.html#SkipUntilTakeUntil">Introduction to Rx: SkipUntil and TakeUntil</a>

***

## skipWhile( ) and skipWhileWithIndex( )
#### discard items emitted by an Observable until a specified condition is false, then emit the remainder
[[images/rx-operators/skipWhile.png]]

The `skipWhile( )` method returns an Observable that discards items emitted by the source Observable until such time as a function applied to an item emitted by that Observable returns `false`, whereupon the new Observable emits that item and the remainder of the items emitted by the source Observable.

```groovy
numbers = Observable.from( [1, 2, 3, 4, 5, 6, 7, 8, 9] );

numbers.skipWhile({ (5 != it) }).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
5
6
7
8
9
Sequence complete
```

> **Note:** in the scala language adaptor for RxJava, this method is called `dropWhile( )`.

[[images/rx-operators/skipWhileWithIndex.png]]

The `skipWhileWithIndex( )` method is similar, but your function takes an additional parameter: the (zero-based) index of the item being emitted by the source Observable.
```groovy
numbers = Observable.from( [1, 2, 3, 4, 5, 6, 7, 8, 9] );

numbers.skipWhileWithIndex({ it, index -> ((it < 6) || (index < 5)) }).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
6
7
8
9
Sequence complete
```

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#skipWhile(rx.util.functions.Func1)">`skipWhile(predicate)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#skipWhileWithIndex(rx.util.functions.Func2)">`skipWhileWithIndex(predicate)`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.skipwhile.aspx">`SkipWhile`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeskipwhilepredicate-thisarg">`skipWhile`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/05_Filtering.html#SkipWhileTakeWhile">Introduction to Rx: SkipWhile and TakeWhile</a>

***

## switchCase( )
#### emit the sequence from a particular Observable based on the results of an evaluation
[[images/rx-operators/switchCase.png]]

The `switchCase( )` operator evaluates a case and passes control to a particular one of a set of Observables based on the case.

#### see also:
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablecaseselector-sources-elsesourcescheduler">`case`</a>
* <a href="http://weblogs.asp.net/podwysocki/archive/2010/06/18/introduction-to-the-reactive-extensions-for-javascript-conditionals.aspx#content2">Introduction to the Reactive Extensions for JavaScript – Conditionals</a>

***

## takeUntil( )
#### emits the items from the source Observable until another Observable emits an item
[[images/rx-operators/takeUntil.png]]

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#takeUntil(rx.Observable)">`takeUntil(other)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypetakeuntilother">`takeUntil`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh229530.aspx">`TakeUntil`</a>

***

## takeWhile( ) and takeWhileWithIndex( )
#### emit items emitted by an Observable as long as a specified condition is true, then skip the remainder
[[images/rx-operators/takeWhile.png]]

The `takeWhile( )` method returns an Observable that mirrors the behavior of the source Observable until such time as a function applied to an item emitted by that Observable returns `false`, whereupon the new Observable invokes `onCompleted( )`.

```groovy
numbers = Observable.from( [1, 2, 3, 4, 5, 6, 7, 8, 9] );

numbers.takeWhile({ ((it < 6) || (0 == (it % 2))) }).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
1
2
3
4
5
6
Sequence complete
```

[[images/rx-operators/takeWhileWithIndex.png]]
The `takeWhileWithIndex( )` method is similar, but your function takes an additional parameter: the (zero-based) index of the item being emitted by the source Observable.
```groovy
numbers = Observable.from( [1, 2, 3, 4, 5, 6, 7, 8, 9] );

numbers.takeWhileWithIndex({ it, index -> ((it < 6) || (index < 5)) }).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
1
2
3
4
5
Sequence complete
```

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#takeWhile(rx.util.functions.Func1)">`takeWhile(predicate)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#takeWhileWithIndex(rx.util.functions.Func2)">`takeWhileWithIndex(predicate)`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.takewhile.aspx">`TakeWhile`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypetakewhilepredicate-thisarg">`takeWhile`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/05_Filtering.html#SkipWhileTakeWhile">Introduction to Rx: SkipWhile and TakeWhile</a>

***

## whileDo( )
#### if a condition is true, emit the source Observable's sequence and then repeat the sequence as long as the condition remains true
[[images/rx-operators/whileDo.png]]

If a specified condition evaluates as true, `whileDo( )` will emit the sequence emitted by the source Observable. It will then check to see if the condition remains true and will resubscribe and reemit the source Observable's sequence if so; repeating this process until the condition becomes false.

#### see also:
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablewhilecondition-source">`while`</a>

***

## all( )
#### determine whether all items emitted by an Observable meet some criteria
[[images/rx-operators/all.png]]

Pass an function to `all( )` that accepts an item emitted by the source Observable and returns a boolean value based on an evaluation of that item, and `all( )` will emit `true` if and only if that function returned true for every item emitted by the source Observable.

```groovy
numbers = Observable.from([1, 2, 3, 4, 5]);

println("all even?" )
numbers.all({ 0 == (it % 2) }).subscribe({ println(it); });

println("all positive?");
numbers.all({ 0 < it }).subscribe({ println(it); });
```
```
all even? 
false
all positive? 
true
```

> **Note:** in the scala language adaptor for RxJava, this operator is called `forall( )`.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#all(rx.util.functions.Func1)">`all(predicate)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeallpredicate-thisarg">`all`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh229537.aspx">`All`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/06_Inspection.html#All">Introduction to Rx: All</a>

***

## contains( )
#### determine whether an Observable emits a particular item or not
[[images/rx-operators/contains.png]]

Pass the `contains( )` operator a particular item, and it will emit `true` if that item is emitted by the source Observable, or `false` if the source Observable terminates without emitting that item.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#contains(T)">`contains(item)`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.contains.aspx">`Contains`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypecontainsvalue-comparer">`contains`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/06_Inspection.html#Contains">Introduction to Rx: Contains</a>

***

## exists( ) and isEmpty( )
#### determine whether an Observable emits any items or not
[[images/rx-operators/exists.png]]

When you apply the `exists( )` operator to a source Observable, the resulting Observable will emit `true` and complete if the source Observable emits one or more items before completing, or it will emit `false` and complete if the source Observable completes without emitting any items.

[[images/rx-operators/isEmpty.png]]
The inverse of this is the `isEmpty( )` operator. Apply it to a source Observable and the resulting Observable will emit `true` and complete if the source Observable completes without emitting any items, or it will emit `false` and complete if the source Observable emits any item before completing.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#exists(rx.util.functions.Func1)">`exists(predicate)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#isEmpty()">`isEmpty()`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeanypredicate-thisarg">`any`</a> and <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeisempty">`isEmpty`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.any.aspx">`Any`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/06_Inspection.html#Any">Introduction to Rx: Any</a>

***

## sequenceEqual( )
#### test the equality of sequences emitted by two Observables
[[images/rx-operators/sequenceEqual.png]]

Pass `sequenceEqual( )` two Observables, and it will compare the items emitted by each Observable, and emit `true` only if both sequences are the same. You can optionally pass a third parameter: a function that accepts two items and returns `true` if they are equal according to a standard of your choosing.
```groovy
def firstfour = Observable.from([1, 2, 3, 4]);
def firstfouragain = Observable.from([1, 2, 3, 4]);
def firstfive = Observable.from([1, 2, 3, 4, 5]);
def firstfourscrambled = Observable.from([3, 2, 1, 4]);

println('firstfour == firstfive?');
Observable.sequenceEqual(firstfour, firstfive).subscribe({ println(it); });
println('firstfour == firstfouragain?');
Observable.sequenceEqual(firstfour, firstfouragain).subscribe({ println(it); });
println('firstfour == firstfourscrambled?');
Observable.sequenceEqual(firstfour, firstfourscrambled).subscribe({ println(it); });
```
```
firstfour == firstfive?
false
firstfour == firstfouragain?
true
firstfour == firstfourscrambled?
false
```

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#sequenceEqual(rx.Observable, rx.Observable)">`sequenceEqual(observable1, observable2)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#sequenceEqual(rx.Observable, rx.Observable, rx.util.functions.Func2)">`sequenceEqual(observable1, observable2, equalityFunction)`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.sequenceequal.aspx">`SequenceEqual`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypesequenceequalsecond-comparer">`sequenceEqual`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/06_Inspection.html#SequenceEqual">Introduction to Rx: SequenceEqual</a>
