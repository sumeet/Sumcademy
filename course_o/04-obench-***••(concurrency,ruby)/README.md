# 4. OBench

![thumb](thumb.png)

Write a Ruby class that implements behavior similar to the ApacheBench tool used for the test in [3. Bank Concurrency](../03-bank-concurrency-***••(distributed-systems,sql,ruby)).

The interface to use it should look something like this. It doesn't have to look exactly the same, but the same basic functionality should be there. **You also don't need to worry about supporting different HTTP methods, if it only works with POST, that's OK.** The important thing is that it works with the banking server from the previous exercise. If the syntax is different that’s OK.

```ruby
bench = HwBench.new(url: "http://localhost:4567/send_money",
                    method: "POST",
                    data: "from_account=1&to_account=2&amount=10")

# This will make 1000 total request, and divide the work between 10 different
# threads.
summary = bench.run(num_threads: 10, num_requests: 1000)
# When all of the requests are finished executing, it should return a final
# summary of all the requests made.
summary.num_total_requests    # => The number of requests made, 1000
summary.num_requests_success  # => The number of requests that resulted in
                              #    response code starting with 2 (for example,
                              #    200)
summary.num_requests_failed   # => The number of requests that either totally
                              #    failed, or had non-200 status code
summary.average_response_time # => The average amount of time it took per
                              #    request.
summary.total_time            # => The total amount of time taken for the test.
```

To actually make the HTTP requests, try `[Net::HTTP](https://ruby-doc.org/stdlib-2.7.1/libdoc/net/http/rdoc/Net/HTTP.html)`.

### Additional resources

- [https://www.rubyguides.com/2015/07/ruby-threads/](https://www.rubyguides.com/2015/07/ruby-threads/)
- [https://ruby-doc.org/core-2.7.1/Queue.html](https://ruby-doc.org/core-2.7.1/Queue.html)
- [https://www.rubyguides.com/2019/10/ruby-queues/](https://www.rubyguides.com/2019/10/ruby-queues/)