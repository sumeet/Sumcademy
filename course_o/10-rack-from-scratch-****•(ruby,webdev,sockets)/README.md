# 10. Rack From Scratch

![thumb](thumb.jpg)

A key component to basically any Ruby web application is the Rack server. Rack is used by Sinatra, Rails, and most other Ruby web frameworks. You may have heard of famous Rack servers such as [Puma](https://puma.io/), [thin](https://github.com/macournoyer/thin) and [unicorn](https://github.com/defunkt/unicorn), and likely use them to serve your webapps. If you've seen it before, it was probably when starting up Sinatra:

```bash
$ ruby main.rb
== Sinatra (v2.1.0) has taken the stage on 4567 for development with backup from **Puma**
**Puma** starting in single mode...
* Version 4.3.6 (ruby 2.7.0-p0), codename: Mysterious Traveller
* Min threads: 0, max threads: 16
* Environment: development
* Listening on tcp://127.0.0.1:4567
* Listening on tcp://[::1]:4567
```

Messages like this one talk mention Rack servers like **Puma**, but we usually don't get to see what Puma or Thin does, adding to the mystique.

You might be surprised to hear they're actually very simple pieces of software. You're already about 90% of the way there.

## Rack

Time to go all the way back to [5. So Long, Frank](../05-so-long-frank-****•(ruby,webdev)) where we converted the banking application from Sinatra to raw Rack. This might be a good time to look back at that project's code, and the [video article](https://thoughtbot.com/upcase/videos/rack).

You will need to modify your [9. My Little HTTP Server](../09-my-little-http-server-***••(ruby,webdev,sockets)) from the previous assignment to serve up Rack applications. Your server should serve up a Rack application like so:

```ruby
app = MyRackApp.new # this is your Rack application, like the one from # 5. So Long, Frank
RackFromScratch.new(app, 'localhost', 8080)
```

This should start a `TCPServer` that serves up the Rack application passed in, on host `localhost` and port `8080`.

### The Rack Specification

The official Rack specification is available at [https://github.com/rack/rack/blob/master/SPEC.rdoc](https://github.com/rack/rack/blob/master/SPEC.rdoc). You'll want to keep this open since you'll be referring to it a lot. This document will dictate how you need to implement your server. Specifically, it explains how all the pieces need to fit together by explaining the **inputs** and **outputs** to a Rack application's `call` function:

> A Rack application is a Ruby object (not a class) that responds to `call`. It takes exactly one argument, the **environment** and returns an Array of exactly three values: The **status**, the **headers**, and the **body**.
> 

```ruby
class MyRackApp
  def call(env)    # env contains information about the request
     # status
    [200,
     # headers
     {"Content-Type": "text/plain"},
	   # body 
     ["Hello, World!"]]
  end
end
```

Your TCPServer will act as a bridge between Ruby code and TCP. You'll need to make a Hash containing information about the request, like `"REQUEST_METHOD"` and `"SCRIPT_NAME"`, and pass it into the Rack application. You may want to use an existing Rack server such as Puma or Thin, and print out the value of `env` just to see what it looks like.

After calling the Rack application, it will return the status code, headers, and the body.

**Tricky ones:**

In order to support advanced features like websockets, file downloads and [response streaming](https://en.wikipedia.org/wiki/Chunked_transfer_encoding), Rack has some tricky parts in the spec. We'll list them out here.

**rack.input**

Grab the request body (which you read using the `Content-Length` header) and put it inside a StringIO with `StringIO.new(body)`

**rack.errors** - Set this to `$stderr`.

**rack.multithread** - Just set this to `false`

**rack.multiprocess** - Just set this to `false`

**rack.run_once** - Just set this to `false`

**rack.hijack?** - Just set this to `false` 

**rack.multipart.buffer_size** - Ignore this

**rack.multipart.tempfile_factory** - Ignore this

### Testing

To make sure your Rack server works, test it against the following use-cases:

1. The "Lobster" test application that's bundled with Rack. To get the application, use:

```ruby
require "rack/lobster"
app = Rack::Lobster.new
RackFromScratch.new(app, 'localhost', 8080)
```

2. The bank [Sinatra](https://github.com/sinatra/sinatra#using-a-classic-style-application-with-a-configru) application from https://github.com/sumcademy/bank:

```ruby
require "./main"
RackFromScratch.new(Sinatra::App, 'localhost', 8080)
```

3. The raw Rack version of BELP from [6. Continuing To Deconstruct The Framework](../06-continuing-to-deconstruct-the-framework-****•(ruby,webdev)).

4. From the root  of any [Rails](https://guides.rubyonrails.org/rails_on_rack.html#rackup) application:

```ruby
require_relative "config/environment"
RackFromScratch.new(Rails.application, 'localhost', 8080)
```

---

This might be a longer assignment, so don't worry about finishing it in one day if it's taking longer.
