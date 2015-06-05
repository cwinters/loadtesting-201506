# Random

## Focus

What is the one (MAYBE two) thing you want people to walk away with?

- Load testing is not rocket science, even if you have an application with
  users and workflow
- Progression of steps
    - why do you want to do load testing at all?
    - what should you expect? (based on the time you put in)
    - how do traditional load testing tools work? (vv quick)
    - some other alternatives: Gatling, JMeter
      (quote about DSLs being a shitty substitute for decent
      library abstractions in your language)

## Example domain

What is a good example that's not hello world but also not too difficult?
(also given that it needs to be session based)

- Maybe just RA stuff? It's pretty straightforward, and there's nothing
  proprietary going on. Even if we show the app!
- Compare/contrast with something like modcloth (WHAT WAS THE NAME OF THE
  RIPOFF SITE?)


## Outsourcing/tools

Relying on external service (NewRelic, whatever) to show graphs, etc:

- outsourcing is a thing that makes you go faster; figure out what's core to
  your business and do that, outsource everything else
- do we want to recreate/reconfigure graphs etc?
- tools that do 80% of what you want with little work are better than tools
  that do 100% of what you want with work

## Different types of apps, different types of load testing

Graphic with different areas:

- venn diagram with rando access (catalog), programmatic access to deal with
  highly dynamic data (TTM)
- what's the gap in the middle? workflows dependent on user activity where
  their actions don't change (as much) based on previous actions
- examples (besides what we're doing):
    - reporting
    - admin actions (?)
    - external interfaces (Braintree)
    - checkout

## Little things

- Watch out for running everything from a single node; be able to run your
  scripts across multiple nodes and do reporting on each node by itself as well
  as all nodes combined
- Avoid averages! I know so little math it's a little embarassing, but I know
  about percentiles and reporting on them
- Load testing is another lever to scale up **your team** -- how much can you
  automate? how much better can your estimates be?

# Roadmap

- Story: start with functionality, deal with scaling when we need to
- "When we need to" is very fluid, and unless you've gone through this ride
  before you'll probably guess it wrong
- What do we want to learn from load testing?
    - Ideal world: every time you make a change, how did that affect performance?
    - Actual world: AHHHHHHH! EVERYTHING STOPPED! WHY DID THAT HAPPEN?!
- What tools exist for load testing? What are their different uses?
- Another aspect of devops mentality -- it's everyone's responsibility, not
  just the DBA, or the sysadmin, or the network engineer
- What prevents us from doing load testing more often?
    - It's hard! Why?
    - Data setup (initial state and old problem of keeping that in-sync with
      code, which we solve in unit tests by having as little as possible)
    - Generating load
    - Lots of numbers, making reports

# Story

Functionality is king.

When we get an idea for software we want to write, we
think about the ways in which it will make some small part of the world a
better place. It might be "disruptive", it might help kids learn to write, it
might make it easier for people to communicate through animated GIFs.

So our team works on our idea and we put it in front of a small circle of
friends and family who tell us good and bad aspects. We enhance and fix and do
that again and again, expanding our circles of people along the way. And if
we're lucky people like it. And our circles expand beyond what we ever thought
possible.

Now we have other problems. Those expanding circles bring expanding traffic, or
*load*. Our carefully constructed table structures mirroring our granular
object relationships break down with higher amounts of concurrent reads and
writes. Even worse, the most frequent API responses return full sets of
user-generated data that pull in too much of the graph.

What we need is a tool (or tools) that:

- allows us to simulate lots of users hitting our site,
- tells us where API bottlenecks are in our application, so that we can
- investigate bottlenecks in detail using profiling or other tools

A quick look around shows lots of mature load testing tools like http-perf, ab,
wrk, siege, and vegeta. Some quick reading shows that those tools are built
for throwing loads of traffic at your app and providing reporting on
response times, which sounds great!

Unfortunately they're more built for random traffic, and our application
requires users to login and move through a workflow. Most of these tools don't
support per-request headers, so they won't even work. Some more looking brings
up tools like JMeter and Gatling. And those make really pretty graphs! But they
also require a good bit of programming and setup, and that feels like I'm
duplicating logic I've already got in my application [[EXPLORE THIS MORE]].

