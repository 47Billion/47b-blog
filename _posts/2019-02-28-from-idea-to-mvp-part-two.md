--- 
layout: post
title:  "From Idea to MVP — Part 2"
author: rajeev
categories: [ startups ]
image: assets/images/2019-02-28-from-idea-to-mvp-part-two-1.png 
featured: true 
hidden: false
---

*In part 1 of this article, I talked about the first two out of five steps for converting your idea to MVP. This article elaborates remaining steps: defining architecture, setting up development process and initial marketing strategies.*


Before we go into these steps, I would like to reiterate: “*Don’t forget your users during MVP phase.*” In the early stages of MVP development, most of the founders with tech background hesitate to go in front of their potential users. It seems easier to deep dive in the comfort zone of product development rather than exploring unknowns in the grey area of product-market fit. If you keep reminding yourself that MVP is not just about developing tech but also to ascertain viability of key business differentiator, you will be well-prepared to start full product development after completing the MVP.

> During MVP phase, there should be an equal focus on uncovering unknowns in operations, content development and go-to-market aspects of your business as developing the product.

Having said that, let’s look in detail at the next three steps of MVP development.

## Architecture

Defining an elaborate architecture for MVP may seem like the overkill. Typical thinking is that the MVP is just for quickly validating the idea, and the software can be rewritten once we decide to develop a complete product. Too many first-time founders fall in this trap. When there is traction to the MVP, rewriting seems to be disruptive, time-consuming and expensive. At the same time, building on top of such a software soon results in spaghetti and bloated code which quickly becomes hard to maintain and expand.

> A few days spent on a high-level architecture in MVP phase build a solid foundation for the product.

-**Logical Component Design**

Logical component design allows visualizing a well-defined boundary around all the internal services of product. It also helps clarifying well-structured contracts between these services. With proper micro-services architecture, you can easily replace one implementation of the service with another one in the future. Services can be defined based on encapsulation of functionality, scalability characteristics, real-time vs non-real-time requirements, CPU or I/O bound operations etc. Each service can be independently deployed and scaled.

A typical logical component diagram shows logical internal and external building blocks of the product such as User and Admin interfaces, Apps, SDKs, Authentication and Authorization Services, Adapters, Gateways, Queues, Aggregators, Processing Engines, Schedulers, etc.

> Use logical component design to clearly define your internal and external services.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-2.jpeg" alt="Logical Component Diagram"/>
  <figcaption>Logical Component Diagram</figcaption>
</figure>


-**Event flows**

Event flows show request/response and asynchronous events between services. It is useful to draw event flows for a few complex features that involve multiple services. They help clarify responsibilities between various services and also can help identify and reduce complexity by moving around functionality between services. Flows that typically involve third-parties, authentication and authorization and a few common request/response flows are good candidates for event flow diagrams.

i> Use event flows to identify complex interactions and redraw boundaries to simplify service interactions.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-3.jpeg" alt="Event Flow Diagram"/>
  <figcaption>Event Flow Diagram</figcaption>
</figure>


-**Entity Relationship Model**

Defining entity relationship model is one of the most important tasks during architecture definition phase. You can refer to use cases written during product definition phase and list down all the entities and relationships between them. This phase can be used to uncover new entities or new relationships. You can revise use cases based on these new insights.

ER model is a logical representation. The entity can map directly to a table, or you can denormalize and combine multiple entities based on read, write attributes of these entities.

> Use ER model to show core entities and define the relationship between them.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-4.png" alt="Entity Relationship Model"/>
  <figcaption>Entity Relationship Model</figcaption>
</figure>


-**Technology stack**

It is easy to fall in the trap of thinking technology as a product and over-engineer during MVP phase. So instead of mapping use cases to product features to technologies, there is a tendency to reverse map. It is tempting to think of machine learning and blockchain as features without mapping them to use cases for your end users. It is important to remember that technology is merely a facilitator of your overall business idea and the tech stack you choose is completely transparent to your end users.

A well-chosen stack during MVP phase can have a significant impact on development speed, stability, reliability, performance, and costs. Another common pitfall is to assume that MVP stack can easily be replaced later with a more robust stack for the product. But in all probability, your MVP stack will become your product stack, at least during the first few of years. So choosing the right stack at this stage reduces a lot of rework in the later stages of product development.

