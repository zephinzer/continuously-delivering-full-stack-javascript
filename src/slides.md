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
<!-- .slide: class="center" data-background="./why-you-should-listen-l.jpg"  -->
# why you should listen

#### if code is written but never deployed, was it ever really written?
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
<!-- .slide: class="center" data-background="./continuous-delivery-l.jpg"  -->
# continuous delivery
#### getting the goods to the user, consistently
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
- enable frequent deployments to production
- reduce time taken to production
- reduce human intervention during deployment

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
<!-- .slide: class="center" data-background="./about-deployments-l.jpg"  -->
# about deployments
#### what it is and what it isn't

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
<!-- .slide: class="center" data-background="./getting-to-deploy-l.jpg"  -->
# getting to deploy
#### tools of the trade
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
<!-- .slide: class="center" data-background="./how-we-did-it-l.jpg"  -->
# how we did it
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
<!-- .slide: class="center" data-background="./deployment-friendly-javascript-l.jpg"  -->
# development

___
## codebase management
#### one codebase; one application

- one ci pipeline per application
- one ci pipeline, multiple deploys
- customised build/test/release process
- no single point of failure
- faster npm install process
___
## tasks management
#### use your package.json

- define tasks in `"scripts"` property
- reference these tasks in the ci pipeline
  - avoids wall of text in ci pipeline definition

```json
{
  "scripts": {
    "start": "node ./entrypoint.js",
    "unit-test": "mocha --recursive \"./test/\"",
    "system-test": "karma start ."
  }
}
```
___
## dependency mangement
#### isolate `devDependencies`

- `"dependencies"` for production
- `"devDependencies"` for development
- prepare `"devDependencies"` to be excluded from production builds
- use `'npm install --dev'` to add a `"devDependencies"` entry
___
## dependency mangement
#### lazy-load `devDependencies`
- <span style="color:#F00">**negative**</span> example:

```javascript
const devDependency = require('dev-dependency');

if ( NODE_ENV === 'development' ) {
  const x = devDependency();
}
```

- <span style="color:#0F0">**positive**</span> example:

```javascript
if ( NODE_ENV === 'development' ) {
  const devDependency = require('dev-dependency');
  const x = devDependency();
}
```
___
## dependency mangement
#### use a lockfile

- npm 5 comes with package-lock.json
- yarn comes with yarn.lock
- standardises dependency version
___
## environment management
#### keep configuration out of the code (I)

- use process.env.* to reference configurations
- <span style="color:#F00">**negative**</span> example:

```javascript
if (process.env.NODE_ENV === 'development')
  server.listen(3000);
else
  server.listen(4000);
```

- <span style="color:#0F0">**positive**</span> example:

```javascript
server.listen(process.env.PORT);
```
___
## environment management
#### keep configuration out of the code (II)
- .env file using `dotenv` npm package
  ```yaml
  NODE_ENV=development
  ```
- docker compose
  ```yaml
  environment:
    - NODE_ENV=development
  ```
- kubernetes
  ```yaml
  env:
  - name: NODE_ENV
    value: development
  ```
___
## environment management
#### keep configuration out of the code (III)
- an exception is for inclusion of development tools:

```javascript
if ( process.env.NODE_ENV === 'development' ) {
  server.use(webpackHotMiddleware);
}
```
___
## environment management
#### minimise dev/prod parity

- reduce number of environments to 2, `dev` and `prod`
- keep logical code execution as similar as possible
- use adapters with common interfaces to reference backing services
___
## environment management
#### services as attached resources
- code always remains the same

```javascript
const {DB_ADAPTER} = process.env;
const DB = require(DB_ADAPTER);
module.exports = new DB({
  hostname: process.env.DB_HOSTNAME,
  username: process.env.DB_USERNAME,
  password: process.env.DB_PASSWORD
})
```

- configure `DB_*` via environment
  - `dotenv` / docker compose / kubernetes
___
## persistent data management
#### version the data schema (I)

- use database migrations
- keeps code database-agnostic
- incremental schema changes specified in code
  - READ: versionable!

```javascript
exports.up = function(knex, Promise) { /* ... */ };
exports.down = function(knex, Promise) { /* ... */ };
```
___
## persistent data management
#### version the data schema (II)

