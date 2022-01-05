# 1. Hello..., World?

![thumbnail](./thumb.png)

Every great web application ([Google](https://www.google.com),
[Yelp](https://www.yelp.com/), [Slashdot](https://slashdot.org/), etc.) had to
start somewhere, and so does ours. To be perfectly honest we're still figuring
out our business ideas, BUT one thing we're sure of is that we'll need users. To
pay us money 💰

We need your help with the engineering work. Can you build us a new web
application with a login page? No need to build a registration page, we'll have
Billie, our DBA help get us all test-logins. Just a login page with username and
password. Once you're logged in, you should just see a message saying something
like "Hello, `username`!". Here I'll whip up a quick wireframe:

### Login page

```
Welcome to SmallSmallCo

Login
username: [jon      ]
password: [******** ]
[Log in]
```

## Welcome page (once logged in)

```
Hello, jon!
```

Looking forward to seeing what you can do, I've heard good things about you,
kiddo!

Jiminy — CEO, SmallSmallCo

## Assignment

Start a new Node.js project with [Express](https://expressjs.com/), and add two
pages. The home page should be the login page. Once the user is logged in, they
should be redirected to the welcome page as described by the CEO.

Use any database you'd like for storing the user credentials, the username and
the password.

### Extra Credit (Optional)

- Add a _Logout_ button to the Welcome page
- If the user navigates to the Login page, and is already logged in, redirect
  them to the welcome page
