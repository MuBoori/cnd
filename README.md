# Cloud Native Development (CND)

[![CircleCI](https://circleci.com/gh/okteto/cnd.svg?style=svg)](https://circleci.com/gh/okteto/cnd)

**Cloud Native Development** (CND) is about moving your entire development workflow to kubernetes, avoiding the time-consuming `docker build/push/pull/redeploy` cycle.

CND helps you achieve this with a mix of kubernetes automation, file synching between your local file system and kubernetes and hot reloading of containers.

## Quickstart

Let's start with something simple to show you the power of cloud native development. First, install [cnd locally](#installation).  

Clone the `welcome` service.

```console
git clone https://github.com/okteto/welcome
```

Deploy the welcome service by running the following command.
```console
$ kubectl create -f k8-specifications 
deployment.apps/welcome created
service/welcome created

$ kubectl get service welcome
NAME      TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)        AGE
welcome   LoadBalancer   10.15.255.73   35.204.101.246   80:30879/TCP   20s
```
It might take a minute or two for the service to be up and running depending on your cluster.

*If you're using minikube, you'll need to either change the service to use a NodePort, or enable load balancers in your instance.*

Open your browser and hit the external-ip. You should see our welcome service, a place to vote on whether you prefer dogs or cats. Go ahead and place a few votes on your preferred species. 

Now that your service is running, it's time to do some **cloud native development**. Run the following command on your terminal

```console
$ cnd up
Activating your cloud native development environment...
Linking '/Users/ramiro/okteto/welcome' to ramiro/welcome...
Ready! Go to your local IDE and continue coding!
```

Open your favorite IDE, go to `app.py` and change the value of  `option_a` (line 7) from `Cats` to `Otters` and save the file. Go to the browser, reload the page, and check the label on the first button. Your changes were applied instantly and automatically!

Congratulations, you're now a **cloud native developer** 😎.

For a more advanced scenario involving a microservices-based application, [check out our voting app cnd demo](https://github.com/okteto/cnd-voting-demo).

## Installation

### Homebrew install

```bash
brew tap okteto/cnd
brew install cnd
```

### Manual install

The synching functionality of **cnd** is provided by [syncthing](https://docs.syncthing.net).

To install `syncthing`, download the corresponding binary from their [releases page](https://github.com/syncthing/syncthing/releases).

**cnd** assumes that synchting is in the path, to verify, run the following:
```
which syncthing
```

Install **cnd** from by executing:

```bash
go get github.com/okteto/cnd
```


## How does it work

Interested in the internal workings of cnd? An in-depth explanation [is available here](docs/how-does-it-work.md). 

## Usage

Note: these instructions assume that you already have a kubernetes-based application running.

Define your Cloud Native Development file (`cnd.yml`). A `cnd.yml` looks like this:

```yaml
swap:
  deployment:
    name: webserver
    container: nginx
    image: nginx:alpine
mount:
  source: .
  target: /src
```

For more information about the Cloud Native Development file, see its [reference](docs/cnd-file.md#cnd-yaml-reference).

To convert your dev environment to a cloud native environment, execute:

```bash
cnd up
```

by default, it uses a `cnd.yml` in your current folder. For using a different file, execute:

```bash
cnd up -f path-to-cnd-file
```

To create a long-running session to your cloud native environment, execute:

```bash
cnd exec sh
```

You can also execute standalone commands like:

```bash
cnd exec go test
```

In order to revert back to your original configuration, execute:

```bash
cnd down
```

For a full demo of Cloud Native Development, check the [Voting App demo](https://github.com/okteto/cnd-voting-demo).

# Stay in Touch
Got questions? Have feedback? Come talk to us in 
our [Slack workspace](https://okteto-community.slack.com/join/shared_invite/enQtNDg3MTMyMzA1OTg3LTY1NzE0MGM5YjMwOTAzN2YxZTU3ZjkzNTNkM2Y1YmJjMjlkODU5Mzc1YzY0OThkNWRhYzhkMTM2NWFlY2RkMDk)

Get in touch with the maintainers!

- [Pablo Chico de Guzman](https://twitter.com/pchico83)
- [Ramiro Berrelleza](https://twitter.com/rberrelleza)
- [Ramon Lamana](https://twitter.com/monchocromo)

# Contributions

Interested in contributing? As an open source project, we'd appreciate any help and contributions! 

We follow the standard [github pull request process](https://help.github.com/articles/about-pull-requests/). We'll try to review your contributions as soon as possible. 

## File an Issue
Not ready to contribute code, but see something that needs work? While we encourage everyone to contribute code, it is also appreciated when someone reports an issue. We use [github issues](https://github.com/okteto/cnd/issues) for this.
Also, check our [troubleshooting section](docs/troubleshooting.md) for known issues.

## Code of Conduct
Please make sure to read and observe our [code of conduct](code-of-conduct.md).

# About cnd
cnd was originally created by [Okteto](https://okteto.com/cnd) and is licensed under the Apache 2.0 License.