The choice of software stack for front-end, middleware and database can depend on variety of factors. Rather than debating pros and cons of different software stacks, below are some of the broad guidelines to choose the stack.

- Have a clear separation between front-end and backend through well-defined APIs.
- Weigh advantages and disadvantages of using native, React native or Progressive Web Apps for development of the app.
- Expose well-defined APIs for each backend service based on the logical architecture and event flows.
- Stick to one or two programming languages to reduce learning curve and overall complexity.
- Your choice of stateless App server framework like node.js+Express/Apollo (JavaScript), Flask (Python), Slim (PHP), SparkJava (Java) may significantly affect hosting costs later when you have large-scale deployment.
- With properly defined service oriented architecture, you have flexibility to use the right tool for the right service. This means your API server can be written in node.js and compute intensive analytics and machine learning code can be in Scala, Java or Python.
- Choice of the database should be based on number of factors such as ACID requirements, eventual consistency, read-write load, frequency, relationships, time-series, search, etc. There are varieties of databases to choose from such as Relational, Document, Columnar, Key-value, Reverse index, Graph. It is easy to underestimate deployment complexity and costs during MVP phase and choose multiple databases. But you might find that your requirements are easily satisfied with a single database given the overlapping features supported in modern databases. For example, simple graph relationships can be modeled in MongoDB or an SQL database.
- Choose popular open-source frameworks with active contributions from community.
- Using external PaaS services reduce time-to-market. This decision can significantly affect time-to-market for your MVP. Your core differentiator and services around it can eventually become your Intellectual Property (IP). It is something that, you hope, cannot be easily replicated by your competitors. You should identify these areas early in the process and develop them in-house.
- Choose a single cloud provider based on core PaaS services offering that fit your need so your deployment is not split across multiple cloud providers. For example, Azure for handwriting recognition service, Amazon for Alexa skill services and Google for BigQuery.
- Design all services for horizontal scaling right from the start.
- Begin collecting as much useful raw data about your users as possible. Besides acting as a source of truth, it can be mined later for additional insights and machine learning model training.
- Progressively add Machine Learning capabilities.
- Most importantly, choose a stack based on your team’s expertise and skills.
Choose software stack based on team’s skills while keeping in mind challenges of deployment and scaling in production.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-5.jpeg" alt="Software Stack"/>
  <figcaption>Software Stack</figcaption>
</figure>


-**Coding**

There are numerous articles and books written on “The art of programming”. Here are a few important guidelines -

- Write modular code.

- Be consistent.

- Choose simplicity over early optimization.

- Build tests as a part of code.


> Write modular, consistent and simple code that closely follows philosophy and structure of the chosen framework.

-**Deployment**

Thinking about deployment architecture during MVP phase helps designing for long-term scalability and high-availability. It also helps in weighing costs vs. time-to-market tradeoffs of IaaS vs. PaaS services.

- PaaS services reduce time-to-market and devops headaches during MVP. But they also introduce vendor lock-in, reduce flexibility and increase costs. With properly designed architecture, you can always replace such services with internally developed services after MVP is done.
Use containers (docker with Kubernetes) for development and deployment. The entire deployment automation becomes easier with the use of containers. The added advantage of cloud vendor agnostic deployment and increased portability.

- Add basic monitoring with services like AWS Cloudwatch, Crashlytics for Apps. Add appropriate logging to aid in debugging any issues. It is important to detect and fix any service outages or app crashes quickly when MVP is rolled out for early adopters.
Database servers and any backend services should be secured behind VPCs.

- Plan your deployment for horizontal scaling and lower costs using deployment design.

- Multi Cloud Deployment Diagram with AWS and GCP (Source: 47Billion)

##Process

Entrepreneurs typically fall into one of the two extreme traps during MVP development: thinking of agile as no planning or focussing too much on the process too early without understanding team dynamics. A proper balance between the two allows focusing on real deliverables without much overhead and provides constant feedback. A few days spent at the beginning on planning and setting up continuous integration and deployment process will go a long way towards smooth execution.

-**Planning**

- Work backwards from a date to go live with MVP. Reduce scope or split releases accordingly to fit the available time. This gives a sense of urgency and help focus on essential features. A typical first release should be planned within 3 to 4 months of the start.

- User visible high-impact features can be prioritized over backend operations.
Use simple planning tools like Kanban boards to associate use cases with each sprint. It is easy to maintain backlog and track progress of the sprint using such tools.

