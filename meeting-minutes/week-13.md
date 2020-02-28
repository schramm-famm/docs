What did we do?
Igor: web sockets stuff, different patterns and concurrency. Unique, not going to be reused anywhere. Thao and igor worked 
on concurrency. Made typing a priority, how to resolve everyone typing at the same time, came up with versioning for conversation
all patches have position and version. Reliance on the client being smart about what it's sending.
Also trying to figure out multiple copies of patches and sync them up. Just trying to get one version of patches working

Thao: Getting front end started, going to use vue.js, it's light weight. Has its own state management VueX that we're going to 
be using. 
Is their rendering more predictable than in react? It's similar build own components. It's templating and dynamic.

Honor: probably will pick up tickets for front end. Picked up tickets for conversations.
tried to do keyword searching but failed because we store our patches by characters by. you can seach by time and keyword, but the 
problem is what do we even return on the searches. Just a word and a time isn't useful, we don't really know what to do.
Try undo-ing the patches to see previous version. Like github rewind. Git squash and then apply? GRANULARITY. Just get it working for 
5 people as a baseline.

Riley: User auth done! now just finishing a few more issues and working on front end mockups

We need working patches, then clients, then UI. Maybe we can skip notifications for now

3 weeks until  poster fair!

minimap! Thought you could forget about me did ye!? hark! You love my lobster!

We need to figure things out now and then figure out the uncertainty.

How do we demo microservices? have extra laptops showing logs. Set up a few scenarios.

Anything we need? do we get the poster board? yes, we get it the day before and glue our stuff on.
