# 8. BATCHAT

![thumb](thumb.gif)

BELP's investors are pleased. The site's metrics are rising, and it seems that users keep coming back to write more and more reviews. You glance at your boss, Mr. Stoppelfarm, from across the room, and see him smiling confidently while typing into his computer. He stands up, and starts heading for... your desk? You know he needs something. What could it be? Is there a bug with account creation? Maybe he wants to add another feature? Whatever it is, looks like we'll have to put away learning about HTTP for the time being and hear what he has to say.

> The investors are happy that people keep coming back to spend time on BELP, mostly to read or write reviews. Our data scientists have analyzed the data, and have found that people only spend 5-10 minutes on the site per day. They say it's probably because most users only eat a few times a day, so once they find a restaurant they like, they leave the site.
>
> What the investors want to is REAL engagement. People spend 1-2 hours a day on YouTube and Twitch, both incredibly successful companies. Our 5-10 minutes is pathetic compared to that. But we're still a new company, we just need to find our optimal growth trajectory.
>
> I had an idea while eating my last mini-tea sandwich at lunch. I think we need a chat feature. We should be the Discord of local!

## BATCHAT: A TCP chat server

This can be a new project, not inside of the existing BELP codebase.

No Gems required for this project, [TCPServer](https://ruby-doc.org/stdlib-2.4.0/libdoc/socket/rdoc/TCPServer.html) and the rest of the Ruby stdlib should have everything you need. You will also need telnet, which should be in your package manager (e.g. `brew install telnet`).

Make a chat server that multiple telnet clients can connect to and chat with each other. Here's an example chat session:

```
$ telnet localhost 1337
   ____      _       _____     ____   _   _      _       _____   
U | __")uU  /"\  u  |_ " _| U /"___| |'| |'| U  /"\  u  |_ " _|  
 \|  _ \/ \/ _ \/     | |   \| | u  /| |_| |\ \/ _ \/     | |    
  | |_) | / ___ \    /| |\   | |/__ U|  _  |u / ___ \    /| |\   
  |____/ /_/   \_\  u |_|U    \____| |_| |_| /_/   \_\  u |_|U   
 _|| \\_  \\    >>  _// \\_  _// \\  //   \\  \\    >>  _// \\_  
(__) (__)(__)  (__)(__) (__)(__)(__)(_") ("_)(__)  (__)(__) (__)

Welcome to BATCHAT local reviews and chat!

Please enter your name, and press enter: mike
Hey, mike! Hope you enjoy the chat.

hey everyone!
<jonny> hi mike!
screw you jonny you dumb loser get THE HELL OUT OF HERE
<jonny> sorry
* jonny has quit the chat
<JStopfarm> mike is that you?
/quit
Connection closed by foreign host. 
```

### Requirements breakdown

- Allows multiple connections
- Prints welcome message and prompts user to enter their name, followed by enter
- Whenever someone types a message, and hits enter, that message should be broadcasted to the rest of the users connected to the server. The message should be broadcasted to everyone **else**, not to the person who sent it.
- Someone can leave the chat by entering the command `/quit` and then enter. They should then be fully disconnected from the server, and their telnet connection should be closed. Their quitting should broadcast to everyone else a message that they quit. There's an example of that in the demo chat above.

### Extra Credit (If this is too short)

- Think about how this relates to [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview#HTTP_flow). Can you able to use a similar code structure to serve a Hello, World! webpage that loads in a browser?
- [This DAS video](https://www.destroyallsoftware.com/screencasts/catalog/http-server-from-scratch) uses the raw `Socket` API to build a server, instead of TCPServer. Would it be hard to use the raw Socket API for this?