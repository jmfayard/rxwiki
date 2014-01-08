This section explains operators you can use to combine multiple Observables.

* [**`startWith( )`**](Combining-Observables#startwith) — emit a specified sequence of items before beginning to emit the items from the Observable
* [**`merge( )`**](Combining-Observables#merge) — combine multiple Observables into one
* [**`mergeDelayError( )`**](Combining-Observables#mergedelayerror) — combine multiple Observables into one, allowing error-free Observables to continue before propagating errors
* [**`parallelMerge( )`**](Combining-Observables#parallelmerge) — combine multiple Observables into a smaller number of Observables, to facilitate parallelism
* [**`zip( )`**](Combining-Observables#zip) — combine sets of items emitted by two or more Observables together via a specified function and emit items based on the results of this function
* [**`and( )`, `then( )`, and `when( )`**](Combining-Observables#and-then-and-when) — combine sets of items emitted by two or more Observables by means of `Pattern` and `Plan` intermediaries
* [**`combineLatest( )`**](Combining-Observables#combinelatest) — when an item is emitted by either of two Observables, combine the latest item emitted by each Observable via a specified function and emit items based on the results of this function
* [**`join( )` and `groupJoin( )`**](Combining-Observables#join-and-groupjoin) — combine the items emitted by two Observables whenever one item from one Observable falls within a window of duration specified by an item emitted by the other Observable
* [**`switchOnNext( )`**](Combining-Observables#switchonnext) — convert an Observable that emits Observables into a single Observable that emits the items emitted by the most-recently emitted of those Observables

***

## startWith( )
#### emit a specified sequence of items before beginning to emit the items from the Observable

[[images/rx-operators/startWith.png]]

If you want an Observable to immediately begin emitting a specific sequence of items before it begins emitting the items normally expected from it, pass that specific sequence of items into that Observable's `startWith( )` method, as in the following example:
```groovy
def myObservable = Observable.from([1, 2, 3]);

myObservable.startWith(-3, -2, -1, 0).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
-3
-2
-1
0
1
2
3
```

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#startWith(T...)">`startWith(x, y, ...)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypestartwithscheduler-args">`startWith`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.startwith.aspx">`StartWith`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/12_CombiningSequences.html#StartWith">Introduction to Rx: StartWith</a>

***

## merge( )
#### combine multiple Observables into one

[[images/rx-operators/merge.png]]

You can combine the output of multiple Observables so that they act like a single Observable, by using the `merge( )` method:

```groovy
myMergedObservable = Observable.merge(observable1, observable2, ... )
```

For example, the following code merges the `odds` and `evens` Observables into a single Observable:

```groovy
odds  = Observable.from([1, 3, 5, 7]);
evens = Observable.from([2, 4, 6]);

Observable.merge(odds,evens).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
1
3
2
5
4
7
6
Sequence complete
```

The items emitted by the merged Observable may appear in any order, regardless of which source Observable they came from.

Instead of passing multiple Observables into `merge( )`, you could also pass in a `List<>` of Observables, or even an Observable that emits Observables, and `merge( )` will merge their output into the output of a single Observable.

If any of the individual Observables passed into `merge( )` aborts by invoking `onError`, the `merge( )` call itself will immediately abort and invoke `onError`. If you would prefer a merge that continues emitting the results of the remaining, error-free Observables before reporting the error, use `mergeDelayError( )` instead.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#merge(java.util.List)">`merge(listOfObservables)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#merge(rx.Observable)">`merge(observableThatEmitsObservables)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#merge(rx.Observable...)">`merge(observable1, observable2, ...)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypemergemaxconcurrent--other">`merge`</a> and <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypemergeobservable">`mergeObservable`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.merge.aspx">`Merge`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/12_CombiningSequences.html#Merge">Introduction to Rx: Merge</a>

***

## mergeDelayError( )
#### combine multiple Observables into one but delay errors until completion

[[images/rx-operators/mergeDelayError.png]]

`mergeDelayError( )` behaves much like `merge( )`. The exception is when one of the Observables being merged throws an error. If this happens with `merge( )`, the merged Observable will immediately throw an error itself (that is, it will invoke the `onError` method of its Observer). `mergeDelayError( )`, on the other hand, will hold off on reporting the error until it has given any other non-error-producing Observables that it is merging a chance to finish emitting their items, and it will emit those itself, and will only invoke `onError` when all of the other merged Observables have finished.

Because it is possible that more than one of the merged observables encountered an error, `mergeDelayError( )` may pass information about multiple errors to the `onError` method (which it will never invoke more than once). For this reason, if you want to know the nature of these errors, you should write your `onError` method so that it accepts a parameter of the class `CompositeException`.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#mergeDelayError(java.util.List)">`mergeDelayError(listOfObservables)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#mergeDelayError(rx.Observable)">`mergeDelayError(observableThatEmitsObservables)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#mergeDelayError(rx.Observable...)">`mergeDelayError(observable1, observable2, ...)`</a>

***

## parallelMerge( )
#### combine multiple Observables into a smaller number of Observables, to facilitate parallelism
[[images/rx-operators/parallelMerge.png]]

Use the `parallelMerge( )` method to take an Observable that emits a large number of Observables and to reduce it to an Observable that emits a particular, smaller number of Observables that emit the same set of items as the original larger set of Observables: for instance a number of Observables that matches the number of parallel processes that you want to use when processing the emissions from the complete set of Observables.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#parallelMerge(rx.Observable, int)">`parallelMerge(source,number)`</a> and <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#parallelMerge(rx.Observable, int, rx.Scheduler)">`parallelMerge(source,number,scheduler)`</a>

***

## zip( )
#### combine Observables together via a specified function and emit items based on the results of this function
[[images/rx-operators/zip.png]]

The `zip( )` method returns an Observable that applies a function of your choosing to the combination of items emitted, in sequence, by two (or more) other Observables, with the results of this function becoming the items emitted by the returned Observable. It applies this function in strict sequence, so the first item emitted by the new zip-Observable will be the result of the function applied to the first item emitted by Observable #1 and the first item emitted by Observable #2; the second item emitted by the new zip-Observable will be the result of the function applied to the second item emitted by Observable #1 and the second item emitted by Observable #2; and so forth.

```groovy
myZipObservable = Observable.zip(observable1, observable2, { response1, response2 -> some operation on those responses } );
```

For example, the following code zips together two Observables, one of which emits a series of odd integers and the other of which emits a series of even integers:

```groovy
odds  = Observable.from([1, 3, 5, 7, 9]);
evens = Observable.from([2, 4, 6]);

Observable.zip(odds, evens, {o, e -> [o, e]}).subscribe(
  { println(it); },                          // onNext
  { println("Error: " + it.getMessage()); }, // onError
  { println("Sequence complete"); }          // onCompleted
);
```
```
[1, 2]
[3, 4]
[5, 6]
Sequence complete
```

**Note:** that the zipped Observable completes normally after emitting three items, which is the number of items emitted by the smaller of the two component Observables (`evens`, which emits three even integers).

There are also versions of `zip( )` that accept three or more Observables, as well as a version that accepts an Observable that _emits_ Observables and zips together the emissions of these emitted Observables:

[[images/rx-operators/zip.o.png]]

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#zip(java.util.Collection, rx.util.functions.FuncN)">`zip()`</a> (several versions)
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablezipargs">`zip`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.zip.aspx">`Zip`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/12_CombiningSequences.html#Zip">Introduction to Rx: Zip</a>

***
# and( ), then( ), and when( )
#### combine sets of items emitted by two or more Observables by means of `Pattern` and `Plan` intermediaries
[[images/rx-operators/and_then_when.png]]

The combination of `and( )`, `then( )`, and `when( )` methods operate much like `zip( )` but they do so by means of intermediary data structures.  `and( )` accepts two or more Observables and combines the emissions from each, one set at a time, into `Pattern` objects. `then( )` operates on such `Pattern` objects, transforming them in a `Plan`. `when( )` then transforms these various `Plan` objects into emissions from an Observable.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#and(rx.Observable)">`and( )`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#then(rx.util.functions.Func1)">`then(selector)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#when(java.lang.Iterable)">`when( )`</a> (multiple varieties)
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh229153.aspx">`And`</a>/<a href="http://msdn.microsoft.com/en-us/library/hh211662.aspx">`Then`</a>/<a href="http://msdn.microsoft.com/en-us/library/hh229889.aspx">`When`</a>
* Intro to Rx: <a href="http://www.introtorx.com/content/v1.0.10621.0/12_CombiningSequences.html#AndThenWhen">And-Then-When</a>

***

## combineLatest( )
#### when an item is emitted by either of two Observables, combine the latest item emitted by each Observable via a specified function and emit items based on the results of this function
[[images/rx-operators/combineLatest.png]]

`combineLatest( )` behaves in a similar way to `zip( )`, but while `zip( )` emits items only when all of the zipped source Observables have emitted a previously unzipped item, `combineLatest( )` emits an item whenever _any_ of the source Observables emits an item (so long as each of the source Observables has emitted at least one item). When any of the source Observables emits an item, `combineLatest( )` combines the most recently emitted items from each of the other source Observables, using the function you provide, and emits the return value from that function.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#combineLatest(rx.Observable, rx.Observable, rx.util.functions.Func2)">`combineLatest(observable1, observable2, combineFunction)`</a> (along with versions that take anywhere from three to nine observables)
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypecombinelatestargs-resultselector">`combineLatest`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh211991.aspx">`CombineLatest`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/12_CombiningSequences.html#CombineLatest">Introduction to Rx: CombineLatest</a>

***

## join( ) and groupJoin( )
#### combine the items emitted by two Observables whenever one item from one Observable falls within a window of duration specified by an item emitted by the other Observable
[[images/rx-operators/join_.png]]

The `join( )` method combines the items emitted by two Observables, and selects which items to combine based on duration-windows that you define on a per-item basis. You implement these windows as Observables whose lifespans begin with each item emitted by either Observable. When such a window-defining Observable either emits an item or completes, the window for the item it is associated with closes. So long as an item's window is open, it will combine with any item emitted by the other Observable. You define the function by which the items combine.

[[images/rx-operators/groupJoin.png]]

The `groupJoin( )` method is similar, except that the function you define to combine items emitted by the two Observables pairs individual items emitted by the source Observable with an Observable that emits items from the second Observable that fall in the same window as that item.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#join(rx.Observable, rx.util.functions.Func1, rx.util.functions.Func1, rx.util.functions.Func2)">`join( )`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#groupJoin(rx.Observable, rx.util.functions.Func1, rx.util.functions.Func1, rx.util.functions.Func2)">`groupJoin( )`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh229750.aspx">`Join`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh244235.aspx">`GroupJoin`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypejoinright-leftdurationselector-rightdurationselector-resultselector">`join`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypegroupjoinright-leftdurationselector-rightdurationselector-resultselector">`groupJoin`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/17_SequencesOfCoincidence.html#Join">Introduction to Rx: Join</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/17_SequencesOfCoincidence.html#GroupJoin">Introduction to Rx: GroupJoin</a>

***

## switchOnNext( )
#### convert an Observable that emits Observables into a single Observable that emits the items emitted by the most-recently emitted of those Observables
[[images/rx-operators/switchDo.png]]

`switchOnNext( )` subscribes to an Observable that emits Observables. Each time it observes one of these emitted Observables, the Observable returned by `switchOnNext( )` begins emitting items from that Observable. When a new Observable is emitted, `switchOnNext( )` stops emitting items from the earlier-emitted Observable and begins emitting items from the new one.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#switchOnNext(rx.Observable)">`switchOnNext(sequenceOfSequences)`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableprototypeswitch">`switchLatest`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/hh229197.aspx">`Switch`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/12_CombiningSequences.html#Switch">Introduction to Rx: Switch</a>