- current tools of the trade:
  - knex (*query builder*)
  - sequelize (*object relational mapper*)

```javascript
knex.schema.createTable('profile', (table) => {
  table.increments();
  table.string('username');
  table.integer('visits');
  table.dateTime('lastVisit');
  table.enum('gender', ['male', 'female'])
  table.timestamps();
});
```
___
## process management
#### get to .listen() fast

- be receptive to requests as soon as possible
- promotes fast startup
- easier and faster deployments
___
## process management
#### keep the application stateless

- avoid file i/o operations
  - eg PID file
- avoid multiple service connections to same service
- promotes scaling via the process model
- promotes fast startups and graceful shutdowns
___
## process management
#### singleton pattern for service connection

- one instance, one connection
- scale via the process model
- promotes faster graceful shutdowns

```javascript
_instance = null;

module.exports = function() {
if ( _instance === null ) {
  _instance = new ServiceAdpater({/* config */});
}
return _instance;
}
```
___
## process management
#### stateless authentication

- prefer jwt over sessions
- use external service to 'remember' sessions
  - eg. redis, mongo
___
## process management
#### log everything, and log to stdout

- logging precedes security
- keeps application stateless
- allows for logs to be collated by process manager/container orchestrator
- do logs filtering from logs collator
_____
<!-- .slide: class="center" data-background="./building-l.jpg"  -->
# building

___
## dependency optimisation
#### version your dependencies

- reusing dependencies shorten the build duration
- hash the lockfile/package.json for the dependency version

```bash
HASH="$(md5 ./yarn.lock)$(md5 ./package.json)";
docker pull registry.com/namespace/dependencies:${HASH};
if [ "$?" != '0' ]; then yarn build; fi;
```
___
## code optimisation
#### code splitting (I)

- improve page load times
- bundle common chunks of code together
- if project is stable, feature level code splits
___
## code optimisation
#### code splitting (II)

- node_modules hardly changes, add them to a 'common chunk'
- `CommonChunksPlugin` for Webpack

```javascript
entry: {
  vendor: ["./node_modules"],
  app: "./entrypoint.js"
},
plugins: [
  new webpack.optimize.CommonsChunkPlugin({
    name: "vendor",
    minChunks: Infinity,
  })
]
```
___
## code optimisation
#### client-side caching (I)

- improve page load times
- use service worker precache by google
- cache code bundles/static assets
___
## code optimisation
#### client-side caching (II)

- using `sw-precache-webpack-plugin' in the build

```javascript
plugins: [
  new SWPrecacheWebpackPlugin(
    {
      cacheId: 'projectId',
      filename: 'sw.js',
      minify: true,
      navigateFallback: PUBLIC_PATH + 'index.html',
      staticFileGlobs: [
        /* paths to files intended for caching */
      ],
      mergeStaticsConfig: true,
    }
  ),
],
```
___
## code optimisation
#### client-side caching (III)

- using `sw-precache-webpack-plugin' in the front-end

```javascript
(function() {
  if('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
  }
})();
```

_____
<!-- .slide: class="center" data-background="./release-l.jpg"  -->
# releasing

___
## versioning
#### avoid package.json

- avoid modifying code when automating the versioning
- adds a useless 'version bump' commit
- every push == requires a pull
- solution: use codebase meta data such as git tags

___
## versioning
#### using git tags

- add a git tag with:
  ```bash
  git tag 1.0.0
  ```
- view git tags with:
  ```bash
  git tag --list
  ```
- get latest tag with:
  ```bash
  git describe --abbrev=1 --tags
  ```

___
## versioning
#### using git tags
- [github.com/zephinzer/version-tagging-scripts](https://github.com/zephinzer/version-tagging-scripts) (DISCLAIMER: mine)
___
## packaging with docker

_____
<!-- .slide: class="center" data-background="./deploying-l.jpg"  -->
# deploying

___
## infrastructure as code

___
## isolate services

___
## configure for quantity

- node is single threaded
- 

___
## don't deploy on fridays

_____
# thank you
## xie xie
## arigato
## kasih