- Plan sprints once in two weeks with daily stand-ups. the team should aim for end user visible features to demo at the end of each sprint. A sprint retrospective at the end of the sprint helps with improving subsequent sprints.
Use a planning tool to focus on core features and track progress.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-6.png" alt="Kanban board in Github"/>
  <figcaption>Kanban board in Github</figcaption>
</figure>


-**Continuous Integration (CI)**

A well-setup continuous integration process enforced with proper tools helps in smooth sprint deliveries.

- Create a source code repository, create a new branch for every new feature, use Pull Requests to merge code to Master at the end of the sprint.

- “Pull Request Review” allows developers to comment on the changes proposed in pull requests, approve the changes, or request further changes before the pull request is merged.

> Setup continuous integration process enforced using tools for smooth deliveries.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-7.png" alt="Continuous Integration"/>
  <figcaption>Continuous Integration</figcaption>
</figure>

-**Continuous Deployment (CD)**

A continuous automated deployment process provides immediate visibility to team’s work.

- Setup dev, stage, production deployment environments.

- Setup auto-build and auto-deployment on checkin.

- Use of containers and trusted registry.

- Number each release so it can be traced back to code repository.

- Develop simple migration scripts early on to take care of model changes after MVP deployment.

- Build and deployment notifications to your team’s messaging system or email help in early detection of issues.

> Setup CI-CD process but make sure you are not spending precious time in maintaining the process itself.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-8.jpeg" alt="Continuous Delivery using Docker and Jenkins"/>
  <figcaption>Continuous Delivery using Docker and Jenkins</figcaption>
</figure>

##Marketing

During MVP development phase, equal emphasis should be given to user acquisition and operational strategies. General thinking is that unless you have a working prototype, it is hard to approach potential users. Though true to some extent, you can start gauging interest from early adopters by talking about the product or giving them glimpses of interactive mockups. You should start putting together product distribution, go-to-market and pricing strategies during MVP development phase. If the product involves operations, putting together an operations team during MVP phase makes you ready to launch as soon as MVP is completed.

-**Website**

A single page marketing website setup early helps generate early interest. A sign up form to notify users when product is launched can be added to the site. When the MVP is ready, this page can include links to Apps in App stores or entry point to registration and login of the web portal. Using CMS like WordPress for marketing site gives flexibility to non-tech founders to easily change content. Plugins for forms, Email, SEO, etc. can also be leveraged.

> Develop a single page marketing website for early signups.

-**Content**

A well-written content for marketing website, App, web portal, user on-boarding, in-product user communication like emails, marketing communication, social media posts, blogs, investor pitches that fit visual design makes a significant difference. A good copywriter or a team member with a flair for writing can take on this job during MVP phase.

If your product is content-focussed, this is the time to put together a solid content plan and team whose entire focus is on generating timely content for different user segments of your product.

> A combination of good writing with visuals portrays sleek image of your company and product.

-**Analytics**

It is important to measure user acquisition channel effectiveness, user engagement and behavior and take corrective actions once MVP is deployed. A simple integration with Google Analytics gives you powerful insights into user behavior. You can also collect activity logs in low-cost storage like S3 which can be used for custom analytics.

> Integrate analytics to measure effectiveness of go-to-market strategies as well as product features.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-9.jpeg" alt="Google Analytics (Retention)"/>
  <figcaption>Google Analytics (Retention)</figcaption>
</figure>


-**Campaigns**

Once MVP is deployed, the focus shifts to acquiring new users, preventing users you have got from leaving, and keeping them actively using your product. One of the ways to achieve this is to integrate campaign management software like Amplitude, MixPanel, CleverTap, Google Firebase, in your product. At a minimum, your early product should include ways to send targeted push notifications with deep linking for user retention and engagement.

> Integrate campaign management in your MVP for user retention and engagement.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-28-from-idea-to-mvp-part-two-10.png" alt="Campaign Manager"/>
  <figcaption>Campaign Manager</figcaption>
</figure>

A few weeks of early preparation as described in these five steps can help you develop a successful MVP and builds a solid foundation for your product. Once MVP is launched, you are ready to start acquiring early adopters and further tune the product and go-to-market strategies.

> In this article I have described broad guidelines for developing MVP based on my experience. There are numerous different ways towards successful MVP. What worked and what didn’t work so well for you during MVP phase?

> If you need help bringing your ideas to life, contact us at info@47billion.com.
