# 9. My Little HTTP Server

![thumb](thumb.png)

It's finally time to build our own HTTP server from scratch. You may want to reference your code from [8. BATCHAT](../08-batchat-***••(ruby,sockets)) since the implementation will be similar.

> 💡 Wait, what?

Yeah, that's right. HTTP is a simple [text-based protocol](https://en.wikipedia.org/wiki/Text-based_protocol), not too different from the protocol we designed in the previous assignment. As such, the socket communication will work mostly the same.

We'll start with some background information on HTTP, though feel free to skip to the Assignment and use the About section as a reference.

## About HTTP

Here are a couple of guides on HTTP if you want more information, though we'll look at the anatomy of an HTTP request together here.
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#HTTP_flow
- https://code.tutsplus.com/tutorials/http-headers-for-dummies--net-8039

### GET request to localhost:4000/route<sup>[1](#modern)</sup>

```yaml
GET /route HTTP/1.1
Host: localhost:4000
User-Agent: Mozilla/5.0 (X11; Fedora; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36

```

An empty line signifies the end of the headers-section. It could be the beginning of the body, if there is one. In the case of a simple GET request, there's no body, but we'll see one below.

### POST request to localhost:4000/submit

```yaml
POST /submit HTTP/1.1
Host: localhost:4000
User-Agent: Mozilla/5.0 (X11; Fedora; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36
Content-Length: 33

first_name=Harry&last_name=Walker

```

A POST request looks very similar to a GET request. The differences are: 

- The verb in the first line of the request is specified as `POST` instead of `GET`
- This request contains a [body](https://en.wikipedia.org/wiki/HTTP_message_body), where the previous request did not.
- Along with the body, there is a `Content-Length` header. This tells the server how many bytes are inside of the body. The server needs to know how long the body is, it will keep trying to read data sent by the browser until it reads N bytes. In the case of our example, `first_name=Harry&last_name=Walker` is 33 bytes.
    - Headers are a structured format. `Key: Value` and they're separated by newlines. An empty line, and it's the end of the header section.
    - However, HTTP request bodies can contain **any data whatsoever**. It's totally unstructured data, a browser could send data in any format. This makes it very easy for a browser to send any sort of data to the server, without requiring [escape characters.](https://en.wikipedia.org/wiki/Escape_character)
    
    In the case of the headers section, two newlines meant that the headers section was over. But imagine you're uploading a file, and it contains two newlines. If we used the same logic to parse the body, then the server would think those two newlines meant the end of the request. And you would just lose the rest of the file. So that's why it's simpler to just send the number of bytes and let the server read that number of bytes from the socket.

### More on sockets

"Socket" is what people call the connection established by a TCP connection. A TCP connection is the most common type of connection there is, and most software uses TCP connections.

TCP sockets don't have much of a concept of "messages." It's bi-directional data. On a socket, you can send data, and receive data. It's up to the **protocol** *over* TCP to decide when a message starts and ends. Many protocols use newlines to delineate messages, but many don't.

Until now, you've been using the `[#gets](https://ruby-doc.org/core-2.7.1/IO.html#method-i-gets)` method to read from a Socket. This method continuously reads from the socket until it encounters a newline, and then returns the data it read up to that point.

There is also a [`#read`](https://ruby-doc.org/core-2.7.1/IO.html#method-i-read) method that takes the number of bytes. You'll want to use this function. In the case of our HTTP server, you'll `read(content_length)` bytes from the browser for the request body. `#gets` may still come in handy for reading the request headers.

## Assignment

Write an HTTP server using Ruby's [TCPServer](https://ruby-doc.org/stdlib-2.4.0/libdoc/socket/rdoc/TCPServer.html), handling the following routes. Make sure it works by testing it in a real web browser.

- `GET /`

The home page! You can start here. Show a nice Hello, World! message in the browser.
- `GET /about`

This is a page that shows some information about the user coming to your server. As part of the response, print out their [User-Agent](https://developer.mozilla.org/en-US/docs/Glossary/user_agent).

For this, you'll need to parse out the request's path, as well as the User-Agent header.
- `GET /form`

Show an HTML form here with `<form method="POST" action="/submit">` and a couple of input fields.
- `POST /submit`

Handle the POST body sent by the previous form. Print out the data, showing that you were able to successfully handle the POST body.

---

<a name="modern"><sup>1</sup></a> Modern browsers send many more headers than this, as you'll see later.