# Front-End Deployment Pipeline

I wanted to set up a pipeline with Docker and Travis CI that will automatically deploy a React application to AWS Elastic Beanstalk.

There are seperate Dockerfiles both for development/testing and production. In the development Dockerfile, we're simply starting the React development server. We're also taking advantage of Docker Compose to spin up another container solely for running tests. The configuration for this container is virtually the same as the the container that we're using to run the application, except we're overriding the containers default command to be `npm run test`.

In the production Dockerfile, we have two steps:

1. Building the React application
2. Copying to the built files to a nginx server

In the `.travis.yml` file, we're first building the container using the development Dockerfile, and then running our tests. If the exit code after the tests are run is 0, our build will succeed and be deployed using the . We also have the configuration for AWS every time changes are made to the master branch.