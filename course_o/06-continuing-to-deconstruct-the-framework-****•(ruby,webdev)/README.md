# 6. Continuing To Deconstruct The Framework

![thumb](thumb.png)

Using your work from [5. So Long, Frank](../05-so-long-frank-****•(ruby,webdev)) as a guide, remove Sinatra from BELP, and convert it into a raw Rack application.

As you progress through your task, think about how your "framework" code compares between BELP and the bank application. How are they similar? How are they different?

## Tips and Resources

- You can do the swap from Sinatra to Rack gradually instead of all at once. Instead of removing the Sinatra gem right away, first add this Sinatra route:
    
    ```ruby
    get "/*" do
      [status_code, out_headers, bodies] = YourRackApp.new.call(request.env)
      status status_code
      headers out_headers
      body bodies.map(&:to_s).join("")
    end
    ```
    
    Any Sinatra routes that aren't defined will be forwarded to your new Rack application. With this in place, you can one-by-one copy the Sinatra routes into your Rack application, and remove just that one route from Sinatra, while the rest of your application will continue to work.
    
    This technique is sometimes called a [shim](https://en.wikipedia.org/wiki/Shim_(computing)), or an [adaptor](https://en.wikipedia.org/wiki/Adapter_pattern), or even a [wrapper](https://en.wikipedia.org/wiki/Wrapper_library), and it is very handy.
    
- Sinatra usually takes care of rendering ERB templates. Thankfully, ERB is built into the Ruby standard library, and doesn't require any other Gems. This is basically all you'll need:
    
    ```ruby
    require "erb"
    erb = ERB.new(File.read("views/mytemplate.html"))
    body = erb.render_with_hash(business: ..., user: ...) 
    # OR (this is more complicated, but lets you use @ variables)
    @business = ...
    @user = ...
    body = erb.render(binding)
    ```
    
- The BELP app is using `Rack::Session::Cookie` to store session information. The way it works may seem a little magical. But it's a Rack middleware, and designed to be very easy to use with any Rack application, including a raw one.
    
    ```ruby
    # normally, when instantiating your Rack application, you would type:
    YourRackApp.new
    # you can however wrap it with Rack::Session::Cookie, which is a Rack middleware. instead,
    # instantiate your Rack application with:
    your_rack_app = YourRackApp.new
    Rack::Session::Cookie.new(your_rack_app, options)
    # if you passed in options to `use Rack::Session:Cookie` inside of Sinatra, you can 
    # pass them in as the options hash above.
    # 
    # now, inside of your Rack handler, you can access the "session" through
    # env["rack.session"] (instead of `session` like in Sinatra).
    # for example:
    env["rack.session"]["user_id"] = 123
    env["rack.session"]["user_id"]
    ```
    

## Extra Credit

Remove `Rack::Session` and [use cookies manually for authentication by using just the incoming and outgoing headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies). It doesn't have to be secure. For extra-extra credit, make it secure.