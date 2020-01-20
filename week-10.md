We met at the beginnging of the break to discuss our goals.

Igor worked on the Terraform for aws. He started deploying the base of the infrastructure on which all of our microservices will be deployed

Were there choices?

* Leaning into AWS or not?
* AWS has its own certain infrastructure.
* you can run on Amazon "serverless" by giving anything to amazon.
* We decided not to go all the way so we didn't have to tailor our services to amazon and keep firing up aws for testing.

What are the services that we're using?
* Load balancer: using for application level, when request is received, if we have multiple instances of our service, the load balancer decides which instance is under the least amout of stress.
* * Load balancer creates DNS entries when specific servers come up so that we can keep track of them.

Each service will have own load balancer.
It's more abstract

Reseting our selves and thinking of designs, thinking of questions coming up for the presentation.
We have our microservices diagram illustrating what our backend looks like. 
Adding another 
There are some dependencies between services, they can't stand alone!

We figured out our database schemas, and then the microservices that would be needed based on it.

Scenarios have matured, how are we going to test all of these features?
* We have pipline for CI, for isolated testing, bring up aws with microservice with dependecies. and then full system test with every api gateway
 * * plus we have unit test and testing for whenever you want to commit something to master.
 * Bespin has our teraform code, when you want to release a new microservice, it triggers end to end testing. Docker tags trigger testing. Bespon contains configurations for all microservices. 
 
 How have our objectives changed? How do you see yourself doing in march?
 * Pretty good
 * Igor: image uploading for user picture is separate, not included in json, might need extra microservice. Might be a stretch goal. It was surprising because we assumed it would be simple. Mayb have to be sacrificed.
 * It's nice that we have our microservice architecture so we can just take these features out.
 
 Presentation is on friday the 31st of january.
 
 Next week: dry run of the presentation. 60 mins, 45 mins of presentations
 
 What is important content?
 
 * Create common understanding, "Is this like a google doc?" Relate it to other ones. Couple formal presentation with informal presentation.
 2 leveles of design, one is the architectional nature of it. the orthoganal requirements. And also the Scalability of our project. Let requirements guide to that
 * tell us what you guys did vs what you put together. what part did you "implement"  Talk about design decisions that were made.
 * Design of UI, design of DB and also the design of the architecture.
 * Inside of that talk about how you're going to test this? how do we test the scalability of this?
 
 
 Complete Tangent: World according to amazon
 
 
 Wants us to plan out how we get to the poster fair: difference bertween what we see at the presentation and what they will see at the poster fair. It's all about how we explain it and learn from it.
 
 Any questions that the second reader has: answer them to the poster fair. Remain true to original objectives. Don't leave our scope. Ideas have merit but can turn 1 product into another. 
 SHould be able to address in presentation or the poster fair.
 The intent is to get a nice relationship for context to our report.
