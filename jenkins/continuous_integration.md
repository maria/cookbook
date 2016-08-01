# Continuous integration

CI is not only about automated processes, it offers security and trust inside a team.

### How others do CI
Martin Fowler talks about CI in the [article](http://martinfowler.com/articles/continuousIntegration.html). Google wrote about
their way of doing things [here](http://google-engtools.blogspot.ro/2011/06/testing-at-speed-and-scale-of-google.html).
Perhaps the best example comes from [Quora](http://engineering.quora.com/Continuous-Deployment-at-Quora).

## Create a Continuous Integration plan

These are some initiatives from where you can start:

  - Automate the infrastructure setup for Jenkins master/slave using configuration management.
  - Create a minimum set of jobs which will run your most popular tasks: periodic tests, builds, deploys.
  - Introduce the team with the system and use it as much as possible.
  - Create jobs for each task you need to do by hand: test, build, deploy, crons etc. Separate them per environment and modules. Like writing code. :)
  - Revise your infrastructure, create enough slaves to sustain your workload on Jenkins.
  - Integrate with your chat. Integrate with all you can yo make your team life easier.

The main aspects which you should take in account: **stable**, **granularity**, **periodic**, **triggered**, **pipeline**.
Having these jobs you can define a pipeline of jobs, which can be triggered before merging code to production. Yes, this is CI.

#### How to define a pipeline?

This [book](https://www.packtpub.com/sites/default/files/9781849517409-Chapter-01.pdf) has a lot of resources which can help you get started,
it's better from a technical point of view than the article above.

Most of Jenkins's functionality comes from plugins. In order to define a pipeline you have to add the plugin:
[Build Pipeline](https://wiki.jenkins-ci.org/display/JENKINS/Build+Pipeline+Plugin).
After you draw the set of jobs to be ran, you use the plugin to draw their diagram.
