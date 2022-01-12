# 14. Other Databases Part 2: Flip A Switch

![thumb](thumb.jpg)

You open up a Pull Request for your MongoDB changes. Within a few minutes, you get a response from the CTO himself, Mr. Swift!

> They will talk about this moment in BELP history for years to come. You are now the messiah, you are the vessel to carry us to the land of scale, web scale.
> 
> With the power granted to me as CTO, I bless this holy PR. Ship it, sir. Ship it good.
> 
> 🚢☕

Now that your PR is approved, you're ready to deploy it to production. Just as you're about to hit the green merge button, you see another comment come in. Someone requested changes.

> What if it doesn't work? Can we add a switch to change back to Postgres if Mongo doesn't work right?
>
> -- Dan Kingsley

The CTO responds right away:

> Dan's right. This ship will have to wait. Add in the switch first, kiddo.

## Assignment

You're not quite ready to deploy your Mongo code yet. The team wants you to add a switch configurable by environment variable — that can easily let you configure if you're using MongoDB, or Postgres. The environment variable should work something like this:

- If `DATABASE_TYPE=mongo` then only use MongoDB to read and write from the database.
- If `DATABASE_TYPE=postgres`, then use Postgres instead of Mongo.

## Extra Video (Not directly related to this assignment)

Watch episode 2 of Clean Code: [**Names++**](https://cleancoders.com/episode/clean-code-episode-2)