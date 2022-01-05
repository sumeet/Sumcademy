# 1. Functional Programming Is For Ner^H^H^HAcademi^W^WFun?

![thumbnail](./thumb.jpg)

Concepts from FP (Functional Programming) are spreading to modern languages like
Scala, Rust, Swift, Kotlin, and even modern JS/TS and Ruby. Chances are you've
used either `map`/`filter`, or the `Result`/`Option` types (e.g.,
[Rust](https://doc.rust-lang.org/book/ch06-01-defining-an-enum.html#the-option-enum-and-its-advantages-over-null-values)'s
or [Scala 3](https://docs.scala-lang.org/scala3/reference/enums/adts.html)'s
enums — also known as
[Algebraic data types](https://en.wikipedia.org/wiki/Algebraic_data_type)),
features imported from functional programming.

Most people wouldn't consider programs written in these languages to be
[purely functional](https://en.wikipedia.org/wiki/Purely_functional_programming)
because they provide an escape hatch from the functional paradigm, namely
mutable bindings and loops. On the theoretical level, functional programming is
fundamentally based on a different model of computing from imperative
programming. As it's unclear if getting into the theory will help you that much
in writing functional programs, we'll be glossing over that<sup>[1](#computation)</sup>.

We'll be using Haskell to explore FP, as it's probably the most mature platform
out there for writing purely functional programs. Other popular functional
languages like F# and OCaml do allow writing loops, which is handy, but doesn't
encourage the same rigor. Haskell _forces_ one to think in the lambda calculus,
which arguably grows and us, and changes the way we look at programming.

## Assignment

Haskell has been around for a while, and has some mature tooling, but is still
for whatever reason notoriously hard to setup. Our assignment this time around
will be focused on getting the dev environment running. Hopefully this guide
will get you around some of the common pitfalls.

1. [Install GHCUp](https://www.haskell.org/ghcup/). _Do NOT install Haskell via
   your OS package manager (brew, pacman, apt, etc.)._
2. Via GHCUp, install latest ghc<sup>[2](#ghc)</sup> 8.10 (GHC 9 still doesn't
   have full IDE support), <sup>[3](#cabal)</sup>cabal, and <sup>[4](#hls)</sup>hls.
3. If you use VSCode, install https://github.com/haskell/vscode-haskell.
   Otherwise,
   [you can read up on how to set up your editor](https://haskell-language-server.readthedocs.io/en/latest/configuration.html).
   If for some reason, you don't want to do any of that, `cabal install hlint`
   and just run it manually from the command line when you need to.

Hopefully everything is now set up properly. To test it out, make a new file
called `Hello.hs` and paste in the following:

```haskell
main :: IO ()
main = putStrLn $ show "Hello, Haskell!"
```

1. You should be able to run this file via `runhaskell Hello.hs`.
2. If your editor integration is working (or just run `hlint helloHello.hs`),
   you should see a warning like this:

   ```haskell
   Found:
     putStrLn $ show "Hello, Haskell!"
   Perhaps:
     print "Hello, Haskell!"
   ```

3. Go ahead and apply the suggestion, and try running the program again.

If you've made it this far, congratulations! You made it through setting up
Haskell! The reason we went through all that particular process was to get
HLint, it's really cool software that actually **teaches you Haskell**.

That was quite a bit, so let's stop for now. If you really want more, you can
check out some of the extra credit.

## Extra Credit

- Watch some of the material on computation.
- Solve [Advent of Code 2019: Day 1](https://adventofcode.com/2019/day/1) in
  Haskell, seeing what you can figure out on your own. Even if you got totally
  stuck after a few minutes, this would still be a worthwhile exercise.

---

<a name="computation"><sup>1</sup></a> If you're interested in looking into it
more closely, I recommend the
[Computation video series from Destroy All
Software](https://www.destroyallsoftware.com/screencasts/catalog#computation).
Most relevant videos **bolded**.

- Intro to Computation
- Computing By Changing (Turing machines)
- Power of Turing Machines
- **Computing by Constructing (Lambda Calculus)**
- **Power of Lambda Calculus**

<a name="ghc"><sup>2</sup></a> Haskell compiler

<a name="cabal"><sup>3</sup></a> Package manager, similar to npm (JS) or bundler (Ruby)<br>

<a name="hls"><sup>4</sup></a> Haskell Language Server, for IDE integration
