# re·ac·tion

> Reaction is a lightweight Async Reactive library for F#.

Reaction is an F# implementation of Async Observables ([ReactiveX](http://reactivex.io/)) and was designed spesifically for targeting [Fable](http://fable.io/) which means that the code may be [transpiled](https://en.wikipedia.org/wiki/Source-to-source_compiler) to JavaScript, and thus the same F# code may be used both client and server side for full stack software development. The project is heavily inspired by [aioreactive](https://github.com/dbrattli/aioreactive).

See [Fable Reaction](https://github.com/dbrattli/Fable.Reaction) for Elmish-ish use of Reaction.

## Documentation

Reaction [documentation](https://dbrattli.github.io/Reaction/) (work in progress)

## Install

```cmd
paket add Reaction --project <project>
```

## Async Observables

Reaction is an implementation of Async Observable. The difference between an "Async Observable" and an "Observable" is that with "Async Observables" you need to await methods such as `Subscribe`, `OnNext`, `OnError`, and `OnCompleted`. In Reaction they are thus called `SubscribeAsync`, `OnNextAsync`, `OnErrorAsync`, and `OnCompletedAsync`. This enables `SubscribeAsync` to await async operations i.e setup network connections, and observers (`OnNext`) may finally await side effects such as writing to disk (observers are all about side-effects right?).

This diagram shows the how Async Observables relates to other collections and values.

|  | Single Value | Multiple Values
| --- | --- | --- |
| Synchronous pull  | unit -> 'a | [seq<'a>](https://msdn.microsoft.com/en-us/visualfsharpdocs/conceptual/collections.seq-module-%5Bfsharp%5D?f=255&MSPPError=-2147217396) |
| Synchronous push  |'a -> unit | [Observable<'a>](http://fsprojects.github.io/FSharp.Control.Reactive/tutorial.html) |
| Asynchronous pull | unit -> [Async<'a>](https://msdn.microsoft.com/en-us/visualfsharpdocs/conceptual/control.async-class-%5Bfsharp%5D) | [AsyncSeq<'a>](http://fsprojects.github.io/FSharp.Control.AsyncSeq/library/AsyncSeq.html) |
| Asynchronous push |'a -> [Async\<unit\>](https://msdn.microsoft.com/en-us/visualfsharpdocs/conceptual/control.async-class-%5Bfsharp%5D) | **AsyncObservable<'a>** |

