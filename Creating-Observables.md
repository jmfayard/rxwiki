This section explains methods that create Observables.

* [**`from( )`**](Creating-Observables#wiki-from) — convert an Iterable, a Future, or an Array into an Observable
* [**`just( )`**](Creating-Observables#wiki-just) — convert an object into an Observable that emits that object
* [**`repeat( )`**](Creating-Observables#wiki-repeat) — create an Observable that emits a particular item or sequence of items repeatedly
* [**`create( )`**](Creating-Observables#wiki-create) — create an Observable from scratch by means of a function
* [**`defer( )`**](Creating-Observables#wiki-defer) — do not create the Observable until a Subscriber subscribes; create a fresh Observable on each subscription
* [**`range( )`**](Creating-Observables#wiki-range) — create an Observable that emits a range of sequential integers
* [**`interval( )`**](Creating-Observables#wiki-interval) — create an Observable that emits a sequence of integers spaced by a given time interval
* [**`timer( )`**](Creating-Observables#wiki-timer) — create an Observable that emits a single item after a given delay
* [**`empty( )`**](Creating-Observables#wiki-empty-error-and-never) — create an Observable that emits nothing and then completes
* [**`error( )`**](Creating-Observables#wiki-empty-error-and-never) — create an Observable that emits nothing and then signals an error
* [**`never( )`**](Creating-Observables#wiki-empty-error-and-never) — create an Observable that emits nothing at all

***

## from( )
#### convert an Iterable, a Future, or an Array into an Observable
[[images/rx-operators/from.png]]

You can convert an object that supports `Iterable` into an Observable that emits each iterable item in the object, or an object that supports `Future` into an Observable that emits the result of the `get` call, simply by passing the object into the `from( )` methods, for example:

```groovy
myObservable = Observable.from(myIterable);
```

You can also do this with arrays, for example:

```groovy
myArray = [1, 2, 3, 4, 5];
myArrayObservable = Observable.from(myArray);
```

This converts the sequence of values in the iterable object or array into a sequence of items emitted, one at a time, by an Observable.

An empty iterable (or array) can be converted to an Observable in this way. The resulting Observable will invoke `onCompleted()` without first invoking `onNext()`.

Note that when the `from( )` method transforms a `Future` into an Observable, such an Observable will be effectively blocking, as its underlying `Future` blocks.

> **Note:** in the scala language adaptor for RxJava, the version of this method that works with sequences (arrays) is called `items( )`.


#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#from(java.util.concurrent.Future)">`from(future)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#from(java.util.concurrent.Future, long, java.util.concurrent.TimeUnit)">`from(future, timeout, unit)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#from(java.util.concurrent.Future, rx.Scheduler)">`from(future, scheduler)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#from(java.lang.Iterable)">`from(iterable)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#from(T...)">`from(array)`</a>
* RxJS: [`fromArray`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablefromarrayarray-scheduler)
* RxJS: [`fromPromise`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablefrompromisepromise)
* Linq: [`ToObservable`](http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.toobservable.aspx)

***

## just( )
#### convert an object into an Observable that emits that object
[[images/rx-operators/just.png]]

To convert any object into an Observable that emits that object, pass that object into the `just( )` method.

```groovy
// Observable emits "some string" as a single item
def observableThatEmitsAString = Observable.just("some string"); 
// Observable emits the list [1, 2, 3, 4, 5] as a single item
def observableThatEmitsAList = Observable.just([1, 2, 3, 4, 5]); 
```

This has some similarities to the `from( )` method, but note that if you pass an iterable to `from( )`, it will convert an iterable object into an Observable that emits each of the items in the iterable, one at a time, while the `just( )` method would convert the iterable into an Observable that emits the entire iterable as a single item.

Note that if you pass `null` to `just( )`, the resulting Observable will _not_ merely call `onCompleted( )` without calling `onNext( )`. It will instead call `onNext( null )` before calling `onCompleted( )`.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#just(T)">`just(value)`</a>

***

## repeat( )
#### create an Observable that emits the sequence of items emitted by the source Observable repeatedly
[[images/rx-operators/repeat.o.png]]

There are also versions of `repeat( )` that operate on a scheduler that you specify, and that repeat only a certain number of times before terminating.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#repeat()">`repeat( )`</a> and <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#repeat(rx.Scheduler)">`repeat(scheduler)`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.repeat.aspx">`Repeat`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablerepeatvalue-repeatcount-scheduler">`repeat`</a>

***

## create( )
#### create an Observable from scratch by means of a function
[[images/rx-operators/create.png]]

You can create an Observable from scratch by using the `create( )` method. You pass this method a function that accepts as its parameter the Subscriber that is passed to an Observable’s `subscribe( )` method (or that is derived from the `Observerer` that is passed to that method). Write the function you pass to `create( )` so that it behaves as an Observable — calling the passed-in Subscriber’s `onNext( )`, `onError( )`, and `onCompleted( )` methods appropriately. For example:

```groovy
def myObservable = Observable.create({ aSubscriber ->
  try {
    for (int i = 1; i < 1000000; i++) {
      if (true == aSubscriber.isUnsubscribed()) {
        return;
      }
      aSubscriber.onNext(i);
    }
    if (false == aSubscriber.isUnsubscribed()) {
      aSubscriber.onCompleted();
    }
  } catch(Throwable t) {
    if (false == aSubscriber.isUnsubscribed()) {
      aSubscriber.onError(t);
    }
  }
})
```

**NOTE:** A well-formed finite Observable must attempt to call either the Subscriber’s `onCompleted( )` method exactly once or its `onError( )` method exactly once, and must not thereafter attempt to call any of the Subscriber’s other methods. It is good practice to check the Subscriber’s `isUnsubscribed( )` state so that your Observable can stop emitting items or doing expensive calculations when there is no longer an interested Subscriber.

> **Note:** in the scala language adaptor for RxJava, this method is called `apply( )`.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#create(rx.Observable.OnSubscribe)">`create(OnSubscribe)`</a>
* RxJS: [`create`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablecreatesubscribe)
* Linq: [`Create`](http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.create.aspx)

***

## defer( )
#### do not create the Observable until a Subscriber subscribes; create a fresh Observable on each subscription
[[images/rx-operators/defer.png]]

Pass `defer( )` an Observable factory function (a function that generates Observables), and `defer( )` will return an Observable that will call this function to generate its Observable sequence afresh each time a new Subscriber subscribes.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#defer(rx.util.functions.Func0)">`defer(observableFactory)`</a>
* RxJS: [`defer`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservabledeferobservablefactory)
* Linq: [`Defer`](http://msdn.microsoft.com/en-us/library/hh229160.aspx)

***

## range( )
#### create an Observable that emits a range of sequential integers
[[images/rx-operators/range.png]]

To create an Observable that emits a range of sequential integers, pass the starting integer and the number of integers to emit to the `range( )` method.
```groovy
// myObservable emits the integers 5, 6, and 7 before completing:
def myObservable = Observable.range(5, 3);
```

In calls to `range(n,m)`, a value of zero for _m_ will result in no numbers being emitted (values less than zero will cause an exception). _n_ may be any integer that can be represented as a `BigDecimal` — posititve, negative, or zero.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#range(int, int)">`range(start, count)`</a>
* RxJS: [`range`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablerangestart-count-scheduler)
* Linq: [`Range`](http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.range.aspx)
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/04_CreatingObservableSequences.html#ObservableRange">Introduction to Rx: Range</a>

***

## interval( )
#### create an Observable that emits a sequence of integers spaced by a given time interval
[[images/rx-operators/interval.png]]

To create an Observable that emits items spaced by a particular interval of time, pass the time interval and the units of time that interval is measured in (and, optionally, a scheduler) to the `interval( )` method.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#interval(long, java.util.concurrent.TimeUnit)">`interval(interval,unit)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#interval(long, java.util.concurrent.TimeUnit, rx.Scheduler)">`interval(interval,unit,scheduler)`</a>
* RxJS: [`interval`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableintervalperiod-scheduler)
* Linq: [`Interval`](http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.interval.aspx)
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/04_CreatingObservableSequences.html#ObservableInterval">Introduction to Rx: Interval</a>

***

## timer( )
#### create an Observable that emits a single item after a given delay
[[images/rx-operators/timer.png]]

The `timer( )` method returns an Observable that, when subscribed to, waits for a span of time that you have defined, then emits a single zero and completes.

There is also a version of `timer( )` that emits a single zero after a specified delay, and then emits incrementally increasing numbers periodically thereafter on a specified periodicity:
[[images/rx-operators/timer.p.png]]

For both of these versions of `timer( )` you can optionally specify a Scheduler on which the timing will take place.

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#timer(long, long, java.util.concurrent.TimeUnit)">timer( )</a>
* RxJS: [`timer`](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservabletimerduetime-period-scheduler)
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.timer.aspx">`Timer`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/04_CreatingObservableSequences.html#ObservableTimer">Introduction to Rx: Timer</a>

***

## empty( ), error( ), and never( )
#### Observables that can be useful for testing purposes

* `empty( )` creates an Observable that does not emit any items but instead immediately calls the Subscriber’s `onCompleted( )` method.
[[images/rx-operators/empty.png]]
* `error( )` creates an Observable that does not emit any items but instead immediately calls the Subscriber’s `onError( )` method.
[[images/rx-operators/error.png]]
* `never( )` creates an Observable that does not emit any items, nor does it call either the Subscriber’s `onCompleted( )` or `onError( )` methods.
[[images/rx-operators/never.png]]

```groovy
import rx.Observable;
import rx.Observer;
import rx.Subscription;
import rx.subscriptions.Subscriptions;
import rx.util.functions.Func1;

println("*** empty() ***");
Observable.empty().subscribe(
  { println("empty: " + it); },             // onNext
  { println("empty: error - " + it.getMessage()); }, // onError
  { println("empty: Sequence complete"); }  // onCompleted
);

println("*** error() ***");
Observable.error(new Throwable("badness")).subscribe(
  { println("error: " + it); },             // onNext
  { println("error: error - " + it.getMessage()); }, // onError
  { println("error: Sequence complete"); }  // onCompleted
);

println("*** never() ***");
Observable.never().subscribe(
  { println("never: " + it); },             // onNext
  { println("never: error - " + it.getMessage()); }, // onError
  { println("never: Sequence complete"); }  // onCompleted
);
println("*** END ***");
```
```
*** empty() ***
empty: Sequence complete
*** error() ***
error: error - badness
*** never() ***
*** END ***
```

#### see also:
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#empty()">`empty()`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#error(java.lang.Throwable)">`error(exception)`</a>
* javadoc: <a href="http://netflix.github.io/RxJava/javadoc/rx/Observable.html#never()">`never()`</a>
* RxJS: <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableemptyscheduler">`empty`</a> and <a href="https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservablenever">`never`</a>
* Linq: <a href="http://msdn.microsoft.com/en-us/library/system.reactive.linq.observable.empty.aspx">`Empty`</a> and <a href="http://msdn.microsoft.com/en-us/library/hh211979.aspx">`Never`</a>
* <a href="http://www.introtorx.com/Content/v1.0.10621.0/04_CreatingObservableSequences.html#SimpleFactoryMethods">Introduction to Rx: Simple factory methods</a>