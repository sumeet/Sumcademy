# 5. So Long, Frank

![thumb](./thumb.jpg)

Sinatra is handy, there's no doubt about that. It lets you make a totally functional website with just a few simple lines of simple and elegant Ruby code. It's front and center on their [homepage](http://sinatrarb.com/), a beautiful Hello, World! example.

```ruby
require 'sinatra'
get '/frank-says' do
  'Put this in your pipe & smoke it!'
end
```

However, as we'll soon see, Sinatra doesn't provide us with as much as it may seem. [Rack](https://thoughtbot.com/upcase/videos/rack) actually does much of the heavy lifting. Yes, Sinatra uses Rack under the hood, and so does Rails, and pretty much any other Ruby web framework or website.

## Assignment

For today's project, we'll work again with the [bank](https://github.com/sumeet/bank) example from [3. Bank Concurrency](../03-bank-concurrency-***••(distributed-systems,sql,ruby)). Remove "sinatra" and "sinatra-contrib" from the Gemfile, as we won't be using them anymore. Get the same application working by following the Rack interface, and serve it up using a Rack compliant webserver, such as Thin.

## Resources and tips

- [https://thoughtbot.com/upcase/videos/rack](https://thoughtbot.com/upcase/videos/rack) — This might be your primary resource. The video is probably good (I haven't watched it yet)
- Make sure to look inside the `env` parameter for routing (this will contain the URL), and the request payload (which you will need for processing POST params)
- Say "Goodbye" to Mr. Sinatra
    
    [https://www.youtube.com/watch?v=fWvWovbWd2o](https://www.youtube.com/watch?v=fWvWovbWd2o)