# 3. Bank Concurrency

![thumb](thumb.png)

A bank needs help with their new experimental Internet banking system. A team of consultants have confirmed there's an issue with reliability in account transfers when there are many transactions going on at the same time. The consultants are threatening to not approve the application, which would cost the bank millions of dollars in business.

One of the engineers on the project sent a note about the issue:

> Please take a look at the code at [https://github.com/sumcademy/bank](https://github.com/sumcademy/bank)
>
> We included a standard Sinatra project in `main.rb`, you can run it using `bundle exec ruby main.rb`.
>
> The consultants used a program called [Apache Bench](https://en.wikipedia.org/wiki/ApacheBench) to find a bug in our online banking software. Their test script in the `test/` folder, and you can run it with `./test/test.sh 10`. The 10 they said simulates the number of concurrent transactions, the higher the number, the more transactions it will do at the same time.
>
> This is very important for us because the banking software needs to be lightning fast, that's one of our requirements from higher up.
>
> The test file creates 2 new bank accounts, and sends $20 between the two accounts. At the end, both account balances should end up at 0, since the same account was transferred to and from both accounts. But something weird is happening.
>
> If we uncomment the line that says `#set :lock, true`, then the test starts to work, both balances end up at 0 after running the test. But the system will be way too slow if we turn on the lock, it will only process one request at a time. Like we said before, it needs to be lightning fast. We'll be deploying it to our MegaBucks SupraCore infrastructure, it's state of the art and has over 1000 cores available. It'd be a waste of all that power if we could only do one transaction at a time.
>
> Please fix the code so that the test results in 0 for both account balances after completing without `set :lock, true`. One of the consultants mentioned something about a [race condition](https://en.wikipedia.org/wiki/Race_condition#Example).

I trust you understand what that guy said, I didn't get much of that computer mumbo jumbo, but our contact did mention the MegaBucks SupraCore. Sounds like they spent a ton of money on that thing, and they're really hoping it gives their bank an edge with the high frequency traders. See if you can fix their problem for them.