## Continuous Integration on Jenkins

[Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins) is an application that monitors executions of repeated jobs, such as building/testing a software project or jobs run by cron.

## How Jenkins works

A **master** is the installation of Jenkins. A web server is configured on the **master**, to provide a User Interface which enables users to configure the main application and jobs.
**Slaves** are instances set up to build projects for a **master**, such an instance is called a **node**.

A **job** is a Jenkins project which has multiple settings/options. You can configure a job from the UI, by clicking from the left Dashboard the `New Item` button. Usually the `Build a free-style software project` option is more popular, but you can configure it using another job.

A **build** is a job instance, it can be ran automatically by configuring the job to run periodically, or you can schedule one using the `Build now` button from the **job** dashboard.

Jenkins has a lot of Plugins, the most used are **Git & GitHub plugin**, which allows the team to connect a job with a GitHub repo. This way you can schedule a build for every new Pull Request or on a push.


## Jobs ##

A job is usually run on one or more **slave**s. On each **slave** there is the `/var/lib/jenkins/` directory containing Jenkins configuration files,
and each job has a workspace with the path: `$ /var/lib/jenkins/workspace/<job-name>`. You can configure a specific path for each job.

A job configuration has the options:
  - Basic:
     - project name
     - description
     - A list of slaves where the job can run

  - Source code configuration:
     - connect the job with a GitHub repository
     - add a branch for which you want to run the job (if there is no special branch use 'master')
     - it's good to know that you can add more repositories here in order to run the build for all of them (or subscribe them to build on change)
     - Jenkins knows to clone the repo so you don't have to add it by hand in job's workspace

  - Build configuration:
     - Trigger jobs:
        - periodically - using the cron syntax
        - when a change is pushed to a connected repository/branch
        - when a catchphrase is written as a comment on a Pull Request
     - Environment:
        - add a timeout for a job run time - this way a job can't run for days, if an error was raised and the job can't stop.
     - Add a shell command
        - you can add a list of shell commands to be ran before the job is ran
        - on all cases you should add (at least) the command to run the build

  - Post build action:
     - send a notification on Slack
     - send an email

and much more, it depends on the installed Plugins.

## Infrastructure

You should have at least one master instance, where you shouldn't run jobs, all jobs should run on slaves.   
You should start small and then increase the number of slaves or concurrent builds based on how many concurrent jobs  
are ran by your team. Nobody should wait more than a minute for the job to start.  

It's a good practice to create a slave per each project, if you have multiple projects with different technological stacks.  
Also, don't run tests and builds/deploys on the same slaves, because tests usually create a lot of boilerplate which can  
be messy.

If you want to go further, you should split the slaves per environment. Imagine you want to upgrade a package used at build time,    
it's best to have a separate slave where you can test that and deploy the application on staging, without having to put any deploys  
for production on hold or better yet break them.

Use configuration management to provision your servers for Jenkins. You may need to add a new one fast or replace one, plus  
you can use the same configuration you use on the actual servers where the app is running.  
