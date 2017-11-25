---
title: Continuously Delivering Full-Stack JavaScript
separator: _____
verticalSeparator: ___
theme: black
revealOptions:
  transition: 'zoom'
  center: false
  controls: true
---

<!-- .slide: class="center" data-background="./front-splash.jpg"  -->
# Continuously Delivering Full-Stack JavaScript

#### IAM: JOSEPH MATTHIAS GOH

___
<!-- .slide: class="center" -->

## about me

<table>
  <tr>
    <td>
      <i class="fa fa-2x fa-info-circle"></i>
    </td>
    <td>
      Software & DevOps/Ops Engineer specialising in full-stack web development  
    </td>
  </tr>
  <tr>
    <td>
      <i class="fa fa-2x fa-briefcase"></i>
    </td>
    <td>
      Government Digital Services, GovTech Singapore
    </td>
  </tr>
  <tr>
    <td>
      <i class="fa fa-2x fa-envelope"></i>
    </td>
    <td>
      <i class="fa fa-comment"></i> | <a href="mailto:hello@joeir.net" target="_blank">hello@joeir.net</a>  
      <i class="fa fa-briefcase"></i> | <a href="mailto:joseph_goh@tech.gov.sg" target="_blank">joseph_goh@tech.gov.sg</a>  
      <i class="fa fa-github" style="font-size: 1.18em;"></i> | <a href="https://github.com/zephinzer" target="_blank">zephinzer</a>  
    </td>
  </tr>
</table>

_____
<!-- .slide: class="center" -->
# why you should listen
if code is written but never deployed, was it ever really written?
___
## got that one big idea?

- code written
- tests passing
- then what?

___
## my story

- music & entertainment startup
- stage was set and ready to go
- a crowd of about 100
- web app was deployed
- at the point of transaction...

___

<!-- .slide: class="center" -->
~10s page load timing

<small>(5s is infinity in internet time)</small>

___
<!-- .slide: class="center" -->
don't be like me

___
## good delivery methodologies

- improve business agility
  - constant iterative improvements
  - frequent updates
- reduce potential for business losses
  - low/no downtime
- enhance user experience
  - quick page loads

___
## the value chain beyond full stack

<!-- .class="icon" -->
<img src="./linkedin-icon.png"
  style="
    border: none;
    height: 100px;
    margin: -1em;
    width:100px;
  "
/>

- software architects
  - 13,737 jobs / 281,179 talents (~4%)
- software engineers
  - 362,957 jobs / 3,225,025 talents (~11%)
- front end developers
  - 23,752 jobs / 121,741 talents (~19%)
- full stack developers
  - 21,817 jobs / 82,875 talents (~26%)

___
## the value chain beyond full stack

<!-- .class="icon" -->
<img src="./linkedin-icon.png"
  style="
    border: none;
    height: 100px;
    margin: -1em;
    width:100px;
  "
/>

- devops engineers
  - 50,516 jobs / 49,095 talents
- ops engineers
  - 2,746 jobs / 19,427 talents
- devops/ops engineers
  - 53,262 jobs / 68,522 talents (~78%)
___
<!-- .slide: class="center" -->
oh, and one more thing...


we're hiring for devops/ops
_____
<!-- .slide: class="center" -->
# continuous delivery
getting the goods to the user, consistently
___
## agile development

- iterative development methodology
- write code, deliver, get feedback, improve
- change is the only const

___
## the delivery cycle

- **business objectives**
- **user stories**
- **development work**
- **delivery**
- **user feedback**
- **improvement**

___
## technical concerns

- development work
- build, test, release & deploy
- - -
- reduce human intervention
- reduce time taken to production
- manifested as...

___
## ci/cd pipeline

- triggered on commit push by developers
  - automated **build**ing
  - automated **test**ing
  - automated **release**
  - automated **deploy**ment

```nonsense
 .----------------------------------------.
 | CODE | BUILD | TEST | RELEASE | DEPLOY |
 .----------------------------------------.
        |             AUTOMATE            |
        \---------------------------------/
```

- **input &nbsp;: code commit**
- **output : deployment(s)**
_____
<!-- .slide: class="center" -->
# about deployments
what it is and what it isn't

___
## deployment

- exposes high level features
  - snapshot of the codebase (aka a release)
  - reference by hash    : 0f1bc668
  - reference by version : v1.12.397

