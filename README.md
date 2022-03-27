---
author: Michal Stefaniuk, Software Engineer at Devapo (www.devapo.io)

# An Azure platform for quick Camunda enablement
Nowadays many companies from banking sector are moving towards process business automation. 
Where there is a process, a tool like Camunda could be introduced. 
Another approach which seems to be very trendy these days would be migrating to cloud. These two solutions combined
present a huge scale of possibilities, but as they say, with great power comes great responsibility.

Introducing new tools into your architecture sometimes might be really tricky, especially if your project is already live
in the production environment. Moving with your product to cloud might be even more challenging, as this usually requires
major changes in the existing implementation.

Here at Devapo, as an official Camunda partner, for one of our clients from the banking sector we develop a solution, which intends to enable developer
teams to quickly move to Azure cloud with Camunda. In this article I would like to present this concept on its technical level as well its business implications.

## How the platform is utilized? The concept's walkthrough
The goal of the platform was to allow developer teams to quickly move with their Camunda products to Azure cloud. The platform is mainly focused
on automating the process of creating Azure repository, pipelines, including build and infrastructure ones thorugh Azure DevOps REST API.
It's user interface allows to simply select the configuration and particular features that the client is interested in. This concept bridges the gaps
between integrations and bringing features to production.

## Concept Building Paragraph
This is where you'll build on the topic you introduced in your lede and introduction. It's an
opportunity to dig deeper into the concept you outlined. This can include going into more detail
about:
* Your use case, including how Camunda and/or process automation has helped your
  organization
* An interesting customer success story made possible with process automation
* How you solved a problem or challenge you were facing
* Why you chose a particular technology, built a specific project, or worked on a piece of
  software
* How you applied what you learned in your introduction

## (Optional) Further Exploration Paragraph
Here's where you can dig into complex topics, back up a customer use case story with
interesting data, or really show off some in-depth code or a technical process. This paragraph is
also an opportunity to explore how you implemented any solutions you outlined above and what
steps you plan to take in the future

## Conclusion
Let the reader know they’ve made it to the end. Finish your post with a brief restatement of your
main point. Tell the reader you hope they found your post helpful and encourage them to get
started with your idea.

## Key Takeaways and CTAs
Here's where you can highlight the top 3-4 key takeaways a reader can bring back to their
organization after having read your article. These are high-level, one-sentence summaries of
each of your paragraphs. For example:
* Here's how you implement process automation
* Why our organization chose Camunda
* Relying on data is important
* In the end, automation = success
  Close out your post with an explicit call to action that says what you’d like the reader to do next:
  sign up for an account, use a particular feature, build something, etc. If nothing else, ask the
  reader to leave you a comment about the post or join us on the Camunda community forums.

@startuml
actor Client as client
participant Frontend as shop
participant AzureAD as azuread
participant Backend as backend
participant AzureDevOps as devops

client -> shop: Enter UI layer
activate shop

shop --> client: redirect /oauth2/authorize
deactivate shop

client -> azuread: /oauth/authorize
activate azuread

azuread --> client: redirect
deactivate azuread

client -> shop: select Camunda's project configuration
activate shop

shop -> backend: generate project
activate backend
backend -> backend: generate source code with chosen Camunda features

backend -> devops: create Azure repository
activate devops
devops --> backend: return value
deactivate devops

backend -> devops: create build pipelines
activate devops
devops --> backend: return value
deactivate devops

backend -> devops: create infrastructure pipelines
activate devops
devops --> backend: return value
deactivate devops

backend --> shop: return ZIP project
deactivate backend
shop --> client: return ZIP project
deactivate shop
@enduml