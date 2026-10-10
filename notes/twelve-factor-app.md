# The Twelve-Factor App

[Link](https://12factor.net/)

## I. Codebase

- One codebase tracked in revision control, many deploys
- Tracked in a version control system (also referred to as revision control system, source control, etc.):
  - Git
  - Mercurial
  - Subversion
- A code repository, or repo, is a copy of the version tracking database
- A codebase is a single repo that shares a root commit (in Git)
- There's always a one-to-one correlation between the codebase and the app
  - multiple codebases (microservices, distributed systems):
    - not an app, a distributed system
    - each component is an app
  - multiple apps sharing the same code is a violation of twelve-factor
    - use shared libraries to share the same code across multiple apps
- One codebase per app, but many deploys of an app
  - Production
  - Staging
  - Local development
- The codebase is the same, but different versions are active in each deploy.

## II. Dependencies

- Explicitly declare and isolate dependencies
- Use package managers
- Don't rely on implicit system-wide packages
- Developers can set up the app locally with only the language runtime and dependency manager.

## III. Config

- Store config in the environment
- Config varies across deploys
- A codebase passes proper config separation if it can be made open-source without leaking credentials.
- Environment variables are independently managed for each deploy

## IV. Backing Services

- Treat backing services as attached resources

A backing service is any service the app consumes over the network:

- Datastores (MySQL, PostgreSQL)
- Messaging/queueing systems (RabbitMQ, Beanstalkd)
- SMTP (email)
- Caching systems (Memcached, Redis)

A twelve-factor app should be able to use local and third-party services interchangeably:

- the app can use a local MySQL, and have no issues using Amazon RDS

Resources can be attached and detached from deploys as needed:

- if there is a database issue, you can spin up a new database restored from a recent backup
- there should be no code changes needed

## V. Build, Release, Run

- Strictly separate build and run stages

Stages:

- **build**: converts code into an executable bundle. Fetches dependencies and compiles binaries and assets.
- **release**: combines the build with the deploy's config.
- **run**: runtime, runs the app in the execution environment.

You can't make code changes at runtime.

### Build

- initiated by app developers when new code is deployed
- can be more complex

### Release

- deployment tools usually have release management tools
  - can roll back to a previous release
- each release should have a unique release ID
  - timestamp
  - incrementing number

### Run

- can happen automatically (e.g. server restart)
- as few moving parts as possible

## VI. Processes

- Execute the app as one or more stateless processes
- A twelve-factor app never assumes that anything cached will be available for a future request
- Data that needs to be persisted must be stored in a stateful backing service (database)
- Memory or the filesystem can be used as a brief, single-transaction cache
- Sticky sessions are a violation of twelve-factor
  - session state should use a datastore with time-expiration, such as Memcached or Redis

## VII. Port Binding

- Export services via port binding
  - HTTP
  - Redis
  - etc.

A twelve-factor app exposes HTTP endpoints and listens for incoming requests on a port:

- local development uses `localhost:8000`
- in deployment, a routing layer handles routing requests

With port binding, one app can be the backing service for another app, by providing the backing service URL as config for the consuming app.

## VIII. Concurrency

- Scale out via the process model
- Processes are first-class citizens
- Scaling up (vertical scaling) an individual VM only goes so far
- Scale out (horizontally) to add more concurrency
- Use a process type for each workload
  - HTTP requests handled by a web process
  - long-running tasks handled by a worker process

## IX. Disposability

- Maximize robustness with fast startup and graceful shutdown
- Processes minimize startup time
- Processes shut down gracefully
  - finish current requests before shutting down
  - HTTP requests should be short
  - worker processes
    - return the job to the queue
    - jobs should be reentrant, workers should be idempotent
- Processes are robust against sudden death
  - the app is architected to handle unexpected, non-graceful terminations

## X. Dev/Prod Parity

- Keep development, staging, and production as similar as possible

Gaps:

- **time gap**: a dev works on a feature that can take a long time to ship
- **personnel gap**: devs write code, ops deploy it
- **tools gap**: different tools in development and production

A twelve-factor app should support continuous deployment:

- devs can write code and deploy it hours or minutes later
- devs are closely involved in deploying their code and observing it in production
- development and production should be as similar as possible

Backing services (database, queueing, cache) should have dev/prod parity:

- don't use different backing services in development and production
- backing services are easy to install (Homebrew, apt-get)
- Docker and Vagrant allow local environments to mimic production environments

Adapters make porting to new backing services easier, but all deploys of the app should use the same type and version of backing services.

## XI. Logs

- Treat logs as event streams

A twelve-factor app doesn't route or store its output logs:

- it doesn't write or manage logfiles
- logs can be:
  - streamed
  - tailed
  - routed to different services for analysis
    - finding events
    - metrics and trends
    - error alerts and monitoring

## XII. Admin Processes

- Run admin/management tasks as one-off processes
- These processes should run in an identical environment
  - run against a release, with the same codebase and config
  - ship admin code with the app code to avoid sync issues
- can use SSH to run the process
