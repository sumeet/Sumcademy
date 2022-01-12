# 13. Other Databases Part 1: MongoDB

![thumb](thumb.jpg)

An announcement plays over the loudspeaker:

> 💡 A new CTO has joined BELP! Please welcome Jonny Swift, previously the head of Thwickr.PK.

Chatter and excitement fill the room as people ooh and aah. "Wow," you even think to yourself. Thwickr.PK, that's the hottest new social network that everyone's talking about (even your grandma has an account). Jonny's really famous, you've heard about him plenty reading Wacker News posts about high scalability. Finally, someone really top-notch to guide our engineering team. Since you're responsible for the database code, and Jonny is famous for scaling databases, you know it's just a matter of time before he talks to you.

A couple of hours later, you get the email you expected.

> Hey kiddo,
> 
> I'm Jonny Swift, great to meet you. Really excited to help out with BELP, I think it's got a real bright future, ya'know.
> 
> The thing is, back at Thwickr.PK, we had billions of users basically. Jiminy's telling me he wants to get there too, and wants me to make sure the infrastructure's all up to snuff to support that kinda usage. Well I asked what's the datastore we're using and they told me PostgresQL. I knew it, the site just kinda felt like it wasn't webscale. I told Jiminy, I'll help the team get to webscale.
> 
> If you haven't heard of MongoDB before, I suggest you check it out. It was the key to our success over at Thwickr.PK and we're gonna use it at BELP.
> 
> Like I told Jiminy, BELP WILL BE WEB SCALE!
> 
> Take BELP totally off of Postgres and switch everything to Mongo. Have it ready by the end of the week.
> 
> - Jonny
> CTO BELP
> "Jonny's my name, web scale's my game."

You heard Jonny. Time to switch all of BELP's databases off of Postgres to MongoDB.

## Assignment

1. Install MongoDB: [https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)
2. Use the [official Ruby Mongo driver](https://docs.mongodb.com/ruby-driver/master/quick-start/#prerequisites) to connect to the database from Ruby. Do **not** use an ORM-wrapper such as Mongoid.
3. Replace all database access in the entire application with MongoDB. Postgres shouldn't be used at all anymore.

### Resources

- [Ruby MongoDB driver docs](https://docs.mongodb.com/ruby-driver/current/) (esp [CRUD Operations](https://docs.mongodb.com/ruby-driver/current/tutorials/ruby-driver-crud-operations/))
- Any Internet sources. Try to figure out how to use the database using online documentation and sources.

### Extra Credit (If you have extra time)

Write a "migration" script to copy all of the data out of Postgres and into MongoDB. So that the changeover from Postgres to Mongo can be seamless.