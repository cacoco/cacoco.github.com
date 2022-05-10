---
title: "Fizzbuzz"
date: "2012-07-11"
draft: false
tags: ["fizzbuzz", "clojure"]
---

*Birds do it. Bees do it. Even educated fleas do it. So let's do it.*

Ask any programmer these days and they've probably heard of it. [Fizzbuzz](https://weblog.raganwald.com/2007/01/dont-overthink-fizzbuzz.html).

#### The Problem

Write a program that prints the numbers from 1 to 100. But for multiples of 3 print "Fizz" instead of the number and for the multiples of 5 print "Buzz".  
For numbers which are multiples of both three and five print "FizzBuzz".

I came across (probably much later than most everyone else) Jeff Atwood's post on [the Fizzbuzz problem](https://www.codinghorror.com/blog/2007/02/why-cant-programmers-program.html) as it pertains to interviewing programmers. Naturally, like [any other progammer](https://www.codinghorror.com/blog/2007/02/fizzbuzz-the-programmers-stairway-to-heaven.html) I set out to prove to myself that I could indeed write a Fizzbuzz. The challenge was to write it as quickly as possible and to handicap myself I decided to do it in a language that I had only little experience with at the time: [Clojure](https://clojure.org/).

#### A Solution in Clojure

```gist {cols="10", id="5562510"}
 https://gist.github.com/cacoco/5562510
```

Full project source available [on github](https://github.com/cacoco/fizzbuzz).