```nonsense
* master (HEAD)
| - bc18a01f             -------------
| - 0f1bc668 ---------> | APPLICATION |
| - 01c2b3d4            | INSTANCE(S) |
| - dd66bc92             -------------
| ...
```
___
## deployment

- configures behaviour of the application
  - application service global variables (eg NODE_ENV)
  - backing services connector configurations
  - admin services schedules

```nonsense
  --------------- -------> - 0 5 * * * knex migrate
 | APPLICATION   |  |      - 0 6 * * * knex seed
 | @ 10.11.12.13 |  |      - ...    
  ---------------   |       
  |                 -> - DB_HOST               
  -> - NODE_ENV        - DB_PORT 
     - PATH            - ...
     - ...
```

___
## deployment

- targets specific users/stakeholders
  - resource locator (eg. https://dev.myapp.com)

```nonsense
  ---------------                             
 | APPLICATION   |     GET / HTTP/1.1           0
 | @ 10.11.12.13 | <-- host: dev.myapp.com <-- /|\
  ---------------                               | 
                            { developers } --> / \
 - - - - - - - - - - - - - - - - - - - - - - - - - -
  ---------------                             
 | APPLICATION   |     GET / HTTP/1.1           0
 | @ 10.11.12.14 | <-- host: uat.myapp.com <-- /|\
  ---------------                               | 
                        { product owners } --> / \
```

___
## deployment

- defines infrastructure & availability
  - what base system should be used?
  - how many vm instances should be running?
  - blue-green deployment parameters?

```nonsense
    (instance 1)        (instance 2)       (instance 3)
  ------------------ - - - - - - - - -  - - - - - - - - -
 | APPLICATION_01i1 | APPLICATION_01i2 | APPLICATION_01i3 |
 | @ 10.11.12.13    | @ 10.11.12.13      @ 10.11.12.14    
 | - node:6.11.4    | - node:6.11.4    | - node:6.11.4    |
  ------------------ - - - - - - - - -  - - - - - - - - - 
  ------------------ - - - - - - - - -  - - - - - - - - -
 | APPLICATION_02i1 | APPLICATION_02i2 | APPLICATION_02i3 |
 | @ 10.11.12.13    | @ 10.11.12.14      @ 10.11.12.15    
 | - node:8.9.1     | - node:8.9.1     | - node:8.9.1     |
  ------------------ - - - - - - - - -  - - - - - - - - - 
```
___
## deployment
#### what it is not

- is **not** the environment
  - avoid correlating environemnts with deployments
  - correlate environments with product behaviour
- is **not** just production
  - deploy to dev after successful build
  - deploy to qa after unit/system tests
  - deploy to uat after integration tests
  - deploy to staging after non-functional tests
  - deploy to production after staging is successful

_____
<!-- .slide: class="center" -->
# getting to deploy
tools of the trade
___
## source control

- a single source of truth for the codebase
- developers push to this repository
- - -
- github, bitbucket, gitlab
- git, mercurial, svn
___
## ci agents/runners

- an automated task runner
- picks up code pushes to the repository
- runs pre-configured tasks (aka jobs)
- - -
- travis, gitlab, teamcity, bamboo
___
## containerisation tool

- for creating container-based deployments
- ensure system environment consistency
- bundle application into an immutable release
- - -
- docker
___
## orchestrator

- for managing deployments
- injection of environment variables
- configuring availability
- - -
- pm2
- docker swarm
- kubernetes
- google container engine
- aws ec2 container service
- azure container service
_____
<!-- .slide: class="center" -->
# how we did it
something that actually, well, works
___
## application architecture
#### front-end
- react.js
- website application

#### back-end
- express/swagger
- web api application
___
## code logistics
- git for revision control
- gitlab for a single source of truth
- yarn for dependency management
- modified trunk-based development
- feature branches for code review
___
## build process
- webpack for coordinating build process
- babel for es7 transpilation
- uglify for code optimisation
- code splitting during bundle creation
- front-end cache reset
___
## testing
#### static analysis
- eslint static code analysis
- nsp for security vulnerability checks
- swagger/docker lint
___
## testing
#### functional tests
- mocha test framework universally
- karma test runner for front-end
- mocha test runner for back-end
- istanbul for unit/system test coverage
- robot framework for integration tests
___
## testing
#### non-functional tests
- gatling for load testing
- nessus for penetration testing
___
## releasing
- versioning using git tags
- docker image building and pushing to private docker registry
___
## source control
#### gitlab
- git
- free
- on-premise
- integrated ci pipeline
- really agile development team
___
## ci agents/runners
#### gitlab ci runners
- ci tasks defined in a .gitlab-ci.yml in the codebase
  - empowers developers to make changes
  - devops as a shared responsibility
- container based build/test/deploy tasks
- multiple remote runners across vm instances
___
## containerisation tool
#### docker
- infrastructure as code
- releasing of application as a versioned, immutable image
- image upload to private, on-premise container registry
___
## orchestrator
#### kubernetes
- infrastructure as code
- works with aws & gcp
- integrates with gitlab ci runners
- deployment done by remote runner on a vm running kubernetes
_____
<!-- .slide: class="center" -->
# deployment-friendly javascript
practical ways to make code more deployable

___
## one codebase; one application

___
## `dependencies` & `devDependencies`


_____
<!-- .slide: class="center" -->
# building the application
the how-to
_____
<!-- .slide: class="center" -->
# automated testing

___
## run tests in containers

___

_____
<!-- .slide: class="center" -->
# code, build, test, release, deploy
technical aspects of the delivery cycle
___


___
## code

- development process
- code logistics handling
- dependency management
- can't be automated... yet

___
## build

- transpilation & optimisation
- trimming of unneeded dependencies
- sensible code spliting
- client-side caching
- automate

___
## test

- ensure things don't break when moving fast
- functional unit/system/integration tests
- non-functional load/pen tests
- can be automated

___
## release

- creating the code snapshot
- giving the snapshot a reference ID
- making the snapshot immutable
- can be automated
___
## deploy

- making a code snapshot accessible to the target user group
- defining availability of application deployment
- specifying update/scaling processes
- can be automated

___


_____
<!-- .slide: class="center" -->
# writing code that is deployable

_____
<!-- .slide: class="center" -->
# building for fast delivery

_____
## building

- version dependencies
  - reduce time code spends in ci
- build with webpack
  - split code
  - bundle common code chunks
  - inject environment
  - client-side cache

___
## building
#### version dependencies

- node_modules is really heavy
  - dependencies don't change with every production deployment
  - version them by their hash to avoid installing dependencies on every commit
  - takes load off ci runners

___
## building
#### split code

- smaller bundle sizes, faster loading

___
## building
#### bundle common code chunks

- one bundle for node_modules
  - dependencies don't change with every production deployment
- one or more bundles for application
  - depends on 

___
## building
#### client-side cache

- allows for faster loading of common code
- client-side loads only what has changed

___
## testing

- static code analysis
- functional unit/system tests
- non-functional tests
- define test tasks in `package.json`

___
## testing
#### static code analysis

___
## testing
#### functional unit/system tests

- we use karma runner for front-end
- universal mocha framework

___
## testing
#### non-functional tests

- gatling
- nessus

___
## testing
#### define tasks in `package.json`

- developers know best
___
## releasing

- use `SEMVER` versioning
- avoid using `version` property in `package.json`

_____
<!-- .slide: class="center" -->
# deployment
(making the application accessible)

___
## infrastructure as code

___
## pm2

___
## docker

___
## kubernetes

_____
<!-- .slide: class="center" -->
# deployment friendly javascript

Twelve Factor in a JavaScript context

___

## twelve factor

- guidelines for creating web applications with deployment in mind
- see more generalised version at https://12factor.net

___

## one codebase, many deploys

- use a revision control system (git)
- one codebase/application

___

## one codebase, many deploys

```md
* ONE  * --------------------------------------------------
* CODE * | build | unit test | integration test | release |
* BASE * --------------------------------------------------
                 |           |                 |          |
                 |           |             UAT <          |
                 |           > QA              PRODUCTION <
                 > CI
```

___

## declare & isolate dependencies

- add node_modules to .gitignore
- specify dependencies in package.json
  - production: &nbsp;**`"dependencies": {...}`**
  - development: **`"devDependencies": {...}`**
- isolate development dependency requiring in code
___

## declare & isolate dependencies
#### lazy-load development dependencies
- <span style="color:#F00">**negative**</span> example:

```javascript
const devDependency = require('dev-dependency');

...

if ( NODE_ENV === 'development' ) {
  const x = devDependency();
}
```

___

## declare & isolate dependencies
#### lazy-load development dependencies
- <span style="color:#0F0">**positive**</span> example:

```javascript
...

if ( NODE_ENV === 'development' ) {
  const devDependency = require('dev-dependency');
  const x = devDependency();
}
```

___

## store config in the environment

- eg. database connection urls, third party services
- use `process.env.*` for ease of injection
- use `"scripts"` property block in `package.json` for tasks

___

## store config in the environment
#### populating process.env in local environment

- using dotenv
  - `npm install dotenv`
  - `vim .env`

```
NODE_ENV=development
DB_HOST=localhost
DB_USER=username
DB_PASS=password
...
```

___

## store config in the environment
#### populating process.env in local environment

- using docker-compose
  - `vim docker-compose.yaml`
  - `docker-compose up`

```yaml
version: "3"
services:
  application:
    env-file: # via dot env
      - ./.env
    environment: # entering it directly
      - NODE_ENV=development
      - DB_HOST=localhost
      - DB_USER=username
      - DB_PASS=password
```
___

## store config in the environment
#### define tasks in package.json

```json
{
  ...,
  "scripts": {
    "start": "node ./entrypoint.js",
    "mocha": "mocha --recursive ...",
    "eslint": "eslint .",
    ...
  },
  ...
}
```
___

## treat backing services as attached resources

- specify urls/service locators in process.env.*
- one code block connecting to service via service locators

```nonsense
       ---------------
       | APPLICATION |
       ---------------
      / in prod  | in dev
     /           ------------------
    /            | localhost:3307 |
   /             ------------------
 ------------------------------------------
 | xxx.yyy.southeast-1b.rds.amazonaws.com |
 ------------------------------------------
```

___

## treat backing services as attached resources
#### one code block connecting to service via service locators

```javascript
const Service = require('service');

module.exports = new Service({
  hostname: process.env.SVC_HOSTNAME,
  username: process.env.SVC_USERNAME,
  password: process.env.SVC_PASSWORD,
  ...
});
```
___

## treat backing services as attached resources
#### one code block connecting to service via service locators

```nonsense
    ---------------
    | APPLICATION |
    ---------------
    | in prod  | in dev
    |          -------------------------------
    /          | SVC_HOSTNAME=localhost:3307 |
   /           | SVC_USERNAME=ci_user        |
  /            | SVC_PASSWORD=ci_password    |
 |             -------------------------------
 -------------------------------------------------------
 | SVC_HOSTNAME=xxx.yyy.southeast-1b.rds.amazonaws.com |
 | SVC_USERNAME=xyzabc                                 |
 | SVC_PASSWORD=zyxcba                                 |
 -------------------------------------------------------
```

___

## execute app as one or more stateless processes

- keep applications stateless
- avoid file read/writes
  - log via a file stream
- implement stateless authentication
  - use `JSON Web Tokens` for authentication
  - use service cluster to store sessions if they're really necessary

___

## export services via port binding

- avoid ports 1 - 1000 (reserved via RFC 1340/IANA)
- use a reverse proxy to access application
  - via Docker Compose
  - via Kubernetes

___

## scale out via process model

- node is single threaded
- prioritise quantity over quality
- high number of instances, low memory allocations

___

## fast startup & graceful shutdown

- start serving requests fast
  - get to .listen() fast
- keep application as stateless as possible
  - avoid session based user authentication
  - singleton instances for service connections

___

## fast startup & graceful shutdown
#### get to .listen() fast

- avoid synchronous processes before .listen()
- 
___

## fast startup & graceful shutdown
#### reduce active service connections

- use singleton instances for service connections

___

## keep development/production similar

- keep behaviour similar across deployments
- avoid development/production specific execution blocks
- expose/hide high level features with feature toggles

___

## logs as event streams

- avoid writing stream to a file
  - use console.*
___

## logs as event streams
#### winston's Console transporter

```javascript
winston.add(winston.transporters.Console);
```

___

## admin tasks as one-off processes

- define tasks in `package.json`
- use a scheduler to start tasks
___

## admin tasks as one-off processes
#### scheduling with cron
___

## admin tasks as one-off processes
#### scheduling with kubernetes

_____

___
## how it all fits in

```nonsense
                 ------ user feedback ------
                /   \                       \
              deploy  -               business objectives/ 
                |       \               model refinement
            release       --                 |
                |            \            user story
              test             --         generation
                |                 \          |
              build                 --     user story
                |                      \ prioritisation
                \                        -- /
                 ---------- code -----------
```