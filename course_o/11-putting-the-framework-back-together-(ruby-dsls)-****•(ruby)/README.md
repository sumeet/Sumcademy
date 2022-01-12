# 11. Putting The Framework Back Together (Ruby DSLs)

![thumb](thumb.jpg)

[DSL, or domain-specific language](https://en.wikipedia.org/wiki/Domain-specific_language) is a fancy term for a "language" that you embed inside of a program, a collection of functions, classes, or other code constructs that can be used to express something. It can be useful to think of a DSL as a UI (user interface). Sinatra is like a UI for making websites and web APIs, and RSpec provides a UI for writing tests using Ruby code.

```ruby
 require 'sinatra'
 get '/frank-says' do
   'Put this in your pipe & smoke it!'
 end
```

One of the reasons for Ruby's popularity is that it's often used to make clean-looking, snazzy DSLs. And the reason it's used so often to write said DSLs is because it's really easy to do, almost as if the language was begging you to do it.

## Assignment

Create your own Sinatra clone to use with the [bank](https://github.com/sumcademy/bank) project that you've worked with earlier. Your ultimate goal is to remove `require "sinatra"`. 

Replace it with your own framework that implements the Rack protocol. You should not need to change any of the code that **uses** Sinatra. Just to be clear, by the end, you should not need to change [main.rb](https://github.com/sumcademy/bank/blob/master/main.rb) except for the `require` statements (however you may need to make changes in the interim. 

You can use your own Rack TCPServer from the previous assignment ([10. Rack From Scratch](../10-rack-from-scratch-****•(ruby,webdev,sockets))) to serve the requests.

### Reference Material

- Gary Bernhardt's [RSpec from Scratch](https://www.destroyallsoftware.com/screencasts/catalog/building-rspec-from-scratch) video where he builds a test runner with a similar DSL
- Gary Bernhardt's [Web Framework From Scratch](https://www.destroyallsoftware.com/screencasts/catalog#web-framework-from-scratch) series
- [https://apidock.com/ruby/BasicObject/instance_eval](https://apidock.com/ruby/BasicObject/instance_eval)
