* [**`aggregate( )`**](Transforming-Observables#reduce-or-aggregate) — apply a function to each emitted item, sequentially, and emit only the final accumulated value
* [**`all( )`**](Observable-Utility-Operators#all) — determine whether all items emitted by an Observable meet some criteria
* [**`amb( )`**](Combining-Observables#amb) — given two or more source Observables, emits all of the items from the first of these Observables to emit an item
* [**`average( )`**](Mathematical-Operators#average) — calculates the average of Integers emitted by an Observable and emits this average
* [**`averageDoubles( )`**](Mathematical-Operators#average) — calculates the average of Doubles emitted by an Observable and emits this average
* [**`averageFloats( )`**](Mathematical-Operators#average) — calculates the average of Floats emitted by an Observable and emits this average
* [**`averageLongs( )`**](Mathematical-Operators#average) — calculates the average of Longs emitted by an Observable and emits this average
* [**`buffer( )`**](Transforming-Observables#buffer) — periodically gather items from an Observable into bundles and emit these bundles rather than emitting the items one at a time
* [**`cache( )`**](Observable-Utility-Operators#cache) — remember the sequence of items emitted by the Observable and emit the same sequence to future Observers
* [**`cast( )`**](Transforming-Observables#cast) — cast all items from the source Observable into a particular type before reemitting them
* [**`combineLatest( )`**](Combining-Observables#combinelatest) — when an item is emitted by either of two Observables, combine the latest item emitted by each Observable via a specified function and emit items based on the results of this function
* [**`concat( )`**](Combining-Observables#concat) — concatenate two or more Observables sequentially
* [**`connect( )`**](Connectable-Observable-Operators#connectableobservableconnect) — instructs a Connectable Observable to begin emitting items
* [**`contains( )`**](Observable-Utility-Operators#contains) — determine whether an Observable emits a particular item or not
* [**`count( )`**](Mathematical-Operators#count) — counts the number of items emitted by an Observable and emits this count
* [**`create( )`**](Creating-Observables#create) — create an Observable from scratch by means of a function
* [**`debounce( )`**](Filtering-Observables#throttlewithtimeout-or-debounce) — only emit an item from the source Observable after a particular timespan has passed without the Observable emitting any other items
* [**`defaultIfEmpty( )`**](Transforming-Observables#defaultifempt) — emit items from the source Observable, or emit a default item if the source Observable completes after emitting no items
* [**`defer( )`**](Creating-Observables#defer) — do not create the Observable until an Observer subscribes; create a fresh Observable on each subscription
* [**`delay( )`**](Observable-Utility-Operators#delay) — shift the emissions from an Observable forward in time by a specified amount
* [**`dematerialize( )`**](Observable-Utility-Operators#dematerialize) — convert a materialized Observable back into its non-materialized form
* [**`distinct( )`**](Filtering-Observables#distinct) — suppress duplicate items emitted by the source Observable
* [**`distinctUntilChanged( )`**](Filtering-Observables#distinctuntilchanged) — suppress duplicate consecutive items emitted by the source Observable
* [**`elementAt( )`**](Filtering-Observables#elementat) — emit item _n_ emitted by the source Observable
* [**`elementAtOrDefault( )`**](Filtering-Observables#elementatordefault) — emit item _n_ emitted by the source Observable, or a default item if the source Observable emits fewer than _n_ items
* [**`empty( )`**](Creating-Observables#empty-error-and-never) — create an Observable that emits nothing and then completes
* [**`error( )`**](Creating-Observables#empty-error-and-never) — create an Observable that emits nothing and then signals an error
* [**`exists( )`**](Observable-Utility-Operators#exists-and-isempty) — determine whether an Observable emits any items or not
* [**`filter( )`**](Filtering-Observables#filter-or-where) — filter items emitted by an Observable
* [**`finallyDo( )`**](Observable-Utility-Operators#finallydo) — register an action to take when an Observable completes
* [**`first( )`**](Filtering-Observables#first) — emit only the first item emitted by an Observable, or the first item that meets some condition
* [**`firstOrDefault( )`**](Filtering-Observables#firstordefault) — emit only the first item emitted by an Observable, or the first item that meets some condition, or a default value if the source Observable is empty
* [**`flatMap( )`**](Transforming-Observables#mapmany-or-flatmap-and-mapmanydelayerror) — transform the items emitted by an Observable into Observables, then flatten this into a single Observable
* [**`forEach( )`**](Blocking-Observable-Operators#foreach) — invoke a function on each item emitted by the Observable; block until the Observable completes
* [**`from( )`**](Creating-Observables#from) — convert an Iterable or a Future into an Observable
* [**`getIterator( )`**](Blocking-Observable-Operators#transformations-tofuture-toiterable-and-toiteratorgetiterator) — convert the sequence emitted by the Observable into an Iterator
* [**`groupBy( )`**](Transforming-Observables#groupby) — divide an Observable into a set of Observables that emit groups of items from the original Observable, organized by key
* [**`ignoreElements( )`**](Filtering-Observables#ignoreelements) — discard the items emitted by the source Observable and only pass through the error or completed notification
* [**`interval( )`**](Creating-Observables#interval) — create an Observable that emits a sequence of integers spaced by a given time interval
* [**`isEmpty( )`**](Observable-Utility-Operators#exists-and-isempty) — determine whether an Observable emits any items or not
* [**`just( )`**](Creating-Observables#just) — convert an object into an Observable that emits that object
* [**`last( )`**](Blocking-Observable-Operators#last-and-lastordefault) (`BlockingObservable`) — block until the Observable completes, then return the last item emitted by the Observable
* [**`last( )`**](Filtering-Observable-Operators#last) (`Observable`) — emit only the last item emitted by the source Observable
* [**`lastOrDefault( )`**](Blocking-Observable-Operators#last-and-lastordefault) — block until the Observable completes, then return the last item emitted by the Observable or a default item if there is no last item
* [**`map( )`**](Transforming-Observables#map) — transform the items emitted by an Observable by applying a function to each of them
* [**`mapMany( )`**](Transforming-Observables#mapmany-or-flatmap-and-mapmanydelayerror) — transform the items emitted by an Observable into Observables, then flatten this into a single Observable
* [**`mapManyDelayError( )`**](Transforming-Observables#mapmany-or-flatmap-and-mapmanydelayerror) — transform the items emitted by an Observable into Observables, then flatten this into a single Observable, waiting to report errors until all error-free observables have a chance to complete
* [**`mapWithIndex( )`**](Transforming-Observables#mapwithindex) — transform the items emitted by an Observable by applying a function to each of them that takes into account the index value of the item
* [**`materialize( )`**](Observable-Utility-Operators#materialize) — convert an Observable into a list of Notifications
* [**`max( )`**](Mathematical-Operators#max) — emits the maximum value emitted by a source Observable
* [**`maxBy( )`**](Mathematical-Operators#maxby) — emits the item emitted by the source Observable that has the maximum key value
* [**`merge( )`**](Combining-Observables#merge) — combine multiple Observables into one
* [**`mergeDelayError( )`**](Combining-Observables#mergedelayerror) — combine multiple Observables into one, allowing error-free Observables to continue before propagating errors
* [**`min( )`**](Mathematical-Operators#min) — emits the minimum value emitted by a source Observable
* [**`minBy( )`**](Mathematical-Operators#minby) — emits the item emitted by the source Observable that has the minimum key value
* [**`mostRecent( )`**](Blocking-Observable-Operators#mostrecent) — returns an iterable that always returns the item most recently emitted by the Observable
* [**`multicast( )`**](Connectable-Observable-Operators#observablepublish-and-observablemulticast) — represents an Observable as a Connectable Observable
* [**`never( )`**](Creating-Observables#empty-error-and-never) — create an Observable that emits nothing at all
* [**`next( )`**](Blocking-Observable-Operators#next) — returns an iterable that blocks until the Observable emits another item, then returns that item
* [**`observeOn( )`**](Observable-Utility-Operators#observeon) — specify on which Scheduler an Observer should observe the Observable
* [**`ofClass( )`**](Filtering-Observables#ofclass) — emit only those items from the source Observable that are of a particular class
* [**`onErrorResumeNext( )`**](Error-Handling-Operators#onerrorresumenext) — instructs an Observable to continue emitting items after it encounters an error
* [**`onErrorReturn( )`**](Error-Handling-Operators#onerrorreturn) — instructs an Observable to emit a particular item when it encounters an error
* [**`onExceptionResumeNextViaObservable( )`**](Error-Handling-Operators#onexceptionresumenextviaobservable) — instructs an Observable to continue emitting items after it encounters an exception (but not another variety of throwable)
* [**`parallel( )`**](Observable-Utility-Operators#parallel) — split the work done on the emissions from an Observable into multiple Observables each operating on its own parallel thread
* [**`publish( )`**](Connectable-Observable-Operators#observablepublish-and-observablemulticast) — represents an Observable as a Connectable Observable
* [**`publishLast( )`**](Connectable-Observable-Operators#observablepublishlast) — represent an Observable as a Connectable Observable that emits only the last item emitted by the source Observable
* [**`range( )`**](Creating-Observables#range) — create an Observable that emits a range of sequential integers
* [**`reduce( )`**](Transforming-Observables#reduce-or-aggregate) — apply a function to each emitted item, sequentially, and emit only the final accumulated value
* [**`refCount( )`**](Connectable-Observable-Operators#connectableobservablerefcount) — makes a Connectable Observable behave like an ordinary Observable
* [**`replay( )`**](Connectable-Observable-Operators#observablereplay) — ensures that all Observers see the same sequence of emitted items, even if they subscribe after the Observable begins emitting the items
* [**`retry( )`**](Error-Handling-Operators#retry) — if a source Observable emits an error, resubscribe to it in the hopes that it will complete without error
* [**`sample( )`**](Filtering-Observables#sample-or-throttlelast) — emit the most recent items emitted by an Observable within periodic time intervals
* [**`scan( )`**](Transforming-Observables#scan) — apply a function to each item emitted by an Observable, sequentially, and emit each successive value
* [**`sequenceEqual( )`**](Observable-Utility-Operators#sequenceequal) — test the equality of pairs of items emitted by two Observables
* [**`single( )`**](Blocking-Observable-Operators#single-and-singleordefault) — if the Observable completes after emitting a single item, return that item, otherwise throw an exception
* [**`singleOrDefault( )`**](Blocking-Observable-Operators#single-and-singleordefault) — if the Observable completes after emitting a single item, return that item, otherwise return a default item
* [**`skip( )`**](Filtering-Observables#skip) — ignore the first _n_ items emitted by an Observable
* [**`skipLast( )`**](Filtering-Observables#skiplast) — ignore the last _n_ items emitted by an Observable
* [**`skipWhile( )` and `skipWhileWithIndex( )`**](Filtering-Observables#skipwhile-and-skipwhilewithindex) — discard items emitted by an Observable until a specified condition is false, then emit the remainder
* [**`startWith( )`**](Combining-Observables#startwith) — emit a specified sequence of items before beginning to emit the items from the Observable
* [**`subscribeOn( )`**](Observable-Utility-Operators#subscribeon) — specify which Scheduler an Observable should use when its subscription is invoked
* [**`sum( )`**](Mathematical-Operators#sum) — adds the Integers emitted by an Observable and emits this sum
* [**`sumDoubles( )`**](Mathematical-Operators#sum) — adds the Doubles emitted by an Observable and emits this sum
* [**`sumFloats( )`**](Mathematical-Operators#sum) — adds the Floats emitted by an Observable and emits this sum
* [**`sumLongs( )`**](Mathematical-Operators#sum) — adds the Longs emitted by an Observable and emits this sum
* [**`switchOnNext( )`**](Combining-Observables#switchonnext) — convert an Observable that emits Observables into a single Observable that emits the items emitted by the most-recently emitted of those Observables
* [**`synchronize( )`**](Observable-Utility-Operators#synchronize) — force an Observable to make synchronous calls and to be well-behaved
* [**`take( )`**](Filtering-Observables#take) — emit only the first _n_ items emitted by an Observable
* [**`takeLast( )`**](Filtering-Observables#takelast) — only emit the last _n_ items emitted by an Observable
* [**`takeUntil( )`**](Combining-Observables#takeuntil) — emits the items from the source Observable until a second Observable emits an item
* [**`takeWhile( )` and `takeWhileWithIndex( )`**](Filtering-Observables#takewhile-and-takewhilewithindex) — emit items emitted by an Observable as long as a specified condition is true, then skip the remainder
* [**`throttleFirst( )`**](Filtering-Observables#throttlefirst) — emit the first items emitted by an Observable within periodic time intervals
* [**`throttleLast( )`**](Filtering-Observables#sample-or-throttlelast) — emit the most recent items emitted by an Observable within periodic time intervals
* [**`throttleWithTimeout( )`**](Filtering-Observables#throttlewithtimeout-or-debounce) — only emit an item from the source Observable after a particular timespan has passed without the Observable emitting any other items
* [**`timeInterval( )`**](Observable-Utility-Operators#timeinterval) — emit the time lapsed between consecutive emissions of a source Observable
* [**`timeout( )`**](Filtering-Observables#timeout) — emit items from a source Observable, but issue an exception if no item is emitted in a specified timespan
* [**`timestamp( )`**](Observable-Utility-Operators#timestamp) — attach a timestamp to every item emitted by an Observable
* [**`toBlockingObservable( )`**](Blocking-Observable-Operators) — transform an Observable into a BlockingObservable
* [**`toFuture( )`**](Blocking-Observable-Operators#transformations-tofuture-toiterable-and-toiteratorgetiterator) — convert the Observable into a Future
* [**`toIterable( )`**](Blocking-Observable-Operators#transformations-tofuture-toiterable-and-toiteratorgetiterator) — convert the sequence emitted by the Observable into an Iterable
* [**`toIterator( )`**](Blocking-Observable-Operators#transformations-tofuture-toiterable-and-toiteratorgetiterator) — convert the sequence emitted by the Observable into an Iterator
* [**`toList( )`**](Observable-Utility-Operators#tolist) — collect all items from an Observable and emit them as a single List
* [**`toSortedList( )`**](Observable-Utility-Operators#tosortedlist) — collect all items from an Observable and emit them as a single, sorted List
* [**`where( )`**](Filtering-Observables#filter-or-where) — filter items emitted by an Observable
* [**`window( )`**](Transforming-Observables#window) — periodically subdivide items from an Observable into Observable windows and emit these windows rather than emitting the items one at a time 
* [**`zip( )`**](Combining-Observables#zip) — combine sets of items emitted by two or more Observables together via a specified function and emit items based on the results of this function