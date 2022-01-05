# 2. My Language Is Faster Than Your Language

![thumbnail](./thumb.jpg)

There have been buzzings through [the grapevine](https://news.ycombinator.com/)
about the Go language created by Google. We heard it's faster than Python, Ruby
and JavaScript because it's a compiled language, have these nifty guys called
goroutines, and apparently they're
[adding generics soon](https://go.dev/blog/generics-proposal)? Whatever the heck
all that means!

Here at SmallSmallCo, we don't shy away from using the latest and greatest
technology! We'll take a competitive edge if we can get it, and besides, great
technology attracts great talent. But we're not fools, either!!! Sometimes hype
is just that, and the thing being hyped up ain't all that great. So I did my
research.

I found an expert on HireAHacker who said they could whip up a demo to show if
Go would be faster for us than Node.js. He warned me that he may not be able to
finish it all in 1 hour, though I figured for $1000/hour, he could do most of
the work and you could finish it up. He mentioned something about the Node.js
demo being functional, and the Go version could work if we used
[atomics](https://pkg.go.dev/sync/atomic) or channels. Could you touch up this
project and explain this to me?

Thanks for your help.

Your CEO, Jiminy Storfenbrat

## Assignment

You will be working with the following repo: https://github.com/sumcademy/tally

It contains two files, `tally.mjs`, and `tally.go`. They both implement the same
algorithm, which adds all the numbers from 1 to 50,000,000 to all the numbers
from -1 to -50,000,000. The result should be 0. Here's what happens when we
execute the code:

```bash
> node tally.mjs
outer job: tallying positives and negatives...
  inner job: tallying 50000000 numbers...
    took 0.652 seconds
  inner job: tallying 50000000 numbers...
    took 0.639 seconds
outer job took 1.293 seconds total
total sum: 0
```

```bash
> go run tally.go
outer job: tallying positives and negatives...
  inner job: tallying 50000000 numbers...
  inner job: tallying 50000000 numbers...
    took 0.098157272 seconds
    took 0.099222299 seconds
outer job took 0.099259584 seconds total
total sum: -575687368580499
```

The Go version is over 10 times faster than the JavaScript version, though it
produces the wrong result. **The assignment is to fix the Go version so it still
works and prints the total sum as 0.** After fixing the Go code, pay attention
to whether or not the Go version is still faster than the Node.js version.

### Keep in mind

- Node.js is single-threaded while Go allows spawning multiple threads
  - Notice how in the Go version, the two inner jobs start at the same time:

    ```
    inner job: tallying 50000000 numbers...
    inner job: tallying 50000000 numbers...
    ```

    Instead of after the other job completes:

    ```
    outer job: tallying positives and negatives...
      inner job: tallying 50000000 numbers...
        took 0.652 seconds
      inner job: tallying 50000000 numbers...
        took 0.639 seconds
    ```

- The contractor's hint about using [atomics](https://pkg.go.dev/sync/atomic).
  Channels or locks could be used instead, though in this case atomics might be
  the easiest to add.
- This looks like a helpful presentation about the JS event loop:

  [What the heck is the event loop anyway? | Philip Roberts | JSConf EU](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

## Extra Credit

[httpbin.org/delay](http://httpbin.org/#/Dynamic_data/get_delay__delay_) is a
test endpoint for simulating slow network requests. See if you can demonstrate
that Node.js is capable of making 3 simultaneous requests to
[`httpbin.org/delay/3`](http://httpbin.org/delay/3) in 3 seconds instead of 9
(3+3+3).
