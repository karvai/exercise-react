## Synopsis

This is a basic website intended to work with React and Bootstrap. This website gives a basic
functionality to show information in a responsive way.

This example is based on the [Sudoku React Component](https://www.npmjs.com/package/sudoku-react-component).

## Installation

This code can be automatically run with docker. Please [install docker](https://docs.docker.com/engine/installation/)
in your local environment before proceed. The installation might be different depending on the
operating system you are running.

Once docker is installed, go to this folder and build the virtual machine with:

```
cd <path-to-this-code>
docker build -t react-exercise .
```

Then execute the following code to run the virtual machine. The webservice will be mapped automatically to the port 80
of our local machine. (ensure no other process is running in the port 80 or it might conflict):

```
docker run -dit --name react-instance -v `pwd`:/storage/app -p 80:8080 react-exercise
```

Note that the container has been created to run as an application. Once running it will
show the standard output and terminating the process will terminate also the container.

To connect to the container we can use (this will allow us to execute commands from
inside the container using the bash shell):

```
docker exec -it react-instance /bin/bash
```

If you need to rerun the virtual machine then we need to remove it first. Maybe the
following commands will help you executing _docker run_ again.

```
docker stop react-instance
docker rm react-instance
```

## Testing

This example comes with two different kinds of tests: unit tests and integration/behavioural
tests to check every aspect of the code. The unit tests code coverage is not great as
it's intended to be kept simple.

### Unit testing

The tests are located altogether with the code, under the .test.js extension.

We can run the tests from inside the container or from outside, with:

```
npm run test
```

The command will output the results of the tests. If any assertion didn't succeed, the
system will show the error and a stack trace to know where the problem started.

### Integration testing

The tests are located under tests_api/ directory.

The tests are build through a library called [frisby](https://www.frisbyjs.com/) and
executed using [jasmine](https://jasmine.github.io/). The dependencies are in a
package.json file and installed through [npm](https://www.npmjs.com/)

The dependencies of nodejs are usually installed inside a folder called node_modules.

To run the tests first we have to connect with the container. And then execute:

```
cd /storage/app/test_api
./node_modules/jasmine-node/bin/jasmine-node . --verbose
```

## Improvements

Several improvements can be done to the code:

- Create a Response class that wraps any response from our webservice, so the
format is consistent across any endpoint (status, message, etc. might be
something present at all of them).
- Create a route (endpoint) that returns the number of students currently
available in the system.
- Create a route (endpoint) that returns the list of students ordered by the
birthdate. A parameter can be sent to specify if the oldest one comes first or the
youngest one instead. Choose one behaviour as default if the parameter is not specified.
- Create a test for the above behaviours.

## Contributors

Gorka Guridi <gorka.guridi@gmail.com>
