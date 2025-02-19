# Awesome Multicore OCaml

A collection of libraries, experiments and ideas relating to OCaml 5 (multicore + effects). With the [merging](https://github.com/ocaml/ocaml/pull/10831#issuecomment-1008935795) of the main `multicore-ocaml` branch into OCaml `trunk`, a parallel and effectful world is fast approaching.

This repository collects useful libraries, ideas and experiments relating to the use of Multicore OCaml features (primarily parallelism with domains and direct-style code with effects).

For contributing, [see the guide](https://github.com/patricoferris/awesome-multicore-ocaml/blob/main/CONTRIBUTING.md).

If you are wondering what even is Multicore OCaml, you could start by watching [a video from 2014 about Multicore OCaml by Stephen Dolan and co.](https://watch.ocaml.org/videos/watch/490b5363-01b6-45d8-9b7e-c883a20026a1), then [one on how to parallelise your OCaml code](https://watch.ocaml.org/videos/watch/ce20839e-4bfc-4d74-925b-485a6b052ddf) and [how we can adapt the existing ecosystem to support Multicore OCaml](https://watch.ocaml.org/videos/watch/629b89a8-bbd5-490d-98b0-d0c740912b02).

For understanding effects in OCaml 5 you can watch [KC Sivaramakrishnan's Effective Programming in OCaml 5 talk](https://www.youtube.com/watch?v=xKUzN-McZUk) and also Thomas Leonard's talk at the [2021 OCaml Workshop](https://v3.ocaml.org/workshops/ocaml-workshop-2021) on [Experiences with Effects](https://watch.ocaml.org/videos/watch/74ece0a8-380f-4e2a-bef5-c6bb9092be89). Note both videos use a syntax for effects that will not exist in OCaml 5.00 (see also [ppx_effects](#ppx_effects)).

For more resources like this, check the [Multicore OCaml wiki](#wiki).

*There's a WIP PR to start submoduling repositories so it can be a one-stop shop for taking OCaml 5.00 for a spin, see [the PR](https://github.com/patricoferris/awesome-multicore-ocaml/pull/1)*.

## Table of Contents
- [Libraries](#libraries)
  - [Eio](#eio)
  - [Affect](#affect)
  - [Domainslib](#domainslib)
  - [Lwt Support](#lwt-support)
- [Experiments](#experiments)
  - [Dream](#dream)
  - [Cohttp](#cohttp)
  - [Ppx_effects](#ppx_effects)
  - [Gemini Protocol](#gemini-protocol)
  - [Multi-shot Continuations](#multi-shot-continuations)
  - [Js_of_ocaml support](#js_of_ocaml)
- [Ideas](#ideas)
  - [Non-blocking Codec](#non-blocking-codec)
- [Resources](#resources)
    - [Wiki](#wiki)
    - [Discuss Threads](#discuss-threads)
    - [Monthlies](#monthlies)
    - [Benchmarks](#benchmarks)

## Libraries

### Eio

Repository: https://github.com/ocaml-multicore/eio

Eio implements an effects-based direct-style IO stack for multicore OCaml. It supports multiple backends including a performant [io-uring](https://unixism.net/loti/what_is_io_uring.html) one and a portable [libuv](http://docs.libuv.org/en/v1.x/) backend. A [0.1 release](https://github.com/ocaml/opam-repository/pull/20695) is now available from opam-repository.

### Affect

Repository: https://erratique.ch/software/affect

> Affect provides composable concurrency primitives for OCaml using the effect handlers available in OCaml 5.0. Affect should be seen as an experiment at that point.

### Domainslib

Repository: https://github.com/ocaml-multicore/domainslib

Domainslib provides data-structures for parallel programming on top of multicore primitives. This includes a work-stealing task pool and channels for inter-domain communication.

### Lwt Support

Some useful and relevant OCaml.5 x Lwt discussions:

 - [Is mixing lwt and multicore safe?](https://discuss.ocaml.org/t/is-mixing-lwt-and-multicore-safe/8714)
 - [Multicore, Async and Lwt](https://discuss.ocaml.org/t/multicore-async-and-lwt/2687)

#### Lwt_eio

Repository: https://github.com/talex5/lwt_eio

`Lwt_eio` provides an "lwt engine" using [Eio](#eio) making it possible to use both Eio and Lwt in the same codebase. A [0.1 release](https://github.com/ocaml/opam-repository/pull/20701) is now available from opam-repository.

#### Lwt_domain

Repository: https://github.com/ocsigen/lwt

Lwt now has a package called [`lwt-domain`](https://github.com/ocsigen/lwt/tree/master/src/domain). This provides useful functions for programming with Lwt and [Domainslib](#domainslib).

## Experiments

### Dream

Repository: https://github.com/talex5/dream/tree/eio

See also the [draft PR](https://github.com/aantron/dream/pull/194) that uses [Dream](https://github.com/aantron/dream), Eio and [lwt_eio](#lwt-eio) to provide a direct-style interface to Dream.

### Cohttp

Repository: https://github.com/bikallem/ocaml-cohttp/tree/eio-3

Two PRs exist on the [cohttp repository](https://github.com/mirage/ocaml-cohttp) (an OCaml library for building HTTP servers and clients). One for adding a [direct-style implementation using just Eio](https://github.com/mirage/ocaml-cohttp/pull/857). Another to [convert the Lwt server implementation to direct-style](https://github.com/mirage/ocaml-cohttp/pull/854) using [lwt_eio](#lwt-eio).

### Ppx_effects

Repository: https://github.com/CraigFe/ppx_effects

The effects in OCaml 5 will not support a dedicated syntax, but plans exist for this perhaps once the effects are typed. Until then this ppx provides an approximation to the proposed syntax.

### Gemini Protocol

Repository: https://gitlab.com/talex5/gemini-eio

The [gemini protocol](https://gemini.circumlunar.space/docs/faq.gmi) implemented in direct-style using [eio](#eio).

### Multi-shot Continuations

Repository: https://github.com/dhil/ocaml-multicont

Built on top of the continuations in Multicore OCaml, `ocaml-multicont` provides a library for using continuations that can be applied more than once. See also [this discussion on discuss](https://discuss.ocaml.org/t/multi-shot-continuations-gone-forever/9072).

### Js_of_ocaml

Repository: https://github.com/ocsigen/js_of_ocaml

It is not immediately clear how (and when) effects will be supported in js_of_ocaml (an OCaml bytecode to Javascript compiler). [This discussion provides more information](https://discuss.ocaml.org/t/ocaml-multicore-effects-and-js-of-ocaml/8502). See also [some work on using CPS to achieve working Javascript](https://github.com/Armael/js_of_ocaml).

## Ideas

Even less further on than [experiments](#experiments), the *ideas* section contains projects that would benefit from the features of Multicore OCaml.

### Non-blocking Codec

Repository: https://github.com/dbuenzli/nbcodec

Many libraries and tools written in the nbcodec style would benefit from continuations given by effect handlers in Multicore OCaml, including libraries like [jsonm](https://github.com/dbuenzli/jsonm) or [xmlm](https://github.com/dbuenzli/xmlm) perhaps.

## Resources

### Wiki

The [Multicore OCaml Wiki](https://github.com/ocaml-multicore/ocaml-multicore/wiki) contains a lot of useful information from design decisions to examples. Two notable repositories are: 

  - [Effects examples](https://github.com/ocaml-multicore/effects-examples): a collection of great examples with effects including cooperative threading and generators.
  - [Parallel Programming in Multicore OCaml](https://github.com/ocaml-multicore/parallel-programming-in-multicore-ocaml): a very good introduction to programming parallel programs in Multicore OCaml, including [using Domainslib](https://github.com/ocaml-multicore/parallel-programming-in-multicore-ocaml#domainslib).

### Discuss Threads

Recently, there has been a lot of great discussion on discuss.ocaml.org around OCaml 5, in particular what the ramifications of adding effects to the language will have to the ecosystem:

 - The [initial release](https://discuss.ocaml.org/t/eio-0-1-effects-based-direct-style-io-for-ocaml-5/9298) of Eio has a lot of dicussion around what it could mean if the library became the official "OCaml IO" library. It also has some useful conversations about the underlying use of effects in Eio and in particular the [set of private effects used](https://v3.ocaml.org/p/eio/0.1/doc/Eio/Private/Effects/index.html).
   + An excellent write up about [scopes and effect handlers](https://hackmd.io/@yF_ntUhmRvKUt15g7m1uGw/Bk-5NXh15) was added in this [thread](https://discuss.ocaml.org/t/eio-0-1-effects-based-direct-style-io-for-ocaml-5/9298/91).
 - Another thread, ["How to block in an agnostic way"](https://discuss.ocaml.org/t/how-to-block-in-an-agnostic-way/9368), is a discussion about blocking code where we are agnostic to the underlying concurrency abstraction (and indeed how to do [interop between libraries](https://discuss.ocaml.org/t/how-to-block-in-an-agnostic-way/9368/4)).
 - Another more Eio-specific thread looks at [cancellation in the presence of concurrency from effects](https://discuss.ocaml.org/t/understanding-cancellation-in-eio/9369).
 - In [How do spawn and join interact with try_with](https://discuss.ocaml.org/t/multicore-how-do-spawn-and-join-interact-with-try-with/9362) there's a great, short discussion about effects in the presence of multiple domains. A "gotcha" many (myself included) are likely to hit when getting started with OCaml 5.
 - There is a great discussion about using effects for a [roguelike](https://en.wikipedia.org/wiki/Roguelike) game in [Tutorial: Roguelike with Effect Handlers](https://discuss.ocaml.org/t/tutorial-roguelike-with-effect-handlers/9422) (the full tutorial [is here](https://hackmd.io/@yF_ntUhmRvKUt15g7m1uGw/BJBZ7TMeq)). Related to that is another excellent article about coding [animations with effect handlers](https://gopiandcode.uk/logs/log-bye-bye-monads-algebraic-effects.html).

### Monthlies

The OCaml monthlies are available on discuss: https://discuss.ocaml.org/tag/multicore-monthly

### Benchmarks

#### Sandmark

Repository: https://github.com/ocaml-bench/sandmark

> Sandmark is a suite of OCaml benchmarks and a collection of tools to configure different compiler variants, run and visualise the results.

#### Http Benchmarks

Repository: https://github.com/ocaml-multicore/retro-httpaf-bench

A collection of HTTP servers including ones in Go, Rust, multiple OCaml implementations and OCaml with effects.
