# 7. Cookie Dough (Raw Cookies)

![thumb](thumb.jpg)

Anyone who's ever made a website before knows that [cookies](https://en.wikipedia.org/wiki/HTTP_cookie) are how you're supposed to implement login. Cookies even sometimes have a bad reputation: Some security-minded folk say that cookies are bad, and can be used to track your identity, spy on you, and show you ads. Under [GDPR](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation), businesses are required to show you a notice about cookies, these notices are all over the Internet.

Cookies can seem magical. Web frameworks encapsulate cookies inside of [authentication](https://github.com/heartcombo/devise) or ["session"](https://guides.rubyonrails.org/action_controller_overview.html#session) systems, and web browsers save, send, and manage cookies without a peep to the user.

### What are cookies, actually?

Cookies are another contract between a web server and a web browser<sup>[1](#js)</sup>. They're a way for the server to store information about the browsing session inside of the browser. The browser then must send that information back to the server in subsequent requests, essentially giving the browsing session ["state"](https://en.wikipedia.org/wiki/State_(computer_science)) that persists across page loads.

The HTTP cookie protocol consists of two headers:

- [Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) ([Response header](https://developer.mozilla.org/en-US/docs/Glossary/Response_header))
    
    > The **`Set-Cookie`** HTTP response header is used to send a cookie from the server to the user agent, so the user agent can send it back to the server later. To send multiple cookies, multiple **`Set-Cookie`** headers should be sent in the same response.
    > 
    
    Example:
    
    ```yaml
    Set-Cookie: sessionId=38afes7a8
    ```
    
- [Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie) ([Request header](https://developer.mozilla.org/en-US/docs/Glossary/Request_header))
    
    > The **`Cookie`** HTTP request header contains stored HTTP cookies previously sent by the server with the `Set-Cookie` header.
    > 
    
    Example:
    
    ```yaml
    Cookie: sessionId=38afes7a8
    ```
    

Cookies are stored in a key-value fashion inside the browser, and sent back to the server on each request. They also eventually expire, though that can be controlled by the `expires` and `Max-Age` directives. After cookies expire, the browser is supposed to delete them.

### WTF?

Cookies have a special power. They can be enormously confusing. Probably partly because they're called "cookies," which isn't the most descriptive name<sup>[1](#name)</sup>. Web browsers hide them from you deep inside the Developer menu. And they're already confusing, so web frameworks hide them inside the authentication or session systems.

Sometimes you just have to go deep to get a feel of what's going on.

## Assignment

Continue working on the raw Rack-converted BELP from [6. Continuing To Deconstruct The Framework](../06-continuing-to-deconstruct-the-framework-****•(ruby,webdev)). Remove the `Rack::Session::Cookie` middleware from the project. As soon as you do that, user login will stop working. Use the `Set-Cookie` response header, and the `Cookie` request header to store enough information about the user (why not their ID?) to identify them from request to request.

The BELP company's investors want to see user engagement, and that means keeping the user logged in forever. By default, cookies expire after quitting the browser. Use the directives for the cookies that last forever.

### Extra Credit (If the assignment is too short)

- Is your website secure or not? If not, how could you make it secure?
- Does the BELP code now seem messier? If so, see if you can figure out a way to clean up the code.

---

<a name="js"><sup>1</sup></a> Not entirely true because cookies can also be set from JavaScript. But that's not important for this lesson.

<a name="name"><sup>2</sup></a> though admittedly cute