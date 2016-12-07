RxJava 2
========

Resources:

- [What's different in 2.0](https://github.com/ReactiveX/RxJava/wiki/What's-different-in-2.0)
- [Reactive Streams Specification for the JVM](https://github.com/reactive-streams/reactive-streams-jvm)
- [Droidcon NYC 2016 - Looking Ahead to RxJava 2](https://www.youtube.com/watch?v=hcxMtomE6fI)
- [GOTO 2016 - Exploring RxJava 2 for Android](https://www.youtube.com/watch?v=htIXKI5gOQU)


Reactive Streams
================

Specification
-------------

```java
public interface Publisher<T> {
	public void subscribe(Subscriber<? super T> s);
}

public interface Subscriber<T> {
	public void onSubscribe(Subscription s);
	public void onNext(T t);
	public void onError(Throwable t);
	public void onComplete();
}

public interface Subscription {
	public void request(long n);
	public void cancel();
}

public interface Processor<T, R> extends Subscriber<T>, Publisher<R> {
}
```

Callbacks `onSubscribe`, `onNext`, `onError`, `onComplete` are not allowed to throw an exception. They must return normally except for throwing the `NullPointerException` for a null parameter (but RxJava 2 does not let null in anyway). RxJava 2 has a wrapper which handles an exceptions automatically (`SafeSubscriber` or `SafeObserver`).

Callbacks invocation
--------------------

```
onSubscribe onNext* (onError | onComplete)?
```


Rx with backpressure
====================

- `Flowable` is an implementation of Reactive Streams `Publisher`.
- Observed with Reactive Streams `Subscriber`.
- Produces `Subscription` on subscribe.
- `FlowableProcessor` is an implementation of Reactive Streams `Processor` with backpressure support aka `Publisher` via `Flowable` + `Subscriber`.


Rx without backpressure
=======================

- `Observable` is an implementation of `ObservableSource`.
- Observed with an `Observer`.
- Produces `Disposable` on subscribe.
- `Subject` is an implementation of `Observable` + `Observer`.


Observable specializations
==========================

Single
------

It's a "reactive scalar".

```
onSubscribe (onSuccess | onError)?
```

Completable
-----------

It's a "reactive runnable".

```
onSubscribe (onComplete | onError)?
```

Maybe
-----

It's a "reactive optional".

```
onSubscribe (onSuccess | onError | onComplete)?
```


Observing sources
=================

How to subscribe:

```java
observable.subscribe(new Observer<Object>() {
	@Override public void onSubscribe(Disposable d) { ... }
	@Override public void onNext(Object o) { ... }
	@Override public void onError(Throwable t) { ... }
	@Override public void onComplete() { ... }
});
```

Better way:

```java
Disposable disposable = observable.subscribeWith(new DisposableObserver<Object>() {
	@Override public void onNext(Object o) { ... }
	@Override public void onError(Throwable t) { ... }
	@Override public void onComplete() { ... }
});
disposable.dispose();
```

You can subscribe with `DisposableObserver`, `DisposableSingleObserver`, `DisposableCompletableObserver`, `DisposableMaybeObserver`, `DisposableSubscriber`. Method `subscribeWith` returns `Disposable` for all these observers/subscribers.

How to dispose all:

```java
CompositeDisposable disposables = new CompositeDisposable();
disposables.add(disposable);
disposables.dispose();
```


Functional interfaces
=====================

All functional interfaces define `throws Exception`.

```java
Flowable.just("file.txt")
	.map(name -> Files.readLines(name))
	.subscribe(lines -> System.out.println(lines.size()), Throwable::printStackTrace);
```

If the file doesn't exist, the end consumer will print out `IOException` directly. Also the `Files.readLines()` is invoked without try-catch.


V1 vs. V2
=========

- Observable with backpressure -> Flowable
- Subject with backpressure -> FlowableProcessor
- Observable.Transformer -> ObservableTransformer
- Subscription without backpressure -> Disposable
- CompositeSubscription -> CompositeDisposable
- Subscriber without backpressure -> Observer | DisposableObserver
- Subscriber with backpressure -> Subscriber | DisposableSubscriber
- Subscriber.onCompleted -> Observer.onComplete | Subscriber.onComplete
- Action0 -> Action
- Action1 -> Consumer
- Action2 -> BiConsumer
- Observable.fromEmitter -> Observable.create
- Observable.doOnCompleted -> Observable.doOnComplete
- Observable.doOnUnsubscribe -> Observable.doOnDispose | Flowable.doOnCancel
